Bash Battle Arena



**Script One:**

Combines directory creation, file manipulation, conditional checks, and file listing into one script.



\#!/bin/bash



mkdir battlefield

touch battlefield/knight.txt battlefield/sorcerer.txt battlefield/rogue.txt



if \[ -f "battlefield/knight.txt" ]; then

&#x20;   mkdir -p archive

&#x20;   mv battlefield/knight.txt archive/

&#x20;   echo "knight.txt has been moved to archive."

else

&#x20;   echo "knight.txt not found."

fi



echo "contents of battlefield:"

ls battlefield



echo "contents of archive:"

ls archive



Running the script after gaining permission (chmod +x bossbattle.sh)



$ ./bossbattle.sh

mkdir: cannot create directory ‘battlefield’: File exists

knight.txt has been moved to archive.

contents of battlefield:

rogue.txt  sorcerer.txt

contents of archive:

knight.txt



Level 6: Argument Parsing

Mission: Write a script that accepts a filename as an argument and prints the number of lines in that file. If no filename is provided, display a message saying 'No file provided'.

\#!/bin/bash



if \[ -z "$1" ]; then

&#x20; echo "no file provided"

&#x20; exit 1

fi



if \[ ! -f "$1" ];then 

&#x20;   echo "file not found"

&#x20;   exit 1

fi



LINE\_COUNT=$(wc -l < "$1")

echo "The file '$1' has $LINE\_COUNT lines."



Explanation:



$1 represents the first argument passed to the script.



wc -l < "$1" counts the number of lines in the file.



The script first checks if an argument is provided and if the file exists, then counts the lines.



To use the script, we pass in a file as an argument



./6arg.sh test.txt



The script then prints the number of lines in test.txt





Level 7: File Sorting Script

Mission: Write a script that sorts all .txt files in a directory by their size, from smallest to largest, and displays the sorted list.

\#!/bin/bash



DIRECTORY="Arena"



if \[ ! -d "$DIRECTORY" ]; then

&#x20;   echo "Directory does not exist."

&#x20;   exit 1

fi



find "$DIRECTORY" -type f -name "\*.txt" -exec ls -lh {} + | sort -k 5,5 -h | awk '{ print $5, $9 }'



Explanation: 



find "$DIRECTORY" -type f -name "\*.txt" finds all .txt files. 



\-exec option executes the command ls -lh



ls -lh lists files with sizes in human-readable format. 



sort -k 5,5 -h sorts the files by the 5th column (size) in human-readable format.



awk '{ print $5, $9 }' prints the 5th and 9th column, the size and file name to filter the output of the ls command



Level 8: Multi-File Searcher

Mission: Create a script that searches for a specific word or phrase across all .log files in a directory and outputs the names of the files that contain the word or phrase.

\#!/bin/bash



DIRECTORY="Arena"

SEARCH\_TERM="Error"



if \[ ! -d "$DIRECTORY" ]; then

&#x20;   echo "Directory does not exist."

&#x20;   exit 1

fi



grep -l "$SEARCH\_TERM" "$DIRECTORY"/\*.log



Explanation: 



grep -l "$SEARCH\_TERM" "$DIRECTORY"/\*.log searches for the term in each .log file and lists the filenames that contain the term.





Level 9: Script to Monitor Directory Changes

Mission: Write a script that monitors a directory for any changes (file creation, modification, or deletion) and logs the changes with a timestamp.



\#!/bin/bash



DIRECTORY="Arena"

LOG\_FILE="change\_log.txt"



if \[ ! -d "$DIRECTORY" ]; then

&#x20;   echo "Directory does not exist."

&#x20;   exit 1

fi



fswatch -r "$DIRECTORY" | while read event; do

&#x20;   if \[ -e "$event" ]; then

&#x20;       echo "$(date +'%Y-%m-%d %H:%M:%S') File modified/created: $event" >> "$LOG\_FILE"

&#x20;   else

&#x20;       echo "$(date +'%Y-%m-%d %H:%M:%S') File deleted: $event" >> "$LOG\_FILE"

&#x20;   fi

done



Explanation:



fswatch -r "$DIRECTORY" watches the directory recursively for changes.



Distinguish between events:



if \[ -e "$event" ]: Checks if the file still exists.



If the file exists, we assume it's either modified or created.



If the file does not exist, we assume it has been deleted.



The script then logs the event with the exact time and details whether a file was "modified/created" or "deleted."



Level 10 - The script combines skills from Levels 6-9, including file creation, random number generation, sorting, and searching within files.

This script reinforces the concept of using loops, conditionals, and file operations together to solve complex tasks.



\#!/bin/bash



mkdir Arena\_Boss



for i in {1..5}

do

&#x20;   FILE="Arena\_Boss/file$i.txt"

&#x20;   LINES=$((RANDOM % 11 + 10))

&#x20;   for j in $(seq 1 $LINES)

&#x20;   do

&#x20;       echo "This is line $j" >> "$FILE"

&#x20;   done

done



echo "Files sorted by size:"

find Arena\_Boss -type f -exec ls -lh {} + | sort -k 5,5 -h





mkdir -p Victory\_Archive

for FILE in Arena\_Boss/\*.txt

do

&#x20;   if grep -q "Victory" "$FILE"; then

&#x20;       mv "$FILE" Victory\_Archive/

&#x20;       echo "$FILE contains 'Victory' and has been moved to Victory\_Archive."

&#x20;   fi

done



Level 11: Automated Disk Space Report

