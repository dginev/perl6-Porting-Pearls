P5 to P6 Regex syntax
===

Related resources:
 - http://perlgeek.de/en/article/5-to-6#post_07
 - http://perlcabal.org/syn/Differences.html#Regexes_and_Rules

Keep in mind that the safest way to port a complex P5 regex would always be the :P5 modifier that allows to use P5 syntax in P6 regexes.

But in the case you want to bite the bullet and do a rewrite using the P6 rules, the following are convenient idioms to keep in mind:
 - P5 ``` [^-\w] ``` to P6 ```<!&alphad>```
  
  Here, I was trying to match "any char except alphabetic or dash", which worked out best as introducing an "alphabetic or dash" token "alphad":
  ```perl6
  my token alphad { <.alpha>|'-' }
  ```
  and negating it. Note that I needed to use ```&alphad``` instead of ```.alphad``` as the token was not inside a grammar.

 - P5 ``` \.\.\.``` to P6 ``` '...' ```

 I found this a rather good example for the elegance of using string literals in regexps, rather than escaping each special char. The payoff increases with the size of your literal.
 
 - P5 ``` \b word \b ``` to P6 ``` << 'word' >> ```
 
 \b has become more fine-grained, as you can explicitly ask for left ``` << ``` and right ``` >> ``` word boundaries. Again, keep in mind the string literal quotes.
