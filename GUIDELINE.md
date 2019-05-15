
## CRASHES

There is two kind of projects :: When your project results in an executable, and when it results in a library.


### EXECUTABLE

1. You crash, you are wrong. -> 0
2. You crash in a corner case : Check 1.
3. You crash but the test is not in correction : Check 1
4. You crash but... : Check 1

> Why ?

Even if you crash for a small mistake that you will fix in 15sec and learn nothing, you should learn something. If you don't, you are missing something. ( Spoiler :: You have to learn to check errors in your functions || You have to learn to test more --> You just have to learn to be more rigorous )



### Library

1. You crash in a defined behavior, you are wrong. -> 0
2. You crash in a defined corner case : Check 1.
3. You crash but the test is not in correction : Check 1
4. You crash but... : Check 1... or ->

___
5. You crash in an undefined behaviour ? There was no behaviour expected, do not care
6. You don't know what to do with the undefined behaviour XYZ ? DO nothing. Build your function with defined behaviour in mind, no more.
( Who cares about what `printf("%#.15-s\n");` does ?)
7. You crash on a strlen(NULL) ? Check 5.



### It is impossible to protect ourself against every segfault

This assertion is _false_. **false**.  We are working on school projects that have small sizes. Protect your open, and you do half the job. You don't have to protect your programm against "if a file is a directory, and then if a file is not readable and then if a file is...", you just have to check your open.

You can't say a program that has only one file to read is impossible to secure. You can say that you did not check your open or you did not check your user input. Nothing else.

( Applies to 21sh to, sorry )

The task to protect a program can become harder if you have to protect it when everything else is done. But as you don't put a condom just at the end of your business, you don't try to protect your program at the end of it.


( nm is known to be more difficult to secure, this assertion may be true, but it is still far from hard / impossible )

### WHAT is a crash ?

Is a segmentation violation a crash ?
> yes

Is an exception in python a crash ?
> yes

Is an exception in js a crash ?
> yes

Is an unintended infinite loop a crash ?
> Like yes

He uses js, can I flag crash ?
> I'd like to say yes, but infortunaly... no

He does not protect his mallocs, can I flag ?
> Dunno, there is too much blabla in slack. At least, tell him why this is *bad* to not protect a malloc.

He protects his mallocs but not his functions that uses malloc, can I flag ?
> Same answer that previous. But you really have to explain why this is bad, the evaluated student probably missed something.

This project receive a segfault when I kill -11 it. Can I Flag ?
> Don't be stupid, the program did not try to do something he was not able to do. So ofc, no.

### Beginner's classics

```
/* Warning :: This loop does not handle get_next_line's errors */
while (get_next_line(0, &str) != 0)
{
    // do something with str
}
```
Exploits :
> ./binary args >&-

( This closes stdin and cause a fail when reading with get_next_line )

```
int fd = open("Some file", O_SOMETHING);

// Use fd
```
Exploit :
> ./binary anything_not_a_openable_file
Even if classic, this happen too often
