java c
CS152 
Lab 6: Searching and Optimization
The   purpose of this lab/project   is to get you thinking about automating   a   scientific   experiment   and optimizing the parameters of a   process. This   is the second   part of our study of the elephant   population   in   Kruger National   Park   in   South      Africa. This week we'll be focusing on how varying the   parameters will   change   the   management   strategy.
Rather than   manually exploring the   parameter space, we will automate the process   and   use   a   search method to find the optimal darting percentage   given   the   simulation   parameters.
Setting up the Lab/Project 
Create a Lab06 folder and open VS   Code   in   it.
L1. Implement binary search on a sorted list 
In your Lab06 folder create a new file, search.py.   Then   create   a function searchSortedList that takes   in two   parameters, a list and a target   value. You   can   use   the   following   template.
def searchSortedList   ( mylist, value   ):
# assign to the variable   done,   the   value   False
# assign to the variable   found,   the   value   False
# assign to the   variable   count,   the   value   0
# assign to the variable   maxIdx,   the   one   less   than   the
length of mylist
# assign to the variable minIdx,   the   value   0
# start a while   loop that   executes   while   done   is   not   True
# increment count      (which   keeps track   of   how many   times
the   loop executes
# assign to testIndex the   average   of maxIdx   and minIdx
(use   integer math)
# if   the myList   value   at   testIndex   is   less   than
value
# assign   to minIdx   the   value   testIndex   +   1
# el   if the myList value   at   testIndex   is   greater
than value
# assign to maxIdx   the value   testIndex   -   1
#   else
#   set done   to   True
#   set   found to   True
# if maxIdx   is   less   than minIdx
#   set done   to   True
#   set   found to   False
return   (found, count)
Once you   have coded that up,   import the random package,   copy the following   test   function,   and   run   it to see   if your function finds the value 42   in the list   (it should).   Think   about why   it   can   take   a   different   number of steps each time you run the program.   Experiment   with   different   values   of   N and relate the number of steps that the function takes   to   complete   to   log2(N).
def   test   ():
a   =   []
N   =   10**6
for   i   in   range   (N):
a.append   ( random.rand   int   (0,N)   )
a.append   (42)
a.sort   ()
print   (searchSortedList   ( a,   42   ))
if   name   ==   "   main   ":
test   ()
This function is practice for creating the optimization function for the   elephant   simulation.   That   function will   have a similar structure, and   it will also execute   a   binary   search,   but   it will   have more   parameters and   be   more flexible   in   how   it works.
L2. Write a function to generate a default parameter list 
Create a Project06 folder and copy your elephant.py file from the   last   project.
Next, add a new function to your elephant.py file. The   function   should   be   called
defaultParameters ().   It should take   no arguments and   return a list with   all 代 写CS152 Lab 6: Searching and Optimization
代做程序编程语言  of the   necessary   parameters for the simulation with their default values.
calvingIn   t   =   3.1
probDart   =   0.0
juvAge   =   12
maxAge   =   60
probCalfSurvival   =   0.85
probAdultSurvival   =   0.996
probSeniorSurvival   =   0.2
carryingCapacity   =   1000
numYears   =   200
NOTE: For this project, set the default carrying capacity to 1000. 
L3. Write an elephant simulation function 
Next, also in your elephant.py file, create a function elephantSim. The   arguments   to   the function should be probDart and a parameter list, which   should   have   a   default   value   of   None.   In other words, set   it up   as   the following.
def   elephantSim   ( probDart, inputParameters   =   None   ):
First, set   up the   parameters.   If inputParameters is equal to the   value   None,   then   assign   to   parameters the result of calling your defaultParameters function. Otherwise, assign   to parameters the value of inputParameters.
Next, store the   parameter value for probDart in the correct location   in   the   parameters   list.
Then, declare an empty list named results where we will   store   the   return   from   the   call   to runSimulation as follows:
results = results + runSimulation (parameters) 
Place this   in a loop which will call runSimulation five times   and   collect   all   of the   results   in   a single   list. The structure of the   results list   is that of a   list of   lists.   Each   sublist   consists   of the   total   population and other statistics for a given   simulation year. 
Finally,   loop over the   results   list and calculate the average total   population.   Remember, the total   population for each year is the first element   in   each sublist.
elephantSim will return the following crucial piece of   information:   (carrying capacity) - (average total population of the five simulations). Cast this value as an   integer   before   returning.   Just like our cost function in all our   search   algorithms, this   metric will   guide   the   search   for   the   optimal   darting probability.
You can think of this return value as specifying whether too   many   or too   few   elephants   are   being   darted.   If the   return value   is   negative, then the   population   is too   big and we   need to tweak the darting   probability   higher so that the elephant   population shrinks; and if the   return value   is positive, then the   population   is too small and we   need to tweak the darting   probability   lower   so   that the elephant population   grows. 
L4. Test your elephantSim function 
Once you have written elephantSim, use the testfile test_elephantSim.py to   evaluate   its      performance.   It tests the percent darted for five different values. The   difference   should   go from negative (darting   probability too low) to positive (darting   probability too   high)   for the   default   simulation parameters.
Example output: (your numbers   may be different   because   of the   random   and   your   elephant   parameter boundaries are different)
probDarting 0.405 diff   -385 
probDarting 0.415 diff   -331 
probDarting 0.425 diff   -172 
probDarting 0.435 diff   -8 
probDarting 0.445 diff   152 





         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
