Assume that we have an alphabet, $\Sigma$. A regular expression describes a set of strings over the characters in $\Sigma$, plus an additional character, $\epsilon$ that represents the empty string. The set of strings defined by an RE is called a *language*. We denote the language described by some RE, $r$, as $L(r)$.

> Concatenation refers to when you conjoin objects together, typically seen in strings. **"Hello,"** **+** **" world!"** **=** **"Hello, world!"**. 

> $\bigcup$ refers to a union (or a combination of two or more sets) of many sets, while $\cup$ refers to the combination of two sets specifically.

Regular expressions are composed of 3 basic operations:

- ***Alternation***  The alternation, or union, of two sets of REs, $r$ and $s$, denoted $r | s$, is {$x | x \in L(r)$ or $x \in L(s)$}.
- ***Concatenation***  The concatenation of two sets of REs, $r$ and $s$, denoted $rs$, contains all strings formed by prepending (adding at the *beginning*) a string from $L(r)$ onto one from $L(s)$, or {$xy | x \in L(r)$ and $y \in L(s)$}.
- ***Closure***  The [Kleene ](https://en.wikipedia.org/wiki/Stephen_Cole_Kleene) closure of $r$, denoted $r*$, is $\bigcup_{i=0}^{\infty} r^i \cdot L(r^*)$ contains all strings that consist of zero or more words from $L(r)$. It's equivalent to writing out: $r^0 \cdot L(r^*) \cup r^1 \cdot L(r^*) \cup r^2 \cdot L(r^*) \cup ...$ going on for infinity.

For convenience, a *finite closure* is typically used instead. The notation $r^ii, i \geq 0$, denotes from one to $i$ occurrences of $r$. A finite closure can always be replaced with an enumeration of the possiblities; for example $r^3$ is just $(\epsilon | r | rr | rrr)$. The *positive closurue*, denoted $r^+$, is just $rr^*$ and consists of one or more occurrences of $r$.

Using alternation, concatenation, and Kleene closures, we can define the set of regular expressions over an alphabet $\Sigma$ as follows:

1. If $a \in \Sigma$, then $a$ is an RE denoting the set {$a$}, and $L(a)$ is $a$.
2. If $r$ and $s$ are REs, denoting sets $L(r)$ and $L(s)$, respectively, then
   $r | s$ is an RE denoting the alternation of $L(r)$ and $L(s)$;
   $rs$ is an RE denoting the concatenation of $L(r)$ and $L(s)$; and
   $r^*$ is an RE denoting the Kleene closure of $L(r)$.
3. $\epsilon$ is an RE denoting the set that only contains the empty string.

To remove ambiguities, parenthesis have the highest precedence, followed by closure, concatenation, and alternation, in that order.