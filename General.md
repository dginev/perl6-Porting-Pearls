Beginning a P5-to-P6 Port
===

So, you have a P5 library that you authored/co-maintain/use daily/simply have a fancy for.
 You've decided to learn/play around with/switch to Perl 6, and you need it by your side, where it belongs.
 
 So let's get porting.

## Preliminary resources
 - Definitely start off with the [Create and Distribute Modules Tutorial](http://wiki.perl6.org/Create%20and%20Distribute%20Modules)
 - Are you porting a CPAN module? Has it been ported already? Check at http://modules.perl6.org/
 - Get used to [panda](https://github.com/tadzik/panda/), the P6 ```cpan``` replacement.

## Tests

At the time of writing, the diversity of P5 testing libraries has not propagated to P6.
The native [Test](http://perl6maven.com/how-to-test-perl6-modules) module usually suffices. 
Porting test files is usually straightforward.

There are some API differences between P5's [Test::More](http://en.wikipedia.org/wiki/Test::More) and P6's [Test](http://perl6maven.com/how-to-test-perl6-modules)

 - P5 ```not_ok``` to P6 ```nok```
 
 Same effect and syntax, just renamed.

*Feel free to contribute porting tips for tests to this section.*

## Documentation

P5 ```perldoc``` to P6  [p6doc](https://github.com/perl6/doc)

