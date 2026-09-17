Some examples from actual programming languages are in order:

1. The rule given for identifiers in Algol-like languages (such as Java), consists of an alphabetic character followed by zero or more alphanumeric characters, is just: $([A...Z] | [a...z]) ([A...Z] | [a...z] | [0...9])^*$.
   
   Typically, modern languages also allow a few special characters that aren't alphanumeric: '\_', '%', '$', etc.
   
   If the language limits the length of an identifier, we can use a finite closure, as in: $([A...Z] | [a...z]) ([A...Z] | [a...z] | [0...9])^5$ to allow a maximum of 6 characters for a variable.

---

2. An unsigned integer can be described as either zero or a nonzero digit, followed by zero or more digits. The RE for this can be: $[0...9]^+$, however this allows for numbers like 0001. A more specific case that doesn't allow this, could be: $0 | [1...9][0...9]^*$.

3. Unsigned real numers are slightly more complex than standard integers. One possible RE might be: $(0 | [1...9][0...9]^*) (\epsilon | .[0...9]^*)$. The first part is just the RE for an integer, the rest generates either the empty string or a decimal point followed by zero or more digits.
   
   Programming languages often allow scientific notation, like the follow notation: $(0 | [1...9][0...9]^*)(\epsilon | .[0...9]^*) E (\epsilon | + | -) (0 | [1...9][0...9]^*)$. This RE describes a real number, followed by an $E$, followed by an integer to specify the exponent.

---

> A "complement" in this case is a type of RE. The RE: $^\wedge c$ specifies the set {$\Sigma - c$}, the complement of $c$ with respect to $\Sigma$. Complement has a higher precedence than '\*', '|', or '+'.

4. Strings have their own complexity. In most languages, a string can contain any character. While we can write an RE for strings using only the basic operators, a complement operator simplifies the RE. Using complement, a string in C or Java can be described as: $"(^\wedge")^*"$.

5. Comments appear in a number of forms. C++ and Java offer two ways of writing a comment. The delimiter '//' indicates a comment that runs to the end of the current line. The RE for this style of comment is straightforward and easy to understand: $// (\wedge \n)^* \n$.
   
   Multiline comments in C, C++ and Java begin with the delimiter $/*$ and end with $*/$. If we could disallow $*$ in a comment, the RE would be simple: $/*(\wedge*)^**/$. With $*$, the RE is a bit more complex: $/*(\wedge* | *^+\wedge/)^**/$.
   
   ![[Pasted image 20260826192712.png]]