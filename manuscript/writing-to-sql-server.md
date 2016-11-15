# Writing to SQL Server
Saving data to SQL Server - versus Excel or some other contraption - is easy.

Assume that you have SQL Server Express installed locally. You've created in it a database called MYDB, and in that a table called MYTABLE. The table has ColumnA and ColumnB, which are both strings (VARCHAR) fields. And the database file is in c:\myfiles\mydb.mdf. This is all easy to set up in a GUI if you download SQL Server Express "with tools" edition. And it's free!

```
$cola = "Data to go into ColumnA"
$colb = "Data to go into ColumnB"

$connection_string = "Server=.\SQLExpress;AttachDbFilename=C:\Myfiles\mydb.mdf;Database=mydb;Trusted_Connection=Yes;"
$connection = New-Object System.Data.SqlClient.SqlConnection
$connection.ConnectionString = $connection_string
$connection.Open()
$command = New-Object System.Data.SqlClient.SqlCommand
$command.Connection = $connection

$sql = "INSERT INTO MYTABLE (ColumnA,ColumnB) VALUES('$cola','$colb')"
$command.CommandText = $sql
$command.ExecuteNonQuery()

$connection.close()
```

You can insert lots of values by just looping through the three lines that define the SQL statement and execute it:

```
$cola = @('Value1','Value2','Value3')
$colb = @('Stuff1','Stuff2','Stuff3')

$connection_string = "Server=.\SQLExpress;AttachDbFilename=C:\Myfiles\mydb.mdf;Database=mydb;Trusted_Connection=Yes;"
$connection = New-Object System.Data.SqlClient.SqlConnection
$connection.ConnectionString = $connection_string
$connection.Open()
$command = New-Object System.Data.SqlClient.SqlCommand
$command.Connection = $connection

for ($i=0; $i -lt 3; $i++) {
  $sql = "INSERT INTO MYTABLE (ColumnA,ColumnB) VALUES('$($cola[$i])','$($colb[$i])')"
  $command.CommandText = $sql
  $command.ExecuteNonQuery()
}

$connection.close()
```

It's just as easy to run UPDATE or DELETE queries in exactly the same way. SELECT queries use ExecuteReader() instead of ExecuteNonQuery(), and return a SqlDataReader object that you can use to read column data or advance to the next row.