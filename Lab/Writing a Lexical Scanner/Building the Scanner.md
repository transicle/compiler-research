![[Building the Scanner.mp3]]

Now, we can actually construct the scanner. In the `src/lexer/lexer.cc` file, we can implement everything in the public-side of our `Lexer` class.

```cpp
#include "lexer.hh"

#include <string>
#include <vector>

Lexer::Lexer(std::string file) : source(source), position{0} {}

Lexer::~Lexer() {}

std::vector<Token> Lexer::lex(std::string_view source)
{
	...
}
```

We can use our private methods in our public function to properly construct the `lex` function. But first, we have to actually define the logic of the private methods in our `src/lexer/lexer.hh` file.

```cpp
char peek(int offset = 0)
{
	if (!is_eof())
	{
		return source[position + offset];
	}
	
	return '\0';
}

char consume()
{
	char current = peek();
	
	if (current == '\n')
	{
		line += 1;
		column = 0;
	}
	else
	{
		column += 1;
	}
	
	position += 1;	
	return current;
}

bool is_eof()
{
	return position >= (int)source.length();
}

void skip_ws()
{
	if (!is_eof() && isspace(peek()))
	{
		consume();
	}
}
```

And we can now properly handle the main `lex` function in the public-side of the class.

```cpp
std::vector<Token> Lexer::lex(std::string_view source)
{
	std::vector<Token> tokens;
	
	while (!is_eof())	
	{
		skip_ws();
		char current = peek();
		
		switch (current)
		{
		case '=':
			tokens.emplace_back(Token{
				TokenKind::Equal,
				"=",
				line,
				column,
			});
			
			break;
		default:
			if (isdigit(current))
			{
				int start_line = line;
				int start_column = column;
				std::string value;
				
				while (!is_eof() && (isdigit(peek()) || peek() == '.'))
				{
					value += consume();
				}
				
				tokens.emplace_back(Token{
					TokenKind::Number,
					value,
					start_line,
					start_column,
				});
			}
			
			else if (isalpha(current))
			{
				int start_line = line;
				int start_column = column;
				std::string word;
				
				while (!is_eof() && (isalpha(peek()) || peek() == '_'))
				{
					word += consume();
				}
				
				if (word == "let")
				{
					tokens.emplace_back(Token{
						TokenKind::Let,
						word,
						start_line,
						start_column,
					});
				}
				else
				{
					tokens.emplace_back(Token{
						TokenKind::Identifier,
						word,
						start_line,
						start_column,
					});
				}
			}
			else
			{
				consume();
			}
			
			break;
		}
	}
	
	return tokens;
}
```