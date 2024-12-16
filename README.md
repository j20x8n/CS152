java c
CS152
Lab   Exercise 3:   Modular Design and   Lists
The goal of this week's lab/project   pair is to   learn   how to   organize   our   Python   programs   in   such   a way that the functions   inside of one   Python file can be   used   by   other   Python   programs. The general term for this   is code   reuse and   it   is a central   idea   in software   engineering. After   all,   what’s the   benefit of spending a lot of time   working on   a   program   if   it   can   only   be   used   once   and   only to solve one specific   problem.   But   in order to achieve efficient   code   reuse, we   will   need   to learn   how to structure our programs   in a   particular way. This organizational   model   is   commonly         referred to as modular design and   means that we will   build   more   complex   programs   by   reusing   modules (collections of functions) also known as   Python   programs.
This   lab will   prepare you for Project 3   by   introducing   more details on   lists,   uses   of the   main   function, more file processing techniques, and command-line   arguments.
So,   let’s get started!
Lab Tasks   (L1-L7)
L1. Set   up your workspace
Make a folder and   name   it   Lab03. Open VS Code and then   open   this   folder from   the   File   menu.   Create a new file,   list_practice.py.
L2. Working with   lists
Lists are an   important data structure   in   Python. A list   is   an   ordered   sequence   of values.   In   Python the values of a   list can   be of any   type,   including other   lists,   and the   list   does   not   have   to all   be of the same type (unlike   in other programming   languages--we’re   looking   at you   Java!).   But   for this assignment, we'll mostly be dealing with   lists   of   numbers.
Put the following assignment   into your list_practice.py file.   It assigns to the variable   numbers   a   new list with five   values:
numbers =   [5,   3,   6,   1,   2]
In   Python a   list   is   indicated   by square   brackets, and the elements of the   list are   separated   by   commas.
We can   make an empty   list   like   this:
my_empty_list =   []


To access one element of a list, we   use   index   notation with   square   brackets   like   this:
first_number = numbers[0]
Note:   In   Python we start counting   indices at zero.
Add two   more   lines to your file to   print out the 5 and   the   1   (the first   element   in   the   list   and   the   fourth element   in the list--be sure to   check   how you   count!).
To add   items to the end of a list,   use   the   append(item to   append   to   end   of   list)   method.
To call a   method on a   list we combine the   name   of the   list, the “dot”   operator,   and   the   method   name as follows:
numbers.append(7)
print( numbers   )
You should   now see a   7   at the   end   of the   list.
Just   like with accessing   list elements, we can   replace elements   in a   list   using   bracket   notation.   For example, the following changes the first element of the   list to a   4   and   then   prints   the
updated   list:
numbers[0] =   4
Modify the value of two other locations   in the list   in   your   Python file,   then   print   out   the   list   and   make sure   it did what you think   it should   have.
L3.   Building   lists
So far, all of our programs   have   processed data while we   read   it from a   file   (Ok,   technically we         created a   list   using the split   method,   but we didn’t   keep that   list around for   later   processing).   For   this   project, we want to   read the file and   build a data   list that stores   the   incoming   data   in   a   list   and then   manipulate the list. The concept   is straightforward: start with   an   empty   list   and   as   your   program reads through the file append each value   to   the   list.
A.   Download the file   hurricanes   .csv    from Google Classroom assignment   and   save   it   in   your   Lab03 folder.




B.    Create a   new   Python file called analyze.py. Add a file   header   (module   string)   at   the   top   that   contains your name, today’s date, and the section   of CS   152   you   are   in.   Then   copy   and   paste the following   pseudocode. Convert each line of pseudocode   into   actual   Python   code.   Each comment will correspond to one   line of code.
def main   ():
# assign to fp the   result   of   opening   the   file hurricanes.csv   for   reading
# assign to line   the   first   line   of   the   data   file
# assign to headers the result   of   splitting   the   line   using   commas
# print headers
# assign to a   list variable   named   data   an   empty   list
# for   each   line   in   the   file
# assign to items the   result   of   splitting   the   line   using   commas
# append the second   item   to data   (be   careful,   which   index   is   that?)
# close the data file
# print data
if __name__ == "__main__":
main()
Program Output:
[   'Year   ',   'Number   ',   'Damage\n   ']
[15,   5,   6,   8,   3,   12,   7,   10,   2,   6,   4,   7,   10,   8]
L4. Work with command-line arguments
One way to get   information from the user into   a   Python   program   is to   use   the   input(“prompt   string”) technique.   But there is   a second way to do this--command-line   arguments.   Information   can   be entered on the command line when the   program   is   started   and   Python   stores that   information in a special variable called sys.argv where argv   stands   for   the   list   of   arguments   read from the command   lineFor example,   it would   be   nice to   modify our analyze.py   program so that we could   use   it with   any   data file and any column. The following steps will show you   how   to   get   access   to   the   command-line information.代 写CS152 Lab Exercise 3: Modular Design and ListsJava
代做程序编程语言
A.   Import the sys   module
Create a   new file com.py. Add a file   header (module string)   at the   top   that   contains   your   name,   today’s date, and the section of CS   152 you are   in. Add   the following   statement   below   your header information:




