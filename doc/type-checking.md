# Type checking

The type checking step checks variable types are compatible.

For example, `var a : integer;` followed by `a = 10;` is correct.

But `var a : string;` followed by `a = 10;` is not, because a string is not an
integer.

## Let's test it

There's a lot of type checking test in the `check/typechecking` folder.

### Example of a valid type checking

```sh
./cubs -T check/execution/func-recursive.mmc
```

Here, you'll see which type each variables and functions have.
```pascal
var a <integer>  : integer <integer>;

function
	/*
	** integer
	*/
factorielle <integer> (nb <integer>  : integer <integer>) : integer <integer>;
begin
	if (((nb <integer> ) <integer>  <= (1 <integer> ) <integer> ) <boolean> ) <boolean>  then
	begin
		return <integer> (1 <integer> ) <integer> ;
	end
	return <integer> ((nb <integer> ) <integer>  * (factorielle <integer> (((nb <integer> ) <integer>  - (1 <integer> ) <integer> ) <integer> )) <integer> ) <integer> ;
end


begin
	a <integer>  = (factorielle <integer> ((5 <integer> ) <integer> )) <integer> ;
end
```

### Example of a failed type checking

In the file `check/typechecking/callfunc-with-multi-bad-type.mmc`:
```pascal
function foo (a, b, c : integer) : integer;
begin
	return 0;
end

begin
  foo ("kikoo", true, false);
end
```

Let's launch it:
```bash
./cubs -T check/typechecking/callfunc-with-multi-bad-type.mmc
```

Execution returns:
```
function
	/*
	** integer
	** integer
	** integer
	*/
foo <integer> (a <integer> , b <integer> , c <integer>  : integer <integer>) : integer <integer>;
begin
	return <integer> (0 <integer> ) <integer> ;
end


begin
	foo <integer> (("kikoo" <string> ) <string> , (true <boolean> ) <boolean> , (false <boolean> ) <boolean> );
end

Line 11: Type mismatch, expected <integer> located at line 5, but was <string>
Line 11: Type mismatch, expected <integer> located at line 5, but was <boolean>
Line 11: Type mismatch, expected <integer> located at line 5, but was <boolean>
```
