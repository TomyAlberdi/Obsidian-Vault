#Cheatsheet #Development
* Localize process running in port:
  ```netstat -ano | findstr :<PORT>```
  
* Kill process by PID:
  ```taskkill /PID <PID> /F```
### Navigation:
- `ls`: Lists files in the folder.
- `ls -a`: Lists all files, including hidden files.
- `ls -l`: Shows all information about a folder (User, group, permissions, size, creation date, and time).
- `ls -R`: Recursively shows folders and the files contained within them.
- `pwd`: Shows the current folder.
- `more [filename]`: Displays the content of a file.
### Create:
- `mkdir [folder name]`: Creates a new folder.
- `touch [filename]`: Creates a new file.
### Delete:
- `rm [filename]`: Deletes a file.
- `rmdir [folder name]`: Deletes an empty folder.
- `rm -r [folder name]`: Deletes a folder and its contents.
### Copy / Move / Rename:
- `mv [path/file 1] [path/file 2]`: Renames file 1 to file 2 (file 2 must not exist or it will be overwritten).
- `mv [path/folder 1] [path/folder 2]`: Renames folder 1 to folder 2 (folder 2 must not exist).
- `mv [path/folder 1] [path/folder 2]`: Moves content from folder 1 to folder 2 (folder 2 must exist).
- `cp [path/file 1] [path/file 2]`: Copies a file or folder.
* `-r`: Indicates to recursively copy the contents of subfolders.
### Folder Navigation:
- `cd ..`: Moves up one folder level.
- `cd [folder name]`: Changes to a specified folder.