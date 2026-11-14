Bash-Scripting 4



**Environmental Variables** 



**The path environment variable is a critical system variable that specifies the directories where the shell should look for executable files.**



**To add a script to the PATH variable you do the following:**



1. create a directory e.g. my\_scripts 

2\. Create a script and edit through - vim my\_scripts/hello\_world.sh

3\. Change executable permissions - chmod +x my\_scripts/hello\_world.sh

4\. echo "export PATH=$PATH:\~/my\_scripts" >> \~/.bashrc or .zshrc

5\. reload the shell - source \~/.bashrc or .zshrc



now the script can run from any directory. 



**Reading environmental variables:**



\#!/bin/bash



echo "Home directory: $HOME"

echo "Current user: $USER"

echo "OS Type: $OSTYPE"



local variables example:



\#!/bin/bash



my\_home= "$HOME"

my\_user= "$USER"

my\_os= "$OSTYPE"





echo "Home directory: $my\_home"

echo "Current user: $my\_user"

echo "OS Type: $my\_os"



**Standard Environment Variables:**



They provide information that can help us create more robust and adaptable batch scripts.



\#!/bin/bash



echo "Username: $LOGNAME"

echo "Shell: $SHELL"

echo "Current Directory: $PWD"

echo "Executable Paths: $PATH"

echo "Default Language: $LANG"



**Reading Files:**



Reading files is an important task in scripting. It allows us to access and extract valuable information from various types of files.



example 1:



\#!/bin/bash



read\_file() {

&#x20;   local file\_path="$1"

&#x20;   while IFS= read -r line; do

&#x20;       echo "$line"

&#x20;   done < "$file\_path"

}



read\_file "./log.txt"



example 2:

process\_files() {

&#x20;   local file\_path="$1"



&#x20;   cat "$file\_path" | while read -r line; do

&#x20;       echo "Processing line: $line"

&#x20;       # Additional processing logic here

&#x20;   done

}



process\_files "./log.txt"



**The while loop can be used to read files line by line, and process their content. And the cat command can also be used to read the content of a file and pipe it for further processing.**



**Writing Files:**



Writing files allows us to create, modify, and store information in various formats.



\#!/bin/bash



write\_to\_file() {

&#x20;   local file\_path="$1"

&#x20;   local data="$2"

&#x20;   echo "$data" > "$file\_path"

}



write\_to\_file "read.txt" "Hello, World!"

$ /bin/bash "c:\\Users\\ahmed\\Desktop\\Bash Practice\\practice.sh"



$ cat read.txt

Hello, World!



**File Checksums:**



File Checksums are cryptographic hashes that provide a unique fingerprint for a file which allows us to verify the authenticity of the file.



Every file has a file Checksum that is different from another file.



\#!/bin/bash



calculate\_md5sum() {

&#x20;   local file\_path="$1"

&#x20;   md5sum "$file\_path"



}



calculate\_md5sum "read.txt"



bea8252ff4e80f41719ea13cdf007273 \*read.txt



or



\#!/bin/bash



calculate\_sha256sum() {

&#x20;   local file\_path="$1"

&#x20;   sha256sum "$file\_path"

}



calculate\_sha256sum "read.txt"



c98c24b677eff44860afea6f493bbaec5bb1c4cbb209c6fc2bbb47f66ff2ad31 \*read.txt



File Checksums are especially useful when we need to compare the integrity of a file over time or across different systems so we can use it.



\#!/bin/bash



compare\_checksums() {

&#x20;   local checksum1="$1"

&#x20;   local checksum2="$2"



&#x20;   if \[\[ "$checksum1" == "$checksum2" ]]; then

&#x20;       echo "Checksums match. File is intact."

&#x20;   else

&#x20;       echo "Checksums do not match. File may be corrupted."

&#x20;   fi

}



compare\_checksums "123" "1234"



Checksums do not match. File may be corrupted.



