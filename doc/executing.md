# Execution

The execution step is not compiling into a binary, but interpret the code.

## Let's test it

There's a lot of execution tests in the `check/execution` folder.

### Example of a recursive execution

```sh
./cubs -X check/execution/func-recursive.mmc
```

This will show where the code path goes. For a recursive function, it's pretty
handy as you'll visually "see" how it unrolls.
```pascal
var a : integer;

begin
	a = factorielle(5);
	function factorielle(nb : integer) : integer;
	begin
		if (nb <= 1) then
		return nb * factorielle(nb - 1);
		function factorielle(nb : integer) : integer;
		begin
			if (nb <= 1) then
			return nb * factorielle(nb - 1);
			function factorielle(nb : integer) : integer;
			begin
				if (nb <= 1) then
				return nb * factorielle(nb - 1);
				function factorielle(nb : integer) : integer;
				begin
					if (nb <= 1) then
					return nb * factorielle(nb - 1);
					function factorielle(nb : integer) : integer;
					begin
						if (nb <= 1) then
						begin
							return 1
						end
					end


				end


			end


		end


	end


end
```
