# $ isn’t Part of the Variable Name
Big gotcha.

![image049.png](images/image049.png)

Can you predict what happened?

![image051.png](images/image051.png)

You see, the $ is not part of the variable's name. If you have a variable named example, that's like having a box with "example" written on the side. Referring to example means you're talking about the box itself. Referring to $example means you're messing with the contents of the box.

So in my example, I used $example=5 to put 5 into the box. I then created a new variable. The new variable's name was $example - that isn't naming it "example," it's naming it the contents of the "example" box, which is 5. So I create a variable named 5, that contains 6, which you can see by referring to $5.

Tricky, right? Comes up all the time:

![image053.png](images/image053.png)

In that example, I used the -ErrorVariable parameter to specify a variable in which I would store any error that would occur. Problem is, I used $x. I should have used x by itself:

![image055.png](images/image055.png)

That will store any error in a variable named x, which I can later access by using $x to get its contents - meaning, whatever error was stored in there.
