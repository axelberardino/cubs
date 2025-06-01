# Lexing

Lexing is the step where we're getting all the tokens. A token is the simplest
atomic piece of a grammar. For example, in a sentence, a token would be a word.

This step ensure there's no impossible token. For example, `if @ then` will
trigger a lexing error because `@` is not a valid token in the grammar.

## Let's test it

There's a lot of lexing test in the `check/lexer` folder.

### Example of a valid lexing

```sh
./cubs -L check/execution/func-recursive.mmc
```

```text
Keyword             (At line 5): 	var
Id                  (At line 5): 	a
Colon               (At line 5): 	:
Type                (At line 5): 	integer
Semi colon          (At line 5): 	;
Keyword             (At line 7): 	function
Id                  (At line 7): 	factorielle
Left bracket        (At line 7): 	(
Id                  (At line 7): 	nb
Colon               (At line 7): 	:
Type                (At line 7): 	integer
Right bracket       (At line 7): 	)
Colon               (At line 7): 	:
Type                (At line 7): 	integer
Semi colon          (At line 7): 	;
Keyword             (At line 8): 	begin
Keyword             (At line 9): 	if
Left bracket        (At line 9): 	(
Id                  (At line 9): 	nb
Comparator          (At line 9): 	<=
Value               (At line 9): 	1
Right bracket       (At line 9): 	)
Keyword             (At line 9): 	then
Keyword             (At line 10): 	begin
Keyword             (At line 11): 	return
Value               (At line 11): 	1
Semi colon          (At line 11): 	;
Keyword             (At line 12): 	end
Keyword             (At line 13): 	return
Id                  (At line 13): 	nb
Operator            (At line 13): 	*
Id                  (At line 13): 	factorielle
Left bracket        (At line 13): 	(
Id                  (At line 13): 	nb
Operator            (At line 13): 	-
Value               (At line 13): 	1
Right bracket       (At line 13): 	)
Semi colon          (At line 13): 	;
Keyword             (At line 14): 	end
Keyword             (At line 16): 	begin
Id                  (At line 17): 	a
Allocation          (At line 17): 	=
Id                  (At line 17): 	factorielle
Left bracket        (At line 17): 	(
Value               (At line 17): 	5
Right bracket       (At line 17): 	)
Semi colon          (At line 17): 	;
Keyword             (At line 18): 	end
```

### Example of a failed lexing

In the file `check/lexer/invalid-id2.mmc`:
```pascal
var _a : integer:
var read : integer;

function read(a : integer) : integer;
begin
end

begin
  a___ = 0;
  _ = 45;
end
```

Let's launch it:
```sh
./cubs -L check/lexer/invalid-id2.mmc
```

Execution returns:
```
Line 5: "_a" is invalid : an ID must have a valid name, ie [a-zA-Z][a-zA-Z0-9_]* and no builtin name
Line 14: "_" is invalid : an ID must have a valid name, ie [a-zA-Z][a-zA-Z0-9_]* and no builtin name
```
