# AST generation

Because the full grammar AST is contained in this program, it's possible to
visit this AST and generate a graphical representation of it.

To achieve that, we're using `dotty` from the `graphviz` package.

## Examples

```sh
./cubs -O check/execution/func-recursive.mmc
```

It will generates a dotty representation:
```dot
digraph G
{
	Program [label="Program",color="0.650 0.700 0.700",];
	Declarations1 [label="Declarations",color="0.650 0.700 0.700",];
	Program -> Declarations1 [];
	Declaration1 [label="Declaration",color="0.650 0.700 0.700",];
	Declarations1 -> Declaration1 [];
	DeclarationBody1 [label="DeclarationBody",color="0.650 0.700 0.700",];
	Declaration1 -> DeclarationBody1 [];
	Ids1 [label="Ids",color="0.650 0.700 0.700",];
	DeclarationBody1 -> Ids1 [];
	Id1 [label="a",color="red",];
	Ids1 -> Id1 [];
	Type1 [label="integer",color="0.650 0.700 0.700",];
	DeclarationBody1 -> Type1 [];
	Functions1 [label="Functions",color="0.650 0.700 0.700",];
	Program -> Functions1 [];
	Function1 [label="Function",color="0.650 0.700 0.700",];
	Functions1 -> Function1 [];
	HeaderFunc1 [label="HeaderFunc",color="0.650 0.700 0.700",];
	Function1 -> HeaderFunc1 [];
	IdFunc1 [label="factorielle",color="orange",];
	HeaderFunc1 -> IdFunc1 [];
	Arguments1 [label="Arguments",color="0.650 0.700 0.700",];
	HeaderFunc1 -> Arguments1 [];
	Argument1 [label="Argument",color="0.650 0.700 0.700",];
	Arguments1 -> Argument1 [];
	DeclarationBody2 [label="DeclarationBody",color="0.650 0.700 0.700",];
	Argument1 -> DeclarationBody2 [];
	Ids2 [label="Ids",color="0.650 0.700 0.700",];
	DeclarationBody2 -> Ids2 [];
	Id2 [label="nb",color="red",];
	Ids2 -> Id2 [];
	Type2 [label="integer",color="0.650 0.700 0.700",];
	DeclarationBody2 -> Type2 [];
	Type3 [label="integer",color="0.650 0.700 0.700",];
	HeaderFunc1 -> Type3 [];
	CompoundInstr1 [label="CompoundInstr",color="0.650 0.700 0.700",];
	Function1 -> CompoundInstr1 [];
	Instrs1 [label="Instrs",color="0.650 0.700 0.700",];
	CompoundInstr1 -> Instrs1 [];
	Instr1 [label="Instr",color="0.650 0.700 0.700",];
	Instrs1 -> Instr1 [];
	If1 [label="If",color="0.650 0.700 0.700",];
	Instr1 -> If1 [];
	Expression1 [label="Expression",color="0.650 0.700 0.700",];
	If1 -> Expression1 [];
	Operation1 [label="NONE",color="yellowGreen",];
	Expression1 -> Operation1 [];
	Factor1 [label="Factor",color="0.650 0.700 0.700",];
	Operation1 -> Factor1 [];
	Expression2 [label="Expression",color="0.650 0.700 0.700",];
	Factor1 -> Expression2 [];
	Operation2 [label="<=",color="yellow",];
	Expression2 -> Operation2 [];
	Factor2 [label="Factor",color="0.650 0.700 0.700",];
	Operation2 -> Factor2 [];
	Id3 [label="nb",color="red",];
	Factor2 -> Id3 [];
	Factor3 [label="Factor",color="0.650 0.700 0.700",];
	Operation2 -> Factor3 [];
	Number1 [label="1",color="goldenrod3",];
	Factor3 -> Number1 [];
	CompoundInstr2 [label="CompoundInstr",color="0.650 0.700 0.700",];
	If1 -> CompoundInstr2 [];
	Instrs2 [label="Instrs",color="0.650 0.700 0.700",];
	CompoundInstr2 -> Instrs2 [];
	Instr2 [label="Instr",color="0.650 0.700 0.700",];
	Instrs2 -> Instr2 [];
	Return1 [label="Return",color="0.650 0.700 0.700",];
	Instr2 -> Return1 [];
	Expression3 [label="Expression",color="0.650 0.700 0.700",];
	Return1 -> Expression3 [];
	Operation3 [label="NONE",color="yellowGreen",];
	Expression3 -> Operation3 [];
	Factor4 [label="Factor",color="0.650 0.700 0.700",];
	Operation3 -> Factor4 [];
	Number2 [label="1",color="goldenrod3",];
	Factor4 -> Number2 [];
	Instrs3 [label="Instrs",color="0.650 0.700 0.700",];
	Instrs1 -> Instrs3 [];
	Instr3 [label="Instr",color="0.650 0.700 0.700",];
	Instrs3 -> Instr3 [];
	Return2 [label="Return",color="0.650 0.700 0.700",];
	Instr3 -> Return2 [];
	Expression4 [label="Expression",color="0.650 0.700 0.700",];
	Return2 -> Expression4 [];
	Operation4 [label="*",color="yellow",];
	Expression4 -> Operation4 [];
	Factor5 [label="Factor",color="0.650 0.700 0.700",];
	Operation4 -> Factor5 [];
	Id4 [label="nb",color="red",];
	Factor5 -> Id4 [];
	Factor6 [label="Factor",color="0.650 0.700 0.700",];
	Operation4 -> Factor6 [];
	CallFunc1 [label="CallFunc",color="0.650 0.700 0.700",];
	Factor6 -> CallFunc1 [];
	IdFunc2 [label="factorielle",color="orange",];
	CallFunc1 -> IdFunc2 [];
	Expressions1 [label="Expressions",color="0.650 0.700 0.700",];
	CallFunc1 -> Expressions1 [];
	Expression5 [label="Expression",color="0.650 0.700 0.700",];
	Expressions1 -> Expression5 [];
	Operation5 [label="-",color="yellow",];
	Expression5 -> Operation5 [];
	Factor7 [label="Factor",color="0.650 0.700 0.700",];
	Operation5 -> Factor7 [];
	Id5 [label="nb",color="red",];
	Factor7 -> Id5 [];
	Factor8 [label="Factor",color="0.650 0.700 0.700",];
	Operation5 -> Factor8 [];
	Number3 [label="1",color="goldenrod3",];
	Factor8 -> Number3 [];
	CompoundInstr3 [label="CompoundInstr",color="0.650 0.700 0.700",];
	Program -> CompoundInstr3 [];
	Instrs4 [label="Instrs",color="0.650 0.700 0.700",];
	CompoundInstr3 -> Instrs4 [];
	Instr4 [label="Instr",color="0.650 0.700 0.700",];
	Instrs4 -> Instr4 [];
	Affect1 [label="Affect",color="0.650 0.700 0.700",];
	Instr4 -> Affect1 [];
	Id6 [label="a",color="red",];
	Affect1 -> Id6 [];
	Expression6 [label="Expression",color="0.650 0.700 0.700",];
	Affect1 -> Expression6 [];
	Operation6 [label="NONE",color="yellowGreen",];
	Expression6 -> Operation6 [];
	Factor9 [label="Factor",color="0.650 0.700 0.700",];
	Operation6 -> Factor9 [];
	CallFunc2 [label="CallFunc",color="0.650 0.700 0.700",];
	Factor9 -> CallFunc2 [];
	IdFunc3 [label="factorielle",color="orange",];
	CallFunc2 -> IdFunc3 [];
	Expressions2 [label="Expressions",color="0.650 0.700 0.700",];
	CallFunc2 -> Expressions2 [];
	Expression7 [label="Expression",color="0.650 0.700 0.700",];
	Expressions2 -> Expression7 [];
	Operation7 [label="NONE",color="yellowGreen",];
	Expression7 -> Operation7 [];
	Factor10 [label="Factor",color="0.650 0.700 0.700",];
	Operation7 -> Factor10 [];
	Number4 [label="5",color="goldenrod3",];
	Factor10 -> Number4 [];
}
```

## Generating an image

```sh
./cubs -O check/execution/func-recursive.mmc > func-recursive.dot
dot -Tpng func-recursive.dot > func-recursive.png
```

Generated image will be:
<img src="ast.png" />
