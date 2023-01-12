---
title: Shell scripting step by step tutoriala
---

In this tutorial, we are going to talk about shell scripting and how to make your first shell script. They are called shell scripts in general, but we are going to call them Bash scripts because we are going to use Bash among the other Linux shells.

There are zsh, tcsh, ksh, and other shells.

In the previous posts, we saw how to use the Bash shell and how to use [Linux commands](https://likegeeks.com/main-linux-commands-easy-guide/).

The concept of a Bash script is to run a series of Commands to get your job done.

To run multiple commands in a single step from the shell, you can type them on one line and separate them with semicolons.

```
pwd ; whoami
```

This is a Bash script!!

The pwd command runs first, displaying the current working directory, then the whoami command runs to show the currently logged in users.

You can run multiple commands as much as you wish, but with a limit. You can determine your max args using this command.

```
 getconf ARG_MAX
```

Well, What about putting the commands into a file, and when we need to run these commands, we run that file only. This is called a Bash script.

First, make a new file using the [touch command](https://likegeeks.com/basic-linux-commands-part2/#Create-Files). At the beginning of any Bash script, we should define which shell we will use because there are many shells on Linux, Bash shell is one of them.

Shell script shebang
----------

The first line you type when writing a Bash script is the (#!) followed by the shell you will use.

#! <=== this sign is called shebang.

```
#!/bin/bash
```

If you use the pound sign (#) in front of any line in your shell script, this line will become a comment which means it will not be processed, but, the above line is a special case . This line defines what shell we will use, which is Bash shell in our case.

The shell commands are entered one per line like this:

```
#!/bin/bash
# This is a comment
pwd
whoami
```

You can type multiple commands on the same line, but you must separate them with semicolons, but it is preferable to write commands on separate lines; this will make it simpler to read later.

Set script permission
----------

After writing your shell script, save the file.

Now, set that file to be executable; otherwise, it will give you permission denied. You can review how to set permissions using the [chmod command](https://likegeeks.com/main-linux-commands-easy-guide/#chmod-Command).

<img alt="shell script permission" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20654%20127'%3E%3C/svg%3E" height="127" width="654" />

```
chmod +x ./myscript
```

Then try run it by just typing it in the shell:

```
./myscript
```

And Yes, it is executed.

<img alt="shell scripting tutorial" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20657%20151'%3E%3C/svg%3E" height="151" width="657" />

Make your first Bash script
----------

As we know from other posts, printing text is don using the

```
echo
```

command.

Edit your file and type this:

```
#!/bin/bash
# our comment is here
echo "The current directory is:"
pwd
echo "The user logged in is:"
whoami
```

Look at the output:

<img alt="echo command" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20656%20161'%3E%3C/svg%3E" height="161" width="656" />

Perfect! Now we can run commands and display text:

```
echo
```

If you don’t know the echo command or how to edit a file, I recommend you to view previous articles about [basic Linux commands](https://likegeeks.com/basic-linux-commands-part2/).

Using variables
----------

Variables allow you to store information to use it in your script.

You can define two types of variables in your shell script:

* Environment variables
* User variables

### Environment variables ###

Sometimes you need to interact with system variables; you can do this by using [environment variables](https://likegeeks.com/linux-environment-variables/).

```
#!/bin/bash
# display user home

echo "Home for the current user is: $HOME"
```

Notice that we put the $HOME system variable between double quotations, and it prints the home variable correctly.

<img alt="global variables" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20658%20105'%3E%3C/svg%3E" height="105" width="658" />

What if we want to print the dollar sign itself?

```
echo "I have $1 in my pocket"
```

Because variable $1 doesn’t exist, it won’t work. So how to overcome that?

You can use the escape character, which is the backslash \\ before the dollar sign like this:

```
echo "I have \$1 in my pocket"
```

Now it works!!

<img alt="escape dollar sign" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20659%20100'%3E%3C/svg%3E" height="100" width="659" />

### User variables ###

Also, you can set and use your custom variables in the script.

You can call user variables in the same way as this:

```
#!/bin/bash
# User variables
grade=5
person="Adam"
echo "$person is a good boy, he is in grade $grade"
```

```
chmod +x myscript

./myscript
```

<img alt="user variables" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20660%20100'%3E%3C/svg%3E" height="100" width="660" />

Command substitution
----------

You can extract information from the result of a command using command substitution.

You can perform command substitution with one of the following methods:

* The backtick character (`).
* The $() format.

Make sure when you type backtick character, it is not the single quotation mark.

You must enclose the command with two backticks like this:

```
mydir=`pwd`
```

Or the other way:

```
mydir=$(pwd)
```

So the script could be like this:

```
#!/bin/bash

mydir=$(pwd)

echo $mydir
```

You can store the output of the command in the mydir variable.

<img alt="command substitution" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20655%20103'%3E%3C/svg%3E" height="103" width="655" />

Math calculation
----------

You can perform basic math calculations using $(( 2 + 2 )) format:

```
#!/bin/bash
var1=$(( 5 + 5 ))
echo $var1
var2=$(( $var1 * 2 ))
echo $var2
```

Just that easy.

<img alt="Bash scripting math" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20655%20122'%3E%3C/svg%3E" height="122" width="655" />

if-then statement
----------

Your shell scripts will need conditional statements. Like if the value is smaller than 10, do this else do that. You can imagine any logic you want.

The most basic structure of the if-then statement is like this:

if command; then

do something

fi

and here is an example:

```
#!/bin/bash
if whoami; then
	echo "It works"
fi
```

Since the

```
whoami
```

will return my user so the condition will return true, and it will print the message.

Let’s dig deeper and use other commands we know.

### Check if a user exists ###

Maybe searching for a specific user in the user’s file

```
/etc/passwd
```

and if a record exists, tell me that in a message.

```
#!/bin/bash
user=likegeeks
if grep $user /etc/passwd; then
	echo "No such a user $user"
fi
```

<img alt="if-else" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20657%20141'%3E%3C/svg%3E" height="141" width="657" />

We use the

```
/etc/passwd
```

file. You can check our tutorial about the[ grep command](https://likegeeks.com/grep-command-in-linux/).

If the user exists, the shell script will print the message.

What if the user doesn’t exist? The script will exit the execution without telling us that the user doesn’t exist. OK, let’s improve the script more.

if-then-else statement
----------

The if-then-else statement takes the following structure:

if command; then

do something

else

do another thing

fi

If the first command runs and returns zero, which means success, it will not hit the commands after the else statement; otherwise, if the if statement returns non-zero; which means the statement condition fails, in this case, the shell will hit the commands after else statement.

```
#!/bin/bash
user=anotherUser
if grep $user /etc/passwd; then
	echo "The user $user Exists"
else
	echo "The user $user doesn’t exist"
fi
```

<img alt="bash script if-else" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20655%20103'%3E%3C/svg%3E" height="103" width="655" />

We are doing good till now, keep moving.

Now, what if we need more else statements.

Well, that is easy, we can achieve that by nesting if statements like this:

if condition1; then

commands

elif condition2; then

commands

fi

If the first command return zero; means success, it will execute the commands after it, else if the second command return zero, it will run the commands after it, else if none of these return zero, it will execute the last commands only.

```
#!/bin/bash
user=anotherUser
if grep $user /etc/passwd; then
	echo "The user $user Exists"
elif ls /home; then
	echo "The user doesn’t exist"
fi
```

You can imagine any scenario, maybe if the user doesn’t exist, create a user using the

```
useradd
```

command or do anything else.

Combine tests
----------

You can combine multiple tests using AND (&&) or OR (||) command.

```
#!/bin/bash
dir=/home/likegeeks
name="likegeeks"
if [ -d $dir ] && [ -n $name ]; then
	echo "The name exists and the folder $dir exists."
else
	echo "One test failed"
fi
```

This example will return true only if both tests succeeded; otherwise, it will fail.

Also, you can use OR (||) the same way:

```
#!/bin/bash
dir=/home/likegeeks
name="likegeeks"
if [ -d $dir ] || [ -n $name ]; then
	echo "Success!"
else
	echo "Both tests failed"
fi
```

This example would return success if one or both of them succeeded.

It would fail only if both of them failed.

Numeric comparisons
----------

You can perform a numeric comparison between two numeric values using numeric comparison checks like this:

number1 -eq number2 Checks if number1 is equal to number2.

number1 -ge number2 Checks if number1 is bigger than or equal number2.

number1 -gt number2 Checks if number1 is bigger than number2.

number1 -le number2 Checks if number1 is smaller than or equal number2.

number1 -lt number2 Checks if number1 is smaller than number2.

number1 -ne number2 Checks if number1 is not equal to number2.

As an example, we will try one of them, and the rest is the same.

Note that the comparison statement is in square brackets as shown.

```
#!/bin/bash
num=11
if [ $num -gt 10]; then
	echo "$num is bigger than 10"
else
	echo "$num is less than 10"
fi
```

<img alt="numeric compare" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20658%2095'%3E%3C/svg%3E" height="95" width="658" />

The num is greater than ten, so it will run the first statement and print the first echo.

String comparisons
----------

You can compare strings with one of the following ways:

string1 = string2 Checks if string1 identical to string2.

string1 != string2 Checks if string1 is not identical to string2.

string1 < string2 Checks if string1 is less than string2.

string1 > string2 Checks if string1 is greater than string2.

\-n string1 Checks if string1 longer than zero.

\-z string1 Checks if string1 is zero length.

We can apply a string comparison to our example:

```
#!/bin/bash
user="likegeeks"
if [ $user = $USER ]; then
	echo "The user $user&nbsp; is the current logged in user"
fi
```

<img alt="string compare" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20656%20118'%3E%3C/svg%3E" height="118" width="656" />

One tricky note about the **greater than and less than** for string comparisons, they **MUST** be **escaped with the backslash** because if you use the greater-than symbol only, it shows wrong results.

So you should do it like that:

```
#!/bin/bash
v1=text
v2="another text"
if [ $v1 \> "$v2" ]; then
	echo "$v1 is greater than $v2"
else
	echo "$v1 is less than $v2"
fi
```

<img alt="string greater than" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20658%20120'%3E%3C/svg%3E" height="120" width="658" />

It runs, but it gives this warning:

```
./myscript: line 5: [: too many arguments
```

To fix it, wrap the $vals with a double quotation, forcing it to stay as one string like this:

```
#!/bin/bash
v1=text
v2="another text"
if [ $v1 \> "$v2" ]; then
	echo "$v1 is greater than $v2"
else
	echo "$v1 is less than $v2"
fi
```

<img alt="string fix" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20657%20103'%3E%3C/svg%3E" height="103" width="657" />

A critical note about **greater than and less than** for string comparisons. Check the following example to understand the difference:

```
#!/bin/bash
v1=Likegeeks
v2=likegeeks
if [ $v1 \> $v2 ]; then
	echo "$v1 is greater than $v2"
else
	echo "$v1 is less than $v2"
fi
```

<img alt="character case" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20657%20124'%3E%3C/svg%3E" height="124" width="657" />

```
sort myfile
```

likegeeks

Likegeeks

<img alt="sort order" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20661%20157'%3E%3C/svg%3E" height="157" width="661" />

The test condition considers the lowercase letters bigger than capital letters.

```
sort
```

Unlike sort command, which does the opposite.

The test condition is based on the ASCII order.

```
sort
```

While the sort command is based on the numbering orders from the system settings.

File comparisons
----------

You can compare and check for files using the following operators:

\-d my\_file Checks if its a folder.

\-e my\_file Checks if the file is available.

\-f my\_file Checks if its a file.

\-r my\_file Checks if it’s readable.

my\_file **–**nt my\_file2 Checks if my\_file is **newer** than my\_file2.

my\_file **–**ot my\_file2 Checks if my\_file is **older** than my\_file2.

\-O my\_file Checks if the owner of the file and the logged user match.

\-G my\_file Checks if the file and the logged user have an identical group.

As they imply, you will never forget them.

Let’s pick one of them and take it as an example:

```
#!/bin/bash
mydir=/home/likegeeks
if [ -d $mydir ]; then
	echo "Directory $mydir exists"
	cd $mydir
	ls
else
	echo "NO such file or directory $mydir"
fi
```

<img alt="file checking" src="data:image/svg+xml,%3Csvg%20xmlns='http://www.w3.org/2000/svg'%20viewBox='0%200%20654%20139'%3E%3C/svg%3E" height="139" width="654" />

We are not going to type every one of them as an example. You just type the comparison between the square brackets as it is and complete your script normally.

There are some other advanced if-then features, but let’s make it in another post.

That’s for now. I hope you enjoy it and keep practicing more and more.

Thank you.

Mokhtar is the founder of LikeGeeks.com. He works as a Linux system administrator since 2010. He is responsible for maintaining, securing, and troubleshooting Linux servers for multiple clients around the world. He loves writing shell and Python scripts to automate his work.