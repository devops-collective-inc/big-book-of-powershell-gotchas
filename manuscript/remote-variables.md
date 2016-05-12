# Remote Variables

When using Remoting, you need to remember that you’re dealing with two or more computers that don’t share information between them. For example, the following command woudl run fine on your local computer:

```
$f1 = "D:\Scripts\folder1"
$f2 = "D:\Scripts\folder2" Copy-Item $f1 -Recurse -Destination $f2 -Verbose -Force
```

But if you try to run just the Copy-Item command on a remote computer, it will fail:

```
 $f1 = "D:\Scripts\folder1"
 $f2 = "D:\Scripts\folder2"

 Invoke-Command -ComputerName MemberServer -ScriptBlock {Copy-Item $f1 - Recurse -Destination $f2 -Verbose -Force}
 
 Cannot bind argument to parameter 'Path' because it is null.
 + CategoryInfo : InvalidData: [:] [Copy-Item], ParameterBindingValidationException
 + FullyQualifiedErrorId : ParameterArgumentValidationErrorNullNotAllowed,Microsoft.PowerShell.Commands.CopyItemCommand
 + PSComputerName : MemberServer

```

The problem here is that $f1 and $f2 are defined on _your_ computer, but not on the remote computer. The script block passed by Invoke-Command isn’t evaluated on _your_ computer, it’s simply passed as-is.

There are two possible fixes. The first is to simply include the variable defintions in the script block:

```
 Invoke-Command -ComputerName MemberServer -ScriptBlock {
 $f1 = "D:\Scripts\folder1"
 $f2 = "D:\Scripts\folder2"
 Copy-Item $f1 -Recurse -Destination $f2 -Verbose -Force
 }
 ```
 
Another technique, available in PowerShell v3 and later, is to use a special variable designator. PowerShell pre-scans the script block for these, and will pass along your local variable values to the remote computer(s);

```
 $f1 = "D:\Scripts\folder1"
 $f2 = "D:\Scripts\folder2"
 
 Invoke-Command -ComputerName MemberServer -ScriptBlock {
 Copy-Item $using:f1 -Recurse -Destination $using:f2 -Verbose -Force}
```

The special $using: syntax is what makes this version of the command work.
 
