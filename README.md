# Bash-Basics

**Types of Shells:**

- **Bourne Shell (sh):** The original Unix shell, developed by Stephen Bourne.
- **C Shell (csh):** Known for its C-like syntax, popular for interactive use.
- **Korn Shell (ksh):** Combines features of sh and csh, offering advanced scripting capabilities.
- **Bash (Bourne Again SHell):** An improved version of sh, with additional features like command history and tab completion.

- Bash stands for Bourne Again SHell
- Actually this is the **default login shell** for most of the Linux distros and macOS.

>[!Note]
>An OS Shell is a computer program that provides relatively broad and direct access to the system.
>Most shells are command line interfaces(CLI) while there are graphical user interfaces as well (GUI).
- To use Bash in command prompt use `ssh root@<ipaddress>` for cloud or remote servers.


## Exercise 1 (Bash Script)

- To check is this bash : `which $SHELL`
- To create a simple file using bash : `nano <filename>` ex. nano himom.sh
- Shell file signature: `#!/bin/bash` (shebang)
- Simple bash file
	```bash
	#!/bin/bash
	
	name="Patricia"
	
	echo "Hi mom"
	sleep 3
	echo "Sleep mom"
	sleep 3
	echo "Get up mom"
	sleep 3
	echo "Love you mom"
	
	echo Hi I'm $name
	```
- To execute the bash file: `bash <filename>` ex. bash himom.sh or `./<filename>` ex: ./himom.sh
>[!Important]
>Make sure the file has execute permission. Unless execute `chmod +x <filename>`

## Exercise 2

- Create the same with name as a variable instead of hardcoded each line. `$name`
- Modified the above with name as input
```bash
$!/bin/bash

echo "Enter your name!"
read name

echo "Hi $name"
sleep 1
echo "You look great today!"
sleep 1
echo "Have a great day $name!"
```

- Modified above with a positional parameter (aka Argument)
```bash
$!/bin/bash

name=$1

echo "Hi $name"
sleep 1
echo "You look great today!"
sleep 1
echo "Have a great day $name!"
```
>[!Note]
>When execute the file pass name along with it.

## Exercise 3 (Built in variables and custom varibles)

- Create a file named `getrichquick.sh` taking name and age as input and echo name and age as output.
```bash
$!/bin/bash

echo "Enter your name"
read name
echo "Enter your age"
read age

echo "Hi $name, you are $age years old."
```

- Bash built in variables. $PWD, $HOSTNAME, $WHOAMI, $RANDOM, $SHELL, $USER etc.
- Create a file including built in variables in it.
```bash
#!/bin/bash


echo "Enter your name"
read name

echo "Enter your age"
read age


echo Hello, $name, you are $age years old!.


echo Hello $USER. You are in $PWD. You are using $SHELL. Here is a random number: $RANDOM


```

- Creating custom built in variables: `<variable_name>="Value"`
- Publishing custom built in variables: `export <variable_name>` NB: To use the variables in bash files. Otherwise not recognize as a variable inside bash files.
>[!Warning]
>To make it persistent. You need to edit and save variable in `.bashrc` file.
>Ex: Insert `export <variable_name>="Value"` to the  file and save it.


## Exercise 4 (Arithmetic Expression)
- Sample basic expression: `$((2+3))`
>[!Important]
>Double brackets are **essential** to make it an arithmetic expression unless it will be an string.

- Update the file `getrichquick.sh` file to have a variable `getRich` where it is a number in between (0-14) and adding input age into it, finally display the variable as the number of years to get rich.

```bash
#!/bin/bash

echo "Enter your age"
read age

getRich=$((($RANDOM % 15)+$age))

echo You have $getRich years to get rich. Good luck!
```


## Exercise 5 (Conditionals)
- Basic conditional
```bash
if [[a==b]]; then
	echo "Enter the process"
else 
	echo "Enter the process"
fi
```

- Simple game using conditionals.
```bash
!/bin/bash

echo You Died!


#First beast battle

beast=$(( $RANDOM % 2))

echo "Your first beast battle approaches. Prepare to battle. Pick a number between 0-1. (0/1)"

read tarnished

if [[ $beast == $tarnished ]]; then
        echo "Beast VANQUISHED!! Congrats fellow tarnished"
else
        echo "You Died"
        exit 1
fi


sleep 2

echo "Boss battle!, Get scared. It's Margit. Pick a number between 0-9.(0-9)"

read boss

beast=$(( $RANDOM % 10))

if [[ $beast == $boss ]]; then
        echo "Beast VANQUISHED!! Congrats fellow tarnished"
else
		echo "You Died"
		exit 1
fi
```

- A bit complex version
```bash
#!/bin/bash

echo "You Died"

#First Beast Battle

beast=$(($RANDOM % 10))

echo Your first beast battle approaches. Prepare to battle. Pick a number 0-1. (0\1)
read tarnished

if [[$beast==$tarnished]]; then
	echo Beast Vanquished!. Congrats fellow tarnished.
else
	echo "You Died"
	exit 1
fi
```

## Exercise 6 (Case)
- Extended code of the game including case
```bash                                                                                                                                    
#!/bin/bash

echo "Welcome tarnished. Please select your starting class:
1 - Samurai
2 - Prisoner
3 - Prophet"

read class

case $class in
        1)
                type="Samurai"
                hp=10
                attack=20
                ;;
        2)
                type="Prisoner"
                hp=20
                attack=4
                ;;
        3)
                type="Prophet"
                hp=30
                attack=4
                ;;
esac

echo You chosen the $type class. Your HP is $hp and your attack is $attack.




#First beast battle

beast=$(( $RANDOM % 2))

echo "Your first beast battle approaches. Prepare to battle. Pick a number between 0-1. (0/1)"

read tarnished

if [[ $beast == $tarnished && 47 > 23 ]]; then
        echo "Beast VANQUISHED!! Congrats fellow tarnished"
else
        echo "You Died"
        exit 1
fi


sleep 2

echo "Boss battle!, Get scared. It's Margit. Pick a number between 0-9.(0-9)"

read boss

beast=$(( $RANDOM % 10))

if [[ $beast == $boss || $boss == "coffee" ]]; then
        echo "Beast VANQUISHED!! Congrats!"
elif [[ $USER == "Don" ]]; then
        echo "Hey Don always wins. You vanquished beast."
else
        echo "You Died"
        exit 1
fi
```

## Exercise 7 (Loops)

- While loop
```bash
#!/bin/bash

x=1

while [[ $x -le 100 ]]
do
        read -p "Pushup $x: Press enter to continue"
        (( x++ ))
done

echo Congrats!, You completed your pushups!!
```

- Until loop
```bash
#!/bin/bash

until [[ $order == "coffee" ]]
do
        echo "Would you like coffee or tea?"
        read order
done
echo "Excellent choice, here is your coffee."
```


- For loop
```bash
#!/bin/bash

for cups in 1 2 3 4 5 6 7 8 9 10;
do
        echo "Hey, you've had $cups of coffee today."

done

```

- Another for loop (Make sure to include some cities in a cities.txt file)
```bash
!/bin/bash

for x in $(cat cities.txt);
do
        weather=$(curl -s http://wttr.in/$x?format=3)
        echo "The weather for $weather"
done

```

- Write a code to print number 1 to 17 skipping 13
```bash
#!/bin/bash

echo Welcome to the Hollywood Tower Hotel!
sleep 1
echo Going up
sleep 1

for x in {1..17};
do
        if [[ $x == 13 ]]; then
                continue
        fi
        echo Floor $x
        sleep 1
done
```
