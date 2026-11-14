Bash-Scripting 2



**Functions:**

A function is a named block of code you can call again and again, like a mini script inside your script.

Define it before you call it.



function\_name() {

&#x09;# Function code goes here

}



example:

\#!/bin/bash



hello\_world() {

&#x09;echo "Hello, World!"

}



hello\_world (by entering the function name you run the script



**using parameters:**

greet\_person() {

&#x09;local name="$1"

&#x09;echo "Hello, $name!"

}



greet\_person "Ahmed"

greet\_person "John"



Hello, Ahmed!

Hello, John!



print\_args() {

&#x09;echo "Number of arguments: $#"

&#x09;echo "Arguments: $@" (script name)

&#x09;echo "First argument: $1"

&#x09;echo "Second argument: $2"

&#x09;echo "All arguments: $@"

}



print\_args "Ahmed" "Ali"

Number of arguments: 2

Arguments: Ahmed Ali

First argument: Ahmed

Second argument: Ali

All arguments: Ahmed Ali



**User inputs:**

greet\_user() {

&#x09;echo "what is your name?"

&#x09;read name

&#x09;echo "Hello, $name!"

}



greet\_user

&#x20;

what is your name?

ahmed

Hello, ahmed!



greet() {

&#x09;local name



&#x09;if \[ $# -eq 0 ]; then

&#x09;	echo "what is your name?"

&#x09;	read name

&#x09;else

&#x09;	name="$1"

&#x09;fi



&#x09;echo "Hello, $name!"

}



greet



what is your name?

Ahmed

Hello, Ahmed!



**Handling Bad Data:**

\#!/bin/bash



validate\_age() {

&#x20; local age=$1

&#x20; if \[\[ ! $age =\~ ^\[0-9]+$ ]]; then

&#x09;echo "Invalid age. Please provide a numeric value."

&#x09;return 1

&#x20; fi



&#x20; if (( age < 18 )); then

&#x09;echo "Sorry, you must be at least 18 years old."

&#x09;return 1

&#x20; fi



&#x20; echo "Congratulations! You are eligible."

&#x20;   return 0

}



echo "Please enter your age: "

read user\_age



validate\_age "$user\_age"

exit\_code=$?



if (( exit\_code != 0 )); then

&#x20; echo "Input validation failed."

else

&#x20; echo "Input validation succeeded."

fi



Please enter your age:

17

Sorry, you must be at least 18 years old.

Input validation failed



Please enter your age:

19

Congratulations! You are eligible.

Input validation succeeded.



There is also a function to sanitize user input to remove what is inputted e.g. symbols



**Piping in functions**



**#!/bin/bash**



get\_file\_count() { (Creates a function named get\_file\_count. A function is a reusable block of commands.)

&#x20; local directory=$1 (Creates a variable called directory and stores the function’s first argument in it. local means it belongs to this function.)

&#x20; local file\_count (Declares another local variable to hold the count.)



&#x20; file count=$(ls "$directory" | wc -l) - Lists the visible items inside the chosen directory. Quotation marks keep paths containing spaces together. | Passes the output of the command on the left to the command on the right.

wc -l Counts the number of lines it receives.



&#x20; echo "Number of files in $directory: $file\_count"

}



get\_file\_count "./" -Calls the function, passing ./ as its first argument. ./ means your terminal’s current directory.



Example 2:

search\_log() {

&#x20;   local search\_term="$1"

&#x20;   grep "search\_term" log.txt | awk '{print $2}'

}



search\_log "ERROR"

