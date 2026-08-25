The set of words accepted by a finite automaton, $F$, forms a language, $L$, denoted $L(F)$. The transition diagram of $F$ specifies how to spell every word in that language.

**Think of $L$ as a question:** "What does this RE/FA accept?", so $L(F)$ would ask, "what does the RE, $F$, accept?", it accepts the *set* of strings defined by $F$. 

Transition diagrams can be complicated and non-intuitive, thus, most systems use a notation called regular expressions (regex) to describe spelling instead. Any language described by regex is considered a *regular language*.

For any given language, there may exist multiple regular expressions that specify the language. For example, $bow | row$ and $(b | r) ow$ both specify the same language.

The different expressions, in turn, suggestion different finite automatons, as shown below:

   ![[Pasted image 20260823002248.png]]

A modern programming language typically includes various symbols, like '{', '}', '\$', '//', ':', '.', etc., and they also include various keywords, like "if", "for", "while", "return", etc.

To model [syntactic categories ](obsidian://open?vault=Compilers&file=Ch.%202%2FCh.%202.1%20%20%E2%80%94%20%20Scanners) that have large numbers of words, such as integers or identifiers, we need a way to denote an FA's cyclic edge.