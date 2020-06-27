# PowerShell Notes

### General Information about PowerShell


- The version of PowerShell changes depending on the OS. This is automatic 

- PowerShell supports all the CMD commands

- PowerShell is integrated with .NET Framework

- By default PowerShell runs under normal user privileges

   - To avoid this the application can by launched as administrator
   - Or you can run the command *Start-process PowerShell -verb runas*

- Use *| more* after a command allows you to read the result 1 page at time. Ex *Get-Command | more*

- Ctrl+c kill the current action

- If a directory has spaces in the name need to be used bracket:

 - Cd Rename File Script wont work

 - Cd “Rename File Script” will work

    





### General info about .NET Framework

- Provides a collection of classes that provides easy access to all aspects of the windows environment (make easy interact and control the OS)



### Things to do after new Powershell installation

- Update Help file with the command *update-help* 

- Update the help file from time to time



- Set the execution policy or otherwise will not be possible execute powershell scripts

- Execute *Set-ExecutionPolicy RemoteSigned*



- Enable PowerShell remoting (if you need that the PC you are working on may **receive** commands remotely

- Execute *Enable-PSRemoting*





### Powershell Profiles



- You don’t have a profile until you create one
- You need to permit the config file execution to load a profile
- *$Profile* shows the path to the profile file
- Is possible that there is no profile created so you can’t reach the profile path. In tis case you can test of the path exist with *Test-Path $Profile*
- If the result of *Test-Path $Profile* is false, you have to create a profile with *New-Item -path $Profile -type file -force*
- Example of a Profile file:





```
# Riccardino's powershell profile



Clear-Host

Write-Host "`t `t `t ---------------ATTENTION!---------------"

Write-Host " `t `t You reached a terminal of the Riccardino's Network"

Write-Host ""

Write-Host ""
```





### Cmdlets



- Cmdlets are commands in the PowerShell environment

- Basic Structure of a Cmdlets: **Verb-Noun -parameter <argument>** where:

-  the **verb** describes the action that is to take place

  - The **noun** describes the target for that action

  - The **parameter** is an optional characteristic of the noun

  - Parameters are always preceded by a hyphen (-)
  - The **argument** is a value that can be provided for a parameters



- There are six common Cmdlets verbs:

  - Get → Queries a specific object
  - Set → Modifies the settings of an object
  - Enable → enables a setting
  - Disable → Disables a setting
  - New → Creates a new instance of an item
  - Remove → Remove an instance of an item
  





### How use the Help



- Help page about the command: Get-Help <cmdlet> ex. *Get-Help Get-Process* 
- To have some examples about the command: *get-help Get-Process -examples* 
- To have more info *Get-Help <cmdlet> -detailed* or *Get-Help <cmdlet> -full*
- To show the help in a separate window: *Get-Help <cmdlet> -ShowWindow*





### Get-Command

- *Get-Command* return a list of all the command in the Powershell version you are working on





### Format



- Format the output print on screen in in a specific format, syntax is command | format. Ex. *Get-Process | Format-Table* 



- There are 4 types of format:

  - Format-Wide: Displays only the default property 
  - Format List: Format as a list
  - Format-Table: format in a tabular layout
  - Format-Custom: use a custom layout





### Get-Member



- The Get-Member cmdlet gets the members, the properties and methods, of objects. Basically make a list of all the characteristics of an object/variable, even if the variable was create by the uses
- Ex in which the variable m is created: $m ="tutto a posto"
- Ex how Get-Member is used: $m | Get-Member







### Scripting



- Script file have extension *.ps1
- A script can be launched from a shortcut but is very complex



### Variables

- You can assign a variable with:
  
  - $<variable name> ex. $a = 4

  - New-Variable cmdlet

  - The variable name can contain letters,numbers, symbols or spaces. If contain spaces must be enclosed in braces {}

  - You can assign a data type to the variable
    
    - Ex. ``` [int]$a=4 ```

  - This are the most common data type:

    - [datetime] → date or time
    - [string] → string of characters
    - [char] → single character
    - [double] → double precision floating number
    - [int] → 32 bit integer
    - [boolean] → true or false value



Set-Variable -name "test" -value "fagianello" → with Set-Variable, the system check if the variable already exist and update it instead of create a new one directly.



Read-Host take the value typed and assign it to the variable

This line will take any data (PowerShell will assign the variable type automatically)



$name = Read-Host "name"



This line will do the same thing but the data type typed must be string or there will be an error



[string]$name = Read-Host "name"



This line works the same way as above but the data will be typed in a secure box



[string]$name = Read-Host "name" -AsSecureString

Variable-Related commands:



Get-Variable → show a list of all the variables actually available in that console 

Remove-Variable → remove the variable and related value

Set-Variable name_variable -option constant -value value → the variable cannot be deleted or edited



#### Constants

- A constant is a variable that once the value is set it can’t be easily changed

- To create a constant use following syntax:

Set-Variable name_variable -option ReadOnly

- To Undo the read only situation use this syntax: 

Set-Variable name_variable -option non -force

- To create directly a a constant and assign a value use this syntax:

Set-Variable name_variable -option Constant -value ‘value_variable’

​	

Comparison Operators

- Most common comparison operators:

  - -eq → Equal to (=)
  - -lt → less than (<)
  - -gt → greater than (>)
  - -ge → greater than or equal to (<=)
  - -ne → not equal (!=)



If you put c before the operator (ex. -ceq) it will be case sensitive

- Logical operators:

  - -not → Not (may be used also !)
  - -and → and
  - -or  → or



### IF statements



- Simple **if** statement: If the condition is true execute the code otherwise skip it

- - Syntax: If (condition) {run this code block}

- **ElseIf** statement, can be added to the If Statement

- - If (condition) {run this code block}

Elseif (condition) {run this code block}

… there may be multiple Elseif statement

- **Else** statement, can be use to provide code that runs if all the other conditions are false
- If (condition) {run this code block}

Elseif (condition) {run this code block}

.

.

Else {run this code block}





- Working example of if cycle. If the day is the 23th the will print “today” else will print “not today”



```
$dat = Get-Date
if($day.day -eq 23)
{
 Write-Host "today"
}
else
{
 Write-Host "not today"
}
```





### Looping



- Looping is a process that allows to execute the same command multiple times 

- This are the most common looping methods:

- - For Each-Object → loops through a collection of objects

```
$a=5,6,7,9,2

ForEach ($Value in $a)

{Write-Host $Value}
```



- - For → executes a specific numbers of times

```
For ($a=1; $a -le 7; $a++)
{Write-Host $a}
```



- - While → executes as loas a a condition remains true, test the condition first
  - Do While → executes one, then test the condition and repeats as long the condition still true



```
$a=1
do {write-host $a; $a++}
while ($a -lt 5)
```





- - Do Until → execute and repeats until a condition become true



```
$a=1
do {write-host $a; $a++}
until ($a -gt 5)
```





### Regular expressions



Match if the word accio is in the word cancaccio (-cmatch for case sensitive match)

"canaccio" -match "accio"



.(period) match a single character

[aeiou] match at least one character within the brackets

[b-g] match at least one character within a range

[^abcde] match any character except the one within the brackets

^ match a character located at the beginning of a string

$ match a character located at the end of a string

\* Match 0 or more occurrences of the preceding character

\ match the character following the escape / char

{n} must match n times

{n,} must match at least n times

{n,m} must match at least n times but not more than m times





## Tested - Specific Commands / Scripts



- This command replace a part of a name of all the files inside a folder:

dir | Rename-Item -NewName {$_.name -replace "part_to_replace" , "new_text"}

- 
  Script that execute the same command as above using input variables:

$oldname = Read-Host -Prompt "Text to replace > "

$newname = Read-Host -Prompt "Replace with > "

dir | Rename-Item -NewName {$_.name -replace $oldname , $newname}



Script that copies only the most recent file from a dir to another:

Get-ChildItem 'root' -File |

  Sort-Object -Property LastWriteTime -Descending |

  Select-Object -First 1 |

  Copy-Item -Destination 'dest' -Force





Order file from a specific data



Get-ChildItem -Path "\home" -Recurse | Where-Object -FilterScript {($_.LastWriteTime -gt "2020-05-01")}

## Advanced File Handling

### Check if a file exist in a folder

```
if (Test-Path "C:\Users\Riccardo Oberdano\OneDrive - Endeco-Technologies\Scripts\Powershell\RiccardinoOS\corso\test.txt")
{
Write-Output "File Exist"
}
else
{
Write-Output " File do not exist"
}
```



### Work with a text file

```
get-content filename.txt
```



To check only the last line (or the last N lines)

```
get-content -tail 1 namefile.txt
```



To check a specific line:

```
(get-content test.txt)[2]
```

To check a range of lines

```
(get-content test.txt)[0..3]
```

`the first line is line 0`  



### Work with a CSV file

```
Import-Csv nomefile.csv
```

