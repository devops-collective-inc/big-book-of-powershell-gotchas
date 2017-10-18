# Where is the ____ Command? I’ve Installed the Latest Version of PowerShell and Can’t Find it!

One tricky thing is understanding that there are a certain number of commands that _come with PowerShell, _while _most_ commands do not.

Every new version of PowerShell includes at least a few new commands. For example, Start-Job appeared for the first time in PowerShell v2, while Invoke-AsWorkflow was introduced in PowerShell v3.

What confuses people is that a new version of PowerShell also tends to correspond with a new version of the Windows operating system? and the OS itself comes with hundreds of commands. For example, you may have used Get-SmbShare for the first time in Windows Server 2012, which included PowerShell v3. But Get-SmbShare is *part of the operating system, not part of PowerShell.* That is, you won't have Get-SmbShare on every system that has PowerShell v3 or later, because the command isn't a "feature of PowerShell," it's a "feature of Windows."

So? where do you get commands?

Usually, with whatever product those commands are a part of. Want the Exchange Server commands? Install the Exchange Server admin tools. Want the Windows Server 2012 commands? Install the Remote Server Administration Toolkit (RSAT), which contains the server admin tools.
