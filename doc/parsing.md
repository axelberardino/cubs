# Parsing

The parsing step ensures every tokens are well-arranged in the order defined by the langage grammar.

This step checks for any wrong order of token. For example, `then if while` will
trigger a parsing error, because even if the tokens are all valid, they are not
in the right order.

## Let's test it

There's a lot of parsing test in the `check/parsing` folder.

### Example of a valid parsing

```sh
./cubs -P check/execution/func-recursive.mmc
```

This will result in a formatted code (parsing can easily be used a a formatting tool).
```pascal
	var a : integer;

	function factorielle(nb : integer) : integer;
	begin
		if (nb <= 1) then
		begin
			return 1;
		end
		return nb * factorielle(nb - 1);
	end


	begin
		a = factorielle(5);
	end
```

### Example of a failed parsing

In the file `check/parser/no-do-in-while.mmc`:
```pascal
begin
  while 6 < 0 // missing "do" at the end
  begin
  end
end
```

Let's launch it:
```bash
./cubs -P check/parser/no-do-in-while.mmc
```

Execution returns:
```
Line 7: Expected <do> but was <begin>
```
