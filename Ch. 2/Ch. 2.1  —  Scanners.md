A scanner (or: *lexical scanner*, *analyzer*, *lexical analyzer*) is a piece of software that transform a stream of characters, or a string, into a stream of tokens. Each word must be set into a specific category, called a token type.

An example of a token type would be the `Ident(String)` variant inside of the `Token` enumerated type, where `Ident` is the actual token, and `String` is the type of value that can be stored in the token.

> **Syntactic Categories** are a classification of words according to their usage grammatically. In a practical sense, these categories correspond to the symbols in the language's grammar.

```rust
enum Token {
	Ident(String)
}
```

A scanner should produce a pair, `{lexeme, category}`, where lexeme is the spelling of the word, and category is its syntactic category. This pair is often seen as a token.

In the context of scanning, any and all symbols are treated as separate words, i.e., '?', ':', '.', or even multi-character symbols such as: '::', '||', '??', etc.