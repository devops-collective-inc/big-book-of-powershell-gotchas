# Commands' Default Output Can Lie
Well, perhaps not “lie,” but certainly “mislead.”

Try running Get-EventLog -LogName Security on your computer. Notice the column headers in the output?

* The output doesn’t include all of the properties that are available behind the scenes.
* Some of the column headers don’t actually list the correct name for that property.

This can be really frustrating, because if you try to use Select-Object with an incorrect name, it’ll just spit out blanks. The confusion arises because many commands’ output are pre-formatted using a default view. That means you’re not actually seeing the command’s “output,” you’re seeing a “massaged” version of it.

To see the complete output, with the correct property names, run your command and pipe it to `| Format-List *` (or fl * if you prefer). With commands that produce a great deal of output, that can take some time to run and create a messy screen; a shorter version can be obtained by piping your command to `| Select -First 1 | Format-List *`. You’ll see one output object, all of its properties, and the correct property names to use in other commands.



