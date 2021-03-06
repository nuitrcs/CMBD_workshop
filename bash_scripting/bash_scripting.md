# Bash Scripting
<hr>

We were issuing the commands on the command line and
finding them again using the arrow key or `history`
command.

When we need to accomplish many tasks, write long command,
and repeat these tasks form time to time, it is better to save your
commands to a file. Instead of executing the commands
one by one on the command line, we can execute the
file. This file is called a shell script.

So let's start with putting some very common programming constructs
in scripts.

## Variables

In programming, variables are information holders, or labels of information.
You can access the same information through out your programme by calling
its label. You can also assign new information to the labels.

Let's start editing our first bash script.

```bash
vim mynumber.sh
```

We will type the following code block in the script file to look at
variable 'myfavnumber'.

```bash
#!/bin/bash    # you may not need this line

myfavnumber=34
echo 'My favorite number is' $myfavnumber

myfavnumber=65
echo 'I changed my mind, it is' $myfavnumber
```

`$` symbol tells the shell interpreter to treat *myfavnumber* as
a **variable** and look what is inside this label. So `$favnumber`
returns the value of the variable which becomes 34 and then 65. In some
bash code, you may see `${favnumber}` which is equivalent to `$favnumber`

## Conditionals

Another important algorithmic construct is conditionals. The basic
conditional statement is `if/then`. Apart from small syntax differences, the
usage of `if/then` statement in bash scripts is same as other languages.
Conditionals help you to execute commands only when certain conditions
are met.

```bash
#!/bin/bash

myfavnumber=34

if [ $myfavnumber -eq 34 ]
    then
        echo "My favorite number is $myfavnumber"
fi
```

`if/then` statement can be extended to `if/then/else` or `if/then/elif/else`
to test more conditions.

Let's work on animals.txt in *bash_scripting/animal_control* folder and
create decision tree about your vegetables when there are rabbits
around. The script we will write is named as *nobunnies.sh*

```bash
vim nobunnies.sh
```


```bash
#!/bin/bash

cd ./bash_scripting/animal_control

nrabbits=`cat animals.txt | grep rabbit | wc -l`
# nrabbits=$(cat animals.txt | grep rabbit | wc -l)

if [ $nrabbits -le 2 ]; then
    echo 'Nothing to worry about my vegetable garden'
elif [ $nrabbits -gt 2 ] && [ $nrabbits -le 10 ]  ; then
    echo 'Yellow alert, check your garden'
else
    echo 'Call animal control'
fi

echo "$nrabbits"
```


## Loops

Loops will make your life very easy for repetitive tasks and automation. 
Let's move to 'bash_scripting/creatures' folder. We will work with the two files but let's
first create backup copies.

```bash
#!/bin/bash

cd ../creautures
pwd
ls -al
cp *.dat original-*.dat
```

When `cp` receives more than two inputs the last should be a directory for
`cp` to be able to copy all files prior to this directory. So the previous
command will not work. We can use a loop to accomplish this task

```bash
#!/bin/bash

for filename in basilisk.dat unicorn.dat
    do
        cp $filename original-$filename
    done

#OR

for filename in basilisk.dat unicorn.dat; do cp $filename original-$filename; done

#OR

for x in basilisk.dat unicorn.dat
    do
        cp $x original-$x
    done
```

We can write the same `for` loop on the command line
```bash
for x in basilisk.dat unicorn.dat; do cp $x original-$x; done
```

If writing everything on the same line is becomes convoluted then we can
hit ENTER/RETURN to go to another line after each complete code block
```bash
for x in basilisk.dat unicorn.dat  #hit enter
>do                                #hit enter
>cp $x original-$x                 #hit enter
>done                              #hit enter
```


`$` symbol tells the shell interpreter to treat *filename* as a **variable** and 
`$filename` returns the value of the variable which becomes *basilisk.dat* and
*unicorn.dat* within the loop. In some code, you may see `${filename}` which
is equivalent to `$filename`

```bash
#!/bin/bash

echo *.dat

for filename in *.dat
    do
        echo $filename
        head -n 100 $filename | tail -n 5  #this selects the lines 96-100
    done
 ```

