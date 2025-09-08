# Introduction to Shell (Bash)

### Where am I? (`pwd`)
To find out where you are at any time, use the command `pwd` (present working directory):
```bash
rbawah@ubuntu:~$ pwd
/home/rbawah
rbawah@ubuntu:~$ 
```
In the above code, the `rbawah@ubuntu:~$` (`username@hostname:current_directory`) indicates that our terminal is currently in the home directory of the user `rbawah`. The `~` is a shorthand for the home directory of the current user. The `pwd` command prints the current working directory. My `hostname` is `ubuntu`. Yours may just be `ubuntu` or something else depending on your system and terminal configurations. The appearance of a blinking cursor after the `$` sign indicates that our terminal is done executing the previous command and is ready for the next command.
- NOTE: It is not guaranteed that your prompt will be in the format `username@hostname:current_directory`. This can be customized by editing your `.bashrc` file found in the home directory. DO NOT start editing this file unless needed (such as setting a path or environment variable).
- `~` - home directory
- `/` - root directory
```bash
rbawah@ubuntu:~/Downloads$ pwd
/home/rbawah/Downloads
rbawah@ubuntu:~/Downloads$ 
```

### Get List of Contents in a Directory (`ls`)
We can list the contents (subdirectories and files) in a directory by using the `ls` command:
```bash
ls
# same as 
ls .
```
It can take the name of a path (relative or absolute path) as an argument. It will then list all contents found in that path (dir):
```bash
ls . # current dir
ls ~ # home dir
ls ~/Downloads # Downloads dir within home dir
ls /home/Downloads # Downloads dir within home dir
```
#### Relative vs Absolute Directory
If we are currently in the `Downloads` directory which contains the subdirectory `BigData`, then:
- `/BigData` is a Relative Path.
- `/home/rbawah/Downloads/BigData` is an Absolute Path.
- `~/Downloads/BigData` is an Absolute Path.

So, `ls` passed with any of the above paths will give us the same output.

#### List all contents in all nested directories (`ls -R`)
With the `-R` flag we can see all contents (lists of directories and files) of all levels of nested directories in the our directory. The flag must come before the directory path:
```bash
ls -R dir_path
```
- NOTE: `ls` has another flag `-F` that prints a `/` after the name of every directory and a `*` after the name of every runnable program.
- NOTE: always pass all flags before the directory path/filepath in bash commands.




## Changing Directory (`cd`)
- If you pass a path to the command `cd`, your terminal will go to that directory. 
- Wherever your terminal is, if you run `ls ~` you will be taken to the home directory.
- If a directory has whitespace in its name, you will have to surround it with quotes (`big data`) when passed to a shell command
```bash
# change/move to another dir/folder
rbawah@ubuntu:~$ cd ~/Downloads/'big data'
rbawah@ubuntu:~/Downloads/big data$ 

# To move up one dir
rbawah@ubuntu:~/Downloads/big data$ cd ..
rbawah@ubuntu:~/Downloads$ 

# To move up 2 dirs
rbawah@ubuntu:~/Downloads/big data$ cd ../..
rbawah@ubuntu:~$ 

# This goes to the root dir `/`
rbawah@ubuntu:~/Downloads/big data$ cd /../..
rbawah@ubuntu:/$ 

rbawah@ubuntu:~/Downloads/big data$ cd ~/../.
rbawah@ubuntu:~$ 

rbawah@ubuntu:~/Downloads/big data$ cd ~
rbawah@ubuntu:~$ 
```


## Copy or Move files (`cp`, `mv`), Rename file (`mv`)
You will often want to copy files, move them into other directories to organize them, or rename them. One command to do this is `cp`, which is short for "copy". If `original.txt` is an existing file, then the command below will duplicate the file in the same directory with a different name.
```bash
cp original.txt original_renamed.txt
```
`mv` on the other hand, is used to rename the file. The `original.txt` is lost afterwards.
```bash
mv original.txt duplicate.txt
```
The command below will copy the file to another location `big data`
```bash
cp original.txt ~/Downloads/'big data'/original.txt # we could also omit the filename in the destination folder to keep the original name, like so:
cp original.txt ~/Downloads/'big data'
```
WARNING: if a file with same name exists, it is overwritten by `cp` and `mv` commands.