Mission: Create a script that checks the disk space usage of a specified directory and sends an alert if the usage exceeds a given threshold.

\#!/bin/bash



DIRECTORY="Arena"

THRESHOLD=1



USAGE=$(du -sm "$DIRECTORY" | awk '{print $1}')



if \[ "$USAGE" -gt "$THRESHOLD" ]; then

&#x20;   echo "Warning: Disk usage for $DIRECTORY is at $USAGE%!"

else

&#x20;   echo "Disk usage for $DIRECTORY is at $USAGE%. All is well."

fi



Explanation:



du -sm "$DIRECTORY" calculates the disk usage of the directory in megabytes (-sm), which is more appropriate for checking the actual size of a small folder.



THRESHOLD=80: You can set this to any value in MB. If you want it in GB, you can modify the script accordingly (e.g., du -sh for human-readable format and use GB in the comparison).



It then compares the size of the directory (USAGE) to the threshold and prints a warning if the threshold is exceeded.



Level 12: Simple Configuration File Parser

Mission: Write a script that reads a configuration file in the format KEY=VALUE and prints each key-value pair.

\#!/bin/bash



CONFIG\_FILE="settings.conf"



if \[ ! -f "$CONFIG\_FILE" ]; then

&#x20;   echo "Configuration file does not exist."

&#x20;   exit 1

fi



while IFS='=' read -r key value; do

&#x20;   echo "Key: $key, Value: $value"

done < "$CONFIG\_FILE"



Explanation: 



IFS='=' sets the internal field separator to = - splitting when it sees equal



The script reads each line of the configuration file, splits it into key and value, and prints them.



Level 13: Backup Script with Rotation

Mission: Create a script that backs up a directory to a specified location and keeps only the last 5 backups.

\#!/bin/bash



SOURCE\_DIR="Arena"

BACKUP\_DIR="Backups"



mkdir -p "$BACKUP\_DIR"



TIMESTAMP=$(date +"%Y-%m-%d\_%H-%M-%S")

BACKUP\_NAME="backup\_$TIMESTAMP.tar.gz"

tar -czf "$BACKUP\_DIR/$BACKUP\_NAME" "$SOURCE\_DIR"

echo "Created backup: $BACKUP\_NAME"



cd "$BACKUP\_DIR" || exit

ls -t | sed -e '1,5d' | while IFS= read -r file; do

&#x20;   rm -f "$file"

done



Explanation: 



tar -czf "$BACKUP\_DIR/$BACKUP\_NAME" "$SOURCE\_DIR" creates a compressed backup. 



ls -t | sed -e '1,5d': This lists the files in the backup directory, sorted by modification time, and removes the first 5 lines from the output, which are the most recent files.



while IFS= read -r file; do rm -f "$file"; done: This loop safely reads each file name (handling spaces or newlines) and deletes the files.





Level 14: User-Friendly Menu Script

Mission: Create an interactive script that presents a menu with options for different system tasks (e.g., check disk space, show system uptime, list users), and executes the chosen task.



\#!/bin/bash



echo "Choose an option:"

echo "1. Check disk space"

echo "2. Show system uptime"

echo "3. List users"



read -rp "Enter your choice \[1-3]: " choice



case $choice in

&#x20;   1) df -h ;;

&#x20;   2) uptime ;;

&#x20;   3) cut -d: -f1 /etc/passwd ;;

&#x20;   \*) echo "Invalid option" ;;

esac



Explanation: 



The script presents a menu and reads the user's choice. 



case matches the user's input to the corresponding command.



Level 15 - This script combines conditional logic, file operations, menu systems, and backup management into a comprehensive script.

Challenge reinforces the key concepts you learned in Levels 11-14, testing your ability to integrate these concepts into a single, functional script.



\#!/bin/bash



echo "Choose an option:"

echo "1. Check disk space"

echo "2. Show system uptime"

echo "3. Backup Arena directory"

echo "4. Parse configuration file"



read -rp "Enter your choice \[1-4]: " choice





case $choice in

&#x20;   1)

&#x20;       df -h

&#x20;       ;;

&#x20;   2)

&#x20;       uptime

&#x20;       ;;

&#x20;   3)

&#x20;       SOURCE\_DIR="Arena"

&#x20;       BACKUP\_DIR="Backups"



&#x20;       mkdir -p "$BACKUP\_DIR"



&#x20;       TIMESTAMP=$(date +"%Y-%m-%d\_%H-%M-%S")

&#x20;       BACKUP\_NAME="backup\_$TIMESTAMP.tar.gz"

&#x20;       tar -czf "$BACKUP\_DIR/$BACKUP\_NAME" "$SOURCE\_DIR"

&#x20;       echo "Created backup: $BACKUP\_NAME"



&#x20;       cd "$BACKUP\_DIR" || exit

&#x20;       ls -t | sed -e '1,5d' | while IFS= read -r file; do

&#x20;           rm -f "$file"

&#x20;       done

&#x20;       ;;

&#x20;   4)

&#x20;       CONFIG\_FILE="settings.conf"

&#x20;       if \[ ! -f "$CONFIG\_FILE" ]; then

&#x20;           echo "Configuration file does not exist."

&#x20;           exit 1

&#x20;       fi

&#x20;       while IFS='=' read -r key value; do

&#x20;           echo "Key: $key, Value: $value"

&#x20;       done < "$CONFIG\_FILE"

&#x20;       ;;

&#x20;   \*)

&#x20;       echo "Invalid option"

&#x20;       ;;

esac

