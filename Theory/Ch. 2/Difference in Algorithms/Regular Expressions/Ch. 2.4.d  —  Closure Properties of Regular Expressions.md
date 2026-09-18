![[Ch. 2.4.d  —  Closure Properties of Regular Expressions.mp3]]

REs and the languages they produce have been the subject of study. They have many highly intruiging and useful properties. Some of which play a role in the constructions that build recognizers from REs.

> A "regular language" is any language that can be specified by a regular expression.

Applying REs to elements of a set always produces another RE. Obvious examples include concatenation, union, and closure. The concatenation of two REs $x$ and $y$ is just $xy$. Their union is $x | y$. The Kleene closure of $x$ is just $x^*$. Using the definition of an RE, these are all also REs.

All of these closure properties employ a critical role in the use of REs to construct scanners. Assume we have an RE for each [syntactic category ](obsidian://open?vault=Compilers&file=Theory%2FCh.%202%2FCh.%202.1%20%20%E2%80%94%20%20Scanners) in the source language, $a_0, a_1, a_2, ..., a_n$. To build an RE with all of the valid words in the language, we can conjoin them with alternation as $a_0 | a_1 | a_2 | ... | a_n$.

Anything that can be done to an RE for a single syntactic category is applicable to the RE for all valid words in the language.

Closure under concatenation allows building of complex REs from simpler ones, allowing us to conjoin REs in systematic ways. CLosure ensures that $ab$ is an RE as long as both $a$ and $b$ are REs. Thus, any technique that applies to either $a$ or $b$ applies to $ab$.

REs are also closed under both Kleene closure and the finite closures. This allows us to specify particular kinds of large, or possibly even infinite sets with finite patterns.
- **Kleene closures** let us specify infinite sets with concise finite patterns; examples include the integers and unbounded-length identifiers.
- **Finite closures** let us specify large but finite sets with equal ease.

The equivalence between REs and FAs suggests other closure properties. For example, given a complete FA, we can construct an FA that recognizes all words $w$ that are not in $L(FA)$, called the complement of $L(FA)$.

To construct the FA for the complement, we can swap the designation of accepting and nonaccepting states in the original FA. As FAs and REs are equal, this result shows that REs are closed under complement. Indeed, many systems that use REs include a complement operator, such as the $^\wedge$ operator in $lex$ and $flex$.