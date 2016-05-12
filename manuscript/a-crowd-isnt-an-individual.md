# A Crowd isn’t an Individual

A very common newcomer mistake:

![image067.png](images/image067.png)

Here, the person is treating everything like it contains only one value. But $computername might contain multiple computer names (that's what [string[]] means), meaning $bios and $os will contain multiple items too. You'll often have to enumerate those to get this working right:

![image069.png](images/image069.png)

Folks will run into this even in simple situations. For example:

![image071.png](images/image071.png)

PowerShell v2 won't react so nicely; in v3, the variable inside double quotes is $procs, and since that variable contains multiple objects, PowerShell implicitly enumerates them and looks for a Name property. You'll notice ".name" from the original string appended to the end - PowerShell didn't do anything with that.

You'd probably want to enumerate these:

![image073.png](images/image073.png)
