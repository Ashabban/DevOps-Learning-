Bash-Scripting 3



**Error Handling:**

\#!/bin/bash



num1=10

num2=0

result=$((num1 / num2))



echo "The result is: $result"



line 5: num1 / num2: division by 0 (error token is "num2")

The result is:



\#!/bin/bash



num1=10

num2=0



if \[ $num2 -eq 0 ]; then

&#x20;   echo "Error: Division by zero is not allowed."

&#x20;   exit 1

fi



result=$((num1 / num2))



echo "The result is: $result"



Error: Division by zero is not allowed.



**The above script was corrected by adding an if statement to check whether num2 is zero and exit with an error message before attempting division.**



**If statements recap**

\#!/bin/bash



FILE="/nonexistent"



if \[\[ -f "$FILE" ]]; then

&#x20;   echo "File exists."

else

&#x20;   echo "File does not exist."

fi

File does not exist.



**Exit Codes**



You can check exit status through the **echo $?** command



0 indicates success



a non-zero exit code i.e. 1 or more indicates an error



\#!/bin/bash



command -v git 2>/dev/null



if \[\[ $? -ne 0 ]]; then

&#x20;   echo "Git is not installed. Please install Git to continue."

&#x20;   exit 1

else

&#x20;   echo "Git is installed."

fi



Git is installed.



**SAFTEY SWITCHES**

**set -e**



**Normally, Bash continues running after a failed command. Adding set -e helps prevent later commands from running after something goes wrong.**



**example -**



\#!/bin/bash



set -e



echo "before the script"



nonexistantcommand



echo "after the script"



before the script



c:\\Users\\ahmed\\Desktop\\Bash Practice\\practice.sh: line 7: nonexistantcommand: command not found



So bash stopped at the second command which is where there was an error.



**set -u** tells Bash to report an error and stop the script if you try to use a variable that has not been defined.



Without set -u, an undefined variable usually expands to an empty value:



set -u



echo "the value of variable X is : $X"



line 5: X: unbound variable



example 2:

set -u



X=10

Y=20

Z=$(( X + Y + **W** ))

echo "z equals: $Z"



line 7: W: unbound variable



**set -x** makes Bash print each command, with variables expanded, before running it. This helps you **debug a script** by seeing what it is doing.



\#!/bin/bash

set -x



name="Ahmed"

echo "Hello $name"



\+ name=Ahmed

\+ echo 'Hello Ahmed'

Hello Ahmed



Lines starting with + show the commands being executed.

Hello Ahmed is the actual output from echo.

Use set +x to turn tracing off.



set -x



echo "this is a test."

x=10

echo "the value of x is $x"



\+ echo 'this is a test.'

this is a test.

\+ x=10

\+ echo 'the value of x is 10'

the value of x is 10



set -x



echo "starting the script"

X=10

Y=20

Z=$((X + Y))

echo "The value of Z is: $Z"



starting the script

\+ X=10

\+ Y=20

\+ Z=30

\+ echo 'The value of Z is: 30'

The value of Z is: 30



**set -eux** enables three Bash options together to help catch errors and debug your script.



\#!/bin/bash



set -eux



echo "this is a test script"



echo "the value of X is $X"



nonexistentcommand



\+ echo 'this is a test script'

this is a test script

c:\\Users\\Ahmed\\Desktop\\Bash Practice\\practice.sh: line 7: X: unbound variable



***More set commands***



**set -o** **nounset** is the longer form of set -u. Both make Bash report an error and stop the script when you use an undefined variable.



**set -o errexit** is the longer form of set -e. It tells Bash to stop the script when a command fails with a non-zero exit status



**set -o pipefail** makes a pipeline report failure if any command in it fails. A pipeline connects commands using |.



\#!/bin/bash



set -o pipefail



cat nonexistentfile | grep "something"



$ /bin/bash "c:\\Users\\Ahmed\\Desktop\\Bash Practice\\practice.sh"

cat: nonexistentfile: No such file or directory

