# FEI VSB-TUO: PLC
![Python](https://img.shields.io/badge/python-3.10-blue) ![ANTLR4](https://img.shields.io/badge/ANTLR-4-orange)

A compiler and stack-based interpreter for a small statically-typed imperative language. The compiler parses source code (ANTLR4-generated grammar), performs type checking, and emits stack-machine instructions; the interpreter executes them.

## Running it

Requires Python 3.10.

```bash
pip install -r requirements.txt
```

Compile a source file to bytecode:
```bash
python compiler.py  
```

Run the bytecode:
```bash
python interpreter.py 
```

Example programs live in [`samples/`](./samples/).


## Language Specification

### Program Structure

- A program is a sequence of commands.
- Formatting (whitespace, comments, etc.) does not affect the meaning of the program.
- Comments are denoted by `//` and continue to the end of the line.

### Literals

- **int**: A sequence of digits (e.g., `123`).
- **float**: A sequence of digits containing a `.` (e.g., `12.34`).
- **bool**: `true` or `false`.
- **string**: Text enclosed in double quotation marks (e.g., `"hello"`).

### Variables

- Variables must be declared before use.
- Types: `int`, `float`, `bool`, `string`.
- Initial values: `0` for `int`, `0.0` for `float`, `false` for `bool`, and `""` for `string`.

### Statements

- **Declaration**: `type variable1, variable2, ...;`
- **Expression**: Evaluates the expression and discards the result (side effects like variable assignment possible).
- **Input**: `read variable1, variable2, ...;`
- **Output**: `write expression1, expression2, ...;`
- **Block**: `{ statement1 statement2 ... }`
- **Conditional**: `if (condition) statement [else statement]`
- **Loop**: `while (condition) statement`
- **For loop**: `for (expression; condition; expression) statement`

### Expressions

- **Unary Operators**: `-` (negation), `!` (logical NOT)
- **Binary Operators**:
  - Arithmetic: `+`, `-`, `*`, `/`, `%`
  - String concatenation: `.`
  - Relational: `<`, `>`
  - Equality: `==`, `!=`
  - Logical: `&&`, `||`
  - Assignment: `=`


## Sample Programs

The [`samples`](./samples/) directory contains several example programs testing and demonstrating various features of the language:

- `first.lang`: Demonstrates constants, variables, expressions, input/output, and multiple assignments.
- `second.lang`: Demonstrates relational and logical operators.
- `third.lang`: Demonstrates if statements, while loops, and for loops.
- `expressions.lang`: Complex expressions and type conversions.
- `errors.lang`: Examples of syntax and type errors.
- `centroids.lang`: Calculates the centroid of points.
- `primes.lang`: Calculates prime numbers and a "prime string".


## Instruction Set

The compiler generates a stack-based instruction set that the interpreter executes. Below are the instructions:

- **Arithmetic**: `add`, `sub`, `mul`, `div`, `mod`
- **Unary Operations**: `uminus`, `not`, `itof`
- **String Concatenation**: `concat`
- **Logical**: `and`, `or`
- **Relational**: `gt` (greater than), `lt` (less than)
- **Equality**: `eq` (equal)
- **Stack Manipulation**: `push <type> <x>`, `pop`, `load <id>`, `save <id>`
- **Control Flow**: `label <n>`, `jmp <n>`, `fjmp <n>`
- **Input/Output**: `print <n>`, `read <type>`
