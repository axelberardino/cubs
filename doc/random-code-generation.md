# Random code generation

Because the full grammar AST is contained in this program, it's possible to
visit this AST randomly and thus generate random valid AST.

Not really useful, but it shows what can be accomplished with an AST.

This is only AST generation, so it doesn't always lead to valid program (there's
no type checking or binding verification).

## Examples

```sh
./cubs -G generate
```

Very simple valid result:
```pascal
var id : string;
var id : boolean;
var id, id, id, id : integer;

function FuncId() : string;
begin
	id = FuncId();
end


begin
	FuncId();
end
```

Bigger, but invalid, example:
```pascal
	var id, id : integer;
	var id : integer;
	var id, id : string;

	function FuncId() : boolean;
	var id : integer;
	begin
		id = FuncId(FuncId() == FuncId(FuncId() * FuncId(FuncId()))) >= "String Expression";
	end

	function FuncId() : string;
	var id : string;
	begin
		id = FuncId(id, id);
	end

	function FuncId() : integer;
	var id, id : boolean;
	var id, id, id, id : integer;
	begin
		id = FuncId();
		return id < FuncId();
	end

	function FuncId() : boolean;
	begin
		FuncId();
	end

	function FuncId() : integer;
	var id, id : integer;
	var id, id : integer;
	begin
		begin
			begin
				FuncId(FuncId(), FuncId() * FuncId(FuncId((FuncId(626) <= FuncId()) * 410), id), id, "String Expression");
			end
			begin
				id = id;
			end
		end
	end


	begin
		FuncId(id * FuncId(FuncId(id, "String Expression" == FuncId(), (FuncId(false, 694))) - FuncId()), id <= 509, id != FuncId());
		id = "String Expression";
	end
```