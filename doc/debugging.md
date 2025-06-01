# Debugging

When executing a binary, it's possible to get a debug view and see the values
of all variables at each step of the execution.

## Simple example

Let's take this simple code from `check/execution/simple-op.mmc`
```pascal
var a : integer;
begin
  a = 5 + 11;
end
```

```sh
./cubs -D check/execution/simple-op.mmc
```

The result will be:
```text
	var a : integer;

____________________________
a=(integer) 0


	begin

____________________________
a=(integer) 0

		a = 5 + 11

____________________________
%nodeexpression%=(integer) 16
%nodefactor%=(integer) 11
%nodeid%=(integer) 0
%nodenumber%=(integer) 11
%nodeoperation%=(integer) 16
a=(integer) 16

	end

____________________________
%nodeexpression%=(integer) 16
%nodefactor%=(integer) 11
%nodeid%=(integer) 0
%nodenumber%=(integer) 11
%nodeoperation%=(integer) 16
a=(integer) 16
```

## Example of a recursive execution debugging

```sh
./cubs -D check/execution/func-recursive.mmc
```

```text
	var a : integer;

____________________________
a=(integer) 0


	begin

____________________________
a=(integer) 0

		a = factorielle(5)
____________________________
%arg0%=(integer) 5
%nodeexpression%=(integer) 5
%nodefactor%=(integer) 5
%nodeid%=(integer) 0
%nodenumber%=(integer) 5
%nodeoperation%=(integer) 5
a=(integer) 0

;
		function factorielle(nb : integer) : integer;
		begin

____________________________
%return%=(integer) 0
nb=(integer) 5
----------------------------
>>%arg0%=(integer) 5
>>%nodeexpression%=(integer) 5
>>%nodefactor%=(integer) 5
>>%nodeid%=(integer) 0
>>%nodenumber%=(integer) 5
>>%nodeoperation%=(integer) 5
>>a=(integer) 0

			if (nb <= 1) then

____________________________
%nodeexpression%=(boolean) false
%nodefactor%=(boolean) false
%nodeid%=(integer) 5
%nodenumber%=(integer) 1
%nodeoperation%=(boolean) false
%return%=(integer) 0
nb=(integer) 5
----------------------------
>>%arg0%=(integer) 5
>>%nodeexpression%=(integer) 5
>>%nodefactor%=(integer) 5
>>%nodeid%=(integer) 0
>>%nodenumber%=(integer) 5
>>%nodeoperation%=(integer) 5
>>a=(integer) 0


____________________________
%nodeexpression%=(boolean) false
%nodefactor%=(boolean) false
%nodeid%=(integer) 5
%nodenumber%=(integer) 1
%nodeoperation%=(boolean) false
%return%=(integer) 0
nb=(integer) 5
----------------------------
>>%arg0%=(integer) 5
>>%nodeexpression%=(integer) 5
>>%nodefactor%=(integer) 5
>>%nodeid%=(integer) 0
>>%nodenumber%=(integer) 5
>>%nodeoperation%=(integer) 5
>>a=(integer) 0

			return nb * factorielle(nb - 1)
____________________________
%arg0%=(integer) 4
%nodeexpression%=(integer) 4
%nodefactor%=(integer) 1
%nodeid%=(integer) 5
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 4
%return%=(integer) 0
nb=(integer) 5
----------------------------
>>%arg0%=(integer) 5
>>%nodeexpression%=(integer) 5
>>%nodefactor%=(integer) 5
>>%nodeid%=(integer) 0
>>%nodenumber%=(integer) 5
>>%nodeoperation%=(integer) 5
>>a=(integer) 0

;
			function factorielle(nb : integer) : integer;
			begin

____________________________
%return%=(integer) 0
nb=(integer) 4
----------------------------
>>%arg0%=(integer) 4
>>%nodeexpression%=(integer) 4
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 5
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 4
>>%return%=(integer) 0
>>nb=(integer) 5
----------------------------
>>>>%arg0%=(integer) 5
>>>>%nodeexpression%=(integer) 5
>>>>%nodefactor%=(integer) 5
>>>>%nodeid%=(integer) 0
>>>>%nodenumber%=(integer) 5
>>>>%nodeoperation%=(integer) 5
>>>>a=(integer) 0

				if (nb <= 1) then

____________________________
%nodeexpression%=(boolean) false
%nodefactor%=(boolean) false
%nodeid%=(integer) 4
%nodenumber%=(integer) 1
%nodeoperation%=(boolean) false
%return%=(integer) 0
nb=(integer) 4
----------------------------
>>%arg0%=(integer) 4
>>%nodeexpression%=(integer) 4
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 5
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 4
>>%return%=(integer) 0
>>nb=(integer) 5
----------------------------
>>>>%arg0%=(integer) 5
>>>>%nodeexpression%=(integer) 5
>>>>%nodefactor%=(integer) 5
>>>>%nodeid%=(integer) 0
>>>>%nodenumber%=(integer) 5
>>>>%nodeoperation%=(integer) 5
>>>>a=(integer) 0


____________________________
%nodeexpression%=(boolean) false
%nodefactor%=(boolean) false
%nodeid%=(integer) 4
%nodenumber%=(integer) 1
%nodeoperation%=(boolean) false
%return%=(integer) 0
nb=(integer) 4
----------------------------
>>%arg0%=(integer) 4
>>%nodeexpression%=(integer) 4
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 5
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 4
>>%return%=(integer) 0
>>nb=(integer) 5
----------------------------
>>>>%arg0%=(integer) 5
>>>>%nodeexpression%=(integer) 5
>>>>%nodefactor%=(integer) 5
>>>>%nodeid%=(integer) 0
>>>>%nodenumber%=(integer) 5
>>>>%nodeoperation%=(integer) 5
>>>>a=(integer) 0

				return nb * factorielle(nb - 1)
____________________________
%arg0%=(integer) 3
%nodeexpression%=(integer) 3
%nodefactor%=(integer) 1
%nodeid%=(integer) 4
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 3
%return%=(integer) 0
nb=(integer) 4
----------------------------
>>%arg0%=(integer) 4
>>%nodeexpression%=(integer) 4
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 5
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 4
>>%return%=(integer) 0
>>nb=(integer) 5
----------------------------
>>>>%arg0%=(integer) 5
>>>>%nodeexpression%=(integer) 5
>>>>%nodefactor%=(integer) 5
>>>>%nodeid%=(integer) 0
>>>>%nodenumber%=(integer) 5
>>>>%nodeoperation%=(integer) 5
>>>>a=(integer) 0

;
				function factorielle(nb : integer) : integer;
				begin

____________________________
%return%=(integer) 0
nb=(integer) 3
----------------------------
>>%arg0%=(integer) 3
>>%nodeexpression%=(integer) 3
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 4
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 3
>>%return%=(integer) 0
>>nb=(integer) 4
----------------------------
>>>>%arg0%=(integer) 4
>>>>%nodeexpression%=(integer) 4
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 5
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 4
>>>>%return%=(integer) 0
>>>>nb=(integer) 5
----------------------------
>>>>>>%arg0%=(integer) 5
>>>>>>%nodeexpression%=(integer) 5
>>>>>>%nodefactor%=(integer) 5
>>>>>>%nodeid%=(integer) 0
>>>>>>%nodenumber%=(integer) 5
>>>>>>%nodeoperation%=(integer) 5
>>>>>>a=(integer) 0

					if (nb <= 1) then

____________________________
%nodeexpression%=(boolean) false
%nodefactor%=(boolean) false
%nodeid%=(integer) 3
%nodenumber%=(integer) 1
%nodeoperation%=(boolean) false
%return%=(integer) 0
nb=(integer) 3
----------------------------
>>%arg0%=(integer) 3
>>%nodeexpression%=(integer) 3
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 4
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 3
>>%return%=(integer) 0
>>nb=(integer) 4
----------------------------
>>>>%arg0%=(integer) 4
>>>>%nodeexpression%=(integer) 4
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 5
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 4
>>>>%return%=(integer) 0
>>>>nb=(integer) 5
----------------------------
>>>>>>%arg0%=(integer) 5
>>>>>>%nodeexpression%=(integer) 5
>>>>>>%nodefactor%=(integer) 5
>>>>>>%nodeid%=(integer) 0
>>>>>>%nodenumber%=(integer) 5
>>>>>>%nodeoperation%=(integer) 5
>>>>>>a=(integer) 0


____________________________
%nodeexpression%=(boolean) false
%nodefactor%=(boolean) false
%nodeid%=(integer) 3
%nodenumber%=(integer) 1
%nodeoperation%=(boolean) false
%return%=(integer) 0
nb=(integer) 3
----------------------------
>>%arg0%=(integer) 3
>>%nodeexpression%=(integer) 3
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 4
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 3
>>%return%=(integer) 0
>>nb=(integer) 4
----------------------------
>>>>%arg0%=(integer) 4
>>>>%nodeexpression%=(integer) 4
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 5
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 4
>>>>%return%=(integer) 0
>>>>nb=(integer) 5
----------------------------
>>>>>>%arg0%=(integer) 5
>>>>>>%nodeexpression%=(integer) 5
>>>>>>%nodefactor%=(integer) 5
>>>>>>%nodeid%=(integer) 0
>>>>>>%nodenumber%=(integer) 5
>>>>>>%nodeoperation%=(integer) 5
>>>>>>a=(integer) 0

					return nb * factorielle(nb - 1)
____________________________
%arg0%=(integer) 2
%nodeexpression%=(integer) 2
%nodefactor%=(integer) 1
%nodeid%=(integer) 3
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 2
%return%=(integer) 0
nb=(integer) 3
----------------------------
>>%arg0%=(integer) 3
>>%nodeexpression%=(integer) 3
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 4
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 3
>>%return%=(integer) 0
>>nb=(integer) 4
----------------------------
>>>>%arg0%=(integer) 4
>>>>%nodeexpression%=(integer) 4
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 5
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 4
>>>>%return%=(integer) 0
>>>>nb=(integer) 5
----------------------------
>>>>>>%arg0%=(integer) 5
>>>>>>%nodeexpression%=(integer) 5
>>>>>>%nodefactor%=(integer) 5
>>>>>>%nodeid%=(integer) 0
>>>>>>%nodenumber%=(integer) 5
>>>>>>%nodeoperation%=(integer) 5
>>>>>>a=(integer) 0

;
					function factorielle(nb : integer) : integer;
					begin

____________________________
%return%=(integer) 0
nb=(integer) 2
----------------------------
>>%arg0%=(integer) 2
>>%nodeexpression%=(integer) 2
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 3
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 2
>>%return%=(integer) 0
>>nb=(integer) 3
----------------------------
>>>>%arg0%=(integer) 3
>>>>%nodeexpression%=(integer) 3
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 4
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 3
>>>>%return%=(integer) 0
>>>>nb=(integer) 4
----------------------------
>>>>>>%arg0%=(integer) 4
>>>>>>%nodeexpression%=(integer) 4
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 5
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 4
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>%arg0%=(integer) 5
>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>a=(integer) 0

						if (nb <= 1) then

____________________________
%nodeexpression%=(boolean) false
%nodefactor%=(boolean) false
%nodeid%=(integer) 2
%nodenumber%=(integer) 1
%nodeoperation%=(boolean) false
%return%=(integer) 0
nb=(integer) 2
----------------------------
>>%arg0%=(integer) 2
>>%nodeexpression%=(integer) 2
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 3
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 2
>>%return%=(integer) 0
>>nb=(integer) 3
----------------------------
>>>>%arg0%=(integer) 3
>>>>%nodeexpression%=(integer) 3
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 4
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 3
>>>>%return%=(integer) 0
>>>>nb=(integer) 4
----------------------------
>>>>>>%arg0%=(integer) 4
>>>>>>%nodeexpression%=(integer) 4
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 5
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 4
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>%arg0%=(integer) 5
>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>a=(integer) 0


____________________________
%nodeexpression%=(boolean) false
%nodefactor%=(boolean) false
%nodeid%=(integer) 2
%nodenumber%=(integer) 1
%nodeoperation%=(boolean) false
%return%=(integer) 0
nb=(integer) 2
----------------------------
>>%arg0%=(integer) 2
>>%nodeexpression%=(integer) 2
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 3
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 2
>>%return%=(integer) 0
>>nb=(integer) 3
----------------------------
>>>>%arg0%=(integer) 3
>>>>%nodeexpression%=(integer) 3
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 4
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 3
>>>>%return%=(integer) 0
>>>>nb=(integer) 4
----------------------------
>>>>>>%arg0%=(integer) 4
>>>>>>%nodeexpression%=(integer) 4
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 5
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 4
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>%arg0%=(integer) 5
>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>a=(integer) 0

						return nb * factorielle(nb - 1)
____________________________
%arg0%=(integer) 1
%nodeexpression%=(integer) 1
%nodefactor%=(integer) 1
%nodeid%=(integer) 2
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 1
%return%=(integer) 0
nb=(integer) 2
----------------------------
>>%arg0%=(integer) 2
>>%nodeexpression%=(integer) 2
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 3
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 2
>>%return%=(integer) 0
>>nb=(integer) 3
----------------------------
>>>>%arg0%=(integer) 3
>>>>%nodeexpression%=(integer) 3
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 4
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 3
>>>>%return%=(integer) 0
>>>>nb=(integer) 4
----------------------------
>>>>>>%arg0%=(integer) 4
>>>>>>%nodeexpression%=(integer) 4
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 5
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 4
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>%arg0%=(integer) 5
>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>a=(integer) 0

;
						function factorielle(nb : integer) : integer;
						begin

____________________________
%return%=(integer) 0
nb=(integer) 1
----------------------------
>>%arg0%=(integer) 1
>>%nodeexpression%=(integer) 1
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 2
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 1
>>%return%=(integer) 0
>>nb=(integer) 2
----------------------------
>>>>%arg0%=(integer) 2
>>>>%nodeexpression%=(integer) 2
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 3
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 2
>>>>%return%=(integer) 0
>>>>nb=(integer) 3
----------------------------
>>>>>>%arg0%=(integer) 3
>>>>>>%nodeexpression%=(integer) 3
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 4
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 3
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 4
----------------------------
>>>>>>>>%arg0%=(integer) 4
>>>>>>>>%nodeexpression%=(integer) 4
>>>>>>>>%nodefactor%=(integer) 1
>>>>>>>>%nodeid%=(integer) 5
>>>>>>>>%nodenumber%=(integer) 1
>>>>>>>>%nodeoperation%=(integer) 4
>>>>>>>>%return%=(integer) 0
>>>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>>>%arg0%=(integer) 5
>>>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>>>a=(integer) 0

							if (nb <= 1) then

____________________________
%nodeexpression%=(boolean) true
%nodefactor%=(boolean) true
%nodeid%=(integer) 1
%nodenumber%=(integer) 1
%nodeoperation%=(boolean) true
%return%=(integer) 0
nb=(integer) 1
----------------------------
>>%arg0%=(integer) 1
>>%nodeexpression%=(integer) 1
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 2
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 1
>>%return%=(integer) 0
>>nb=(integer) 2
----------------------------
>>>>%arg0%=(integer) 2
>>>>%nodeexpression%=(integer) 2
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 3
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 2
>>>>%return%=(integer) 0
>>>>nb=(integer) 3
----------------------------
>>>>>>%arg0%=(integer) 3
>>>>>>%nodeexpression%=(integer) 3
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 4
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 3
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 4
----------------------------
>>>>>>>>%arg0%=(integer) 4
>>>>>>>>%nodeexpression%=(integer) 4
>>>>>>>>%nodefactor%=(integer) 1
>>>>>>>>%nodeid%=(integer) 5
>>>>>>>>%nodenumber%=(integer) 1
>>>>>>>>%nodeoperation%=(integer) 4
>>>>>>>>%return%=(integer) 0
>>>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>>>%arg0%=(integer) 5
>>>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>>>a=(integer) 0

							begin

____________________________
%nodeexpression%=(boolean) true
%nodefactor%=(boolean) true
%nodeid%=(integer) 1
%nodenumber%=(integer) 1
%nodeoperation%=(boolean) true
%return%=(integer) 0
nb=(integer) 1
----------------------------
>>%arg0%=(integer) 1
>>%nodeexpression%=(integer) 1
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 2
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 1
>>%return%=(integer) 0
>>nb=(integer) 2
----------------------------
>>>>%arg0%=(integer) 2
>>>>%nodeexpression%=(integer) 2
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 3
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 2
>>>>%return%=(integer) 0
>>>>nb=(integer) 3
----------------------------
>>>>>>%arg0%=(integer) 3
>>>>>>%nodeexpression%=(integer) 3
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 4
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 3
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 4
----------------------------
>>>>>>>>%arg0%=(integer) 4
>>>>>>>>%nodeexpression%=(integer) 4
>>>>>>>>%nodefactor%=(integer) 1
>>>>>>>>%nodeid%=(integer) 5
>>>>>>>>%nodenumber%=(integer) 1
>>>>>>>>%nodeoperation%=(integer) 4
>>>>>>>>%return%=(integer) 0
>>>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>>>%arg0%=(integer) 5
>>>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>>>a=(integer) 0

								return 1
____________________________
%nodeexpression%=(integer) 1
%nodefactor%=(integer) 1
%nodeid%=(integer) 1
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 1
%return%=(integer) 0
nb=(integer) 1
----------------------------
>>%arg0%=(integer) 1
>>%nodeexpression%=(integer) 1
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 2
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 1
>>%return%=(integer) 0
>>nb=(integer) 2
----------------------------
>>>>%arg0%=(integer) 2
>>>>%nodeexpression%=(integer) 2
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 3
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 2
>>>>%return%=(integer) 0
>>>>nb=(integer) 3
----------------------------
>>>>>>%arg0%=(integer) 3
>>>>>>%nodeexpression%=(integer) 3
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 4
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 3
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 4
----------------------------
>>>>>>>>%arg0%=(integer) 4
>>>>>>>>%nodeexpression%=(integer) 4
>>>>>>>>%nodefactor%=(integer) 1
>>>>>>>>%nodeid%=(integer) 5
>>>>>>>>%nodenumber%=(integer) 1
>>>>>>>>%nodeoperation%=(integer) 4
>>>>>>>>%return%=(integer) 0
>>>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>>>%arg0%=(integer) 5
>>>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>>>a=(integer) 0



____________________________
%nodeexpression%=(integer) 1
%nodefactor%=(integer) 1
%nodeid%=(integer) 1
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 1
%return%=(integer) 1
nb=(integer) 1
----------------------------
>>%arg0%=(integer) 1
>>%nodeexpression%=(integer) 1
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 2
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 1
>>%return%=(integer) 0
>>nb=(integer) 2
----------------------------
>>>>%arg0%=(integer) 2
>>>>%nodeexpression%=(integer) 2
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 3
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 2
>>>>%return%=(integer) 0
>>>>nb=(integer) 3
----------------------------
>>>>>>%arg0%=(integer) 3
>>>>>>%nodeexpression%=(integer) 3
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 4
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 3
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 4
----------------------------
>>>>>>>>%arg0%=(integer) 4
>>>>>>>>%nodeexpression%=(integer) 4
>>>>>>>>%nodefactor%=(integer) 1
>>>>>>>>%nodeid%=(integer) 5
>>>>>>>>%nodenumber%=(integer) 1
>>>>>>>>%nodeoperation%=(integer) 4
>>>>>>>>%return%=(integer) 0
>>>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>>>%arg0%=(integer) 5
>>>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>>>a=(integer) 0

							end

____________________________
%nodeexpression%=(integer) 1
%nodefactor%=(integer) 1
%nodeid%=(integer) 1
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 1
%return%=(integer) 1
nb=(integer) 1
----------------------------
>>%arg0%=(integer) 1
>>%nodeexpression%=(integer) 1
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 2
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 1
>>%return%=(integer) 0
>>nb=(integer) 2
----------------------------
>>>>%arg0%=(integer) 2
>>>>%nodeexpression%=(integer) 2
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 3
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 2
>>>>%return%=(integer) 0
>>>>nb=(integer) 3
----------------------------
>>>>>>%arg0%=(integer) 3
>>>>>>%nodeexpression%=(integer) 3
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 4
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 3
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 4
----------------------------
>>>>>>>>%arg0%=(integer) 4
>>>>>>>>%nodeexpression%=(integer) 4
>>>>>>>>%nodefactor%=(integer) 1
>>>>>>>>%nodeid%=(integer) 5
>>>>>>>>%nodenumber%=(integer) 1
>>>>>>>>%nodeoperation%=(integer) 4
>>>>>>>>%return%=(integer) 0
>>>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>>>%arg0%=(integer) 5
>>>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>>>a=(integer) 0


____________________________
%nodeexpression%=(integer) 1
%nodefactor%=(integer) 1
%nodeid%=(integer) 1
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 1
%return%=(integer) 1
nb=(integer) 1
----------------------------
>>%arg0%=(integer) 1
>>%nodeexpression%=(integer) 1
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 2
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 1
>>%return%=(integer) 0
>>nb=(integer) 2
----------------------------
>>>>%arg0%=(integer) 2
>>>>%nodeexpression%=(integer) 2
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 3
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 2
>>>>%return%=(integer) 0
>>>>nb=(integer) 3
----------------------------
>>>>>>%arg0%=(integer) 3
>>>>>>%nodeexpression%=(integer) 3
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 4
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 3
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 4
----------------------------
>>>>>>>>%arg0%=(integer) 4
>>>>>>>>%nodeexpression%=(integer) 4
>>>>>>>>%nodefactor%=(integer) 1
>>>>>>>>%nodeid%=(integer) 5
>>>>>>>>%nodenumber%=(integer) 1
>>>>>>>>%nodeoperation%=(integer) 4
>>>>>>>>%return%=(integer) 0
>>>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>>>%arg0%=(integer) 5
>>>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>>>a=(integer) 0

						end

____________________________
%nodeexpression%=(integer) 1
%nodefactor%=(integer) 1
%nodeid%=(integer) 1
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 1
%return%=(integer) 1
nb=(integer) 1
----------------------------
>>%arg0%=(integer) 1
>>%nodeexpression%=(integer) 1
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 2
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 1
>>%return%=(integer) 0
>>nb=(integer) 2
----------------------------
>>>>%arg0%=(integer) 2
>>>>%nodeexpression%=(integer) 2
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 3
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 2
>>>>%return%=(integer) 0
>>>>nb=(integer) 3
----------------------------
>>>>>>%arg0%=(integer) 3
>>>>>>%nodeexpression%=(integer) 3
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 4
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 3
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 4
----------------------------
>>>>>>>>%arg0%=(integer) 4
>>>>>>>>%nodeexpression%=(integer) 4
>>>>>>>>%nodefactor%=(integer) 1
>>>>>>>>%nodeid%=(integer) 5
>>>>>>>>%nodenumber%=(integer) 1
>>>>>>>>%nodeoperation%=(integer) 4
>>>>>>>>%return%=(integer) 0
>>>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>>>%arg0%=(integer) 5
>>>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>>>a=(integer) 0



____________________________
%arg0%=(integer) 1
%nodecallfunc%=(integer) 1
%nodeexpression%=(integer) 2
%nodefactor%=(integer) 1
%nodeid%=(integer) 2
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 2
%return%=(integer) 0
nb=(integer) 2
----------------------------
>>%arg0%=(integer) 2
>>%nodeexpression%=(integer) 2
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 3
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 2
>>%return%=(integer) 0
>>nb=(integer) 3
----------------------------
>>>>%arg0%=(integer) 3
>>>>%nodeexpression%=(integer) 3
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 4
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 3
>>>>%return%=(integer) 0
>>>>nb=(integer) 4
----------------------------
>>>>>>%arg0%=(integer) 4
>>>>>>%nodeexpression%=(integer) 4
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 5
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 4
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>%arg0%=(integer) 5
>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>a=(integer) 0



____________________________
%arg0%=(integer) 1
%nodecallfunc%=(integer) 1
%nodeexpression%=(integer) 2
%nodefactor%=(integer) 1
%nodeid%=(integer) 2
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 2
%return%=(integer) 2
nb=(integer) 2
----------------------------
>>%arg0%=(integer) 2
>>%nodeexpression%=(integer) 2
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 3
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 2
>>%return%=(integer) 0
>>nb=(integer) 3
----------------------------
>>>>%arg0%=(integer) 3
>>>>%nodeexpression%=(integer) 3
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 4
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 3
>>>>%return%=(integer) 0
>>>>nb=(integer) 4
----------------------------
>>>>>>%arg0%=(integer) 4
>>>>>>%nodeexpression%=(integer) 4
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 5
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 4
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>%arg0%=(integer) 5
>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>a=(integer) 0

					end

____________________________
%arg0%=(integer) 1
%nodecallfunc%=(integer) 1
%nodeexpression%=(integer) 2
%nodefactor%=(integer) 1
%nodeid%=(integer) 2
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 2
%return%=(integer) 2
nb=(integer) 2
----------------------------
>>%arg0%=(integer) 2
>>%nodeexpression%=(integer) 2
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 3
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 2
>>%return%=(integer) 0
>>nb=(integer) 3
----------------------------
>>>>%arg0%=(integer) 3
>>>>%nodeexpression%=(integer) 3
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 4
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 3
>>>>%return%=(integer) 0
>>>>nb=(integer) 4
----------------------------
>>>>>>%arg0%=(integer) 4
>>>>>>%nodeexpression%=(integer) 4
>>>>>>%nodefactor%=(integer) 1
>>>>>>%nodeid%=(integer) 5
>>>>>>%nodenumber%=(integer) 1
>>>>>>%nodeoperation%=(integer) 4
>>>>>>%return%=(integer) 0
>>>>>>nb=(integer) 5
----------------------------
>>>>>>>>%arg0%=(integer) 5
>>>>>>>>%nodeexpression%=(integer) 5
>>>>>>>>%nodefactor%=(integer) 5
>>>>>>>>%nodeid%=(integer) 0
>>>>>>>>%nodenumber%=(integer) 5
>>>>>>>>%nodeoperation%=(integer) 5
>>>>>>>>a=(integer) 0



____________________________
%arg0%=(integer) 2
%nodecallfunc%=(integer) 2
%nodeexpression%=(integer) 6
%nodefactor%=(integer) 2
%nodeid%=(integer) 3
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 6
%return%=(integer) 0
nb=(integer) 3
----------------------------
>>%arg0%=(integer) 3
>>%nodeexpression%=(integer) 3
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 4
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 3
>>%return%=(integer) 0
>>nb=(integer) 4
----------------------------
>>>>%arg0%=(integer) 4
>>>>%nodeexpression%=(integer) 4
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 5
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 4
>>>>%return%=(integer) 0
>>>>nb=(integer) 5
----------------------------
>>>>>>%arg0%=(integer) 5
>>>>>>%nodeexpression%=(integer) 5
>>>>>>%nodefactor%=(integer) 5
>>>>>>%nodeid%=(integer) 0
>>>>>>%nodenumber%=(integer) 5
>>>>>>%nodeoperation%=(integer) 5
>>>>>>a=(integer) 0



____________________________
%arg0%=(integer) 2
%nodecallfunc%=(integer) 2
%nodeexpression%=(integer) 6
%nodefactor%=(integer) 2
%nodeid%=(integer) 3
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 6
%return%=(integer) 6
nb=(integer) 3
----------------------------
>>%arg0%=(integer) 3
>>%nodeexpression%=(integer) 3
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 4
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 3
>>%return%=(integer) 0
>>nb=(integer) 4
----------------------------
>>>>%arg0%=(integer) 4
>>>>%nodeexpression%=(integer) 4
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 5
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 4
>>>>%return%=(integer) 0
>>>>nb=(integer) 5
----------------------------
>>>>>>%arg0%=(integer) 5
>>>>>>%nodeexpression%=(integer) 5
>>>>>>%nodefactor%=(integer) 5
>>>>>>%nodeid%=(integer) 0
>>>>>>%nodenumber%=(integer) 5
>>>>>>%nodeoperation%=(integer) 5
>>>>>>a=(integer) 0

				end

____________________________
%arg0%=(integer) 2
%nodecallfunc%=(integer) 2
%nodeexpression%=(integer) 6
%nodefactor%=(integer) 2
%nodeid%=(integer) 3
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 6
%return%=(integer) 6
nb=(integer) 3
----------------------------
>>%arg0%=(integer) 3
>>%nodeexpression%=(integer) 3
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 4
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 3
>>%return%=(integer) 0
>>nb=(integer) 4
----------------------------
>>>>%arg0%=(integer) 4
>>>>%nodeexpression%=(integer) 4
>>>>%nodefactor%=(integer) 1
>>>>%nodeid%=(integer) 5
>>>>%nodenumber%=(integer) 1
>>>>%nodeoperation%=(integer) 4
>>>>%return%=(integer) 0
>>>>nb=(integer) 5
----------------------------
>>>>>>%arg0%=(integer) 5
>>>>>>%nodeexpression%=(integer) 5
>>>>>>%nodefactor%=(integer) 5
>>>>>>%nodeid%=(integer) 0
>>>>>>%nodenumber%=(integer) 5
>>>>>>%nodeoperation%=(integer) 5
>>>>>>a=(integer) 0



____________________________
%arg0%=(integer) 3
%nodecallfunc%=(integer) 6
%nodeexpression%=(integer) 24
%nodefactor%=(integer) 6
%nodeid%=(integer) 4
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 24
%return%=(integer) 0
nb=(integer) 4
----------------------------
>>%arg0%=(integer) 4
>>%nodeexpression%=(integer) 4
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 5
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 4
>>%return%=(integer) 0
>>nb=(integer) 5
----------------------------
>>>>%arg0%=(integer) 5
>>>>%nodeexpression%=(integer) 5
>>>>%nodefactor%=(integer) 5
>>>>%nodeid%=(integer) 0
>>>>%nodenumber%=(integer) 5
>>>>%nodeoperation%=(integer) 5
>>>>a=(integer) 0



____________________________
%arg0%=(integer) 3
%nodecallfunc%=(integer) 6
%nodeexpression%=(integer) 24
%nodefactor%=(integer) 6
%nodeid%=(integer) 4
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 24
%return%=(integer) 24
nb=(integer) 4
----------------------------
>>%arg0%=(integer) 4
>>%nodeexpression%=(integer) 4
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 5
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 4
>>%return%=(integer) 0
>>nb=(integer) 5
----------------------------
>>>>%arg0%=(integer) 5
>>>>%nodeexpression%=(integer) 5
>>>>%nodefactor%=(integer) 5
>>>>%nodeid%=(integer) 0
>>>>%nodenumber%=(integer) 5
>>>>%nodeoperation%=(integer) 5
>>>>a=(integer) 0

			end

____________________________
%arg0%=(integer) 3
%nodecallfunc%=(integer) 6
%nodeexpression%=(integer) 24
%nodefactor%=(integer) 6
%nodeid%=(integer) 4
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 24
%return%=(integer) 24
nb=(integer) 4
----------------------------
>>%arg0%=(integer) 4
>>%nodeexpression%=(integer) 4
>>%nodefactor%=(integer) 1
>>%nodeid%=(integer) 5
>>%nodenumber%=(integer) 1
>>%nodeoperation%=(integer) 4
>>%return%=(integer) 0
>>nb=(integer) 5
----------------------------
>>>>%arg0%=(integer) 5
>>>>%nodeexpression%=(integer) 5
>>>>%nodefactor%=(integer) 5
>>>>%nodeid%=(integer) 0
>>>>%nodenumber%=(integer) 5
>>>>%nodeoperation%=(integer) 5
>>>>a=(integer) 0



____________________________
%arg0%=(integer) 4
%nodecallfunc%=(integer) 24
%nodeexpression%=(integer) 120
%nodefactor%=(integer) 24
%nodeid%=(integer) 5
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 120
%return%=(integer) 0
nb=(integer) 5
----------------------------
>>%arg0%=(integer) 5
>>%nodeexpression%=(integer) 5
>>%nodefactor%=(integer) 5
>>%nodeid%=(integer) 0
>>%nodenumber%=(integer) 5
>>%nodeoperation%=(integer) 5
>>a=(integer) 0



____________________________
%arg0%=(integer) 4
%nodecallfunc%=(integer) 24
%nodeexpression%=(integer) 120
%nodefactor%=(integer) 24
%nodeid%=(integer) 5
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 120
%return%=(integer) 120
nb=(integer) 5
----------------------------
>>%arg0%=(integer) 5
>>%nodeexpression%=(integer) 5
>>%nodefactor%=(integer) 5
>>%nodeid%=(integer) 0
>>%nodenumber%=(integer) 5
>>%nodeoperation%=(integer) 5
>>a=(integer) 0

		end

____________________________
%arg0%=(integer) 4
%nodecallfunc%=(integer) 24
%nodeexpression%=(integer) 120
%nodefactor%=(integer) 24
%nodeid%=(integer) 5
%nodenumber%=(integer) 1
%nodeoperation%=(integer) 120
%return%=(integer) 120
nb=(integer) 5
----------------------------
>>%arg0%=(integer) 5
>>%nodeexpression%=(integer) 5
>>%nodefactor%=(integer) 5
>>%nodeid%=(integer) 0
>>%nodenumber%=(integer) 5
>>%nodeoperation%=(integer) 5
>>a=(integer) 0




____________________________
%arg0%=(integer) 5
%nodecallfunc%=(integer) 120
%nodeexpression%=(integer) 120
%nodefactor%=(integer) 120
%nodeid%=(integer) 0
%nodenumber%=(integer) 5
%nodeoperation%=(integer) 120
a=(integer) 120

	end

____________________________
%arg0%=(integer) 5
%nodecallfunc%=(integer) 120
%nodeexpression%=(integer) 120
%nodefactor%=(integer) 120
%nodeid%=(integer) 0
%nodenumber%=(integer) 5
%nodeoperation%=(integer) 120
a=(integer) 120
```
