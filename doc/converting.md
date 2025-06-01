# Conversion into other language (like C++)

It's possible to convert this language into others like C++. Because we got the
full AST, we control the flow and it's possible to adapt it to print that into
antoher language.

## Example

```sh
./cubs -C check/execution/func-recursive.mmc
```

```cpp
#include <iostream>

int a;

int factorielle(int nb);

int factorielle(int nb)
{
	if ((nb <= 1))
	{
		return 1;
	}
	return nb * factorielle(nb - 1);
}

int main()
{
	a = factorielle(5);
}
```