We can put an empty line before each filename when printing for a better
look

```bash
#!/bin/bash

echo *.dat

for filename in *.dat
    do
        echo ""
        echo $filename
        head -n 100 $filename | tail -n 5  #this selects the lines 96-100
    done
 ```

Say you have white spaces in your file names:

```bash
#!/bin/bash

cp basilisk.dat 'green snake.dat'
cp unicorn.dat 'white horse.dat'

for filename in green snake.dat white horse.dat #hit enter#
    do
        echo $filename
        head -n 100 $filename | tail -n 20  #this selects the lines 81-100
    done
```

This code should be as below:

```bash
#!/bin/bash

for filename in 'green snake.dat' 'white horse.dat' #hit enter#
    do
        echo $filename
        head -n 100 $filename | tail -n 20  #this selects the lines 81-100
    done
 ```

Let's go back to our "bash_scripting/molecules" folder do more looping

```bash
cd ../molecules
```

Say we want to write all molecules in one file:

```bash
#!/bin/bash

for molecule in *.pdb
    do
        echo $molecule
        cat $molecule > all_molecules.dat
    done

cat all_molecules.dat
```

We could not write all molecules in a single file because each iteration
of the loop we overwrite the previous file. Instead we should have used 
append `>>`

```bash
#!/bin/bash

rm all_molecules.dat

for molecule in *.pdb
    do
        echo $molecule
        cat $molecule >> all_molecules.dat
    done
```

What if we only want to write molecules if their names start with "p"

```bash
#!/bin/bash

for molecule in p*
    do
        echo $molecule
        cat $molecule >> p_molecules.dat
    done
```

What if we only want to write molecules if their names include c

```bash
#!/bin/bash

for molecule in *c*
    do
        echo $molecule
        cat $molecule >> c_molecules.dat
    done
```

We can construct nested loops for instance creating a grid of folders
for organizing our data

```bash
#!/bin/bash

for temperature in 10 20; do
    for molecule in propane pentane; do
        mkdir $molecule-$temperature
    done
done

#OR 

for temperature in 10 20; do
    for molecule in propane pentane; do
        mkdir "$molecule-$temperature"
    done
done

#BUT NOT SAME

for temperature in 10 20; do
    for molecule in propane pentane; do
        mkdir '$molecule-$temperature'
    done
done
```

There are other loop constructions such as `while` and `until`.

```bash
#!/bin/bash

counter=0
while [ $counter -lt 10 ]
    do
        echo $counter
        let counter=counter+1
    done
 ```

`while` iterates as long as the condition is true where as `until` stops
the loop when the condition is true
 
```bash
#!/bin/bash

counter=0
until [ $counter -ge 10 ]
    do
        echo $counter
        let counter=counter+1
    done

echo $counter
```


## Script Arguments

Let's go to molecules folder and start writing a script
 
```bash
cd ../molecules
vim middle.sh
```

When we start vim, to write characters we first hit
**i** (entering inset mode) and then we write the following

```bash
#!/usr/bin/env bash     # you may not need this line
head -n 15 octane.pdb | tail -n 5
```

Then we hit **Esc**, then we hit **:** (entering  command mode) 
and type **wq** (save and quit) and hit **Enter**.

```bash
bash middle.sh
```

Your input in the `head` command was octane.pdb.
Instead of hard coding the file name in the script
we can make it a variable. Let's edit our script
with vim again

```bash
vim middle.sh
```

hit **i** (inset mode) and then we write the 
following

```bash
#!/usr/bin/env bash

# head -n 15 octane.pdb | tail -n 5
head -n 15 "$1" | tail -n 5
```

A comment starts with a `#` character and runs to 
the end of the line. The computer ignores comments. 

In case the filename happens to contain any spaces, 
we surround $1 with double-quotes.

Then we hit **Esc**, then we hit **:** and type
**wq** and hit **Enter**. Now we can identify 
our file as an input to the script on the command line

```bash
bash middle.sh octane.pdb
bash middle.sh pentane.pdb
```

Let's make the number of lines printed by `head` and
`tail` also variables

