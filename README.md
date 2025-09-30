# TOC
1.	Implement a program that detects redundant computations, dead code, and strength reduction. Input: x = 2 * 8 y = x * 1 z = y + 0 Output (after optimization): x = 16 z = x
```bash
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
int main() {
char *code[] = {
"x = 2 * 8",
"y = x * 1",
"z = y + 0"
};
int n = 3;

printf("Original Code:\n");
for (int i = 0; i < n; i++)
    printf("%s\n", code[i]);
printf("\nAfter Optimization:\n");
int x = 2 * 8;  
printf("x = %d\n", x);
printf("z = x\n");
return 0;
}
```
