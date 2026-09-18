![[Creating the Scanner's Design.mp3]]

A lexical scanner can be written using various algorithms — that of which, I will use the [CBC algorithm ](obsidian://open?vault=Compilers&file=Theory%2FCh.%202%2FDifference%20in%20Algorithms%2FCh.%202.2.a%20%20%E2%80%94%20%20The%20CBC%20Algorithm). The scanner's job is to process source code, and output a stream (or a kind of array) of "tokens". A token holds information such as the line and column numbers, the character scanned, and the type of the token.

We need a few files:
- `src/main.cc`
- `src/lexer/lexer.cc` — Where we'll store actual implementations.
- `src/lexer/lexer.hh` — Where we'll declare the existence of everything.
- `src/lexer/tokens.hh` — Where we'll declare the tokens themselves.

We're able to declare the `Token` struct and the `TokenKind` enum. In this example, our lexer will only be able to handle simple variables, using the syntax: `let x = y`, expressions (formulas or symbols like '+', '-', '(', or ')') won't be handled.

```cpp
#pragma once

#include <string>

enum class TokenKind
{
	Identifier,
	Number,
	
//  Keywords
	Let,
	
//  Symbols
	Equal,
};

struct Token
{
	TokenKind kind;
	std::string_view lexeme;
	int line;
	int column;
};
```

In the `scanner.hh` file, we can have the following source for defining our lexer class.

```cpp
#include <string>
#include <vector>
#include <cctype>

class Lexer
{
public:
	Lexer();
	~Lexer();
	
	std::vector<Token> lex(std::string_view source_code);
		
private:
	std::string source;
	int position{};
	int line{};
	int column{};

	char peek(int offset = 0);
	
	char consume();
	
	bool is_eof();
	
	void skip_ws();
};
```
