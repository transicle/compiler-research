![[Debugging & Using the Scanner.mp3]]

Before anything else, we need to turn the instances from the `TokenKind` enum into a string. We can do this using a helper function in `src/lexer/tokens.hh`. We can also add a method to the `Token` struct, allowing to directly convert it to a string.

(Add the `#include <format>` line at the start of the file!)

```cpp
static inline std::string kind_to_string(TokenKind kind)
{
	switch (kind)
	{
	case TokenKind::Identifier:
		return "Identifier";
	case TokenKind::Number:
		return "Number";
	case TokenKind::Let:
		return "Let";
	case TokenKind::Equal:
		return "Equal";
	default:
		return "Unknown";
	}
}

struct Token
{
    TokenKind kind;
    std::string value;
    int line;
    int column;

    std::string to_string() const
    {
        return std::format(
	        "Token({}, \"{}\", {}:{})",
	        kind_to_string(kind), value, line, column
	    );
    }
};
```

Then we can edit our main file at `src/main.cc`, with the source containing the following:

```cpp
#include "lexer.hh"

#include <print>

int main()
{
	std::string source = "let x = 1";
	
	Lexer lexer(source);
	
	auto tokens = lexer.lex(source);
	for (const auto &token : tokens)
		println("{}", token.to_string());
	
	return 0;
}
```

And finally, we can see the program's output is clean!

   ![[Pasted image 20260916212447.png|569]]