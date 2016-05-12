# PowerShell.exe isn’t PowerShell

It’s important to understand that Windows PowerShell is actually an untouchable, behind-the-scenes engine. You as a mere human being cannot easily interact directly with PowerShell.

Instead, you need a host application. A host embeds the engine internally, and then gives you a way to interact with it. For example, PowerShell.exe is a host application. It is built around the same Windows console host (ConHost.exe) as the old Cmd.exe command-line shell, but it embeds the PowerShell engine. You type commands, and the host hands those to the engine for execution. The host is also responsible for displaying any results ? in this case, on-screen.

Why is this distinction important?

Because different hosts can behave in different ways. For example, the PowerShell ISE behaves a bit differently than the console host, and both of them behave very differently from Active Directory Administration Center ? another PowerShell host.
