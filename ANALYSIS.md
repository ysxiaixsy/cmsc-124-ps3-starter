# Environments and the Toy Evaluator

## Why the host needs funcall

CLISP keeps 2 separate namespaces, one for variables and one for functions.
A name in head position is looked up only in the function namespace, so a
variable that holds a function needs funcall to be called. Our toy language
keeps every name in one environment, env, so it is a Lisp-1. The last branch
of eval-expr evaluates the head with eval-expr, which calls lookup on that
env, so (f 1) finds the closure without funcall.
