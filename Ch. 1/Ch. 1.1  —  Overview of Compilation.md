A compiler is some translation software that turns a program written in one language, into a program written in another language, typically a lower-level form, like Assembly.

To do so, the compiler *must* understand the form (or syntax), and the content (or meaning) of the input language, as well as needing to understand the rules that control syntax and meaning in the output language.

   ![[Pasted image 20260820151550.png|559]]

The way a typical compiler is designed derives from a few core processes. The compiler has a *front end*, which handles the source language and a *back end* to handle the target language.

Connecting the front end and the back end is where you will see a formal representation of the program in what is called an *intermediate representation* (IR), whose meaning is largely independent of either language.

Modern compilers typically include an optimizer that sits between the front and back end; the optimizer analyzes the IR and rewrites it into a form that is, under one one or more metrics, better than the original input.