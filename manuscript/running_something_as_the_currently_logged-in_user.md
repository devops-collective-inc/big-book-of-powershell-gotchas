# Running Something as the "Currently Logged-in User"
A common PowerShell request is to be able to remotely kick off some code that runs under the account of the user that’s currently logged on to the remote machine, or the user who most often uses the remote machine.

This is really difficult, and usually impractical.

First, understand that Windows is inherently a multi-user operating system. It doesn’t have a concept for “the currently logged-on user” because there might be many logged-on users. Even though client versions of Windows don’t technically permit multiple interactive logons, the base operating system acts as if it can.

Second, as a multi-user OS, Windows’ job is to maintain a strict firewall around each user’s process space. You don’t want one user jumping into another’s space, because that would be a huge risk to security and stability. So you can’t easily log in as one user and run something that another user can “see.”

For example, a common version of this request is for an admin to remotely make Notepad pop up in front of users, so they can remotely convey some important message. Sadly, Notepad is not a good instant messaging app, and Windows doesn’t make this easy. And, if you think about it, what would malware be able to do if this was possible? It’d be horrible!

With very few, difficult exceptions, you can’t really run something “as another user on a remote machine.” One exception is if you know the remote user’s user name and password. If you do, you can establish a Remoting session to the computer using their credentials, and potentially have applications run in that user’s process space. But you can see how impractical that is in most situations.

