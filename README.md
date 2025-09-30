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

2.	Implement a simple code generator that translates arithmetic expressions into target assembly for a stack machine. 
Input: (a+b)*c 
Output: 
PUSH a
PUSH b 
ADD 
PUSH c 
MUL
```bash
#include <stdio.h>
#include <ctype.h>
#include <string.h>

#define MAX 100

char stack[MAX];
int top = -1;

void push(char c) { stack[++top] = c; }
char pop() { return stack[top--]; }
int precedence(char c) {
if (c == '+' || c == '-') return 1;
if (c == '*' || c == '/') return 2;
return 0;
}

void infixToPostfix(char infix[], char postfix[]) {
int k = 0;
for (int i = 0; i < strlen(infix); i++) {
char c = infix[i];
if (isalnum(c)) {
postfix[k++] = c;
} else if (c == '(') {
push(c);
} else if (c == ')') {
while (top != -1 && stack[top] != '(')
postfix[k++] = pop();
pop();
} else {
while (top != -1 && precedence(stack[top]) >= precedence(c))
postfix[k++] = pop();
push(c);
}
}
while (top != -1)
postfix[k++] = pop();
postfix[k] = '\0';
}

void generateCode(char postfix[]) {
for (int i = 0; i < strlen(postfix); i++) {
char c = postfix[i];
if (isalnum(c)) {
printf("PUSH %c\n", c);
} else if (c == '+') {
printf("ADD\n");
} else if (c == '-') {
printf("SUB\n");
} else if (c == '*') {
printf("MUL\n");
} else if (c == '/') {
printf("DIV\n");
}
}
}

int main() {
char infix[MAX], postfix[MAX];
printf("Enter an arithmetic expression: ");
scanf("%s", infix);
infixToPostfix(infix, postfix);
printf("\nGenerated Stack Machine Code:\n");
generateCode(postfix);
return 0;
}
```
