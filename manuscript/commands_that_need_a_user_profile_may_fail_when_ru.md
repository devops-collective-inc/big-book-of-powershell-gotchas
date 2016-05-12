# Commands that Need a User Profile May Fail When Run Remotely
Many commands act against the currently logged-on user’s profile. Those commands can sometimes fail when you run them over a Remoting connection, such as by using Invoke-Command or Enter-PSSession. For example, many installers default to creating per-user icons, and those can fail when run remotely – even when run in a “silent install” mode.

The problem is that, when you connect to a remote computer, you aren’t spinning up a complete user environment. You’re technically not “logging on” to the machine in the usual sense. You’re authenticating, yes, but in much the same way that you’d authenticate to a shared folder. Your remote connection doesn’t have a complete user profile, and so anything that’s expecting one can get errors and fail (even if they don’t show those errors).

There’s no easy fix for this, unfortunately. 

