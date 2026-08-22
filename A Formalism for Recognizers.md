These diagrams serve as abstractions of the code that would be required to implement them. They can also be viewed as formal mathematical objects, called *finite automata*, that specify recognizers. Formally, a finite automaton (FA) is a five-tuple ($S$, $\Sigma$, $\delta$, $s_0$, $S_A$).

> $\in$ simply refers to membership, $x \in y$ refers to $x$ *is a member of* $y$.
> $\notin$ refers to non-membership. $x \notin y$ refers to $x$ *not* being a member of $y$.

> $\subseteq$ refers to subset-equals. $x \subseteq y$ refers to every element of $x$ is also in $y$, and $x$ could equal $y$ entirely.

- $S$ is the finite amount of states in the recognizer, including $S_e$.
- $\Sigma$ is the finite alphabet, or a finite set of symbols.
- $\delta$ (s, c) is the recognizer's transition function. It maps each state $s \in S$ and each character $c \in \Sigma$ into some next state. In state $s_i$ with input character $c$, the FA takes the transition $s_i \xrightarrow{c} \delta(s_i, c)$ .
- $s_0 \in S$ is the designated start state.
- $S_A$ is the set of accepting states, $S_A \subseteq S$ . Each state in $S_A$ appears as a double circle in the transition diagram.
- $S_e$ is an error state.
‎ 
   ![[Pasted image 20260820152148.png|497]]

$\delta$ right now is only *partially* specified. For all other combinations of state $s_i$ (any state) and input character $c$ , we define $\delta(s_i, c) = s_e$ , which can be understood
as: any state can carry any character over to the error state.

---

A finite automaton accepts a string $x$ if and only if, starting $s_0$ , the sequence of characters in $x$ takes the fininite automaton through a series of transitions that leaves us in an accepting state when the entire string has been consumed.

This corresponds to our intuition for the transition diagram. For the string "new", our example recognizer runs through the transitions: $s_0 \xrightarrow{n} s_1$ , $s_1 \xrightarrow{e} s_2$ , and $s_2 \xrightarrow{w} s_3$ .

Because $s_3 \in S_A$ , and there are no characters left for consumption, the finite automaton accepts "new". However, the same cannot be said for the input: "nut". On the letter 'n', the FA takes $s_0 \xrightarrow{n} s_1$ . On 'u', it takes $s_1 \xrightarrow{u} s_e$ , because it does not match with any of the available characters in the finite alphabet ($\Sigma$). Once the FA enters $S_e$ , it stays in $S_e$ until it reaches the end of the string.

If the string $x$ consists of characters $x_1$ $x_2$ $x_3$ $...$ $x_n$ then the FA accepts $x$ if and
only if:

				$\delta(\delta(... \delta(\delta(\delta(s_0, x_1), x_2), x_3)..., x_n-1), x_n) \in S_A$

The base case, $\delta(s_0, x_1)$ means we're carrying the first character of string $x$ from state 0. Then, we're using the state $\delta(s_0, x_1)$ as the input for the next transition, $\delta(\delta(s_0, x_1), x_2)$ , along with $x_2$ , which yields the next state, and so on, until all of the input has been consumed.

The result of the final application of $\delta$ is another state. If that state is an accepting state, then the FA accepts $x_1$ $x_2$ $x_3$ $...$ $x_n$ .

The FA can encounter a lexical error in the input. Some character $x_j$ might take it into the error state $s_e$ . Entry into $s_e$ occurs because $x_1$ $x_2$ $x_3$ $...$ $x_j$ is not a valid prefix for any word in the language accepted by the FA. Alternatively, the FA can reach the end of the string while in a nonaccepting state. Either case shows that the input string is not a word in the language.