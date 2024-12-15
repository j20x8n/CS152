java c
CS152 
Project 4: Penguin Population Viability Analysis (PVA)
For project 4 we're going to move   to   the world   of ecological   modeling.   In   particular, we're going to   model the change   in the population of Galapagos   Penguins over time given certain ecological pressures.
Our goal   is to   model the risk of extinction over   some   number   of years. The   model we will use   is fairly simple, but   you   can choose to add complexity to the   model once   the   basic system is   working.
One   new aspect for this   project   is the use of   random values   in the simulation.   Because the world doesn't exhibit strong regularity, we're going to   model this uncertainty   by   using a   random number generator. 
For example,   El   Nino, an   important factor in Galapagos   Penguin survival,   does   not   occur on   a   perfectly   regular schedule,   but   it does tend to occur at least   once   every   5-7 years.   We   can model this   by assigning a   1.0/5.0 or   1.0/7.0   probability of an   El   Nino to any   given   year.
Then, each year of the simulation, we effectively roll a   5-sided   or   a   7-sided   die   and   declare   an   El   Nino year if it comes   up with a   1.   If the year   is   an   El   Nino year,   then   the   penguin   population drops significantly.   If it   is   not an   El   Nino year, the   population sees a   small   amount   of growth.
Because of the   random variables   in the   model, each time we   model   100 years the computer will   generate a different   result.   In one simulation, the   population   may go extinct   in   20   years,   in another simulation   it   may   not go extinct at all.   In order to   achieve   a   reasonable   estimate of the   true   probability of extinction over   100 years, we   have to run the simulation   many,   many   times and aggregate the   results. 
For example, the   probability of extinction   in   100 years   is the   number of simulations where the      population goes extinct, divided by the total   number of simulations.   Researchers   using   PVA   to   evaluate the   risk of extinction   in actual   populations   might   run the simulation   10,000 times or more   in order to get a stable estimate of extinction   risk.   Stability,   in   this   case,   means   that   if you      run the simulation   10,000 times, then the difference between that   average   and the   average   of   a   different   run of   10,000 simulations will be   small.
To design the simulation, we're going to use   a modular and hierarchical design   in   order to keep each function simple to write, test,   and debug.   By following this workflow we will   maintain   our momentum as developers and not   get   bogged   down with   code that   does   execute   properly. 
Outline of Project 4 Program Development 
Part 1. Developing a set of simulation functions 
A.    Write a function to set up the   parameters for the   simulated   population   using the   random module and test   it.   (initPopulation).
B. Write a function to simulate   population   in a single year and   test   it   (simulateYear)
C. Write a function to run a single year   of the   simulation   and test   it   (runSimulation)
D. Write your main ()function that takes command line arguments and   tests   it. Part 2. Calculate the Cumulative Extinction Probability Distribution (CEPD) 
A. Write a function that takes the result of your simulation   and test   it   (computeCEPD)   B. Compare the extinction distribution curves for a 3-year,   a   5-year,   and   a   7-year   El Nino   cycle.
Tasks 
T1. Setup 
If you   haven't already set yourself up for working on the project,   then   do   so   now.
Navigate to your project folder. Open VSCode and create   a   new   file penguin.py. For this   week,   all of the simulation functions will be in this file, though   you   can   use   the   functions   in   your stats.py file from   Lab 3 to analyze the results,   if you choose   to   pursue   an   extension   that   requires   it. 
T2. Write a function to initialize the population 
Create a function initPopulation, which takes two parameters: the   initial   population   size   and the   probability of an   individual being female. The function should   return a   list   of the specified size.   Each entry   in the list will   be either   an 'f' or   an 'm'.
The pseudocode would   be:
1.       Define a function initPopulation with two   parameters   (e.g. N,   and probFemale)
2.       Initialize a variable (e.g. population) to   the   empty   list.
3.       Start an   indexed for loop based on the   size   of the   population.   On   each   iteration   generate   a   random   number using random.random().   If the value   is less than the   probability of an   individual   being female (probFemale), append an 'f' to the   population   list.
Otherwise, append an 'm' to the   population   list.
4.       Finally,   return the   population   list.
Use the following test function to see   if your initPopulation function is working   properly.   It should   print out a   list of   10   individuals with an appropriate   mix of   'f'   and   'm'   elements.   Run   it   a   few times to convince yourself that you are getting randomized   lists.   If the   lists   are   all   one   or the   other sex then go back   and   review your   code.
# test   function   for   initPopulations
def   test   ():
pop   size   =   10
probFemale   =   0.5
pop   = initPopulation   (pop   size,   probFemale)
print   (   pop   )
if __name__ == "__main__":
test()
T3. Write a function to simulate a single year 
Create a function simulateYear that takes six parameters in the   following   order:
● pop: the   population   list
● elNinoProb: the   probability of an   El   Nino
● stdRho: the growth factor in a   regular year. This   number   is   meant to   allow   the   population to grow each year and   is expected to   be greater   than   1.
● elNinoRho: the growth factor in an   El   Nino year. This   number   is   meant to   reduce   the   population and   is therefore less   than   1.
● probFemale: the   probability   of a   new   individual   being female,
● maxCapacity: the   max   carrying   capacity   of the ecosystem.
The first step   in the function   is to determine   if it   is an   El   Nino year.   Set   a   variable   (e.g.
elNinoYear) to False. Then compare the result of random.random() to   the   El   Nino
probability.   If the random.random() result   is   less than the   El   Nino   probability, then set
elNinoYear to True.The second   part of the function   is a loop over the   existing   population   list.   Before starting the   loop, create a   list   called newpop and set   it   to   the   empty   list.   Inside   the   loop, implement the following algorithm given in   pseudocode   below:
#newpop   =   []
#for each penguin in the   original population   list
# if the length of   the   new population   list   is   greater   than maxCapacity
# break, since we don't want   to make   any more penguins
# if   it   is   an   El   Nino   year
# if random.random   () is   less   than   the El Nino   growth/reduction   factor
# append the penguin to   the   new population   list
#   else
# append the penguin to   the   new population   list
# if random.random   () is   less   than   the   standard   growth   factor   -   1.0
# if random.random   () is   less   than   the   probability   of   a   female
# append an   'f'   to   the   new population   list
#   else
# append an   'm   to   the   new population   list
#return newpop
T4. Test the simulateYear function 
To test your simulateYear function, add   the following code to your test   function.   newpop = simulateYear   (pop,   1.0,   1.188,   0.41,   0.5,   2000)
print   (   "El Nino   year"   )
print   (   newpop   )
newpop = simulateYear   (pop,   0.0,   1.188,   0.41,   0.5,   2000)
print   (   "Standard year"   )
print   (   newpop   )
You should see the   population   reduce to 3-6   individuals   in the   El   Nino year and   grow   to   11-14   individuals   in the standard year.   Run   it a few times to see the variation.
T5. Write a function to run a single simulation 
The next step is to write the   runSimulation   function. This function   takes   in   8   parameters.   You can use   the   definitions   below:
def runSimulation( N,                                                               # numb of years to run the
simulation
initPopSize,                                # initial population size
probFemale,                               # prob a penguin is female
elNinoProb,                                # prob El Nino occurs in a given
year
stdRho,                                           # pop growth in non-El Nino year
elNinoRho,                                   # pop growth in an El Nino year
maxCapacity,                           # max carrying capacity of ecosystem
minViable ):                               # min viable population
The function should   initialize a   population, then loop   N times.   Inside the   loop   it should   call
simulateYear and assign the return value back   to   the   population   list.   If,   after   simulating   a year, the   population   is smaller than the   minimum viable   population or it consists   of   only   one               gender, then the function should return the year of extinction.   If the   loop completes   all   N   times   and there   is still a viable population, the function   should   return   N.
The detailed pseudocode   is   below:
The function should first assign to a variable (e.g. population) the   result   of   calling
initPopulation with the appropriate arguments. Then it should set   another variable   (e.g. endDate) to N (the number of years to run the   simulation).   The   variable endDate will   be   what   the function   returns.
The   main   part of the function should   be a   loop that   runs N times.   Each time through the   loop   it   should:
1.       call simulateYear with the appropriate arguments, assigning the   result   to a   new   list   variable   (e.g. newPopulation),
2.       test   if there   is a viable   population, and
3.       assign to   population the   new   population
A viable   population   must   have at minViable individuals and there   has to   be at least   one   male   and one female.   If any of these tests fails, then set endDate to the   loop variable value   and
break out of the loop. The   Python keyword break will cause   execution   to   stop   looping   and   start   executing the code after the   loop
If you want to view the   population   numbers over time,   print out the length of the   population   list   at   the end   of each   loop.
T6. Test runSimulation 
Add some test code to your test function that calls runSimulation a   few   times   with   some
appropriate arguments.   Make sure the initPopSize argument is   larger than the minViable argument.   Using a small value for the   probability of an   El   Nino (e.g.   0.1) should   result   in   a   return   value of N (the   population should survive).   If you   use a   large   probability   of   El   Nino   (e.g.   0.5)   the      return value should   be   much less than   N.
Default values for the simulation arguments are as follows:
N  201
Initial Population Size  500
Probability of Females 0.5
Probability of an El Nino 1.0/7.0
Growth Factor in a standard year 1.188
Growth Factor in an El Nino year 0.41
Maximum Carrying Capacity 2000
Minimum Viable Population 10
T7. Define a main function that runs many simulations 
The top level function   is your main function. Give   it   one   argument, argv, which will   be   the   list   of   strings from the command   line.
A. Usage statement 
Start the main function by testing if there are at   least three   arguments   on   the   command line. The first argument will be the name   of the   program, the   second   should   be   the   numbe代 写CS152 Project 4: Penguin Population Viability AnalysisPython
代做程序编程语言r   of simulations to   run, and the third should be the typical   number   of years   between   an   El Nino event.   If there are   less than three    (len   (argv) < 3), print out a usage statement and exit. 
B. Extract values from the command line arguments 
After the test for arguments, cast the second argument    (argv   [1])   to   an   integer   and assign   it to a variable that specifies the number of simulations to   run   (e.g.   numSim).   Cast   the third argument    (argv   [2])   to an   integer and assign   it to   a variable   that   specifies   the   typical   number of years   between an   El   Nino event.
C. Set up local variables 
Create variables for each of the simulation parameters in the   table   above   not   already assigned and give them the default values. You should also   create   a   variable   to   hold   the   results of the simulations and   initialize   it to the empty   list. 
D. Write the main loop that runs simulations 
Loop for the   number of simulations.   Inside the loop, append to your   result   list the   result   of   calling runSimulation with the appropriate arguments. This list will   hold   the   year   of extinction for each simulation   run.
E. Calculate the probability of survival after N years 
Count   how   many of the   results   in the   result   list are   less than   N (the   number of years to simulate).   Divide that count   by the total   number of simulations and print   out the   result.   This   is the overall   probability that the   penguins will go extinct within the   next   N years. 
Test it: Run your program   using   100 simulations and see what you   get.   Does   it   change   a   lot   if   you   run   it   repeatedly?   Run   it with   1000 simulations and see   if the   results are   more stable.
T8. Compute the Cumulative Extinction Probability Distribution The   next task   is to write a function that takes the list   of   results, which   is   a   set   of   numbers   indicating the last year in which the population   was   viable,   and   convert   it   to   a cumulative extinction probability distribution (CEPD).The CEPD will   be a   list that   is as   long as the   number of years   in   the   simulation.   Each   entry Y   in      the CEPD   is the   number of simulations where the population has   gone   extinct   by   year Y   divided   by the total number of simulations.
The computeCEPD function should take two arguments: the list   of   results from
runSimulation (a list of integers), and the   number of years the simulation   ran   (N).   The computeCEPD function has three   parts.
a.       The first   part   is to create a   list (e.g.   CEPD) with   N zeros. You   can   do   this   by   appending   N   zeros to an   empty   list   in a   loop.
b.       The second   part   is to loop over the list   of   results   (extinction   years).   If the   extinction year   is   less than   N,   loop from the extinction year to   N and add one   to   each   of those   entries   in   the   CEPD   list.
c.       The third   part   is to   loop over   the CEPD   list and   divide   each   entry   by   the   length   of the
extinction year results list, which is also   the   number   of simulations. After this,   return   the   CEPD   list.Add a call to the computeCEPD function to the end   of your top   level function.   Then   have   your         top   level function   print out every   10th entry   in the CEPD   list   (remember   how the   range function   works).   Run your penguin simulation   1000 times using the standard   parameters.   Repeat   the process three times and show the results   in your writeup.   How   much variation   is there   in   the   results?
Required plot 1: Generate three plots of the CEPD for three runs of 1000 simulations for 201 years with the default parameters.
T9. Compare 3, 5, and 7-year El Nino cycles 
The final step is to use your simulation to compare the extinction distribution curves for a 3-year El Nino cycle, a 5-year El Nino cycle, and a 7-year cycle. What do your results indicate?
Required plot 2: a plot of the CEPD for the three El Nino cycle options. 
Required Element 1: 
Follow-up Questions 
1. What is the difference between the following two code snippets?
# example 1
a = [5, 10, 15, 20]
for i in range(len(a)):
print(a[i])
# example 2
a = [5, 10, 15, 20]
for x in a:
print(x)
2. Why do we test code incrementally? Why not write all of the code and test it once?
3. Why do we use random numbers in this population model?
4. What is your favorite wild (undomesticated) animal?
Extensions 
Extensions are your opportunity to customize your project,   learn something   else   of   interest   to you, and improve your grade. The following are some   suggested   extensions,   but   you   are free   to   choose your own.   Be sure to describe any extensions you   complete   in your   report.
●          Use matplotlib to automate the   process of creating   plots.
●          In addition to the   required   plots, show a   plot of the   population   levels for   a   single   simulation.
●       Add other model   parameters to   the   command   line.   The   complex   version
of this extension   is to   have flags for your program so that the   user    can   use   a flag,   like   -E, to specify a given   parameter.   For example,   running   python   penguin.py -E 5 would   modify the   El   Nino frequency,   but   leave all other parameters at their default   values. 
●          Display the CEPD data   in a graph   using   matplotlib, or   have   your   code write   out   the   results as a CSV file   and   use   a   graphing   program.
To write the data, adjust the code   in   penguin.py so that   it   prints   out the   year   and   CEPD   for all years.   Redirect the output to a   .csv file.   Use   Excel or other   software   to   plot   the data and   post the image   on the wiki with a thorough   description   of   its   contents.
●          Explore variations on the   model.   For example, what effect on the   extinction   probability   do   you see   if you adjust the   number of years   in the   El   Nino cycle?   Does changing the carrying capacity to 3000, for example, modify the   100-year extinction   probability   for   the 5 year   El   Nino cycle?
●          More rigorously test the variation in the simulation outcomes.   Use   your   standard
deviation function to compare the standard deviation of the probability that   the population goes extinct at a particular time.   For example,   consider   200   years when   the   El   Nino cycle   is 5 years.   Running the simulation with   numSim=100 will   likely   yield   a larger standard deviation in the values of the CPEF   at t=200   (the   final   year   of the   simulation) than running the simulation with numSim=1000 will. 
Submit your code 
Turn   in your code   by zipping the file and uploading   it to   Google   Classroom.   When submitting your code, double check the following.
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
From week to week, you can assume your audience   has read   your   prior   reports.   Your   goal should   be to explain to   peers what you accomplished   in the   project and   to   give
them a sense of how you did   it. The following   is   a   list   and   description   of the mandatory sections you   must   include   in your report.   Do   not   include the descriptions   in your report,      but   use them as a guide   in writing   your   report.
● Abstract 
A summary of the   project,   in your own words. This should be   no   more   than   a few
sentences. Give the   reader context and   identify the   key purpose   of the
assignment. An abstract should define the   project's   key lecture concepts   in   your         own words for a general,   non-CS audience.   It should also describe the   program's   context and output,   highlighting a couple of important   algorithmic   and/or scientific   details. Writing an effective abstract   is an important   skill.   Consider the   following questions while writing it.
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
