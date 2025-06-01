# Language definition

This language handles:
  * 3 types (integer, boolean, string).
  * 2 controle structure (if, while)
  * 3 builtins (read, print, exit)
  * No pointers
  * No arrays
  * Functions and recursive functions
  * 5 compute operators: +, -, /, *, %
  * 6 comparison operators ==, !=, >, >=, <, <=
  * No boolean comperator (no `and`, no `or`)
  * Mandatory parenthesis around expressions.\
    Example: `1 + 2 + 3` will not work, you need to write: `1 + (2 + 3)`
  * Local or global variables

## Language example

This is a simple example of the langage:
```pascal
var a, b, c : integer;
var f : string;
var truc : string;

function nothing () : integer;
begin
end

function my_func (a: integer; d,e,f:string) : integer;
var local_a, local_b : integer;
var local_f : string;
begin
  return 34;
end

function test_this_function (a: integer; d,e,f:string ) : integer;
var local_a, local_b : integer;
var local_f : string;
begin
  a = 34;
  b = my_func(0, "hello", "str3", "str4");
  nothing();
  begin
    if a == b then
    begin
      printf ("Hellooo");
      return "kikoo";
    end
  end
  local_b = (55 * 56) + 37;
  local_f = "cou" + "cou";
end


begin
  foo = " this \\\\\\anoth\\\er very \" \\small\\ test\tess\n";
  print (test_this_function(42, "42", "quarante-deux", "Forty Two"));
  // This is a comment test
  return 0;
end
```

## Formal Grammar

This is the grammar definition for this language

```pascal
program ::= [declarations] [funcs] [compound_instruction]

declarations := declaration
              | declaration declarations

declaration ::= "var" declaration_body ";"

declaration_body ::= ids ":" type

ids ::= id
      | id "," ids

funcs ::= func
        | func funcs

func ::= header_func compound_instruction
       | header_func declarations compound_instruction

header_func ::= "function" idfunc "(" [arguments] ")" ":" type ";"

arguments ::= argument
	    | argument ";" arguments

argument ::= declaration_body
           | declaration_body ";" argument

compound_instruction ::= "begin" "end"
		       | "begin" instructions "end"

instructions ::= instruction
               | instruction instructions

instruction ::= affect ";"
              | call_func ";"
              | compound_instruction
              | if
              | while
              | return ";"
              | exit ";"
              | builtin_print ";"
              | builtin_read ";"

affect ::= id "=" expression

return ::= "return" expression
exit ::= "return" expression

builtin_print ::= "print" "(" expression ")" /* builtin */

builtin_read ::= "read" "(" id ")" /* builtin */

if ::= "if" expression "then" compound_instruction
     | "if" expression "then" compound_instruction "else" compound_instruction

while ::= "while" cond "do" compound_instruction

call_func ::= idfunc "(" ")"
            | idfunc "(" expressions ")"

expressions ::= expression
              | expression "," expressions

expression ::= operation

operation ::= factor symb factor
            | factor /* operation with no right factor */
	    | "-" factor /* left factor = 0 */

factor ::= id
         | call_func
         | number
	 | stringexpr
	 | boolean
         | "(" expression ")"

Sup ::= expression ">" expression
Inf ::= expression "<" expression
InfEqual ::= expression "<=" expression
SupEqual ::= expression ">=" expression
Equal ::= expression "==" expression
Diff ::= expression "!=" expression


id ::= [a-zA-Z]([a-zA-Z0-9_]*[a-zA-Z0-9])?
type ::= "integer" | "string" | "boolean"
symb ::= ">" | "<" | ">=" | "<=" | "!=" | "==" | "+" | "-" | "*" | "/" | "%"
number ::= [0-9]+
stringexpr ::= ".*"
boolean ::= true | false
```