If the last parameter to cp is an existing directory, then below command copies all of the files into that directory:
```bash
cp year/season/summer.csv year/season/winter.csv all_seasons_backup
```
Move the files, like cut-paste:
```bash
mv year/season/summer.csv year/season/winter.csv all_seasons_backup
```
- `cp` and `mv` can take a variable number of arguments, but the last argument will be the destination directory:
- `cp file1 file2 file3 destination_dir/`
- `mv file1 file2 file3 destination_dir/`

`mv` treats directories the same way it does files. You move them, or rename them as desired.



## Delete files and directories (`rm`, `rmdir`), Create directories (`mkdir`)
We can delete one or even multiple files at a time:
```bash
rm thesis.txt backup/thesis-2025-09.txt
```
`rm` does exactly what its name says, and it does it right away: unlike graphical file browsers, the shell doesn't have a trash can, so when you type the command above, your thesis is gone for good.

- To delete a directory, use `rmdir`, but the dir must be empty for this to work (`rmdir old_projects`).
- To create a directory: `mkdir dir_name`
- To create a subdirectory within `dir_name` without changing directories: `mkdir dir_name/sub_dir_name`



## View file Contents (`cat`)
The simplest way to see the contents of a file is with `cat`, which just prints the contents of files onto the screen. (Its name is short for "concatenate", meaning "to link things together", since it will print all the files whose names you give it, one after the other.)
```
cat filename
``` 
or for multiple files: 
```
cat file1 file2 file3
```
#### View file contents in Pages (`less`)
When we use the `less` command, we get to display file(s) contents in pages (smaller chunks) rather than the whole thing at once where we have to scroll through to find what we are looking for.
With `less`, we can then page through the content of each file with the spacebar, go to the next file with `:n`, previous file with `:p`, and use `:q` to quit viewing the contents and exit. (`less filepath1 filepath2`)

#### View start of a file (`head`)
Pass a filepath to the `head` command to view the first few (10) lines of the file. This is a very useful tool used by data scientists to figure out what fields a dataset has before analyses. (`head filepath`)

We can, however, control how many lines are displayed by passing the flag `-n` (number of lines):
```bash
head -n 4 filepath
```
The above command will print out only top 4 lines instead of the default top 10. 
- NOTE: It is considered best practice to always pass all flags before the filepath in bash commands.


## View end of file (`tail`)
- `tail filename` - view last 10 lines of the file(s).
- `tail file1 file2 file3` 
- `tail -n 50 filename` - view last 50 lines.
- `tail -n +100 filename` - view all lines after the first 100.


## Line count, Word count, Character count (`wc`)
- `wc filepath` - returns line count, word count, and character count
- `wc filepath1 filepath2 filepath3` - do same for many files
- you can use the flags `l`, `w`, `m`, or `c` to return only line, word, character, or byte count, respectively.

## 'Slice' - remove/select certain sections of text/file (`cut`)

- `cut -d [delimeter] -f [sections/slices] file/text`
- `cut -d , -f 2,4,6 sales.csv`
- `cut -d ; -f 1-3 employees.txt`

## Search for patterns (`grep`)
`grep` can search for patterns. It returns all lines containing the matching text.
- `grep 'text-to-find' filepath`

`grep` takes the following flags:
- `c`: print a count of matching lines rather than the lines themselves
- `h`: do not print the names of files when searching multiple files
- `i`: ignore case/case insensitive-match ("Big Data" == "big data")
- `l`: print the names of files that contain matches, not the matches
- `n`: print line numbers for matching lines
- `v`: invert the match, i.e., only show lines that don't match

## Unique lines (`uniq`)
The `uniq` command returns unique lines of text in a file. 
`uniq` is used with `sort` because it only considers adjacent duplicate lines.
- `sort duplicates.txt | uniq`


## Filter text and Edit text/files (`sed`)
`sed` (short for stream editor) is a Unix/Linux command-line tool used to **find**, **replace**, **insert**, **delete**, or **transform** text as it streams through — without opening a full text editor.
If `cut` is like scissors, `sed` is like a Swiss Army knife for text: it can slice, rearrange, and even rewrite on the fly.
- `sed 's/old text/new text/' filepath` -  replace text
- `sed -i 's/old/new/g' filepath` - edit file inplace
- `echo "I like cats" | sed 's/cats/dogs/'`
- `echo -e "I like cats\nYou like dogs\nWe all like animals" | sed '/^Y/d'` - the 2nd line, starting with Y is deleted.
- `sed -n '2,4p' file.txt ` - `p`: print only lines 2-4. `n`: suppress default printing.
- `sed '2i\This is a new line' file.txt` - insert new text before line 2 (`2i`)

