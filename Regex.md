P5 to P6 Regex syntax
===

Related resources:
 - http://perlgeek.de/en/article/5-to-6#post_07
 - http://perlcabal.org/syn/Differences.html#Regexes_and_Rules

Keep in mind that the safest way to port a complex P5 regex would always be the :P5 modifier that allows to use P5 syntax in P6 regexes.

But in the case you want to bite the bullet and do a rewrite using the P6 rules, the following are convenient idioms to keep in mind:
(stumbled on while porting [Lingua::EN::Sentence](https://github.com/dginev/perl6-Lingua-EN-Sentence))
 - P5 ``` [abcd] ``` to P6 ``` <[abcd]> ```
 
 P6 repurposes square brackets for uncaptured groups, and introduces the ``` <[ ]> ``` notation for the P5 character class.
 
 - P5 ``` [^a] ``` to P6 ``` <-[a]> ```
 
 The P5 carrot character class negation is now replaced by the dash. Inside the square brackets, the dash behaves as in P5, and hence needs to be escaped,
 when used literally, ```<-[\-]>``` being the character class for "not a dash". When not escape, the dash stands for a range.
 (Well, if the dash comes first or last in the [] you can leave it unescaped, but escaping it is the safe rule of thumb.)

 - P5 ``` [^-\w] ``` to P6 ```<-[\-\w]>```
  
 Here, I was trying to match "any char except alphabetic or dash". As mentioned above, the dash negates the character class.
  
 **Ignorant workaround:** P6 ```<!&alphad>```
 
 Before knowing how to use the dashed negation, what worked out best was introducing an "alphabetic or dash" token "alphad":
 ```perl6
 my token alphad { <.alpha>|'-' }
 ```
 and negating it. Note that I needed to use ```&alphad``` instead of ```.alphad``` as the token was not inside a grammar.
 
 **Important:** ```<alpha>``` and ```\w``` are **not** identical. ```\w``` includes ```<alpha>```, which matches alphabeteic characters, and additionally matches digits and the underscore.
 For my particular application the difference was not crucial, although being careless will certainly invite hard to trace bugs.
 
 The **right** way (pmichaud++) of matching "any char except alphabetic or dash" would be the P6 ``` <-alpha-[\-]> ```.
 One more example of composition is "no alphabetic characters, except lowercase ascii vowels" written ``` <-alpha+[aeiou]>```.

 - P5 ``` \.\.\.``` to P6 ``` '...' ```

 I found this a rather good example for the elegance of using string literals in regexps, rather than escaping each special char. The payoff increases with the size of your literal.
 
 - P5 ``` \b word \b ``` to P6 ``` << 'word' >> ```
 
 \b has become more fine-grained, as you can explicitly ask for left (``` << ```) and right (``` >> ```) word boundaries. Again, keep in mind the string literal quotes.

 - P5 ``` [[:lower:]] ``` and ``` [[:upper:]]``` to P6 ``` <lower> ``` and ``` <upper> ```
 
 This one is rather self-explanatory, matching a lowercase or uppercase character. 
 If you don't want to capture the match, use ```<.lower>``` or ```<.upper>``` instead.

 - P5 ``` (?!\d) ``` to P6 ```<!before \d>```
 
 The regexes above match "not followed by/matched before a digit", using negative lookahead.
 
 **Note:** Before you read on, keep in mind regexes are space sensitive in P5 by default, while they are space agnostic in P6.

 In P5, ```(?! )``` would delimit a negative lookahead, while ```(?= )``` would delimit a positive lookahead (see a [lookahead](http://www.regular-expressions.info/lookaround.html) tutorial for more details).
 In P6, this is made more readable via "before".
 Negative lookahead is now ```<!before  >``` and positive lookahead is simply ```<before  >```.
 
 Similarly, in P5 ```(?<! )``` would delimit a negative lookbehind and ```(?<= )``` would delimit a positive lookbehind.
 P6 again improves on readability, substituting them with ```<!after  >``` and ```<after  >``` respectively.
 

 - P5 ``` ``` to P6 ``` ```
