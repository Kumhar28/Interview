# Most asked shell scripts
## Odd/ Even numver
```bash
#!/bin/bash
echo -n "Enter a number:"
read n
echo -n "RESULT: "
if [ `expr $n % 2` == 0 ]
then
	echo "$n is even"
else
	echo "$n is Odd"
fi
```
### Palindrome or Not
```bash
#!/bin/bash

read -p “Enter a string: ” input_string

# Reverse the string and compare with the original

if [[ “$input_string” == “$(rev <<< “$input_string”)” ]]; then
echo “The entered string ‘$input_string’ is a palindrome.”
else
echo “The entered string ‘$input_string’ is not a palindrome.”
fi

```
### febonacci

```bash

echo  "Enter the number:"
read num
clear # to clear the input from terminal
# Initial Values 
# First Number of the
# Fibonacci Series
a=0
 
# Second Number of the
# Fibonacci Series
b=1 
  
echo "The Fibonacci series is : "
  
for (( i=0; i<num; i++ ))
do
    echo -n "$a "
    fn=$((a + b))
    a=$b
    b=$fn
done


################################################


#!/bin/bash

echo  "Enter the number:"
read num
clear # to clear the input from terminal
# Initial Values
a=0
b=1
while [ `expr $a + $b` -le $num ]
do 
    c=`expr $a + $b`
echo $c
a=$b
b=$c
done
```
## prime or not 
- is divide by ony 1 that number is prime number
- 6 not prime number 6/2, 6/3, 6/1, 6/6.  So its non prime number (n-1) 

```bash

#!/bin/bash
echo -e "Enter Number : \c"
read n
for((i=2; i<=$n/2; i++))
do
# if the remainder of a certain value divided by 2 would be zero, then the condition would be fulfilled
  ans=$(( n%i ))
  if [ $ans -eq 0 ]
  then
    echo "$n is not a prime number."
    exit 0
  fi
done
echo "$n is a prime number."
```
### factorial of a number
- A function that multiplies a number by every number below it till 1

```bash
echo "Enter a number"
read num                     
fact=1                    
for((i=2;i<=num;i++))
{
  fact=$((fact * i)) 
}

echo $fact

```
### Check service active or not
```bash
#!/bin/bash
result=$(systemctl is-active cassandra)
if [ "${result}" = "active"  ]; then
  echo "Cassandra is running..."
else
  usermod -s /bin/bash cassandra
  systemctl restart cassandra
  echo "Cassandra was not running..."
fi
```
## Run command on remote hosts
```bash
#!/usr/bin/bash
date=`date '+%d'`
for i in `cat /export/home/ss0747/scripts/hosterror`; do
ssh $i "uname -a;date;echo;/usr/local/bin/sudo tail -100 /var/adm/messages | egrep 'error|warning' | grep $date; uname -a;echo;echo;echo;echo;echo"
done

## You can add the StrictHostKeyChecking=no option to ssh:
## ssh -o StrictHostKeyChecking=no -l username hostname "pwd; ls"
```
## archive

```bash
#!/bin/bash

echo "Archiving $1"
tar -czvf scripts.tar.gz $1

echo "Moving the archive to $2"
mv scripts.tar.gz $2

echo "Backup of $1 completed"
```
----------------------------------
## script to check if a file exists on the system?
```bash
if [-f /var/www/html]
then 
echo “file exists”
fi
```
## check if a directory exists?
```bash
#!/bin/sh

if [ -d $mydir ]
then
echo "Directory exists"
fi
```
----------------------------

## script to compare numbers
```bash
#!/bin/bash
X=10
Y=20
if [ $x –gt $y ]
then 
echo “ x is greater than y”
else 
echo “y is greater than x”
fi
```
-----------------------

