# Compilers, parsers etc
## Lexical analysis (Lexing)
### Overview
- Splits source code into a sequence of small pieces (lexical tokens)
- may be implemented in 2 phases, *scanning* (segment the text into lexemes) and *evaluating* (convert lexemes into values)
- A token pair consists of the token name and an optional value
- Lexeme syntax is usually a regular language, so a finite state automaton can be used to recognize it

## Syntax analysis (Parsing)
### Overview
- Parsing the tokens to identify syntactic structure of the program
- Involves building a parse tree
- The parse tree is built from the rules of the language formal grammar

## Abstract syntax tree (AST)

## Parse trees
### Overview
- Ordered rooted tree representing the syntax structure of a string according to a context-free grammar
- Concretely reflect the syntax of the input language

