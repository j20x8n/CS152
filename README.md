java c
CS152
Project 3: Calculating Thermoclines 
The first task of this   project   is to   build a library of functions that   can   be   reused   by   other programs.   In   particular, we are going to write a set of functions that can   calculate statistics for   us.
The second task will   involve computing the depth of the thermocline on   Great   Pond   and   plotting   it for the   month of July. The thermocline is the depth at which there   is the   largest   difference   in water density, with a layer of denser water below and   a   layer   of   less   dense water   above.
Outline of Lab/Project 3 Program Development 
Lab: Developing and working with libraries 
A.    Write a module that contains   common   statistics   named stats.py 
B.   Use the library functions   in analyze.py using command   line   arguments
Project:    Calculating thermoclines 
A. Write a function that converts water temperatures into water   densities
B. Write a function that computes the depth of the   maximum change   in   density
C. Write a top-level function that reads in   the   data   file   and   guides   the   computation.
Setup your workspace for the project 
1.   Create a   Project 3 folder in a   conveniently   accessible   location
2.   Download GoldieJuly2019.csv, testDensity.py and testThermocline.py 
3. Copy stats.py and analyze.py from lab folder   into   the Project03 folder
Project Tasks (T1-T3) 
T1. Write your library of useful statistical functions 
In the stats.py file you started in the   lab, add the   following   four   (4)   functions.   Each   function should   have a single   parameter, which should be a   list of   numbers.   The   functions   should   loop   over the   numbers   in the list, compute the given statistic,   and return it.
1.      mean(data) - computes the   mean of the list   of   data.
2.      min(data) - computes the min   of the   list   of data.
3.      max(data) - computes the   max of the   list   of data.
4.    variance(data) - computes   the   variance   of the   list   of data.
As you   probably   recall, to compute the mean you sum   all the   values   in   the   list   and   divide   by   the   number of items.   Notice that stats.py already has a function   to   do   the   summing   up.   Instead   of reinventing the wheel why not have the mean function   call   the sum function   you   already wrote?   This   is an example of code reuse.
The   number of items   in the   list   is the same as the   length of the   list.   In   this   case,   do   use   the   Python   built-in function len() to determine   how   many   items are   in the list. This   is   another example of code   reuse. 
Write functions to calculate the min and max of the   items   in the   list. Do NOT use built-in functions to do this. 
Finally, to calculate the variance you can use the   following   formula:
The algorithm for this formula says that you will sum up   all   of the squared   differences   between         each   list   item and the   mean of the   items and divide   by the total   number of   items   minus   1.   There   is a   mathematical   reason why you divide   by   N-1 and   not   N.
Run stats.py and   make sure that   it   is working correctly.
Required Output 1: Include a description   in your report   how you determined   your   stats functions were working correctly. (e.g., take a screenshot of the output   of   calling   functions   with   a   simple list(s) of values and display   the   result) 
T2. Write a program to compute statistics of a column of data 
Using your analyze.py file from the lab, update   it so   that   it   computes   the sum, mean, variance, max, and min statistics.   Recall that we are   using command   line   arguments   to   obtain   the file name and column number from the user.   Print the statistics to   the   terminal.
Calling analyze.py with the hurricanes.csv file and column 1 as command   line   arguments   should produce the following statistics:
sum : 103.00
mean: 7.36
var : 12.55
min : 2.00
max : 15.00
Required Output 2: Demonstrate   that your program works with a column   from GoldieJuly2019.csv data file   provided with this project. One way to do   this   is   to   insert   a function   in the cell at the bottom of a   column to   calculate   a   statistic.   For   example,   placing =Average(B2:B2977)   in the cell below any column will calculate   the   average   of all   the   cells above   it.   For column 2 this would give a value of   10.795.   Compare this value with   your   stats   mean function.   Include a screenshot of the printed output of your   program   and   a screenshot   of   the data files calculation as evidence that your library function   works. 
T3. Calculate the thermocline depth in Great Pond for July 2019 
The   next task will be to write a program that   computes   the   depth   of the thermocline   on   Great   Pond for each day in July 2019. The thermocline   is   the   depth   at which   the   water   density changes   most quickly, creating a layer of colder, denser water   below   a   layer   of warmer   water   that tends   not to   mix. 
To do this you will write three functions:
1. a function that converts water temperatures into water densities
2. a function that computes the depth of the maximum   change   in   density
3. a top-level function that reads in the   data file   and   guides   the   computation.
T3a. Setup 
Create a   new file, thermocline.py.   Put your name, date, and   class at   the   top,   along   with   a   comment indicating what the program will do (compute   the   thermocline).
T3b. Convert temperatures to densities 
Write a function called density that takes   in one   parameter, temps,   that   is   a   list   of temperatures. The function should first create a new   empty   list to   hold   density   values,   typically   designated with the Greek letter rho. Then,   it   should   loop   over the temps   list   and   for   each temperature value compute the density using the following   equation:
rho = 1000 * (1 - (t + 288.9414) * (t - 3.9863)**2 / (508929.2*(t + 68.12963)))
It should then append each computed density to   a   list that   will   be   returned   to   the   caller.
Test your function using the   included testDensity.py file.   It should   print out the following   if your   density function is working   correctly.
24.47 -> 997.21 
23.95 -> 997.34 
24.41 -> 997.22 
23.81 -> 997.37 
19.92 -> 998.25 
16.88 -> 998.82 
14.06 -> 999.26 
11.56 -> 999.57 
9.82 -> 999.74 
9.13 -> 999.80 
8.82 -> 999.82
T3c. Compute the derivative of the densities 
Note: If you   have   not taken   Univariate Calculus yet a derivative   is just a slope at   a   point.   Slope   is defined as the rise of the function over the   run.   So   in   this   program we   are   going   to   calculate         the change   in density as the depth increases   and   locate the   depth   where   the   maximum   change   occurs.
Add a function named thermocline_depth to thermocline.py that computes the   derivative   of   density with   respect to depth, or how fast the density   is   changing   as you   get   deeper.   The function will take   in two lists: one is the   set   of temperatures, the   other   is   the   set   of corresponding   depths. The function will return one value: the depth of the maximum change in density.   The      algorithm below gives the function. 
def thermocline_depth( temps, depths ): 
# assign to rhos the result of calling the density function with temps as the argument 
# create an empty list named drho_dz 
# loop for one less than the length of rhos 
# append to drho_dz the quantity rhos[i+1] minus rhos[i] divided by the quantity depths[i+1] minus depths[i]
# sanity check (optional): print out temps[i], rhos[i], and drho_dz[i] for visual inspection 
# assign to max_drho_dz the value -1.0 
# assign the maxindex the value -1 
# loop for the length of drho_dz (loop variable i) 
# if drho_dz[i] is greater than max_drho_dz 
# assign to max_drho_dz the value drho_dz[i] 
# assign to maxindex the value i 
# assign to thermoDepth the average of depths[maxindex] and depths[maxindex+1]
return thermoDepth
Test your thermocline_depth function using the included testThermocline.py file.   It should output a depth of 6.0m (note that the   maximum   change   of   0.44   at   that   depth   --   you   do   not   need   to   report this,   but   if you   run   into   problems,   knowing what the   maximum change   is supposed to         be can help you   debug   your   code). 
T3d. Compute the thermocline for each day in July The final step   is to 代 写CS152 Project 3: Calculating ThermoclinesPython
代做程序编程语言write the main function that reads   in   data   from   the   included GoldieJuly2019 file, extracts all of the temperature fields in order,   computes the thermocline_depth and   prints      the day and thermocline_depth value.
The file   includes all of the data fields for the month of July   and   a   single   header   line.
Note: Pay   particular attention to the   indices. The field   indices for the depths (in   meters)   [1,   3,   5,   7, 9,   11,   13,   15] are   located at field   numbers      [10,   11,   16,   17,   15,   14,   13,   12]   in the
GoldieJuly2019 file. You   may want to double-check the field numbers before   starting   by   looking   at the   header   line.
The algorithm given   below   is not strictly line   by line.   Each   comment will   correspond   to   one   or   more lines   of   Python.
def main():
# these are the fields corresponding to the temperatures in order by depth
# note they use 0-indexing
fields = [10, 11, 16, 17, 15, 14, 13, 12]
# these are the depth values for each temperature measurement
depths = [ 1, 3, 5, 7, 9, 11, 13, 15 ]
# open the data file and read past the header line
# assign to day the value 0
# for each line in the file
# split the line on commas and assign it to words
# if the time is about noon (12:03:00 PM)
# add one to the day variable
# assign to temps the empty list
# loop over the number of items in depths (loop variable i)
# append to temps the result of casting words[ fields[i] ] to a float
# assign to thermo_depth the result of calling thermocline_depth with temps and depths as arguments
# print (or save to a file) the day of the month and thermo_depth separated by a comma
if __name__ == "__main__":
main()
Required Output 3: Run your program and create a plot of the results with day on the x-axis and thermocline depth on the y-axis. Include this plot in your report
Reflection Questions: Required Element    4: Follow-up Questions: 
1.      Explain what   is   meant   by the term “code   reuse” and give an   example?
2.       Explain what   is   meant   by the term “modular design” and give   an   example?
3.      Perform. a Google search for a woman statistician and   give   a   one   sentence   description   of   a contribution they   made.
Extensions Each assignment will   have a set of suggested extensions. The   required tasks   constitute   about   85% of the assignment, and if you do only the   required   tasks   and   do   them well   you will   earn   a   B+. To earn a   higher grade, you   need to undertake   one   or   more   extensions.   The   difficulty   and      quality of the extension or extensions will determine your final grade for the assignment.   One complex extension, done well, or 2-3 smaller extensions are typical.
● Write functions in your stats.py file to   compute   more types   of statistics.
● Use your code to   compute statistics   on   a   data   set   of your   own   choosing.
● Compare different times   or time   periods   in the   Goldie   data.
●       Add more command-line control options,   such   as   specifying   what   time   of day   to   compute   the thermocline.
●       Explore   how the thermocline changes   and why?   What   are   the   min   and   max   thermocline   values for July? What if you graph wind direction and thermocline together,   is there   a relationship?
● Automate the   process of making a graph   from   data(   Hint:   Matplotlib)
Submit your code 
Turn   in your code (all files ending with   .py)   by zipping the file   and   uploading   it   to   Google   Classroom.
When submitting your code, double check the following.
1.       Is your name   at   the   top   of   each   Python   file?
2.       Does every function   have a docstring (‘’’ ‘’’)   specifying   what   it   does?
3.       Is your Lab   04   folder   in   your   Project   04   folder?
4.       Have you checked to   make sure you   have   included all   required   elements   and   outputs   in   your project   report?
5.       If you   have done an   Extension,   have you   included this   information   in your   report   under   the   Extension   heading?   Even   if you   have   not done any extensions,   include a section   in   your report where you   state   this.
6.       Have you acknowledged any help you   may   have   received from   classmates,   your
instructor, the TAs, or outside sources (internet,   books, videos,   etc.)?   If you   received   no   help at all,   have you   indicated that under the Sources   heading   of the   report?
Write your project report 
Reports are not included in the compressed file! Please don’t   make the graders   hunt for your report.
You can write your report   in any word   processor you like   and   submit   a PDF document   in   the Google Classroom assignment folder. Or   just   use a   Google   Document   format.
Review the Writeup Guidelines document.
Your intended audience for your report   is your peers who   are   not   taking   CS   classes.
From week to week, you can assume your audience   has read   your   prior   reports.   Your   goal should   be to explain to   peers what you accomplished   in the   project and   to   give them a sense of how you did   it. The following   is   a   list   and   description   of the mandatory sections you   must   include   in your report.   Do   not   include the descriptions   in your report,   but   use them as a guide   in writing   your   report.
● Abstract 
A summary of the   project,   in your own words. This should be   no   more   than   a few
sentences. Give the   reader context and   identify the   key purpose   of the assignment. An abstract should define the   project's   key lecture concepts   in   your own words for a general,   non-CS audience.   It should also describe the   program's   context and output,   highlighting a couple of important   algorithmic   and/or scientific   details. Writing an effective abstract   is an important   skill.   Consider the   following questions while writing it.
○       Does   it describe the   CS   concepts   of the   project   (e.g. writing   well-organized and efficient code)?
○       Does it describe the specific   project   application   (e.g.   generating   data)?
○       Does   it describe your solution   and   how   it was   developed   (e.g. what   code   did you write)?
○       Does   it describe the   results   or outputs   (e.g.   did   your   code   work   as   expected and what did the   results tell you)?
○ Is   it concise?
○       Are all of the terms well-defined?
○       Does it   read   logically   and   in   the   proper   order?
● Methods 
The   method section should describe   in clear sentences (without   pasting   any code) at least one example of your own   computational thinking   that   helped   you   complete your project. This could   involve   illustrating   how a key   lecture   concept   was applied to creating an image,   how you   solved   a   challenging   problem,   or explaining an algorithmic feature that   is essential to your program   as well   as why   it   is so essential. The explanation should be   suitable for   a   general   audience   who      does   not   know   Python.
● Results 
Present your results   in a clear manner   using   human-friendly   images or   graphs labeled with captions and   interpreted for a general audience such   as your   peers   not   in the course.   Explain, for a general,   non-CS audience, what your output means and whether it   makes   sense.
● Reflection and Follow-up questions 
Draw connections   between   lecture concepts   utilized   in this   project and real-world   problems that   interest you.   How else could these concepts apply to our everyday lives? What are some specific things   you   had   to   learn   or   discover   in   order to complete the   project?   Look for a set of short answer questions   in   this section of the report   template.
● Extensions (Required   even   if you did   not   do   any)A description of any extensions you undertook,   including text output   or   images   demonstrating those extensions.   If you added any modules, functions, or   other   design components,   note their structure and the algorithms you   used.
● References/Acknowledgements (Required even   if there   are   none)
Identify your collaborators,   including TAs and   professors.   Include   in that   list   anyone whose code you   may have seen, such as   those   of friends who   have   taken the course   in a   previous semester. Cite any   other sources,   imported   libraries, or tutorials you used to complete   the   project.

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
