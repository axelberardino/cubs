# Compilation

The compilation step transforms a code into an assembly representation and
compile the code.

## Let's test it

There's a lot of compilation tests in the `check/execution` folder.

### Example of a compilation

```sh
./cubs -S check/execution/func-recursive.mmc
```

It will generates the assembly representation.
```nasm
factorielle:
	push	ebp		; Begin
	mov	ebp, esp
	mov	edx, [ebp + 8]

	push	edx		; Save edx into the stack to help computing expression
	mov	edx, 1
	mov	ecx, edx	; Move current edx into ecx
	pop	edx		; Restore edx from the stack to help computing expression
	push	ecx		; Infeq cmp : second arg
	push	edx		; Infeq cmp : first arg
	call	__is_infeq		; Check if edx <= ecx, and store result in eax
	mov	edx, eax	; Copy resulting strings in eax
	test	eax, eax
	jz	if_jump_1	; If expr then
	mov	edx, 1
	mov	eax, edx	; eax is used to put returned value
	mov	esp, ebp
	pop	ebp
	ret			; Return
if_jump_1:
	mov	edx, [ebp + 8]

	push	edx		; Save edx into the stack to help computing expression
	push	ebp		; Create a scope to save arguments
	mov	ebp, esp
	mov	edx, [ebp + 8]

	push	edx		; Save edx into the stack to help computing expression
	mov	edx, 1
	mov	ecx, edx	; Move current edx into ecx
	pop	edx		; Restore edx from the stack to help computing expression
	sub	edx, ecx	; Compute chunk's sub expression in edx
	push	edx		; Save argument
	call	factorielle	; Just call the function using __cdecl convention
	mov	edx, eax	; Copy result of the function into edx
	mov	esp, ebp
	pop	ebp		; Close the arguments scope
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
	push	ebp		; Create a scope to save arguments
	mov	ebp, esp
	mov	edx, 5
	push	edx		; Save argument
	call	factorielle	; Just call the function using __cdecl convention
	mov	edx, eax	; Copy result of the function into edx
	mov	esp, ebp
	pop	ebp		; Close the arguments scope
	mov	[a], edx	; Just affect an expression
	mov	eax, 1		; The system call for exit (sys_exit)
	mov	ebx, 0		; Exit with return code of 0 (no error)
	int	80h
```

You can compile it using:
```bash
./cubs -S check/execution/func-recursive.mmc > /tmp/func-recursive.asm
nasm -o prog.o -f elf -d ELF_TYPE /tmp/func-recursive.asm
ld -s --dynamic-linker /lib/ld-linux.so.2 -lc prog.o -o prog
```
