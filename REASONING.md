# Reasoning for the Predictions Table

Write one entry under every heading below, then commit this file together with
`predictions.tsv`, before you run a case or open `tests/expected.tsv`.

Each entry names the rule that produces the four predicted fields for that
case. One to three sentences is enough. The grader checks structure only. It
does not judge quality, and it sets no word minimum.

After you run the cases, add a short correction under each case you predicted
wrongly. Say what you predicted, what CLISP printed, and which rule you
misread. Those entries belong in the correction commits.

## P01
Value: 7 since we evaluate the 2 * 3 before adding 1
Kind: Integer, since it returns a number
Length: 1, since 1 item is returned
Operator: function, since its a cons
## P02
Value: (+,1,2) since it is preceeded by a quote
Kind: cons, since it returns a list
Length: 3, since 3 items is returned from the list
Operator: special-operator, since quote is a special operator

## P03
Value: nil since it only nil
Kind: null, since value is nil
Length: 0, since null value
Operator: special-operator, since quote is a special operator

## P04
Value: t since its a bare t
Kind: symbol, since its only a letter
Length: none, since it doesnt return a list
Operator: special-operator, since quote is a special operator

## P05
Value: p since symbolp we treated as symbol p
Kind: symbol, since again its a symbol
Length: none, since doesnt return list
Operator: function, since its a normal function

## P06
Value: nil since () is the same as nil
Kind: null, since nil is null
Length: none, since doesnt return a list
Operator: special-operator, since car is a special operator

## P07
Value: (1,(2,3)) since we have a list of elements
Kind: cons, since its a list of elements
Length: 2, since theres 2 list values
Operator: function, since its a normal function

## P08
Value: empty since if statement evaluates true 
Kind: symbol, since its a string
Length: none, since it doesnt return a list 
Operator: function, since its a normal if else

## P09
Value: (and,1,3) since we have no operator evaluates as list
Kind: cons, since we have a list
Length: 3, since we have a 3 element list
Operator: function, since its a normal function

## P10
Value: 30 since we call ps3-scale 3 with ps3-rate 10
Kind: integer, since we return a number
Length: none, since its not a list
Operator: macro, since its a defun head

## P11
Value: ps3-twice since its a defun with no caller we return the name
Kind: symbol, since name is a string
Length: none, since we do not return a list
Operator: macro, since its a defun head

## P12
Value: 2 since we call down(3) it should go to n - 1 block
Kind: integer, since we return a number
Length: none, since we return a number
Operator: special-operator, since we have a label head

## P13
Value: (2,0,1) since we apply mapcar length to all elements
Kind: cons, since we return a list
Length: 3, since theres 3 items in the list
Operator: function, since mapcar is a normal function

## P14
Value: (1,4,9) since we apply mapchar lambda to all elements
Kind: cons, since we return a list
Length: 3, since theres 3 elements in the list
Operator: function, since mapcar is a normal function

## P15
Value: nil since there nothing calling lambda
Kind: null, since no value returned
Length: none, since no value returned
Operator: function, since lambda is a normal function

## P16
Value: 6 since this case is a static lookup and binds factor 2
Kind: integer, since we return a number
Length: none, since we return a number
Operator: function, since its a normal function
