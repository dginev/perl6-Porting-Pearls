P5 to P6 Object Oriented Syntax
===
**Disclaimer:** I can't Moo (yet?). I am writing about porting OO code written in P5's own [OO framework](http://perldoc.perl.org/perlootut.html),
rather than porting code based on the Modern Perl lingo for object orientation ([Moose](http://moose.iinteractive.com/) and his friends).

 - ```class``` or ```module``` ?
 
 **Rule of thumb:** Always use ```class```.
 
 It's that simple. ```module``` is usually a convenient way to capture procedural code that provides static utility subroutines,
 such as the ones in [File::Spec](https://github.com/FROGGS/p6-File-Spec/).

 However, a ```class``` can also be used to achieve anything a ```module``` would and it additionally provides, well, all of object oriented programming.
 
 From what I understand so far, you can forget about using the ```package``` keyword for declaring classes and modules,
   as it will be exclusively used for package namespaces (see [S10](http://perlcabal.org/syn/S10.html)).
   
 So if you are unsure about the API of your library and just want to start off quickly, port the P5 ```package``` into a P6 ```class```.

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
