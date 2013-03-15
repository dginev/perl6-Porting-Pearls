P5 to P6 Object Oriented Syntax
===
**Disclaimer:** I can't Moo (yet?). I am writing about porting OO code written in P5's own [OO framework](http://perldoc.perl.org/perlootut.html),
rather than porting code based on the Modern Perl lingo for object orientation ([Moose](http://moose.iinteractive.com/) and his friends).

 - ```class``` or ```module``` ?

  **TODO:** Discuss choice of ```class``` vs ```module``` in P6. Also, what happened to ```package```?

 - All attributes must be pre-declared

 ... well unless you want to be MOPing around that is.
 
 - P5 ```constant``` to P6 ```constant```

  **TODO:** 
 - P5 ```$VERSION``` to P6 ```:ver```

  **TODO:**  
 - P5 ```Exporter``` to P6 ```is export```

  **TODO:**   
 - P5 flexible arguments to P6 ```multi method```s

  **TODO:**   
