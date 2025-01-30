Created: 2024-09-17 16:25
## Family Tree:
1. Computer
2. Infrastructure Administration
3. [[Shell Scripting]]
-- -
## Commands
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
### Text Files Commands:
#### `cat >archivo1.txt`:
This is one of the most frequently used commands for handling text files (.txt format) in the terminal. Among its many options is the ability to create a file and print its content to the screen.
This will open `archivo1.txt`, allowing you to edit it. Use **CTRL+D** to end editing and save the content.
##### `cat dir1/archivo1.txt` :
Invoking the command without the `>` symbol will display the file's content on the screen. It can be used with the `-n` option to number the lines and with `-b` to avoid showing blank lines.
#### `more /var/log/dpkg.log`:
This command is also useful for printing the contents of a text file to the screen. It is essentially similar to `cat`, but the difference is that it paginates the content, making it more suitable for reading long files.
#### `nano dir1/archivo1.txt`:
Nano is a terminal-based text editor, primarily used for editing rather than just reading files. However, for this guide, it works perfectly to open a file and view its content from the command line.
At the bottom, different key combinations needed to work with files are displayed:
- **CTRL+R**: Specify a text file for Nano to open and display its content in the terminal.
- **CTRL+V**: Advance to the next page within Nano while the file is open.
- **CTRL+Y**: Go back to the previous page.
- **CTRL+W**: Search for a specific character or word in the text.
- **CTRL+X**: Close the file and return to the Bash prompt.
#### `grep "Hello world" * -r`:
This command, part of the Unix family, is one of the most versatile and useful tools available. It searches for a pattern we define within a text file. The first parameter is the string to search for, followed by the file or files (it accepts wildcards like `*`, and with the `-r` modifier, it can search recursively).
In this case, we are searching for the string "Hello World" in all files, recursively.
#### `tee`:
Reads from standard input and writes to standard output and one or more files. Normally, when redirecting output, the lines from a command are written to a file, but we cannot see the output at the same time. By using the `tee` command, this is possible!
* `ls -l | tee list.txt`: This command, besides displaying the directory content, will save it as a file.
- `ls -l | tee -a list.txt`: Using the `-a` flag, the content will be appended to the file without overwriting the previous content.
### Web Service commands:
The Linux terminal is so versatile and powerful that it allows us to connect to a web service, retrieve data, and process it for purposes such as adding it to files on our server, modifying it, or republishing it. Options include retrieving a JSON from an external URL, processing its contents, extracting specific attributes, and then creating new files or inserting them into a database based on the data.
#### `cURL` :
`cURL` is a command available on most Unix-based systems. It stands for “Client URL.” `cURL` commands are designed to check connectivity to URLs and serve as a great tool for data transfer. It supports many commonly used protocols.
The simplest use of `cURL` is to display the contents of a webpage. The following example will display the homepage of google.com:
```sh
curl https://www.google.com
```
While this is not very useful for visualizing information, you can use the `-o` option to write the HTML content of the homepage to a file on your computer:
```sh
curl https://www.google.com -o mypage.html
```
This saves the HTML to the file `mypage.html`.
This option can also be extended to process downloads:
```sh
curl https://ubuntu.zero.com.ar/ubuntu-releases/20.04/ubuntu-20.04.2.0-desktop-amd64.iso -o ubuntu.iso
```
This command downloads the ISO from the specified URL and names it `ubuntu.iso`.
```sh
curl https://ubuntu.zero.com.ar/ubuntu-releases/20.04/ubuntu-20.04.2.0-desktop-amd64.iso -O -C 0
```
In this case, the destination file is not renamed (with the `-O` option), and the download continues from where it left off (using the `-C` option).
The `-v` option allows you to verify connectivity to a remote site:
```sh
curl https://www.google.com -v
```
This provides additional information, such as the destination IP, security protocols, and certificates used.
To see all the request headers, use:
```sh
curl https://www.gogle.com -I
```
This shows headers such as the default path and web publisher.
**JSON Content**: One of the most useful applications of `cURL` is to retrieve JSON data from an endpoint. For example, using OpenStreetMap's API to get an address by passing coordinates:
```sh
curl "https://nominatim.openstreetmap.org/reverse.php?lat=-34.60378&lon=-58.38161&zoom=18&format=jsonv2" -o resultado.json
```
This saves the result from the web service into the file `resultado.json`. Remember to enclose the URL in single or double quotes.
#### `jq`:
JSON is a widely used structured data format, common in modern APIs and data services, especially in web applications. Unfortunately, shells like Bash cannot directly interpret JSON, making it cumbersome to work with JSON data in the terminal. That's where `jq` comes in, a powerful JSON processor for the terminal.
`jq` uses filters that operate on a stream of JSON. Each filter takes input and outputs JSON to standard output. Running a simple `jq` command on the JSON file retrieved with cURL returns the entire content:
```sh
jq '.' resultado.json
```
This command does not access any specific attribute since the filter `.` returns the entire JSON object.
To access a specific property, you need to specify it after the dot using its name:
```sh
jq '.display_name' resultado.json
```
This accesses the `display_name` property of the JSON. To access multiple properties, separate them with commas:
```
jq '.display_name, .type' resultado.json
```
This accesses both `display_name` and `type`.
**TIP:** If a property contains spaces in its name, it must be enclosed in double quotes.
#### Combining `cURL` and `jq` with Pipelines:
The **pipeline** feature allows you to use the output of one program as input to another. In Linux, a pipeline is represented by a vertical bar (`|`), which separates commands. For example, to get your machine's IP address:
```sh
ip address | grep "192.168"
```
This uses `grep` to filter the output of `ip address` for the string "192.168."
You can also combine `cURL` and `jq` with a pipeline to fetch external data, parse a specific property, and save it to a file:
```sh
curl "https://nominatim.openstreetmap.org/reverse.php?lat=-34.60378&lon=-58.38161&zoom=18&format=jsonv2" | jq ".display_name,.type" | tee consultapipe.txt
```
This command fetches the JSON with `cURL`, processes it with `jq` to extract `display_name` and `type`, and then saves the output to `consultapipe.txt`.