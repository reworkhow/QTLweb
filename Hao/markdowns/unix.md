# Unix


*****

# UNIX POWER TOOLS

[Read this typefully at first.](http://www.ee.surrey.ac.uk/Teaching/Unix/)

This is an encyclopedia-like book. I need to use it as reference as reading several chapters. Below is some note I made. Most are just copy-and-paste.

## Basic

Bourne-type shells, such as bash , usually have $ in the prompt. The C shell uses % (but tcsh users often use >).

Some commands that you type are internal, which means they are built into the shell, and it's the shell that performs the action. For example, the cd command is built-in. The ls command, on the other hand, is an external program stored in the file /bin/ls. The shell doesn't start a separate process to run internal commands. External commands require the shell to fork and exec (Section 27.2) a new subprocess (Section 24.3); this takes some time, especially on a busy system.

The search path is exactly what its name implies: a list of directories that the shell should look through for a command whose name matches what is typed.

The search path isn't built into the shell; it's something you specify in your shell setup files.

By tradition, Unix system programs are kept in directories called /bin and /usr/bin. With additional programs usually used only by system administrators in either /etc and /usr/etc or /sbin and /usr/sbin.

The search path is stored in an environment variable (Section 35.3) called PATH (Section 35.6).

You can issue the ps x (Section 24.5) command to get a list of all processes running on your system.

**[Filename Extentions](http://docstore.mik.ua/orelly/unix3/upt/ch01_12.htm)**

Scripting languages and scripting applications differ from compiled languages and applications in that the application is interpreted as run rather than compiled into a machine-understandable format. You can use shell scripting for many of your scripting needs, but there are times when you'll want to use something more sophisticated. Though not directly a part of a Unix system, most Unix installations come with the tools you need for this more complex scripting -- Perl (Chapter 41), Python (Chapter 42), and Tcl.

### Pathname

You can use either the abbreviation ~ (tilde) or the environment variables $HOME or $LOGDIR, to refer to your home directory. In most shells, ~name refers to the home directory of the user name.

Here's a summary of the rules that Unix uses to interpret paths:

If the pathname begins with / It is an absolute path, starting from the root. If the pathname begins with ~ or with ~name Most shells turn it into an absolute pathname starting at your home directory (~) or at the home directory of the user name (~name). If the pathname does not begin with a / The pathname is relative to the current directory. Two relative special cases use entries that are in every Unix directory: If the pathname begins with ./, the path is relative to the current directory, e.g., ./textfile, though this can also execute the file if it is given executable file permissions.

If the pathname begins with ../, the path is relative to the parent of the current directory. For example, if your current directory is /home/mike/work, then ../src means /home/mike/src.

### [File Access Permission](http://docstore.mik.ua/orelly/unix3/upt/ch01_17.htm)

* * *

* * *

## Symbols

### wildcard

? (a question mark). When it appears in a filename, the ? matches any single character. For example, letter? refers to any filename that begins with letter and has exactly one character after that. This would include letterA, letter1, as well as filenames with a nonprinting character as their last letter, such as letterC

The * wildcard matches any character or group of zero or more characters. For example, *.txt matches all files whose names end with .txt; c* matches all files whose names start with c; c*b* matches names starting with c and containing at least one b; and so on. [advanced](http://docstore.mik.ua/orelly/unix3/upt/ch01_13.htm)



```
$ ls pr*
```



The shells' [](http://reworkhow.github.io/2013/05/23/square%20bracket)wildcards will match a range of files. For instance, if you have files named afile, bfile, cfile, and dfile, you can print the first three by typing as following. ([ ]is only for files exists,cannot create)



```
$ lpr [a-c]file
$ rm "[e-h]file"
```



Build Strings with { }



```
$ mv hao{3,5}.c
$ echo mv hao{3,5}.c # see whst it did using echo
$ cp hao{,cpp}
$ lpr /usr3/hannah/training/{ed,vi,mail}/lab.{ms,out}    #To print files from other directory(s) without retyping the whole pathname
$ vi /usr/foo/file{a,b,c,d,e,f,g,h,i,j} #make 
$ mkdir desktop/{man,cat}{1,2,3,4}
```



String editing with :



```
% echo /a/b/c
/a/b/c
% echo !$:h
echo /a/b
/a/b

% echo xyz.c abc.c
xyz.c abc.c
% echo !$:r
echo abc
abc

% set x = (a.a b.b c.c) #add g to make it universal/global
% echo $x:gr
a b c

% set x=(abc.c)
% echo $x:e
c

% echo /a/b/c
/a/b/c
% echo !$:t
c   
```



Substitution with ^



```
$ echo how are you
how are you
$ ^how^hao
hao are you
```



Command sustituion with a pair of backquptes('')

If you want to edit all files in the current directory that contain the word "error." Before



```
$ grep error *.c
bar.c:  error("input too long");
bar.c:  error("input too long");
baz.c:  error("data formatted incorrectly");
foo.c:  error("can't divide by zero"):
foo.c:  error("insufficient memory"):
$ vi bar.c baz.c foo.c
```



Now



```
$ vi `grep -l error *.c`
3 files to edit
"bar.c" 254 lines, 28338 characters
 ...
```



Attention, here 'grep -l' produce only a list of filenames instead of file names and text.



```
$ grep -l error *.c
bar.c
baz.c
foo.c
```



Another example for sending an email to many people,before



```
$ mail joe lisa franka mondo bozo harpo ...
```



Now



```
$ mail `who | cut -c1-8 | sort -u`
```



Since



```
% who | cut -c1-8
joe
lisa
franka
lisa
...
```



Test



```
$ echo `who | cut -c1-8 | sort -u`
bozo franka harpo joe lisa mondo
```



After using Unix for a while, you'll find that this is one of its most useful features. You'll find many situations where you use one command to generate a list of words, then put that command in backquotes and use it as an argument to something else. Sometimes you'll want to nest (Section 36.24) the backquotes -- this is where the bash, ksh, bash, and zsh $( ) operators (which replace the opening and closing backquote, respectively) come in handy. There are some problems with command substitution, but you usually won't run into them.[This book has many, many examples of command substitution. Here are some of them: making unique filenames (Section 8.17), removing some files from a list (Section 14.18), setting your shell prompt (Section 4.6, Section 4.8, Section 4.14), and setting variables (Section 4.8, Section 36.23).](http://docstore.mik.ua/orelly/unix3/upt/ch28_14.htm)

#### Bourne Shell Quoting

A **backslash** ( \ ) turns off the special meaning (if any) of the next character. For example, * is a literal asterisk, not a filename wildcard (Section 1.13). So, the first expr (Section 36.21) command gets the three arguments 79 * 45 and multiplies those two numbers:



```
$ expr 79 \* 45
3555
$ expr 79 * 45
expr: syntax error
$echo 79 \* 45
79 * 45
$echo 79 * 45
a lot of messy
```



A **Single quote** turn off the special meaning of all characters until the next quote is found. Here the question mark has no special meaning now.



```
$ echo Hey!       What's next?  Mike's #1 friend has $.
Hey! Whats next?  Mikes
```



A **Double quotes** work almost like single quotes. The difference is that double quoting allows the characters $ (dollar sign), ' (backquote), and \ (backslash) to keep their special meanings.



```
    $ echo "Hey!       What's next?  Mike's #1 friend has $."
    Hey!       What's next?  Mike's #1 friend has 18437.
```



quote special Characters in **Filenames**. Because, the shell uses spaces to determine the end of each arguments.



```
    cp /dev/null 'a file with spaces in the name'
    mv a\ file a_file
    mv '$a' a
```



Separating Commands with **Semicolons**. [Something unread](http://docstore.mik.ua/orelly/unix3/upt/ch28_16.htm)

## Scripting

### Anyone can program the shell

[click here hardly](http://docstore.mik.ua/orelly/unix3/upt/ch01_08.htm#upt3-CHP-1-SECT-8)

### Shell, the command interpreter

You don't really need to know this little tidbit about what goes on behind the scenes, but it sure helps to know about [fork and exec](http://docstore.mik.ua/orelly/unix3/upt/ch27_02.htm) when reading some Unix manuals.

### Default Command

One more thing to note is that when dealing with shell scripts, which store sequences of commands that you want to be able to run at one time, you will likely need to specify the shell or other program that will run the commands by default. This is normally done using the special #! notation (Section 36.2) in the first line of the script.



```
#!/bin/sh
# everything in this script will be run under the Bourne shell

...

#!/bin/tcsh
# everything in this script will be run under tcsh

...

#!/usr/bin/perl
# everything in this script will be interpreted as a perl command

...
```



### Script files

[showargs](http://docstore.mik.ua/orelly/unix3/upt/ch27_05.htm)

[ftpfile](http://docstore.mik.ua/orelly/unix3/upt/ch27_16.htm) ???

[ispell](http://docstore.mik.ua/orelly/unix3/upt/ch16_02.htm#upt3-CHP-16-SECT-2)

[count.it](http://docstore.mik.ua/orelly/unix3/upt/ch16_06.htm)

[ww.sh](http://docstore.mik.ua/orelly/unix3/upt/ch16_07.htm)

### eval

"Give me another chance. Re-evaluate this line and execute it." It's like a loop.

### Command

[spell](http://docstore.mik.ua/orelly/unix3/upt/ch16_01.htm) [look](http://docstore.mik.ua/orelly/unix3/upt/ch16_03.htm)

[wc](http://docstore.mik.ua/orelly/unix3/upt/ch16_06.htm)

#### for loop



```
$ for file in /usr/fran/report /usr/rob/file[23]
> do cat -t -v $file | less
> done
```



If you want the loop to stop before or after running each command,add the shell's read command (Section 35.18). It reads keyboard input and waits for a RETURN. In this case, you can ignore the input; you'll use read just to make the loop wait.



```
$ for file in /usr/fran/report /usr/rob/file[23]
> do
> echo -n "Press RETURN to see $file--"
> read x
> cat -t -v $file | less
> done
Press RETURN to see /usr/fran/report--RETURN
    Shell runs cat -t -v /usr/fran/report | less...
Press RETURN to see /usr/rob/file2--RETURN
    Shell runs cat -t -v /usr/rob/file2 | less...
Press RETURN to see /usr/rob/file3--RETURN
    Shell runs cat -t -v /usr/rob/file3 | less...
```



In Bourne-type shells, a newline following an open quote (' or "), pipe symbol (|), or backslash () will not cause the command to be executed. Instead, you'll get a secondary prompt (from the PS2 shell variable, set to > by default), and you can continue the command on the next line.(in the example, ['write'](http://docstore.mik.ua/orelly/unix3/upt/ch01_21.htm#upt3-CHP-1-SECT-21) means 'This sends messsages to another user's screen. Two users can have a discussion with write')



```
$ echo "We're leaving in 10 minutes. See you downstairs." |
> write joanne
```



#### here document operator 

```
sort >file <<EndOfSort
zygote
abacus
EndOfSort
```



The here document operator 

```
for person in "Mary Smith" "Doug Jones" "Alison Eddy"
do
    lpr <<- ENDMSG

    'date'

    Dear $person,

    This is your last notice. Buy me pizza tonight or else I'll type "rm -r *"      when you are not looking.

    signed,
    The midnight skulker
    ENDMSG
done
```



###### Handling Lots of Text with Temporary Files

Sometimes you need to execute a command with a long list of files for arguments. Here's an easy way to create that list without having to type each filename yourself -- put the list in a temporary file:



```
% ls > /tmp/mikel
% vi /tmp/mikel
...edit out any files you don't want...
% process-the-files `cat /tmp/mikel`
% rm /tmp/mikel
```



Here use a pair of back quotes for file substitution.

Possible problems: if the list is long enough, you may end up with a command line that's **too long** for your shell to process. If this happens, use **xargs** (Section 28.17). If your system doesn't have xargs, there are other workarounds doesn't that should solve the problem.

##### Dealing with too many Arguments

[xargs](http://docstore.mik.ua/orelly/unix3/upt/ch28_17.htm) Maybe important, Reading NEED

##### Expect [to be continued…](http://docstore.mik.ua/orelly/unix3/upt/ch28_18.htm)

### Vi(chapter17,18)

### Aliases

## Q&A

### Which Shell am I running in lightning?



```
grep haocheng /etc/passwd
```



### How can I change my login directory in lightning(tcsh)? --NOT WORKING now!



```
setenv HOME /working004a/an_sci2/Hao
```



### I don't want others to go access to my folder. How can I do that?

Once you've created a private directory, you should set its file access mode ( Section 50.2) to 700; this means that you're the only person allowed to read, write, or even list the files that are in the directory. Here's how:



```
    $ mkdir private
    $ chmod 700 private
```



On any Unix system, anyone who knows the root password can become superuser (Section 49.9) and read any files he wants. So a private personal directory doesn't give you complete protection by any means -- especially on systems where most users know the root password. If you really need security, you can always encrypt your files.



* * *



## Unix

#### system



```
uname -a
```



#### script



```
chmod u+x hao.sh 
```



#### mis



```
find /opt/apps/intel/11.1/mkl -name 'mkl_lapack.h'
locate mkl
```



#### less



```
shift + f : keep updating
shift +g : go to the end
/search from the beginning
/search from the end
```



#### data



```
wc
grep -i -B 1 -A 1 steal data.csv
sed -e 's/Block/Rejection/g' data.csv
sort -f -t'|' -k2       :columns separated by '|', sort on column 2 (-k2), case insensitive (-f)
uniq -d -u          :-d duplicate -u unique
```



#### awk



```
cat data.csv | awk -F "|" '{ sum += $4 } END { printf "%.2f\n", sum }'      :sum the fourth column
```



#### vi



```
:set nu                 :show the line numbers
# + shift + g           :go to a certain line
:5,12 s/foo/bar/g       :substitute line 5 to 12

/search             :search forward for string
?search             :search back for string
n               :search for next instance
N               :search for previous instance

u               :undo last change
dd              :delete current line
yy              :yank(copy) one line
p               :paste

:x              exit, saving changes
:q              exit as long as there have been no changes
:q!             exit and ignore any change
ZZ              exit and save change

:noh            remove highlight
:e              copy another file into this one
```



#### real problem

###### rename mutiple files with few change



```
for file in *.mp3; 
do mv "$file" `echo $file| sed -e 's/_E//g'`;  
done
```



###### show disk usage



```
du -sh          disk usage -summary human-readable 
```



###### reference:

[useful unix commands for data science](http://www.gregreda.com/2013/07/15/unix-commands-for-data-science/)




















