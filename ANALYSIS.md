# Environments and the Toy Evaluator

## Tracing one form

We trace this form through eval-expr, starting from the empty env:

```lisp
(let ((x 2))
  (let ((f (lambda (y) (+ x y))))
    (let ((x 100))
      (f 1))))
```

1. The head is `let`, so eval-expr calls eval-let. It evaluates the init 2
   and calls extend-env, giving `((x . 2))`.
2. The inner `let` evaluates `(lambda (y) (+ x y))` in `((x . 2))`. The
   lambda branch calls make-closure, which returns
   `(:closure (y) (+ x y) ((x . 2)))`. The env becomes
   `((f . <closure>) (x . 2))`.
3. The third `let` binds x to 100 in front, so the env is
   `((x . 100) (f . <closure>) (x . 2))`.
4. `(f 1)` reaches the last branch. eval-expr evaluates the head f, and lookup
   returns the closure. eval-operands gives `(1)`.
5. apply-closure checks the tag and the count, then extends the saved env,
   not the current one, to `((y . 1) (x . 2))`.
6. The body `(+ x y)` goes through apply-op. lookup finds x as 2 and y as 1,
   so the result is 3.

## Where the defining environment is captured

The capture happens at `src/evaluator.lisp:113` having environment `((x . 2))`,
 where the lambda branch hands
make-closure the env that is current when the lambda is evaluated. Line 97
then uses that saved env in apply-closure, which is what makes the scope
lexical.

## Joining arguments to the caller's environment

If apply-closure extended the caller's env instead, step 5 would build
`((y . 1) (x . 100) (f . <closure>) (x . 2))`. lookup returns the first
match, so x would be 100 and the form would return 101. That is dynamic
scope: a function's free variables would depend on where it is called, so
any `let` around a call site could silently change what the function does.
The closure would also no longer need to store an env at all.

## Why the host needs funcall

CLISP keeps 2 separate namespaces, one for variables and one for functions.
A name in head position is looked up only in the function namespace, so a
variable that holds a function needs funcall to be called. Our toy language
keeps every name in one environment, env, so it is a Lisp-1. The last branch
of eval-expr evaluates the head with eval-expr, which calls lookup on that
env, so (f 1) finds the closure without funcall.
