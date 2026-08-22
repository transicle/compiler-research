The CBC, or Character-by-Character algorithm is a type of algorithm for functional [lexical scanners ](obsidian://open?vault=Compilers&file=Ch.%202%2FCh.%202.1%20%20%E2%80%94%20%20Scanners) that proceed 1 character at a time when processing a string.

Take for example, the word "new", the CBC algorithm will look for 'n', if found, proceed, then check for 'e', if found, proceed, then check for 'w', if found, proceed. If one fails, the whole thing is rejected.

   ![[Pasted image 20260820151726.png|420]]
   
Read about and understand [Finite-State Machine (FSM) Diagrams ](obsidian://open?vault=Compilers&file=Understanding%20FSM%20Diagrams)

   ![[Pasted image 20260820151829.png|290]]

The scanner uses a common test for 'n' that takes it from $s_0$ to $s_1$, denotes
that $s_0 \xrightarrow{n} s_1$ . If the next character is 'e', it takes the transition $s_1 \xrightarrow{e} s_2$  . If, instead, the next character is 'o', it makes the move $s_1 \xrightarrow{o} s_4$ .

Finally, a 'w' in $s_2$ causes the transition $s_2 \xrightarrow{w} s_3$ , and a 't' in $s_4$ produces $s_4 \xrightarrow{t} s_5$ . State $s_3$ indicates that the input *was* "new", while $s_5$ indicates that it was not.

## Scanning Numbers

The CBC algorithm allows us to very easy handle simple words like "new", "while", or "not", but we can also handle numbers very easily as well.

   ![[Pasted image 20260821232039.png]]

In this transition diagram, if $s_0$ is 0, we can transition to $s_1$ , an acceptance state, as we don't really want 01 to be a value (If we did, we could just omit the 0 case and just keep it always $0...9$ ). However, for the second plausible option, it checks if the value provided to $s_0$ is 1 through 9, if so, it indefinitely checks the next character's input until it is an invalid input.

   ![[Pasted image 20260822003609.png]]

We can develop similar FAs for signed integers, real numbers, and complex numbers too! A simplified version of the rule that governs variable names in Algol-like languages, such as C or Java, might be:

>   *an identifier consists of an alphabetic character, followed by zero or more alphanumeric characters.*

This definition allows an infinite set of variables. It can be specified with the simple two-state FA:

   ![[Pasted image 20260822021340.png]]

A lot of modern languages allow '\_' and characters like '&' to also be used in variable names.

To simplify scanner construction, we need a concise notation to specify the lexical structure of words, and a way to turn such specification into an FA and into code to implement the FA.