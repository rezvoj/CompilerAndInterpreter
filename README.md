# FEI VSB-TUO: PLC
![Python](https://img.shields.io/badge/python-3.10-blue) ![ANTLR4](https://img.shields.io/badge/ANTLR-4-orange)

A compiler and stack-based interpreter for a small statically-typed imperative language. The compiler parses source code (ANTLR4-generated grammar), performs type checking, and emits stack-machine instructions; the interpreter executes them.

## Running it

Requires Python 3.10+.

```bash
pip install -r requirements.txt
```

Compile a source file to bytecode:
```bash
python compiler.py <source_file> <compiled_file>
```

Run the bytecode:
```bash
python interpreter.py <compiled_file>
```

Example programs live in [`samples/`](./samples/).


## The language

Statically typed, four primitive types: `int`, `float`, `bool`, `string`. Variables must be declared before use and are zero-initialized (`0`, `0.0`, `false`, `""`).

### Statements

- **Declaration** — `type var1, var2, ...;`
- **Assignment / expression** — evaluated and discarded (assignment is an expression)
- **I/O** — `read var1, ...;` and `write expr1, ...;`
- **Block** — `{ stmt1 stmt2 ... }`
- **Conditional** — `if (cond) stmt [else stmt]`
- **Loops** — `while (cond) stmt` and `for (init; cond; step) stmt`

Comments are `// ...` to end of line. Whitespace is insignificant.

### Operators

| Category | Operators |
| --- | --- |
| Arithmetic | `+` `-` `*` `/` `%` |
| String | `.` (concatenation) |
| Relational | `<` `>` |
| Equality | `==` `!=` |
| Logical | `&&` `\|\|` `!` |
| Unary | `-` `!` |
| Assignment | `=` |


## Sample programs

| File | Demonstrates |
| --- | --- |
| `first.lang` | Variables, expressions, I/O, multiple assignment |
| `second.lang` | Relational and logical operators |
| `third.lang` | `if`, `while`, `for` |
| `expressions.lang` | Complex expressions and type conversion |
| `errors.lang` | Syntax and type errors (rejected by the compiler) |
| `centroids.lang` | Centroid of a set of points |
| `primes.lang` | Prime number generation |


## Bytecode

Stack-based instruction set produced by the compiler:

| Category | Instructions |
| --- | --- |
| Arithmetic | `add` `sub` `mul` `div` `mod` |
| Unary | `uminus` `not` `itof` (int → float coercion) |
| String | `concat` |
| Logical | `and` `or` |
| Relational | `gt` `lt` |
| Equality | `eq` |
| Stack | `push <type> <value>` `pop` `load <id>` `save <id>` |
| Control flow | `label <n>` `jmp <n>` `fjmp <n>` (jump if false) |
| I/O | `print <n>` `read <type>` |
