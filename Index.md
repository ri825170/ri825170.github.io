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

