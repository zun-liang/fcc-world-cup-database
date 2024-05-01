# freeCodeCamp - Build a World Cup Database

This is a solution to the [Build a World Cup Database](https://www.freecodecamp.org/learn/relational-database/build-a-world-cup-database-project/build-a-world-cup-database).

## What I learned

### Learn Bash Scripting by Building Five Programs

- Commands can run in the terminal or be put in a file run as a script.
- ```sh <file_name>``` will run the script in the file. “sh” stands for “shell”. It means that the command will be run by the shell interpreter.
- ```bash <file_name>``` will run the script in the bash interpreter. “bash” stands for “bourne-again shell”.
- to find out where the bash interpreter is located: ```which bash```
- to use your bash interpreter, ```#!<path_to_interpreter>```. ```#!``` is shebang
- ```-rw-r--r--```, ```r``` means read, ```w``` means write, ```x``` means execute
- ```chmod +x <file_name>``` makes file executable, turn into ```-rwxr-xr-x```
- ```./file_name``` can execute a file if it is an executable file
- to run to commands in the file, ```./file_name```
- create variables in bash: ```VARIABLE_NAME=VALUE```. there cannot be any spaces around the equal sign
- to use a variable: ```$VARIABLE_NAME```
- to accept input from a user and store it in a new variable: ```read VARIABLE_NAME```
- to show echo’s manual: ```man echo```
- ```echo -e``` can interpret backslash
- ```ctrl+c``` will terminate process
- echo will only print empty lines if the value is enclosed in quotes.
- to comment in bash: ```# <comment>```
- Programs can take arguments, for example, ```./countdown.sh arg1 arg2 arg3```
- to access arguments: ```$<number>```, to access them all: ```$*``` or ```$@```, to access arg1: ```$1```, the first argument is index 1
- type ```help``` in terminal can get manual
- to find more about a command, can also use ```help <command>```, for example, ```help if```
- if statement:
	```
	if [[ CONDITION ]]
	then
		STATEMENTS
	elif [[ CONDITION ]]
	then
		STATEMENTS
	else
		STATEMENTS 
	fi
	```
- to compare integers in ```[[ … ]]```, ```-eq``` (equal), ```-ne``` (not equal), ```-lt``` (less than), ```-le``` (less than or equal), ```-gt``` (greater than), ```-ge``` (greater than or equal)
- to compare integers in ```(( … ))```, use the regular ```>``` ```<``` ```<=``` ```>=```…, this can be used in if statements too
- to view the exit status of a command: ```<command> <press enter> echo $? <press enter>``` or ```<command>; echo $?```
- exit status indicates whether the command executed successfully or encountered an error, ```0``` means success
- command not found will show exit status ```127```
- to see if a file exists: ```[[ -a file_name ]]; echo $?```
- to see if a file is executable: ```[[ -x file_name ]]; echo $?```
- ```help [[ expression ]]``` is the same as ```help [[```
- can use ```&&``` and ```||``` in expression too, for example, ```[[ -x countdown.sh && 5 -le 4 ]]; echo $?```
- for loop:
	```
	for (( i = 10; i > 0; i-- ))
	do
		echo $i
	done
	```
- to list the contents in the root of the file system: ```ls /```
- to list what’s inside a folder: ```ls /<folder_name>```
- to delay for a specified amount of time: ```sleep <seconds>```
- multiline comment:
	```
	: '
		comment here
		more comment here
	'
	```
- while loop:
	```
	while [[ CONDITION ]]
	do
		STATEMENTS
	done
	```
- ```[[ ]]``` is used for conditional expressions and string comparisons, ```(( ))``` is used for arithmetic operations and numerical comparisons, for example, ```[[ $I -gt 0 ]]```, ```(( I-- ))```, when variables using inside ```(( ))```, no need to use $ as it is referring to its value already
- A shell comes with environment variables. View them by entering ```printenv``` in the terminal.
- to view one env in terminal: ```echo $ENV_NAME```
- to view all envs in terminal: ```declare -p```, ```p``` means print; ```declare -p <VARIABLE>``` can view this variable
- ```declare``` can also be used to create variables
- modulus operator: ```%```, calculates the remainder
- to assign a variable some calculations: ```VARIABLE=$(( … ))```
- ```(( ... ))``` will perform a calculation or operation and output nothing. ```$(( ... ))``` will replace the calculation with the result of it.
- to create an array: ```ARRAY_NAME=(VALUE1 VALUE2 VALUE3)```
- in array, first item index 0. to access the first item, ```echo ${ARRAY_NAME[0]}```
- to print your whole array: ```echo ${ARRAY_NAME[*]}``` or ```echo ${ARRAY_NAME[@]}```
- ```declare -p ARRAY_NAME``` will show ```declare -a ARRAY_NAME=([0]=VALUE1 [1]=VALUE2 [2]=VALUE3)```, ```-a``` means array
- function:
	```
	FUNCTION_NAME() {
  	 STATEMENTS
	}
	```
- to call a function: ```FUNCTION_NAME```
- until loop:
	```
	until [[ CONDITION ]]
	do
  		STATEMENTS
	done
	```
- to check pattern matching for literal and regular expression: ```=~```, for example, ```[[ "hello world" =~ "lo wor" ]]; echo $?```, ```[[ "hello world" =~ ^h ]]; echo $?```
- to pass arguments in function: ```FUNCTION_NAME ARG1 ARG2 ARG3```
- to view the type of a command: ```type <command>```

### Learn SQL by Building a Student Database

- ```cat``` is a terminal command for printing the contents of a file
    ```
    cat <filename>
    ```
- pipe output into a while loop so you can go through the rows one at a time, for example:
    ```
	cat courses.csv | while read MAJOR COURSE
	do
  		<STATEMENTS>
	done
    ```
- IFS stands for “Internal Field Separator”, it is used to determine word boundaries. It defaults to spaces, tabs, and new lines. to view it: declare -p IFS, to use it, for example:
    ```
	cat courses.csv | while IFS="," read MAJOR COURSE
	do 
  		echo $MAJOR
	done
    ```
- ```psql``` command can be used to log in and interact with database, it can also just run a single command and exit, for example: ```PSQL="psql -X --username=freecodecamp --dbname=students --no-align --tuples-only -c”```. ```PSQL``` is a variable to store the command; ```-X``` tells psql to disable any startup file processing;``` --no-align``` tells psql not to align the output columns; ```--tuples-only``` instructs psql to only output data rows (tuples), without any headers, footers, or other formatting; ```-c``` tells psql to execute a single SQL command and then exit.
- terminal can be split and process different commands
- you can query your database using the PSQL variable like this: ```$($PSQL "<query_here>”)```, for example, ```MAJOR_ID=$($PSQL "SELECT major_id FROM majors WHERE major='$MAJOR'")```
- ```-z``` flag is used to check if the length of the string is zero, for example, ```[[ -z $MAJOR_ID ]]```
- TRUNCATE deletes all data/ rows from a table: ```TRUNCATE <table_name>```, to delete multiple tables, separate tables by commas
- can also use ```echo``` to query database, for example, ```echo $($PSQL "TRUNCATE students, majors, courses, majors_courses”)```, when run the file in terminal, truncate will execute automatically
- ```pg_dump``` is a PostgreSQL utility used for backing up PostgreSQL databases. It allows you to create a text file containing SQL commands that can later be used to restore the database to its current state.
- ```pg_dump --clean --create --inserts --username=freecodecamp students > students.sql```
	- ```--clean```: This option instructs ```pg_dump``` to include SQL commands to clean (drop) database objects (tables, indexes, etc.) before recreating them. This ensures that the backup file contains a set of SQL commands that, when executed, would create a fresh copy of the database structure without any existing data.
	- ```--create```: This option tells pg_dump to include SQL commands to create the database objects (tables, indexes, etc.). It ensures that the backup file contains SQL commands to recreate the database schema.
	- ```--inserts```: This option directs pg_dump to include SQL commands to insert data into tables using INSERT statements. 
- ```psql -U postgres < students.sql``` will execute SQL commands contained in the file “students.sql” on a PostgreSQL database server. ```-U postgres``` specifies the uer postgres
- SQL stands for “Structured Query Language”, it is used to manage relational databases
- in SQL, compare numbers or strings equal or not, use ```=```. ```==``` or ```===``` are not valid comparison operators. while, in bash, still ``==``
- when using ```>``` ```<``` ```>=``` ```<=``` in string comparison, it compares alphabetically
- Place double quotes around it like this: ```echo "$($PSQL "<query_here>")"```. This will make it so the output isn't all on one line.
- You can use multiple conditions after ```WHERE``` with ```AND``` or ```OR```, among others. Just add the keyword and another condition.
- You can group conditions together with parenthesis like this: ```WHERE <condition_1> AND (<condition_2> OR <condition_2>)```
- You can use LIKE to find patterns in text like this:``` WHERE <column> LIKE '<pattern>'```. An underscore (_) in a pattern will return rows that have any character in that spot. ```%```: Matches zero or more characters. ```_```: Matches exactly one character. For example, ```SELECT * FROM courses WHERE course LIKE '_e%';```
- You can use ```NOT LIKE``` to find things that don't match a pattern. 
- ```ILIKE``` will ignore the case of the letters when matching.
- ```NOT ILIKE``` will rule out the pattern no matter it is capitalized or not
- when combining two conditions: 
	```
	SELECT * FROM courses WHERE course NOT ILIKE '%A%' AND course LIKE '% %';
	```
- All the fields that are empty or blank are null. You can access them using ```IS NULL``` as a condition like this: ```WHERE <column> IS NULL```. Inversely, you can use ```IS NOT NULL``` to see rows that aren't null.
- ```SELECT columns FROM table_name ORDER BY column_name;``` will order ascending (ASC) by default, add ```DESC``` at the end
- You can add more columns to the order by separating them with a comma like this: ```ORDER BY <column_1>, <column_2>```. Any matching values in the first ordered column will then be ordered by the next
- Many times, you only want to return a certain number of rows. You can add ```LIMIT <number>``` at the end of the query to only get the amount you want.
- If have ```WHERE```, ```ORDER BY```, and ```LIMIT```, ```WHERE``` goes first, ```ORDER BY``` second, last is ```LIMIT```
- There's a number of mathematic functions to use with numerical columns. One of them is ```MIN```, you can use it when selecting a column like this: ```SELECT MIN(<column>) FROM <table>```. It will find the lowest value in the column. 
- MAX to find the largest value
- ```SUM```: values add up to
- to add up two columns: SUM(COLUMN1 + COLUMN2)
- ```AVG```: average value
- You can round decimals up or down to the nearest whole number with ```CEIL``` and ```FLOOR```, respectively. Here's an example: ```CEIL(<number_to_round>)```.
- you can round a number to the nearest whole number with ```ROUND```.
- You can round to a specific number of decimal places by adding a comma and number to ```ROUND```, like this: ```ROUND(<number_to_round>, <decimals_places>)```.
- Another function is ```COUNT```. You can use it like this: ```COUNT(<column>)```. It will tell you how many entries are in a table for the column. ```COUNT(*)``` will count all rows
- ```DISTINCT``` is a function that will show you only unique values. You can use it like this: ```DISTINCT(<column>)```
- ```GROUP BY```. Here's an example of how to use it: 
	```
	SELECT <column> FROM <table> GROUP BY <column>
	```
- The output was the same as DISTINCT, but with GROUP BY you can add any of the aggregate functions (MIN, MAX, COUNT, etc) to it to find more information. For instance, if you wanted to see how many students were in each major you could use 
	```
	SELECT  major_id, COUNT(*) FROM students GROUP BY major_id
	```
- Another option with ```GROUP BY``` is ```HAVING```. You can add it at the end like this: 
	```
	SELECT <column> FROM <table> GROUP BY <column> HAVING <condition>
	```
	The condition must be an aggregate function with a test. Aggregate functions such as ```COUNT```, ```SUM```, ```AVG```, ```MIN```, and ```MAX``` are commonly used in the HAVING clause to perform calculations on groups of rows. An example to might be to use ```HAVING COUNT(*) > 0``` to only show what whatever column is grouped that have at least one row. 
- You can rename a column with AS like this: ```SELECT <column> AS <new_column_name>```
- FULL JOIN: 
	```
	SELECT * FROM <table_1> FULL JOIN <table_2> ON <table_1>.<foreign_key_column> = <table_2>.<foreign_key_column>;
	```
- LEFT JOIN: A LEFT JOIN gets all rows from the left table, but only rows from the right table that are linked to from the left one. 
- RIGHT JOIN
- INNER JOIN: it only returned rows if they have a value in the foreign key column (major_id) of the opposite table. 
- ```SELECT * FROM students RIGHT JOIN majors ON students.major_id = majors.major_id WHERE student_id IS NULL;```
- If you look at the column names, it shows two major_id columns. One from the students table and one from the majors table. If you were to try and query it using major_id, you would get an error. You would need to specify what table you want the column from like this: ```<table>.<column>```. 
- Earlier, you used AS to rename columns. You can use it to rename tables, or give them aliases, as well. Here's an example: ```SELECT * FROM <table> AS <new_name>;```. Enter the same query you just entered, but rename the majors table to m. 
	```
	SELECT students.major_id FROM students FULL JOIN majors AS m ON students.major_id = m.major_id;
	```
- There's a shortcut keyword, ```USING``` to join tables if the foreign key column has the same name in both tables. Here's an example: 
	```
	SELECT * FROM <table_1> FULL JOIN <table_2> USING(<column>); Note that the two major_id columns were turned into one with USING.
	```