```bash
vim middle.sh
```

hit **i** (inset mode) and then we write the 
following

```bash
#!/usr/bin/env bash

# head -n 15 octane.pdb | tail -n 5
head -n "$2" "$1" | tail -n "$3"
```

Then we hit **Esc**, then we hit **:** and type
**wq** and hit **Enter**. Now let's change the 
number of lines on the command line.

```bash
bash middle.sh pentane.pdb 15 5
bash middle.sh pentane.pdb 20 5
```

It is a good coding practice to add comments 
in your script to explain what is being done
to another user of your script.

```bash
vim middle.sh
```

We will repeat the routine to insert save and
quit in vim.

```bash
#!/usr/bin/env bash

# Select lines from the middle of a file.
# Usage: bash middle.sh filename end_line num_lines
# head -n 15 octane.pdb | tail -n 5

head -n "$2" "$1" | tail -n "$3"
```

Comments are invaluable for helping people (including 
your future self) understand and use scripts. However 
each time you modify the script, you should check that 
the comment is still accurate.

Let's write another script to find the number of lines
for each file and sort them according to these
numbers. 

```bash
vim sorted.sh
```

Repeat the routine to insert save and
quit in vim.

```bash
#!/usr/bin/env bash

wc -l "$1" "$2" | sort -n
```

Let's execute the script

```bash
bash sorted.sh *.pdb
```

As you see we did not get all the files. Only two files
reported because we entered two variables in the script.
If we want to enter any number of input arguments,
instead of using `"$1"`, `"$2"` etc., we could use 
`"$@"`

```bash
vim sorted.sh
```

Repeat the routine to insert save and quit in vim.

```bash
#!/usr/bin/env bash

wc -l "$@" | sort -n
```

Let's execute the script

```bash
bash sorted.sh *.pdb ../creatures/*.dat
```

If you forget to provide input as show below, the script
will start but not do anything. To exit from this state
hit Ctrl+C

```bash
bash sorted.sh
```

A short cut to save some useful commands is to redirect 
the current history to a file which becomes a script

```bash
#!/usr/bin/env bash

history | tail -n 5 > redo-commands.sh
```

Let's write a script that takes any number of files (i.e. *.pdb* files)
in molecules folder as input and
<br>
1. Prints the file names that are provided 
2. Prints out 4<sup>th</sup> line from each 
file 
3. Combines all files in "all_molecules.txt"
4. Create copies with names "bckp-<file_name>"

except if the file name is cubane.pdb

```bash
vim myscript.sh
```

Repeat the routine to insert save and
quit in vim.

```bash
#!/usr/bin/env bash

for filename in "$@"
    do
        if [ "$filename" == "cubane.pdb" ] ; then
            continue
        fi

        echo $filename
        head -n 4 $filename | tail -n 1
        cat $filename >> all_molecules.txt
        cp $filename bckp-$filename
    done
```

Issue the following command to see the result:
```bash
bash myscript.sh *.pdb
```

We can convert this script to an executable and run without identifying
the interpreter (i.e. bash)

```bash
chmod u+x myscript.sh
./myscript.sh *.pdb
```

Let's do some scripting with random numbers. 
Write a bash script to generate 1000 random numbers 
between 1 and 1000 and write them to a file. Find 
out how many unique numbers are obtained. <br>
(Hint: Try issuing `echo $RANDOM`, what do you get?)

```bash
#!/usr/bin/env bash

rm randomnumbers.txt
touch randomnumbers.txt

for i in `seq 1000`
    do
        echo $(((RANDOM%1000)+1)) >> randomnumbers.txt
    done

sort -n randomnumbers.txt | uniq | wc -l
```

Write a script that creates a folder at every 2 seconds with names
folder_01, ... folder_10 and lets you know when each folder is created
and the operation is ended. Finally, the script should show the created
folders and then delete them.

```bash
#!/usr/bin/env bash
counter=1

while [ $counter -le 10 ]; do
    sleep 2 #wait for 2 seconds
    mkdir folder_$(printf "%02d" $counter)

    if [ $counter -eq 10 ]; then
        echo "Folder ${counter} has been created"
        echo 'All folders are created'
    else
        echo "Folder ${counter} has been created"
    fi

    let counter=counter+1
done

ls -al | grep folder_
rm -Rf folder_*
```

