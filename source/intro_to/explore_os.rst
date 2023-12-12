Intro to Linux
=======================

.. role:: bash(code)
   :language: bash

Exploring the OS
""""""""""""""""

Linux is a free and open-source operating system that is available in many different flavors or distributions. Unlike Windows or MacOS, Linux is not controlled or owned by a single company and is instead developed by a global team of volunteers. It is best known for its stability, reliability, and flexibility, and is used in many industries, including web hosting, supercomputing, and embedded systems. It is also well-suited for users who want to customize their system to their specific needs. Linux is also known for its great security features and its ability to run a variety of software, from web browsers to games. With Linux, you can create your own custom computer experience, from the desktop environment to the look and feel of the system itself.

Naviguation
-----------

.. figure:: /images/intro_to_linux_boot.png
    :scale: 25 %
    :align: center

    To get to Linux you will have to restart the computer and select the Linux option using the BIOS.

Ubuntu is not much different than Windows or MacOS. You can right-click to create new documents or folders, compress files, and search in specific directories. You have a Home folder with Download, Documents, Pictures, Videos, etc. You can use Firefox or Google Chrome, install software and customize the background or change your screen resolution

.. figure:: /images/intro_to_linux_desktop.png
    :scale: 25 %
    :align: center

    Linux is not much different from Windows or MacOS. There is a file explorer, web browser, text editor and everything.

.. figure:: /images/intro_to_linux_terminal.png
    :scale: 25 %
    :align: center

    You can search for tools and software by clicking in the upper-top corner.

.. figure:: /images/intro_to_linux_nautilus.jpg
    :scale: 50 %
    :align: center

    The file explorer is very similar to any OS. If you press CTRL+H you will see hidden files and folders.

.. figure:: /images/intro_to_linux_language.png
    :scale: 50 %
    :align: center

    If you intend to code, you should make sure to have access to the keyboard layout you want.


In order to learn about these functionalities, we recommend going through a tutorial `here <https://www.tutorialspoint.com/ubuntu/index.htm>`__. You can also look up YouTube tutorials to introduce features you want to know better, but be sure to check your Ubuntu version before (search for 'system info' in the applications)

Package Manager
---------------

Synaptic is a graphical package management tool for Debian systems. It is designed to allow users to easily install, upgrade, and remove software packages on their systems. It also provides a graphical user interface for viewing the contents of installed packages and managing the packages on the system. Synaptic is useful for users who want to install new software and keep their systems up to date. It is also useful for managing packages that have been installed from sources outside of the official Debian repositories, such as third-party repositories or manual downloads. It is easy to use and provides users with an intuitive and straightforward way to find, install, and manage software packages on their systems.

.. figure:: /images/intro_to_linux_synaptic.png
    :scale: 60 %
    :align: center

    Synaptic is installed by default on Ubuntu (any Debian OS) and will help you look for packages to install or repair mistakes you made.

This can install both libraries required for other software as well as the software itself, it is common to try to launch a new tool and be unable to install or use it until you try something like what is described in Section **Installing Stuff** (below). Synaptic is only the Graphical User Interface (GUI) for package management, but everything you do in Synaptic can be done in the Terminal.

Software Center
---------------

Syanptic is more powerful and was designed as a package manager. Software Center was designed as an "app-store" like program. The software center can install only one thing at a time and is a lot easier to navigate and you can read reviews and ratings.

.. figure:: /images/intro_to_linux_ubuntu_software_center.png
    :scale: 40 %
    :align: center

    The Software Center allows you to install much useful software often less related to coding and programming.


The Terminal
""""""""""""

The bash terminal, also known as the command line, is a powerful tool for interacting with your Linux system. It allows you to quickly execute commands, manage files and folders, and automate tasks. Bash is especially useful for system administration, scripting, and programming. 

Unlike a graphical user interface (GUI), which uses graphical elements like windows, icons, and menus, the command line requires you to type in commands to execute them. This might sound intimidating at first, but the command line can be much faster and more powerful than a GUI. Plus, with a little practice, you can become an expert in no time!

Navigating Files
----------------

Using the Terminal you can do anything that the GUI File Explorer can, and even more. 
The advantage of the Terminal is that operations can be automated.

**Renaming file:**
   - To rename a file in the Bash shell, you will need to use the mv command.
   - To use the mv command, you will need to specify the current name of the file and the new name you wish to give it.
   - For example, if you wanted to rename a file called “example.txt” to “newname.txt”, you would type the following command into the shell: :bash:`mv example.txt newname.txt`

**Changing directory:**
   - To change the directory you are currently located in, you will need to use the cd command.
   - To use the cd command, you will need to specify the path of the directory you wish to change to.
   - For example, if you wanted to change to the “Documents” directory, located in your home ($\sim$) directory, you would type the following command into the shell: :bash:`cd ~/Documents/`

**Copy-Pasting:**
   - To copy a file in the Bash shell, you will need to use the cp command.
   - To use the cp command, you will need to specify the file you wish to copy and the location you wish to copy it to.
   - For example, if you wanted to copy a file called “example.txt” to the “Documents” directory, located in your home directory, you would type the following command into the shell: :bash:`cp example.txt ~/Documents/`

**Ressources:**
    - Bash cheat sheet \#1 `[link] <https://www.educative.io/blog/bash-shell-command-cheat-sheet>`__
    - Bash cheat sheet \#2 `[link] <https://devhints.io/bash>`__
    - Bash cheat sheet \#3 `[link] <https://www.linuxtrainingacademy.com/linux-commands-cheat-sheet/>`__
    - Advanced concepts in Bash `[link] <https://www.pcwdld.com/bash-cheat-sheet>`__
    - Help with the :bash:`~/.bashrc` file `[link] <https://www.marquette.edu/high-performance-computing/bashrc.php>`__

Editing Text
------------

The easiest way to edit text is often using the native *Text Editor* in Ubuntu, but you can install software like gEdit, Atom or Sublime for more advance text editing. When dealing with code or processing everything is in text (C++ or Python or Bash), it all depends on the extension. Raw text in a *FILE.py* is in Python and raw text in a *FILE.cpp* is C++, while *FILE.sh* is for Bash. Microsoft Word *FILE.docx*) documents can be edited using LibreOffice (LibreOffice use *FILE.odt* by default, not *FILE.docx*), but these are not suitable for coding.

So keep in mind that to edit code you need very simple software like Sublime or Atom. When not writing code, but just simple text you can use the *FILE.txt* extension, or for more advanced formatting you can try Markdown (*FILE.md*). 

If you want to edit your text file directly in the terminal, as a starting point we recommend :bash:`nano`. This will allow you to edit raw text (no formatting). It is not as intuitive as a good old GUI, but some online resources will help you with it. It is as simple as :bash:`nano ~/PATH/TO/YOUR/FILE.txt`

.. figure:: /images/intro_to_linux_nano_bashrc.png
    :scale: 65 %
    :align: center

    Nano is very useful to edit text file in the terminal and basic operation like replacing or copy-pasting lines.


**Ressources:**
    - Nano guide for novices `[link] <https://itsfoss.com/nano-editor-guide/>`__
    - Introduction to Markdown `[link] <https://www.markdownguide.org/getting-started/>`__
    - Test your Markdown online `[link] <https://stackedit.io/>`__

Installing Stuff
----------------

Installing packages in Linux with :bash:`apt install` is an easy and straightforward process. :bash:`apt install` is a command-line utility that is used to install, remove, and manage packages on Linux systems. It is the most commonly used package manager on Debian and Ubuntu systems.

To install a package with apt install, open up a terminal window and type in the command:
:bash:`sudo apt install <package-name>`
You will be prompted for your password to authenticate the command. After entering your password, the package will be downloaded and installed.

If you want to remove a package, you can use the command:
:bash:`sudo apt remove <package-name>`

You can also use apt to update existing packages and keep them up to date. To update all packages, you can use the command:
:bash:`sudo apt update`

Finally, you can search for packages available for installation. To do this, use the command:
:bash:`sudo apt search <package-name>`

Bash Language
"""""""""""""

Bash scripting is a powerful tool for users of the Linux operating system. It allows users to automate tasks, create powerful and efficient programs and scripts, and generally make life easier. Bash scripting is based on the syntax of the Bourne Shell, a shell used on the UNIX operating system in the late 1970s.

Bash Scripting
--------------

The usefulness of bash scripting lies in its ability to automate repetitive tasks and create powerful programs and scripts that can be used to perform many different tasks. For instance, it can be used to create scripts that can be used to automate backups, create directories, or even perform complex calculations.

To start using bash scripting, you will need to have access to a Linux system with the bash shell installed, such as Ubuntu or Debian. Once you have access to the shell, you can start writing and running your scripts.

When you are learning bash scripting, there are a few key functions that you should be familiar with. These include, looping (for and while), conditionals (if, elif, else), and variables.

Once you have mastered the basics of bash scripting, you can start exploring more advanced topics, such as regular expressions, arrays, and string manipulation. Learning these topics will help make your scripts more powerful and efficient.

Basic Operation
---------------

First it is crucial to look at the ressources Navigating Files section to learn about basic command (such as echo, cd, or ls)

.. code-block:: bash

    # Variable Declaration
    # Syntax: VARIABLE_NAME=VALUE 
    NUMBER=10

.. code-block:: bash

    # For Loop
    # Syntax: for VARIABLE_NAME in [LIST]; do [COMMANDS]; done 
    for NUM in 1 2 3 4 5; do 
      echo "Number $NUM"
    done

.. code-block:: bash

    # While Loop
    # Syntax: while [CONDITION]; do [COMMANDS]; done
    while [ $NUMBER -gt 0 ]; do 
      echo "Number is $NUMBER"
      NUMBER=$[$NUMBER-1]
    done

.. code-block:: bash

    # If/Else
    # Syntax: if [CONDITION]; then [COMMANDS]; else [COMMANDS]; fi
    if [ $NUMBER -gt 5 ]; then
      echo "$NUMBER is greater than 5"
    else 
      echo "$NUMBER is less than 5"
    fi


Basename:
:bash:`basename /usr/local/bin/python`
Output: python

Dirname:
:bash:`dirname /usr/local/bin/python`
Output: /usr/local/bin

Regular Expressions
-------------------

Regular expressions are a powerful tool used in Bash to match text strings. A regular expression, or regex, is a sequence of characters that define a search pattern used to match strings of text.

For example, the regex `[0-9]` will match any single digit number.

Using a for loop and an if/else statement, we can use regular expressions to search for specific patterns in a string. For example, let's say we want to find all of the words in a sentence that start with the letter 'a'. We could use the following for loop:

.. code-block:: bash

    for word in $(echo "This is an amazing test sentence"); do
      if [[ $word =~ ^a[a-z]* ]]; then
        echo "$word"
      fi
    done


This loop will iterate through each word in the sentence and check if it matches the regex `^a[a-z]*`. If it does, it will print that word out. In this case, it will print 'an' and 'amazing'.

The most common use of regular expressions in our context is for files management. For example imagine you have a list of folder using IDs: sub-1010/, sub-1011/, sub-1012/, sub-2000/, sub-2001/, sub-2002/, sub-3010/. By using the regular expressions:
    - :bash:`ls sub-*` (get all folders)
    - :bash:`ls sub-10*` (get all 3 folder starting with sub-10)
    - :bash:`ls sub-*1` (get the 2 folders ending with the number 1)
    - :bash:`ls sub-??1?` (get the 2 folders that has 1 as the third number)
    - :bash:`ls sub[1,3]?1` (get the folders that start with either 1 or 3, but finish with 1)

This can be used with for loops to navigate and apply command to different directories or files.

Advanced Commands
-----------------

Here is a few tasks with example commands:
.. code-block:: bash

    # Iterate over all unique filenames in the directory (similar to a set)
    for i in $(ls */*.trk | xargs -n 1 basename | sort | uniq); do echo $i; done

.. code-block:: bash

    # Find and replace all spaces in filenames of the current directory
    find *.* -type f  | grep " " | while read FILE; do mv "${FILE}" ${FILE// /_}; done

.. code-block:: bash

    # Find all files in the directory clusters that are above 10 kilobytes
    for i in $(find clusters/ -type f -size +10k); do echo $i; done

These are examples of what can be done in bash in short one-line, but to get there you need to read a lot of tutorials and practices. Also everytime you do something that works, save it and keep it safe.

1. Using awk to print the first three characters of a string:
    :bash:`echo "stringexample" | awk '{print substr($0,0,3)}'`
    This command will print the first three characters of the string "stringexample".


2. Using a for loop to rename multiple files:
    :bash:`for file in *.txt; do mv ${file} ${file/.txt/.docx}; done`
    This command will loop through all files in the current directory with a .txt extension and rename them with a .docx extension.


3. Using sed to remove all blank lines from a file:
    :bash:`sed '/^$/d' file.txt`
    This command will remove all blank lines from the file "file.txt".


4. Using the command find and sed to find and replace a string: 
    :bash:`find /path/to/file -type f -exec sed -i 's/original_string/replace_string/g' {} \;`
    This command will find all files in the directory specified by /path/to/file and replace any instances of the string "original_string" with "replacement_string".


5. Using a for loop and the command find to delete all files with a given extension:
    :bash:`for file in $(find . -name "*.ext"); do rm ${file}; done`
    This command will loop through all files in the current directory with the extension ".ext" and delete them.


6. Using a for loop and sed to insert text into multiple files:
    :bash:`for file in *.txt; do sed -i '1i\text_to_insert' ${file}; done`
    This command will loop through all files in the current directory with a .txt extension and insert the text "text_to_insert" at the beginning of each file.


7. Using sed and a regular expression to remove lines containing a specific pattern from a file:
    :bash:`sed -i '/patternToRemove/d' file.txt`
    This command will remove all lines from the file "file.txt" that contain the pattern "patternToRemove".

Bash environment
----------------

When a program is invoked it is given an array of strings called the environment. This is a list of name-value pairs, of the form name=value.

You can view all environment variables set on your system with the env command. The list is long, so pipe the output through more to make it easier to read:

.. code-block:: bash

    env | more

Environment variables can be useful when you want to override default settings, or when you need to manage new settings.

When you type a command, the only reason your computer knows how to find the application corresponding to that command is that the PATH environment variable tells it where to look. 

You can add a location to your path the way you create throw-away variables. It works, but only as long as the shell you used to modify your system path remains open.

.. code-block:: bash

    # Modify your system path:modify an environment variable
    export PATH=$PATH:/home/seth/bin

.. code-block:: bash

    # Show your new path:
    echo $PATH

Then close your session and open a new one. You'll see that the PATH has returned to its default state.

You can set your own persistent environment variables in your shell configuration file, which is ~/.bashrc.

To edit your .bashrc file use a command line editor like vim or nano:

.. code-block:: bash

    vim ~/.bashrc
    nano ~/.bashrc

From your .bashrc you can modify your part default environment by adding lines to it. This includes defining alias, modifying environment variables, and activating Python virtual environments.

.. code-block:: bash

    # To define an alias:
    alias ..='cd ..'

.. code-block:: bash

    # To modify an environment variable:
    export PATH=$PATH:<path/to/dir>

.. code-block:: bash

    # To activate a Python environment:
    source <path/to/env>/bin/activate

    