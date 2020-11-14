# Uniform pointer syntax for c variables/fields/parameters

My strategy of declaring pointer/array/pointer array/etc. variables or fields in C.

I recently came up with this idea that might help to solve the confusion when declaring any sort of pointer in C.

## The problem

`char *str;`

In C, a '\*' in a variable declaration could mean two things: 
* a pointer to a character array
* a pointer to a single char

Anyone reading this code might guess from the name of the variable that this is a character array, but with unconventional types any variable names, things get hard to read quickly. Yeah, you could just write a comment to say what this type expresses... but some people are too lazy to write a lot of documentation or are to lazy to read it. So how do you tell the reader of your code quickly and efficiently what exact types you're using?

## General idea

*Note: please dont do this: `char* a,* b;`, do this: `char* a; char* b;` when possible*

Lets start with some examples:

1. `int * x;` -> int pointer
1. `int* x;` -> int array
1. `int * * x;` -> int pointer pointer
1. `int** x;` -> int array array
1. `int ** x;` -> int pointer array
1. `int* * x;` -> int array pointer
1. `int ** ** x;` -> int pointer array pointer array

This principle is suitable for any number of pointer-indirections, as you might have noticed. It's quite simple: for pointer types use ' \*' (whitespace!) and for array types, use '\*'. Thats it! Don't forget to leave a whitespace between the asteristics and the variable name.

Lets examine the last example:

1. `int *` is a int pointer, because of the ' \*', which stands for *pointer*
1. `int **` is a int pointer *array*, because of the ' \*' for *pointer* and the following '\*' which stands for *array*
1. `int ** *` consists of ' \*', '\*' and ' \*'
1. `int ** **` consists of ' \*', '\*', ' \*' and '\*', so you've got a int *pointer array pointer array*.

Makes sense, doesn't it?

## Criticism
### When do you even use double pointers? Couldn't you just document the field/parameter using comments?

Yes, you could just put a comment above the function that uses double indirection pointers. And (At least I hope) nobody uses these frequently. But this syntax convention should help in any situation with pointers, double indirection or not. Even when using single pointers, i think this convention makes C code more easily understandable. One could also argue that this pointer syntax is faster to read and comprehend than a comment.

### This looks so ugly!

It's  probeably a different convention than you use, so it's unfamiliar to you. No problem. Your code might look 'uglier', but at least it differentiates pointer types correctly.

### Why not use '\[' and '\]' instead of some weird whitespace placement?

Because thats not how C variable syntax works. You can do this in Java, but Java has no pointers, so...

More criticism is welcomed.

Have a nice day!
