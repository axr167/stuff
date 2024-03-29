
## Overview

Shell scripts are lightweight scripts that help us automate system tasks. Scripts are interpreted - this means we scan and execute line by line. They usually have the .sh extension. Simply put, shell scripts are a combination of commands with some logic.

A simple hello world script is as follows:

    echo hello world

Save this as HelloWorld.sh. To run the script simply type the following command in the terminal:

    sh HelloWorld.sh

Before we proceed a quick note: 

- Shell scripts are very inconsistent when it comes to whitespaces. This is due to historical reasons and is something you are going to have to live with. 
    - https://unix.stackexchange.com/questions/117438/why-are-bash-tests-so-picky-about-whitespace
- I will be mentioning cases where whitespaces can cause problems as note pointers.

----------------------------------

### Variables and Datatypes

When it comes to shell scripts, **there is only 1 datatype - this is String**. Similar to languages like python or ruby, shell scripts are dynamically typed so variables can be assigned on the fly 

To reference variables we use thr ```$``` symbol. Below is a script where we declare a variable and print it on screen.

    #echo hello world
    x=10
    echo value of x is: $x

- [Note: in ```x=10``` there should be no whitespaces]. 

----------------------------------

### I/O operations

Write is done using the ```echo``` command as seen above.
Read can be done using the ```read``` keyword. This reads a variable from the command line.

A sample script is as follows:

    echo enter the value of x:
    read x
    echo the value of x is: $x

----------------------------------

### Arithmetic operations (+, -, *, /)

The following **DOES NOT** work:

    echo Example
    x=20
    y=30

    c=$x+$y

    echo c is: $c

It prints out: ```c is: 20+30``` instead of 5. The reason is that shell scripts treat everything as strings - here in the case of x, it is giving x the value of String "20" and not Integer 20.

So to perform arithmetic operations we can use the ```expr``` command. 

    echo Example
    x=2
    y=3

    expr $x + $y

- [Note in ```expr $x + $y``` you need to leave whitespace]

This performs the add operation correctly.

To store the value of a command such as ```expr $x + $y``` in a variable we use the backtick command ( ` ).

    echo Example
    x=2
    y=3

    c=`expr $x + $y`

    echo c is: $c

Now let us try performing multiplication operation.
        
    expr 5 * 2

This will throw a syntax error. This is because in shell ```*``` means all (wildcard) so in order to indicate that * is simply * and not wildcard, we need to use the escape character ' \ '.

    expr 5 \* 2
    
This returns the correct answer

----------------------------------

### Comparision operations

For comparisons operators like >, <, =, != do not work because everything is represented as strings. So to compare properly we need to use flags. They are shown below:


    >           -gt
    <           -lt
    >=          -ge
    <=          -le
    ==          -eq
    !=          -ne

When we use these operations in conditionals, remember to use the flags.

----------------------------------

### Conditional Statements

The format is as follows:

    if [ cond ]
    then
        # something
    else    # else is optional
        # something 
    fi

- Note here remember to leave space between the square brackets ```[ cond ]```

        echo Enter a
        read a

        echo Enter b
        read b

        if [ $a -gt $b ]
        then
          echo "a > b"
        fi

To use the else conditional do the following:

        echo Enter a
        read a

        echo Enter b
        read b

        if [ $a -gt $b ]
        then
          echo "a more than b"
        else
          echo "a less than b"
        fi

