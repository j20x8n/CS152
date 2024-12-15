java c
CS152
Lab 4: The   Random   Package and matplotlib
The goal of this week's project is to get further   experience   with   modules   and   hierarchical   design.   In the lab, we'll work with the   Python random   package and   some   basic   capabilities   of the plotting   package   matplotlib. And then for the   project   …   .Penguins!!!
Lab Tasks
If you   have   not already done so, create a   new   Lab04 folder.
L1. Creating   Random   Numbers
In   Python, we create   random   numbers   using the   random   package. Start a   new file, rand.py,   and put your standard file header   at   the   top.   Then write:
import random
A. Write a function that generates   N random   numbers between   0   and   1
Define a function    gen_random()that has one   argument N which   is   the   number   of   random   numbers to create.
The first step   is to assign to a variable   (e.g. numbers =   [])   an   empty   list.
The second step   is to start a counted-for loop   that   executes   N   times.   Each   time   through   the   loop, append to your numbers list the   result of calling   the   function   random.random().
The function random.random() returns a randomly   generated floating-point   number   between 0 and   1.   It   is one of the   useful functions   in the   random   package.
Finally, the function should   return the list of   random   numbers.
B. Test the function
Define a test function. The test function should assign to a   variable   the   result   of   calling
gen_random()with an argument of   10.   It should then use   a   loop   to   print   out   the   10   numbers.   Run your code and   make   sure   it works   properly.
L2. Write a function that generates   N   random   integers   between a   lower bound   and   an   upper   bound
Define a function    genNintegers   ()   that   has three arguments: the   number of   points   to   create,   a lower bound, and an   upper bound. All   three   arguments   should   be   integers.
In the function, assign to a variable (e.g.   numbers   =   [])   an   empty   list.
Loop   N times and each time through the loop   append   the   result   of calling   random.randint(lowerBound,upperBound)to your numbers list.
The function random.randint(L,B)   returns a randomly generated   number between   L,   B,   inclusive.
Return the   number list.
Add code to your test function to call and then   print   out the   result   of   calling   genN   integers   ()   with arguments of   10, -10, and   10.   Make sure   it   produces expected values.
L3. Write a function that generates   N random values drawn from   a   normal/Gaussian   distributionDefine a function genNnormal   ()   that   has three arguments: the   number of points to   create,   a   mean, and a standard deviation. The second and   third   arguments  代 写CS152 Lab 4: The Random Package and matplotlibPython
代做程序编程语言 can   be   integers   or floating         point values.
In the function, assign to a variable (e.g.   numbers)   an   empty   list.
Loop   by the   number of points to create, and each time   through   the   loop   append   the   result   of   calling   random.gauss   ( mean, std   )   to your   numbers   list.
The function random.gauss   ( mean, std )   returns   a   randomly   generated   number   drawn   from a normal or Gaussian   distribution with the   given   mean   and   standard   deviation.
Return the   number list.
Add code to your test function to call and then   print   out the   result   of   calling   genNnormal   ()   with   arguments of   10, 0, and 0.2.   Make sure   it   produces   expected   values.
L4.   Installing and Creating   plots with matplotlib
NOTE:   Navigate to the   install   instructions matplotlib   installation   page.
You will   need to open   up a   regular terminal (NOT a   Python   interactive shell)   for   installing   matplotlib   package for Python.
For guidance on   installing on other platforms, see the matplotlib   installation   page.   As well as a GeeksforGeeks tutorial: Pyplot   in   Matplotlib
Continuing with the same file, add a new   import   statement   at the   top.
import matplotlib.pyplot as plt
Now   plot some of the   numbers you created   in the   prior exercise.
In the test function, you should   have three variables that all contain   random   numbers.   One   holds   values   between 0 and   1 (call   it x), one   holds values   between   -10   and   10   (call   it y),   and   one
holds values distributed around zero (call it z).   The   following   walks   through   the   process   of   plotting x versus z.
1.      At the end of the test function, call the function plt.plot() with the arguments   x,   z,   and the string 'o' (‘o’   means the   points will   be   represented as   circles).   The   lists x   and   z   must   have the same number of elements.
2.      After the call to   plot, call the function plt.show   (). Then   run your code.   It   should   create   a simple   plot.
3.      After the call to   plot and   before the call to show,   you   can   modify   aspects   of the   plot.   For   example, plt.title   () sets the title to whatever string you   pass   in as an   argument.
4.       Set the X axis   label   using plt.xlabel   () with "X" as the   argument.
5.       Set the Y axis   label   using plt.ylabel   ()   with "Y" as the   argument.
Now you   know   how to generate simple   plots with an x-label, a y-label,   and   a title.   Look   at   the
matplotlib documentation for PyPlot   for more information   on   how   to   create   more   complex   graphs   and charts.
When you are done with the lab exercises,   please   begin the   project.

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