import   sys
B.   Find out what the sys   package can   do
Put the following line of code   in the   com.py   file:
print(sys.argv)
Save your file and run the com.py file.   What   do   you   see?
Rerun the last command line, but   add   additional   data   after python3   com.py.   For example, try:
python3 com.py   hello world   1   2   3
Now, what do you   see?
The sys   package gives you the ability to see what the   user   has typed   on   the   command   line.
Each   individual string (separated   by spaces) from the command   line   is an   entry   in   the   argv   list.
C. Access   individual strings from the command   line
Add the following three lines to your com.py   file:


print("Running program", sys.argv[0])
print("I'm going to open the file", sys.argv[1])
print("I'm going to extract column", int(sys.argv[2]))


Run the program using the   following   command.
python3 com.py hurricanes.csv   1
Do you   begin to see   how the command-line arguments can control   both   the   file   and   the   column   of data to extract without the need to edit the   Python   file   each   time?


L5. Get   user input from the   command-line
Edit your analyze.py file so that the csv filename and   column   index   are   given   on the   command   line.
A. Add the   import sys statement to   the top of the file.
B. Change the definition of main() so that   it   has two   parameters:   filename,   column_id.   C. Change the hardcoded value,   hurricanes.csv, with the filename   parameter.
D. On the line that appends the data   to   your   list,   replace   the   index   with   the   column_id   parameter.
E. When the   main function   is called from the conditional block   at the   bottom   of the   file,   use   sys.argv[1] and   int(sys.argv[2]) as arguments to be   passed   into the   main function:
main(sys.argv[1], int(sys.argv[2])
And add two parameters to the definition   of the   main function:
def main(filename, column_id):
Run your program   using:
python3 analyze.py hurricanes.csv   1
The   result should   be   identical   to the   prior case. Try changing the   1 to   a   2   and   see what   happens.
What   happens   if youtube                      forget the extra data on   the   command   line?
L6. A   Library of Useful   Functions
In the   next task we're going to create a file   (module) that   holds   a   library   of   useful functions.   In   Python, a    library, or package, or   module,   is   a file   that   contains   functions.   When   you   import   the   module   into another Python file, you can use   those functions.   We've   already   done   this   by   importing the sys   package   into our program.   Now we're going to create   our   own   module   and   then   import   it   into other Python files.


Create a   new file called stats.py. Add a file header   (module   string)   at the   top   that   contains   your   name, today’s date, and the   section of   CS   152   you   are   in.
A. Write a function to compute the sum of a   list   of   numbers
Create a   new function called sum(numbers) that takes one argument. You   can   assume that   the   argument will   be a list of numbers. This function should   add   together   all   of the values   in   the   list and return the sum. The   algorithm   is   as follows:
# Create a variable   to   hold   the   sum
#   Initialize the variable to 0.0 (explicitly make   it   a floating   point   number).
#   Define a for loop to   iterate over the list   passed   in   as   the   function   parameter.   # On each iteration, add the current   number   to   the   variable   holding   the   sum.         # Once the loop   completes,   return   the   sum.
B. Write a test function
To test your function,   make a second function called   test   at the bottom   of your   stats.py   file.   The function does not require any arguments. As   the   first   instruction   in   the   test   function,   assign      to a variable the list   [1, 2, 3, 4].   For the   second   instruction   assign   to   a   second   variable   the   result   of calling sum with the list as the argument.   For the third   instruction,   print   out   the   variable
holding the   result.
Put the following at the end of your stats.py   file   (just   below your test function)   to   call   the   test   function when stats.py   is run directly (i.e.,   not   imported). The test   function will   not   run   when
stats.py   is   imported   into   another Python file.


if __name__ == "__main__":
test()
Run your program and   make sure you get the value   10.0   as   an   output.
L7.   Using a   LibraryThe   last step   in the   lab   is to   import your stats   library   into another file and   use a   function   in   that      module.   Reopen your analyze.py file. At the top, after the import sys,   and   add   the   following   line of code:
import   stats


To call a function   in your stats   library, all you   have to   do   is   put   stats.   in front   of the   name   of   the function you want to use (e.g., stats.sum(numbers)   )
Edit your main function so it uses   the   stats.sum(numbers) function   to   compute   the   sum   of the   values stored   in the data list   and   prints   out the   sum.
If you   run your analyze.py   program using the   hurricanes.csv file and the index   of the   second   column, you should get a sum   of   103   as the   answer.
When you are done with the   lab exercises, begin the   project.

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
