Based on lessons in the PCDA course by Steve McLaughlin and Tanya Clement: 
https://github.com/stevemclaugh/pcda

#### **1.** Command Line Basics

While in many cases we can use the terms “command line,” “terminal,” and “shell” interchangeably, each has a slightly different denotation. 

“**Command line**” has the broadest scope, referring to a style of interface. A command-line interface, also known as a command-line interpreter (CLI) is any system in which all interaction occurs via text-based commands issued through a keyboard.

A **terminal**, or more accurately a terminal emulator, is an application in your local operating system that essentially just provides a window to type in. We’ll be using the built-in Mac OSX terminal emulator, called **Terminal**, which you can usually find under “Utilities” in your Applications folder (`/Applications/Utilities/Terminal.app`). If you can't find it there, use your spotlight search box in your finder window. 

Open Terminal, then type the following (note the space between echo and $SHELL!) and press return.
    echo $SHELL

A **shell** is the software layer between user input and the rote world of file system maintenance. The graphical user interface (GUI) provided by Mac OS X is itself technically considered a shell, but if someone refers to “the shell” they typically mean a command-line interpreter like [Bash](#). The command you entered above should have returned something like `/bin/bash`, which is the location of Bash’s “binary,” or machine-readable application file. 

#### **2.** Exploring the File System

Create a new terminal window by pressing ⌘+N. Before we go further, you may find it helpful to pull up the following cheat sheet: [https://files.fosswire.com/2007/08/fwunixref.pdf](#).

Unix-like operating systems are based on a metaphor: a nested set of directories and data files, forming a tree structure that begins at the root directory `/`. A benefit of this arrangement is that each file can be uniquely identified using a pathname of the following format:`/Users/yourname/Desktop/file.txt`.

At any given moment in a shell session, the user metaphorically occupies a particular “working directory” within this greater tree structure. Enter the `pwd` (“print working directory”) command to see your current location.

    pwd

The root directory, `/`, is just like any other folder in the system. Enter the following to change your working directory to root.

    cd /

You can view the contents of the current directory with the `ls` command. 

    ls


You should see a list of directories including “Library,” “Users,” “bin,” “dev” and so on. Add the `-a` option and you’ll see a longer list including the hidden files “.DS\_Store” “.Trashes.” You can find dozens of other options in the `ls` manual, which you can read using the following line. Press “q” to return to the shell.

    man ls

In OS X, the file path `~/` is a shortcut to the current user’s home directory, which contains the “Documents” and “Downloads” folders users see foregrounded in the Finder. From the perspective of the command line, “Desktop” is a directory like any other. Let’s `cd` there.

    cd ~/Desktop

> **Tip:** Hold down the Option key and click within the current line to move the cursor.

#### **3.** Command Line Basics Continued
Next, let’s create a new directory and brief text file on the desktop. 
    mkdir test_dir
    echo "This is some text." > test.txt
    
List out your files to see what is on your Desktop. 

    ls

You should see both the directory "test_dir" and the file "test.txt"

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

> **Tip:** It is significant in Python to use the tab when you see a tabbed space in the code. Below, even though the terminal give you a new line after the colon (:) you should tab once before typing the word "print" or you'll get an error. Further, you must hit 'return' twice to run the piece of code after the closing quotation marks (").
  
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

Next, we'll use Python’s read-eval-print loop (REPL). Open a new Terminal window and enter the following line to open the Python shell.

    python
    
Assign a sentence to the variable `sentence` — in this case the opening line from John Kennedy Toole’s  _A Confederacy of Dunces_. Type the name of the variable and hit return to view your new string.

```    
sentence="A green hunting cap squeezed the top of a fleshy balloon of a head."
    
sentence
```

**Output:**

    A green hunting cap squeezed the top of a fleshy balloon of a head.

Making lists happens more often than any other data structure, so it’s worth reviewing the details of Python’s slice notation. Let’s create a list of strings, then view a subset of the list to a new variable. Enter the variable “words2” to view the result.
    words=['A', 'green', 'hunting', 'cap', 'squeezed']
    words2=words[2:4]
    words2

The Python shell should print `['hunting', 'cap']`, i.e., the subset of the list “words” from index 2 to index 3. In general, `list_name[start:end]`, where “start” and “end” are integers, returns a subset of “list-name” from index `start` to `end-1`. The “end minus 1” bit may seem odd, but in practice it makes slice notation more readable. The snippet above, for instance, gives us a list containing 2 items, equal to 4-2. And if we want to excerpt the first three items in a list, the following notation will do the trick.

    words[:3]
    
Recall that omitting an index number before or after the colon means you want to include all items on that end of the list. The following returns everything from index 2 to the end of “words”: `['hunting', 'cap', 'squeezed']`.

    words[2:]

If you want to excerpt the last three entries in a list without counting from the beginning, use a negative number before the colon.

    words[-3:]

Likewise, the following will slice off the final 3 items in our list, returning `['A', 'green']`.

    words[:-3]

To reverse the order of a list, add an extra colon and “-1.”

    words[::-1]

It’s important to note that in Python, every string is a list of characters under the hood. We can thus reverse the spelling of a sentence like so.

    sentence="A green hunting cap squeezed the top of a fleshy balloon of a head."
    sentence[::-1]

If want to break our sentence into words, we can use the `split()` function to create a list of substrings with the space character as delimiter.

    words=sentence.split(' ')
    words

The `join()` function reverses the process, inserting a chosen string (here, a space) between each item in a list. Note that “sentence2” below is identical to our original “sentence” string.

    sentence2=' '.join(words)
    sentence2
    sentence

#### **6.** Text I/O in Python
This week we’ll review reading and writing text files from the Python environment. Download the following file from Project Gutenberg or the mirror provided and save it to your Desktop. It’s a collection of essays by Jonathan Swift, including a line that Toole references in the title _A Confederacy of Dunces_.
- [http://www.gutenberg.org/cache/epub/623/pg623.txt](http://www.gutenberg.org/cache/epub/623/pg623.txt)
- [mirror](http://www.stephenmclaughlin.net/pcda/sample_data/week-2/pg623.txt)


> **Tip:** Take a look at the file anyway you would like. You may notice that our text file from Project Gutenberg is broken into short lines, none longer than 74 characters. Many ASCII text files follow this fixed-width convention, designed to fit the 80-character width of many early PC displays. That display format, in turn, was chosen to work with data from 80-column punch cards, introduced by IBM in the 1920s.

First we’ll assign the file’s pathname to the variable `filepath` and create the file stream object we’ll use to read its contents. Open the Python shell and enter the following lines.

> **Tip:** In OS X you can drag a file from Finder to a Terminal window instead of entering the pathname by hand. If the path contains any spaces, these will be escaped (preceded by a backslash) in keeping with the conventions of Unix-like interfaces.
> Python’s `os` module, however, doesn’t recognize escaped characters. In order to avoid confusion, it’s probably best to avoid using spaces in filenames.

    filepath="/Users/yourname/Desktop/pg623.txt"
    file=open(filepath)
    

Then we’ll make an empty list called `swift_lines` and iterate through our file stream using a for loop, adding each line to the list as we go.

    swift_lines=[]
    for line in file:
         swift_lines.append(line)

Finally, we’ll close our file stream and view a line from our list.

    file.close()
    swift_lines[1000]


Each line ends with `\r\n` , a carriage return followed by a line feed character, suggesting the file was created in a Windows text editor. As Oualline and Noria discuss in this week’s readings, Unix-like systems generally use `\n` to indicate newlines, while `\r\n` is standard in Windows and DOS. To complicate matters, early Apple computers used `\r` on its own for the same purpose. 

> **Tip:** While the term “newline” refers to any character or character combination used to mark the end of a line, when we say “newline character” for the rest of the course we’ll mean `\n` (formally called “line feed”) unless otherwise noted.

Whether we’re adapting to quirks of history or fixing typing mistakes, we’ll often find it helpful to get rid of whitespace characters (newlines, spaces, tabs) at the beginning and end of a given string. For a string named `line`, `line.strip()` will return a copy of the string with all newlines and other whitespace characters removed from either end.

    line=lines[1000]
    line
    line.strip()

#### **7.**  Python Text I/O Continued

Closing a file stream with `close()` when you’re done with it is good style, though it’s not strictly required. If you want to keep your code compliant yet crisp, the following format closes a file stream automatically.

    lines=[]
    with open(filepath) as file:
         for line in file:
               lines.append(line) 

Or you can use this command, which does the same in one line.

    lines=open(filepath).readlines()

Note that calling `readlines()` creates a list of all lines in a text file, including any newline characters (in this case, `\r\n` ). We could easily use a for loop with the `strip()` function to remove newlines from each string in the list, but the following line does the same in a shorter form. Here `open()` creates a file stream and `read()` returns the file’s contents as a single string. Finally, `some_text.splitlines()` returns a list of lines in the string `some_text`, removing newline characters along the way.

    lines=open(filepath).read().splitlines()

If we’d like to convert our list of lines to a block of flowable text, we can use `join()` to combine all items in the list `lines`, each separated by a space. Note that we end up losing the paragraph breaks that we saw in the original file.

    ' '.join(lines)

#### **8.**  Accessing Text Files on the Web

The Python module `urllib2`  makes grabbing text from the Web as easy as working with local files. Let’s download the first two chapters of _A Confederacy of Dunces_ in plain ASCII format.

    import urllib2
    url="http://www.stephenmclaughlin.net/pcda/sample-data/week-2/Toole_A-Confederacy-of-Dunces_Ch1-2.txt"
    toole_lines=urllib2.urlopen(url).read().splitlines()

Let’s look at the 200th line in the file.

    toole_lines[199]

> _Output:_
>
>     'Ignatius had himself broken the baseball machine by kicking it.'

Someties you'll want to do some text filtering to check whether a string includes a specified substring.

    if "Reilly" in "Ignatius J. Reilly":
         print "yes"

To do a case-insensitive substring search, use the `lower()` function to convert your original string to lowercase. If your search term contains any capital letters, you’ll want to convert it to lowercase as well.

    if "reilly" in "Ignatius J. Reilly".lower():
         print "yes"

Try creating a simple text filter or two, printing all lines that contain a given substring.

    for line in toole_lines:
         if "orleans" in line.lower():
              print line
    
    for line in toole_lines:
         if "doughnut" in line.lower():
              print line

While you’re at it, use a for loop to identify the sentence by Jonathan Swift (in `swift_lines`) that Toole references in his title _A Confederacy of Dunces_. Try to resist the urge to use ⌘+F in TextWrangler.