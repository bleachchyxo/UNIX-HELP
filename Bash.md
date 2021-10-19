# Bash Guide
A bash script simple guide I made since I had trouble looking for information around the internet.

## Start scripting
In order to start coding in bash you must have to start your scripts by adding `#!/bin/bash` at the top of everything.
Now we can start printing the classic "Hello World".
     
    #!/bin/bash
    echo "Hello World!"
     
Now we must get into the terminal in order to compile the script and run it. The file must be saved as `.sh` type. In my case the file name is `script.sh`.

There are two ways of running the script in the terminal. The first one is by simply typing `bash` and your file name:

    $ bash script.sh
And the output must be:

    $ Hello World!

The other way is by making the file an executable, this method is in order to run it faster but the process is longer (Not that much). To make our file an executable we need to type the next command:

    $ sudo chmod +x script.sh
Doing this now we can run our script by simply typing in the terminal:

    $ ./script.sh

And the output should be:

    $ Hello World!

## Variables
Now we know how to start a script and how to print text we can also make variables.

    #!/bin/bash
    
    greetings="Welcome"
    user="Chuxo"
    
    echo "$greetings back $user!"
And the output should be:
 
    $ Welcome back Chuxo!
## Input Variables
Another way to make variables is by setting them as an input. Which means that this variables arent set by default, you only set them once you running your script.

    #!/bin/bash
    
    echo "Enter your name:"
    read name
    echo "Welcome $name!"
And the output must be:

    Enter your name:
    Chuxo
    Welcome Chuxo!
You can also be able to alter the behavor of the command `read` by simply adding flags (You can find more on the man page). Two most commonly used options however are `-p` which allows you to specify a prompt and `-s` which makes the input silent. This can make it easy to ask for a username and password combination like the example below:

    !#/bin/bash
    
    read -p 'Username:' uservar
    read -sp 'Password:' passvar
    echo
    echo "You are loged in"
And the output would be:

    Username: Chuxo
    Password:
    You are loged in
## Add comments to your scripts
Now that you will start working with many kinds of methods you can start adding comments between your script to give yourself a clue about whats going on. To make a coment just add a `#` before the line and you cant type whatever you want without interrupting your script.

    #!/bin/bash
    
    #this comment wont appear in the terminal
    echo "Hello World"
And the output will be:
    
    $ Hello World
## Functions
Now we can start using functions.

    #!/bin/bash

    function greetings {
            echo "Hello world!"
    }

    greetings

The output:

    $ Hello world!

## Math
This is isn't that bad as it sounds.

How to sum variables?
    
    #!/bin/bash
    
    a=100
    b=100
    echo $((a + b))
Output:

    $ 200
Number Comparison

    #!/bin/bash
    
    num_a=100
    num_b=100
    
    echo "is $num_a equal to $num_b ?"
    echo $
Output:

    $ True
