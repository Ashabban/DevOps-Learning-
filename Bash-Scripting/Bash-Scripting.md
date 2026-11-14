**Bash-Scripting**



**What is Bash Scripting?**



Bash: A command-line tool to interact with your computer.



Bash Script: A file containing a series of commands you want the computer to execute automatically.



**Why Learn It?**



Automate tasks: Save time on repetitive actions.



Manage systems: Handle files, software installs, and system configurations.



Boost efficiency: Get more done with less typing!





**Basics in Scripting:**



Shebang or hashbang - #! (how you start every bash script)



In Vim command after creating a file using the touch command you then enter #!/bin/bash followed by your script



/bin/bash this is the specific SHELL or Interpreter that should handle the script



You must give permission chmod to make your script executable



To run the in the three ways:



1. ./scriptname
2. sh scriptname
3. bash scriptname





**Comments in scripts:**

information on what the script is to help with understanding.



You add comment using 'i' in vim text editor



\#These comments are not executable through the following.



For single comments you enter # followed by your comment



For multiline comments you enter : 'complete all your lines then conclude with quotation mark'





**Running scripts from ANYWHERE:**



**You use the sudo mv command to complete this e.g.**



1. sudo mv greet.sh /usr/local/bin/**greet** - moved file to the following PATH and changed name to greet
2. sudo chmod +x /usr/local/bin/greet



Now you can run 'greet' from any directory





**Variables \& Parameters:**



***Variables*** are created using the assignment operator equals (=) to access the value of a variable, we propend the name of the variable with a dollar sign ($)



Example - greeting="hello world" -> echo $greeting



Variables can hold different types of data, such as strings, numbers, and arrays. And variable interpolation allows you to use variables within strings to create dynamic output.



Example - name="ahmed" -> echo "hello, $name"



***Parameters*** - Bash scripts can receive input values, known as parameters or arguments from the command line when they are executed. These parameters allow you to customize the behavior of your script and make it more flexible.



You execute parameters by adding them to your script e.g. echo "parameter 1: $1" echo "Parameter 2: $2" echo "Parameter 2: $2" or echo "All Parameters: $@"



Parameters are provided after a script name. When executing a script inside the script parameters can be accessed using dollar one, dollar two, dollar three, and so on based on their position.



And the special variable dollar @ can be used to access all the parameters passed to the script. So by allowing inputs through parameters, you can make your script more interactive and versatile.



***Arithmetic expansion basics*** -



Allows us to perform calculations using the values of variables and parameters, which provides a convenient way to incorporate dynamic calculations into our scripts.



Example 1:



\#!/bin/bash



num1=5

num2=10



result=$((num1 + num2))



echo "The sum of $num1 and $num2 is: $result"



Example 2:



\#!/bin/bash



length=5

width=8



area=$((length \* width))

perimeter=$((2 \* (length + width)))



echo "Rectangle Area: $area"

echo "Rectangle Perimeter: $perimeter"



***Adding parameters to Arithmetic expansions*** -



\#!/bin/bash



length="$1"

width="$2"



area=$((length \* width))

perimeter=$((2 \* (length + width)))



echo "Rectangle Area: $area"

echo "Rectangle Perimeter: $perimeter"



chmod +x arithmetic.sh



./arithmetic.sh 8 5 (these numbers have been added into the parameters)



Rectangle area: 40

Rectangle perimeter: 26



**If statements:**



\#!/bin/bash

if condition

then

&#x20;   # code block to be executed

fi (end of statement)



Example conditions:

eq = equals

ne = not equals

lt = less than

gt = greater than

le = less than or equal to

ge = greater than or equal to



Example:

\#!/bin/bash



age=25



if \[ $age -gt 18 ]

then

&#x20;   echo "You are an adult!"

fi



**Logical operators** in bash scripting are used to combine multiple conditions. The most common logical operators are:

1\. \&\& (AND): This operator returns true if both conditions are true. For example:

if \[ $age -gt 18 ] \&\& \[ $age -lt 65 ]

|| (OR): This operator returns true if at least one of the conditions is true. For example:

if \[ $age -lt 18 ] || \[ $age -gt 65 ]



**String comparison operators** in bash scripting are used to compare strings. Some common string comparison operators are:

1\. = : This operator checks if two strings are equal. For example:

if \[ "$name" = "John" ]

2\. != : This operator checks if two strings are not equal. For example:

if \[ "$name" != "John" ]

3\. < : This operator checks if one string is less than another. For example:

if \[\[ "$name" < "John" ]]

4\. > : This operator checks if one string is greater than another. For example:

if \[\[ "$name" > "John" ]]

5\. -z : This operator checks if a string is empty. For example:

if \[ -z "$name" ]

6\. -n : This operator checks if a string is not empty. For example:

if \[ -n "$name" ]



**else and elif** statements in bash scripting are used to create multiple conditional branches. The syntax is as follows:

if \[ condition1 ]

then

&#x20;   # commands to execute if condition1 is true

elif \[ condition2 ]

then

&#x20;   # commands to execute if condition2 is true

else

&#x20;   # commands to execute if none of the above conditions are true

fi



**nested if statements** in bash scripting are used to evaluate multiple conditions within a single if statement.

This allows for more complex decision-making processes in your scripts. Here's an example of how to use nested if statements in a bash script:

\#!/bin/bash

\# Example of nested if statements in bash scripting



age=18

grade=85



\# Check if the age is valid and the grade is passing

if \[ $age -ge 18 ]; then

&#x20;   echo "The age is valid."

&#x20;   if \[ $grade -ge 60 ]; then

&#x20;       echo "The grade is passing."

&#x20;   else

&#x20;       echo "The grade is not passing."

&#x20;   fi

else

&#x20;   echo "The age is not valid."

fi

In this example, the script first checks if the age is greater than or equal to 18.

If this condition is true, it then checks if the grade is greater than or equal to 60.

Depending on the results of these checks, it will print appropriate messages to the console.

If the age is not valid, it will skip the grade check and print that the age is not valid.



**while loops** A while loop in bash scripting is used to execute a block of code repeatedly as long as a specified condition is true. The syntax for a while loop is as follows:



while \[ condition ]
do

commands to be executed

done



example:

\#!/bin/bash

count=1



while \[ $count -le 5 ] (less than or equal to 5)
do
echo "Count: $count"
((count++))
done



example of an array:
#!/bin/bash



fruits=("apple" "banana" "orange")
index=0



while \[ $index -lt ${#fruits\[@]} ]
do
echo "Fruit: ${fruits\[$index]}"
((index++))
done



for loops 

\#!/bin/bash



for variable in sequence 

do

&#x20; echo $variable

done



example:

\#!/bin/bash



for  (( i=1; i<=5; i++ ))

do

&#x20; echo "Number: $i"

done	



