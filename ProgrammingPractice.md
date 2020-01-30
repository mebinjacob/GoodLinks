
1. Use active names for functions
==================================

Use active names for functions

Function names should be based on active verbs, perhaps followed by nouns :
	now = date.getTime();
	putChar('\n');

Functions that return a boolean(true or false) value should be named so that the return value is unambigious. Thus 
? if(checktotal(c))


Be accurate 
===========
A name not only labels, it conveys information to the reader. A misleading name can result in mystifying bugs. 

In this case, then name conveyed the correct intent but the implementation was wrong; it's easy for a sensible name to disguise a broken implementation. 

```
public boolean inTable(Object obj) {

	int j = this.getIndex(obj);
	return (j == nTable);
}
```

The function getIndex returns a value between zero and nTable - 1 if it finds the object, and returns nTable if not. The boolean value returned by inTable is thus the opposite of what the name implies. At the time the code is written, this might cause trouble, but if the program is modified later, perhaps by a different programmer, the name is sure to confuse. 

Excercise 1.1 :- 

Comment on the choice of names and values in the following code.

```
#define TRUE 0
#define FALSE 1

if((ch = getchar()) == EOF)
	not_eof = FALSE;

```
Excercise 1-2. Improve this function

```
	int smaller(char *s, char *t) {
		if(strcmp(s, t) < 1)
			return 1;
		else 
			return 0;
	}
```



1. Indent to show structure.
2. Use the natural form for expression. 
3. Parenthesize to resolve ambiguity.
4. Break up complex expressions. 
5. Be clear. 
6. Be careful of side effects. 


Consistency and Idioms 

Consistency leads to better programs. If formatting varies unpredictably, or a loop over an array runs uphill this time and downhill the next, or strings are copied with strcpy here and a for loop there, the variations make it harder to see what's really going on. But if the same computation is done the same way every time it appears, any variation suggests a genuine difference, one worth noting. 

Use a consistent indentation and brace style.
--------------------------------------------

if(month == FEB) {
	if(year%4 == 0)
		if(day > 29)
			legal = FALSE;
	else
		if(day > 28)
			legal=FALSE;
}

The above code is confusing as its not clear to which if does the else bind to. 


Use idioms for consistency
-------------------------

Like natural languages, programming languages have idioms, conventional ways that experienced programmer use. Learn it and get used to it. 

The do-while statement is used much less often than for and while loop, because it always executes at least once, testing at the bottom of the loop instead of the top. In many cases, that behaviour is a bug waiting to bite, as in this rewrite of the getchar loop :

do {
 c = getchar()
 putchar(c);
} while(c != EOF); 



Avoid function macros
---------------------

In C++, inline functions render function macros unnecessary; in Java, there are no macros. In C, they cause more problems than they solve. 

It's always better to use the ctype function than to implement them yourself, and its safer not to nest routines like getchar that have side effects. Rewriting the test to use two 
expressions rather than one makes it clearer and also gives an opportunity to catch end-of-file explicitly. 

```
	while((c = getchar()) != EOF && isupper(c))
		...
```

Sometimes multiple evaluations causes a performance problem rather than an outright error. 


Parenthesize the macros body and arguments
-----------------------------------------

If you insist on using function macros, be careful. Macros work by textual 


1.5 Magic Numbers
-----------------
-----------------

Magic numbers are the constants, array sizes, character positions, conversion factors, and other literal numeric values that appear in programs. 

Give names to magic numbers 
 As a guideline, any number other than 0 or 1 is likely to be magic and should have a name of its own. A raw number in program source gives no indication of its importance or derivation, making the program harder to understand and modify. This excerpt 

Magic numbers are constants, array sizes, characters positions, conversion factors, and other literal numeric values that appear in the programs. 

Give names to magic numbers 
---------------------------



