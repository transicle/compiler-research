Finite-State Machine (FSM) diagrams are ways to represent how a system processes input one piece at a time, as well as changes between different states.

   ![[Pasted image 20260820151726.png|372]]

Each labeled circle represents a state during computation of the program. The initial state is $s_0$—$s_3$ is an accepting state; the recognizer reaches $s_3$ only when the input is "new." The double circle (or rings) denotes $s_3$ as an accepting state.

Arrows represent transitions from state-to-state based on input characters. If the recognizer starts in $s_0$, and read the characters 'n', 'e', 'w', the transitions take us to $s_3$. Because each character shifts the state up by 1.

**What happens on any other input, like 'n', 'o', 't'?** The letter 'o' does not match any edge leaving $s_1$. In the code, cases that do not match "new", execute *try something else*.

The recognizer takes a transition to the error state. When we draw the transition diagram of a recognizer, we usually omit transitions to the error state, since each state has an implicit transition to the error state on each unspecified input.

   ![[Pasted image 20260820152031.png|279]]