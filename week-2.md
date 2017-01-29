Based on lessons in the PCDA course by Steve McLaughlin and Tanya Clement: 
https://github.com/stevemclaugh/pcda

#### **1.** Command Line Basics

While in many cases we can use the terms “command line,” “terminal,” and “shell” interchangeably, each has a slightly different denotation. 

“**Command line**” has the broadest scope, referring to a style of interface. A command-line interface, also known as a command-line interpreter (CLI) is any system in which all interaction occurs via text-based commands issued through a keyboard.

A **terminal**, or more accurately a terminal emulator, is an application in your local operating system that essentially just provides a window to type in. We’ll be using the built-in Mac OSX terminal emulator, called **Terminal**, which you can find under “Utilities” in your Applications folder (`/Applications/Utilities/Terminal.app`). Open Terminal, then type the following and press return.
    echo $SHELL

A **shell** is the software layer between user input and the rote world of file system maintenance. The graphical user interface (GUI) provided by Mac OS X is itself technically considered a shell, but if someone refers to “the shell” they typically mean a command-line interpreter like [Bash](#). The command you entered above should have returned something like `/bin/bash`, which is the location of Bash’s “binary,” or machine-readable application file. 

#### **2.** Exploring the File System

Create a new terminal window by pressing ⌘+N. Before we go further, you may find it helpful to pull up the following cheat sheet: [Unix/Linux Command Reference](#).

Unix-like operating systems are based on a metaphor: a nested set of directories and data files, forming a tree structure that begins at the root directory `/`. A benefit of this arrangement is that each file can be uniquely identified using a pathname of the following format:`/Users/yourname/Desktop/file.txt`.

At any given moment in a shell session, the user metaphorically occupies a particular “working directory” within this greater tree structure. Enter the `pwd` (“print working directory”) command to see your current location.

    pwd

The root directory, `/`, is just like any other folder in the system. Enter the following to change your working directory to root.

    cd /

You can view the contents of the current directory with the `ls` command. 

    ls

![](DraggedImage-5.png)

You should see a list of directories including “Library,” “Users,” “bin,” “dev” and so on. Add the `-a` option and you’ll see a longer list including the hidden files “.DS\_Store” “.Trashes.” You can find dozens of other options in the `ls` manual, which you can read using the following line. Press “q” to return to the shell.

    man ls

In OS X, the file path `~/` is a shortcut to the current user’s home directory, which contains the “Documents” and “Downloads” folders users see foregrounded in the Finder. From the perspective of the command line, “Desktop” is a directory like any other. Let’s `cd` there.

    cd ~/Desktop

> **Tip:** Hold down the Option key and click within the current line to move the cursor.

#### **3.** Command Line Basics Continued
Next, let’s create a new directory and brief text file on the desktop. 
    mkdir test_dir
    echo "This is some text." > test.txt
    
List out your files to see what is on your Desktop. You should see both the directory "test_dir" and the file "test.txt"

    ls

To move our text document into our directory we can use the `mv` tool. We’ll then `cd` into the folder.

    mv test.txt test_dir
    cd test_dir

> **Tip:** `cd` interprets `test_dir` as a relative file path in the above lines. Because a folder with that names is indeed present in the working directory, we can refer to it by its local name rather than its full pathname beginning with `/`.

Let’s make a copy of our text file with `cp` and check the updated directory contents.

    cp test.txt test2.txt
    ls

> **Tip:** If you’re midway through typing the name of a pre-existing file in the shell, you can press tab to compete the name automatically.

Let’s rename our new text file using `mv` then check the change with `ls`. Then we’ll delete the file with `rm`.

    mv test2.txt test3.txt
    ls
    rm test3.txt

Another useful file path shortcut is `../`, which refers to the parent directory of our current location on the file tree. Let’s use it to `cd` back to Desktop.

    cd ../

Finally, we’ll delete our test directory and the file inside. Adding the `-r` option tells `rm`  to remove files recursively, meaning everything in the specified folder gets wiped out. 

    rm -r test_dir

Be careful with `rm`, especially in recursive mode. It deletes files permanently rather than sending them to a Trash folder, so a small mistake can really ruin your day.


#### **4.** Text I/O from the Command Line

Below, we create a text file in the Desktop directory using the `>` operator. We then append a second line using `>>` and view the contents of Desktop to confirm we’ve made a new file.

> **Tip:** If `>` is directed at an existing file, it will overwrite the original without warning. 

    cd ~/Desktop
    echo "Hello there." > note.txt
    echo "Hello again." >> note.txt
    ls

If we want to view our new text file, we have lots of options to choose from. By default, **head** will read the first 10 lines of a text file and print them in the shell. You can specify any number of lines with the `-n` option. 

    head note.txt
    head -n 1 note.txt



**tail** is similar, printing a file’s final lines instead.

    tail note.txt
    tail -n 1 note.txt

**less** is a program that lets us scroll through longer files. To close less when you’re finished, press the `q` key.

    less note.txt



**Nano** is a simple text editor that is available in most Unix-like systems.

    nano note.txt



Use the arrow keys to move your cursor around in the document. Add another line to the file and save it by pressing `ctrl+o`, followed by `return` to confirm the filename. Press `ctrl+x` to exit Nano.


#### **5.** Programming basics in Python
To get started using Python, simply enter `python` in the shell.

    python

We’ve just switched from the standard shell to the Python environment, which you can tell at a glance by the “\>\>\>” to the left of your cursor. We’re in what’s known as a language shell or a read-eval-print loop (REPL), in which any commands we enter will be interpreted as Python code. You can leave Python at any time by entering the `quit()` command.

We’ll begin by assigning some data to variables.

    x=5
    y=5.0
    z="Hello"

If you type `x` and hit return, you’ll notice the variable’s current value is output on the line below. Trying the same with with `x+2` will return 7.

    x+2

> Output:
>
>     7

Note that `x+x` gives a result of 10, while `x+y` returns 10.0. That’s because 5 and 5.0 are different data types in Python. The former is an **int**, or integer, while the latter is a **float**, or floating point value. 

Now try using the `+` operator on two strings.
    z+" world"

> Output:
>
>     'Hello world'

Note that `+` is used for two entirely different purposes: adding numbers and concatenating strings. When the same symbol performs multiple tasks in different contexts, it’s described as overloaded.


Next we’ll link a series of values using Python’s list data type. There several ways to represent an ordered sequence of items in Python, but we’ll be using list most frequently.

    eu_countries=['Austria', 'Belgium', 'Bulgaria', 'Croatia', 'Republic of Cyprus', 'Czech Republic', 'Denmark', 'Estonia', 'Finland', 'France', 'Germany', 'Greece', 'Hungary', 'Ireland', 'Italy', 'Latvia', 'Lithuania', 'Luxembourg', 'Malta', 'Netherlands', 'Poland', 'Portugal', 'Romania', 'Slovakia', 'Slovenia', 'Spain', 'Sweden', 'UK']

We can now refer to individual list members using bracket annotation.

    eu_countries[3]

The command above returns the string “Croatia,” which is located at index 3. As in most programming languages, we begin counting from 0 when working with ordered data.

If you try to access an out-of-range index value you’ll get an error.

    eu_countries[99]

We can also create a subset of a list using Python’s slice notation. The following will return a list containing four items, beginning at index 3 in `eu_countries`.

    eu_countries[3:7]

Leaving one side of the colon blank will include all items on that end of the list.

    eu_countries[5:]
    eu_countries[:10]

We can also use negative numbers to count backwards from the end of a list. The following will return “UK,” the final string in the list.

    eu_countries[-1]

Under the hood, every string in Python is actually a list of individual characters. In the example below, `word[7]` returns the letter “e,” while `word[7:20]` returns “establishment.”

    word="antidisestablishmentarianism"
    word[7]
    word[7:20]

If we need to know the length of a list or string, the `len` function can tell us.

    len(eu_countries)
    len(word)

Conditional statements are a fundamental part of all programming languages. We use the `if` operator to evaluate conditionals.

    number=12
    if number==12:
         print "The value is 12, an integer."

By adding `else`, we can tell Python to do something if the conditional isn’t true.

    number=10
    if number==12:
         print "The value is 12, an integer."
    else: 
         print "The value is not 12."

A **for loop** is a structure that lets us iterate through lists and other data structures so we can refer to each item one at a time.
    
    for country in eu_countries:
        print country + ' is great.'

Finally, we can create functions to automate repetitive processes. Use the `def` declaration to start s function definition. The code below will produce the same output as the last example.

```python
def is_great(word):
    return word + ' is great.'

for country in eu_countries:
    print is_great(country)
```

In this case we’re not saving much effort, but as we proceed you’ll find that functions will help you write simpler, more readable code.

