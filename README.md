# Cubs

Cubs is a very basic compiler project. It can check errors and executes a pseudo
pascal code source.

The goal of this project is to show every classical steps of a compilation.
Everys aspects of the compilation is handled and can be seen visually.
More about the language definition here: [Language definition](doc/language.md)

Each steps of the compilation is described separately here:
  * [Lexing](doc/lexing.md)
  * [Parsing](doc/parsing.md)
  * [AST building](doc/ast.md)
  * [Binding](doc/binding.md)
  * [Type checking](doc/type-checking.md)
  * [Transpiling into assembly/making the binary](doc/compiling.md)

As a bonus, it also handles:
  * [Execution](doc/executing.md)
  * [Debugging](doc/debugging.md)
  * [Converting into C++](doc/converting.md)
  * [Generating random valid code](doc/random-code-generation.md)

## Quickstart

Compile the project using:
```sh
./configure && make
```

Choose one of the file among the many provided examples, and use the `-V` option
to get a tour of what this program is capable of.
Example:
```sh
./cubs -V check/execution/func-recursive.mmc
```


## Simple demo and capabilities

### Langage example

This is a simple example of the langage:
```pascal
#!/bin/cubs

var a: integer;

function double(i: integer) : integer;
begin
  return i*i;
end

begin
  a = 5;
  a = double(a);
  print(a);
  print("\n");
end
```

### Lexing

```text
Keyword             (At line 3): 	var
Id                  (At line 3): 	a
Colon               (At line 3): 	:
Type                (At line 3): 	integer
Semi colon          (At line 3): 	;
Keyword             (At line 5): 	function
Id                  (At line 5): 	double
Left bracket        (At line 5): 	(
Id                  (At line 5): 	i
Colon               (At line 5): 	:
Type                (At line 5): 	integer
Right bracket       (At line 5): 	)
Colon               (At line 5): 	:
Type                (At line 5): 	integer
Semi colon          (At line 5): 	;
Keyword             (At line 6): 	begin
Keyword             (At line 7): 	return
Id                  (At line 7): 	i
Operator            (At line 7): 	*
Id                  (At line 7): 	i
Semi colon          (At line 7): 	;
Keyword             (At line 8): 	end
Keyword             (At line 10): 	begin
Id                  (At line 11): 	a
Allocation          (At line 11): 	=
Value               (At line 11): 	5
Semi colon          (At line 11): 	;
Id                  (At line 12): 	a
Allocation          (At line 12): 	=
Id                  (At line 12): 	double
Left bracket        (At line 12): 	(
Id                  (At line 12): 	a
Right bracket       (At line 12): 	)
Semi colon          (At line 12): 	;
Id                  (At line 13): 	print
Left bracket        (At line 13): 	(
Id                  (At line 13): 	a
Right bracket       (At line 13): 	)
Semi colon          (At line 13): 	;
Id                  (At line 14): 	print
Left bracket        (At line 14): 	(
String expression   (At line 14): 	\n
Right bracket       (At line 14): 	)
Semi colon          (At line 14): 	;
Keyword             (At line 15): 	end
```

### Binding

```pascal
Program __main__ /* 0x6000001a8360 */ () : integer;
begin
	var a /* 0x600001aa8600 */ : integer;

	function
		/*
		** 0x600001aa86c0
		*/
	double /* 0x600001aa8640 */(i /* 0x600001aa86c0 */ : integer) : integer;
	begin
		return /* 0x600001aa8640 */ i /* 0x600001aa86c0 */ * i /* 0x600001aa86c0 */;
	end


	begin
		a /* 0x600001aa8600 */ = 5;
		a /* 0x600001aa8600 */ = double /* 0x600001aa8640 */(a /* 0x600001aa8600 */ /* 0x600001aa86c0 */);
		print(a /* 0x600001aa8600 */);
		print("\n");
	end

end
```

### Type checking

```pascal
	var a <integer>  : integer <integer>;

	function
		/*
		** integer
		*/
	double <integer> (i <integer>  : integer <integer>) : integer <integer>;
	begin
		return <integer> ((i <integer> ) <integer>  * (i <integer> ) <integer> ) <integer> ;
	end


	begin
		a <integer>  = (5 <integer> ) <integer> ;
		a <integer>  = (double <integer> ((a <integer> ) <integer> )) <integer> ;
		print((a <integer> ) <integer> );
		print(("\n" <string> ) <string> );
	end
```

### Assembly

```nasm
double:
	push	ebp		; Begin
	mov	ebp, esp
	mov	edx, [ebp + 8]

	push	edx		; Save edx into the stack to help computing expression
	mov	edx, [ebp + 8]
	mov	ecx, edx	; Move current edx into ecx
	pop	edx		; Restore edx from the stack to help computing expression
	mov	eax, edx	; The eax register must contains the left factor
	xor	edx, edx	; Put edx to 0
	mul	ecx		; The ecx register must contains the right factor
	mov	edx, eax	; Result of the multiplication is written into eax
	mov	eax, edx	; eax is used to put returned value
	mov	esp, ebp
	pop	ebp
	ret			; Return
	mov	esp, ebp
	pop	ebp		; End
	ret		; exit function

_start:
	mov	dword [a], 0	; Automatic initialization
	mov	edx, 5
	mov	[a], edx	; Just affect an expression
	push	ebp		; Create a scope to save arguments
	mov	ebp, esp
	mov	edx, [a]
	push	edx		; Save argument
	call	double	; Just call the function using __cdecl convention
	mov	edx, eax	; Copy result of the function into edx
	mov	esp, ebp
	pop	ebp		; Close the arguments scope
	mov	[a], edx	; Just affect an expression
	mov	edx, [a]
	mov eax, edx	; Prepare to being print
	call	__print_int	; print value contained in eax
	mov	edx, _string1
	mov eax, edx	; Prepare to being print
	call	__print_string	; print value contained in eax
	mov	eax, 1		; The system call for exit (sys_exit)
	mov	ebx, 0		; Exit with return code of 0 (no error)
	int	80h
  ```