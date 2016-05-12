# Properties vs. Values

```
$names = Get-ADComputer -filter * |
 Select-Object -Property Name
 
 Get-CimInstance -Class Win32_BIOS -ComputerName $names 
 ```
 
Know why that won’t work? It’s because the result of Get-ADComputer is an object, which has properties. You probably knew that. But the result of Select-Object is also an object that has properties. Specifically, in this case, it’s “Selected” ADComputer object, having a single property: Name. 

Look at the help for Get-CimInstance. The -ComputerName parameter accepts objects of the type String. It says so, right in the help! But a Selected ADComputer object isn’t the same thing as a String. The Name property you selected contains strings, but it isn’t a string itself. This is a huge distinction, and one that trips people up all the time.

Think of a property as a box. That box can contain things, but it’s a thing in and of itself, also. In this case, the box is called Name, and it contains strings. But you can’t shove that whole box into something that was just expecting strings. “Hey, I wanted a string, not a box!”

Think about a fax machine. Do you remember those? They accept pages, and transmit those pages. Now suppose you have an envelope full of pages. You can’t just shove the envelope into the fax machine and expect good results. In that analogy, the envelope is a property, and the pages inside it are values. To get the pages into the fax machine, you have to take them out of the envelope first.

What you want to do in this case is get the strings out of the box, and Select-Object offers a way of doing that:

```
$names = Get-ADComputer -filter * |
 Select-Object -ExpandProperty Name
 
 Get-CimInstance -Class Win32_BIOS -ComputerName $names
```

See the difference? -ExpandProperty gets just the contents of the specified property, rather than returning an object that only has that property. Want a simple way to test this in the shell? Run these commands:

```
Get-Service | Select -Property Name | Get-Member
 Get-Service | Select -ExpandProperty Name | Get-Member
```