----------------------------
## print PID of the current shell
```bash
#!/bin/sh

for PID in $$
do
echo $PID
done
```
----------------------
## print all array elements and their respective indexes?
```bash
!/bin/sh
array=("This" "is" "Shell" "Scripting")
echo ${array[@]}
echo ${!array[@]}
```
------------------------
# print the first array element
```bash
#!/bin/sh
array=("This" "is" "Shell" "Scripting" )
echo ${array[0]}
```
-------------------------
## a shell script to get current date, time, user name and current working directory
```bash
#!/bin/sh
echo "Hello, $LOGNAME"
echo "Today's date is `date`"
echo "Username is `who i am`"
echo "Current directory is `pwd`"
```
-----------------------------------------
# Print a given number, in reverse order using a Shell script such that the input is provided using command Line Argument only
```bash
#!/bin/sh
if [ $# -ne 1 ]
then
echo "Usage: $0 number"
echo " Reverse of the given number will be printed"
echo " For eg. $0 0123, 3210 will be printed"
exit 1
fi

n=$1
rev=0
sd=0

while [ $n -gt 0 ]
do
sd=`expr $n % 10`
rev=`expr $rev * 10 + $sd`
n=`expr $n / 10`
done
```
---------------------------------------------------------
### we pass arguments to a script in Linux
```bash
#!/bin/bash
# Call this script with at least 3 parameters
echo "First parameter is $1"
echo "Second parameter is $2"
echo "Third parameter is $3"
exit 0
```
- # sh parameters.sh 50 51 52

------------------------------------------------------
#### differences between $* and $@?

- $* treats all the arguments as a single entity and doesn’t preserve whitespace or quote characters.
- $@ treats each argument as a separate entity while it ensures to preserve the whitespace and quotes.

--------------------------------------------------------
### While loop
```bash
#!/bin/bash

COUNT=0
while [ $COUNT -lt 10 ]; do
    echo The counter value is $COUNT
    let COUNT+=1
done
```
------------------------

----
## $? 
- represents the exit status of the previous command
- As a rule, most commands return an exit status of 0 if they were successful, and 1 if they were unsuccessful.
```
echo "$?"
```
## tr command
- The tr command is a UNIX command-line utility for translating or deleting characters. 

## cut command
- The cut command in UNIX is a command for cutting out the sections from each line of files and writing the result to standard output. 
- It can be used to cut parts of a line by byte position, character and field.

## paste command
- Paste command is one of the useful commands in Unix or Linux operating system. 
- It is used to join files horizontally (parallel merging) by outputting lines consisting of lines from each file specified, separated by tab as delimiter, to the standard output.
-----
### run script in debug mode
https://tldp.org/LDP/Bash-Beginners-Guide/html/sect_02_03.html

```
set -x			# activate debugging from here
w
set +x			# stop debugging from here
```

### rsync vs cp
- rsync can be used to sync files remotely(machine to machine) while cp is only used to copy files from one directory to another on a single machine
- cp will copy (cp) all files every time
- rsync will only copy changed files

### find text in a file linux
```
grep -Rnw '/path/to/somewhere/' -e 'pattern'
```
```
-r or -R is recursive ; use -R to search entirely
-n is line number, and
-w stands for match the whole word.
-l (lower-case L) can be added to just give the file name of matching files.
-e is the pattern used during the search

```
## AWK Scripting
- Its a text processing
- AWK as a command
- Find and replace the text
- NR = number record
- NF = Number field
- Syntax

```bash
awk options 'pattern {action}' file
command | awk options 'pattern {action}'
```
- Options
  - -F :- seperate filed seperation
  ```bash
  awk -F : '{print $1}' /etc/passwd
  ```  

## sed Scripting
- Stream editor
- Viewing, searching, find and replace, insertion ar deletion file content

### Viewing
```bash

```
### searching 
```bash

```

###  find and replace
```bash
sed 's/root/raju/' demo.txt
sed 's/root/raju/g' demo.txt # g for globallly means all content
sed -i 's/root/raju/g' demo.txt # replace in file 
sed -i.back 's/root/raju/g' demo.txt # replace in file and take backup
```

### insertion ar deletion
```bash

```