# Bash Scripting Exercises

**i-** Write a bash script that takes an integer and your first name as
inputs:
- If the input integer is larger than 1000, it will print out “I cannot
write [yourfirstname] [integer] times”
- If the input integer is less than 100, it will print out “Don’t you
like your name, [yourfirstname]?”
- If the input integer is between 100 and 1000, it will write your name
integer times to a file called *myname.txt*. Each name entry should be
on a single line in the output file.
<details><summary>Click me for answer</summary>
<p>

#### Answer
```bash
#!/usr/bin/env bash

NumName="$1"
Name="$2"

if [ $NumName -gt 1000 ]; then
    echo "I cannot write ${Name} ${NumName} times"
elif [ $NumName -lt 100 ]; then
    echo "Don’t you like your name, ${Name}?”"
else
    for i in `seq 1 ${NumName}`
        do
            echo $Name >> myname.txt
        done
fi
```
</p>
</details>
<p></p>

**ii-** Create a backup for your script then modify the original to
read your first name from an input file named as *input_myname.txt*.
The integer should still be provided as an argument on the command line.

Hint: You can assign the contents of a file to a variable using
command below:
```bash
variable=`cat input_myname.txt`
```

<details><summary>Click me for answer</summary>
<p>

#### Answer
```bash
#!/usr/bin/env bash

NumName="$1"
Name=`cat input_myname.txt`

if [ $NumName -gt 1000 ]; then
    echo "I cannot write ${Name} ${NumName} times"
elif [ $NumName -lt 100 ]; then
    echo "Don’t you like your name, ${Name}?”"
else
    for i in `seq 1 ${NumName}`
        do
            echo $Name >> myname.txt
        done
fi
```
</p>
</details>
<p></p>

# Quest Job Submission Exercises

**i-** Run the script that you have written in the first exercise of
bash scripting by submitting a job to Quest. Check if the job
appropriately produced output file *myname.txt*, log and error files.
<details><summary>Click me for answer</summary>
<p>

#### Answer

```bash
#!/bin/bash
#MSUB -A w10001
#MSUB -q admin
#MSUB -l nodes=1:ppn=1
#MSUB -l walltime=00:10:00
#MSUB -N sample_job
#MSUB -o r.outlog
#MSUB -e r.errlog

cd $PBS_O_WORKDIR

bash myscript.sh 300 yourfirstname ## Replace yourfirstname with your
                                   ## actual name
```
</p>
</details>
<p></p>

**ii-** Run the script that you have written in the second exercise of
bash scripting by submitting a job to Quest. Check if the job
appropriately produced output file *myname.txt*, log and error files.
<details><summary>Click me for answer</summary>
<p>

#### Answer

```bash
#!/bin/bash
#MSUB -A w10001
#MSUB -q admin
#MSUB -l nodes=1:ppn=1
#MSUB -l walltime=00:10:00
#MSUB -N sample_job
#MSUB -o r.outlog
#MSUB -e r.errlog

cd $PBS_O_WORKDIR

bash myscript.sh 300  ## Replace myscript.sh with your actual
                      ## script file name
```
</p>
</details>
<p></p>

**iii-** Submit a job that prints out help information for R in your
log file.

Hint: You need to load R module
Hint: You can see help information for R with the command below:

```bash
R --help
```

Extra credit: You can redirect the help information to file of your
choice instead of the log file.


<details><summary>Click me for answer</summary>
<p>

#### Answer

```bash
#!/bin/bash
#MSUB -A w10001
#MSUB -q admin
#MSUB -l nodes=1:ppn=1
#MSUB -l walltime=00:10:00
#MSUB -N sample_job
#MSUB -o r.outlog
#MSUB -e r.errlog

cd $PBS_O_WORKDIR
module load R

R --help             ## Help info will be written to log file
#R --help > r.help   ## Redirect the help info to r.help file
```
</p>
</details>
<p></p>
