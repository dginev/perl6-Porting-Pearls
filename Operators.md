P5 to P6 Opeartors
===
 
 - P5 to P6 Bitwise operators
 
 Bitwise operations in P5 (```~```,```|```,```&```) are prefixed by typing [coercion operators](http://perl6.wikia.com/wiki/Coercion_Operator) in P6.
 **Note** that binary negation in P5 is now written in P6 with a caret(```^```) instead of a tilde(```~```) and the additional prefix is still required.

 So, a P5 expression, with integer variables:
 
  ```$flags &= ~$value;```
 
 becomes the P6 expression:
 
 ```$flags = $flags +& (+^$value);```
