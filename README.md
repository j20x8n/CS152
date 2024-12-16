java c
CS152 
Lab Exercise 5: Representing Elephants as Lists 
The   purpose of this   project   is to   practice   modular   design of code with a   larger, slightly   more complex simulation than the penguin simulation.   We will   be   making use of nested lists--lists   of lists--in order to manage   more complex   data. 
This is the first of a two-part project where   we   will be simulating the elephant   population   in Kruger National   Park, South Africa. The   carrying   capacity of the park   is approximately   7000 elephants (1 elephant   per square   mile of   park).   Previous efforts to manage the   population involved culling approximately 400 animals   per   year. After the development of an elephant contraceptive, the current effort to   manage the population   involves using a contraceptive dart   on   adult female elephants to limit   the   birth   rate.
The elephant   population simulation will be more detailed   than   the   penguin   simulation,   because   there will be more characteristics of each animal   which   need   to   be   accounted   for.
Lab Tasks (L1-L6) 
L1. Setup and problem description 
Make a folder called Project_05 where you keep your current work.   Because the   code you   write   for the lab will also be used   in   the   project we   will   dispense   with   the   lab   folder   this   week.   Create   a   new file, elephant.py, and save   it   in your Project_05 folder.   Because we will   need to   calculate some statistics   in this   project (e.g., the mean), copy   your stats.py file   into   your Project_05 folder.   Make sure to test your statistics functions to assure you that they   are working   properly.
The design of the simulation this week will be similar to the   penguin   simulation   in   the   last project. The   main function (that serves as the conductor of your   program) will   handle   setting   parameters, calling the function that runs   the simulation, and   summarizing   the   results.   The diagram below shows the hierarchical relationship   of all   of the functions   you will   be writing. 

Recall that last week we represented penguins   using   only   a variable   for the   animal’s   sex.   This   week we will represent elephants using sex, age,   and   the breeding status of each   individual animal   in order to   more accurately   model the   number of births each year and   the   effects   of   using   a contraceptive dart.Here are some of the assumptions we will make about   the   elephant   population. READ them   carefully because there are   important details that   you will   need   to   accurately   represent   your elephant   model.   Make sure that you understand the boundaries   between   categories   and the   differences for males and females, calves, adults and   seniors.
1.       Elephants   live about   60   years.
2.       Female elephants over age   12 and   less than   or   equal to   60   can   become   pregnant.
3.       The gestation   period   is 22   months.
4.       Elephants over age 60 (seniors)   have   a   survival   rate   of only   20%   per year   (it   is   unlikely,   but   not   impossible to   live   beyond 60).
5.       For adult elephants ages 2 through   60, the   survival   rate   is very   high:   99.6%.
6.       The survival   rate of a calf (age   ==   1),   is   85%.
7.       The average time between births for an   adult female   is   3.1   years.   Since   the gestation   period   is 22   months, that   means that when a female   is   not already pregnant, the chance,   per month, of getting   pregnant   is   1.0 / (3.1*12   -   22),   if she   is   not on contraceptive.
8.      A contraceptive dart ends any existing pregnancy   and   prevents   the   elephant   from   getting   pregnant for the   next 22 months.
For this simulation, we're going to   model gestation and contraception on   a   per   month   basis. However, we'll   model survival and darting on a per   year   basis.   We   do   this   because   gestation and contraception don't follow simple yearly intervals,   but survival   rates   are   easier to   compute   per year.
As with last week, you'll employ modular design and start   building   your   program incrementally one function at a time. After   you have written each function you   will test it   carefully   to   make   sure   that   it works as specified. Note: Not following this advice is guaranteed to lead you down a path of pain! Understand that this is a two-part project and that next week’s project depends on this week’s project working properly! 
New this week: Unlike last week, where we gave each function   many,   many   parameters, we're      going to collect all of the   parameters for the simulation   in a list and   pass the   list   as   an   argument   into our functions.   For this to work, we   have to   invest a little time   into   setting   up   a   connection between a variable and   its   index   in the   parameter list. The   benefit   is that our function   definitions   will   be simpler (one composite   parameter instead of many   individual   parameters)   and   more uniform.   It   is   important that we set   up the   list of parameters carefully and   use   the   same   location   in the list for the same   parameter throughout the   code.
The following list shows all of the parameters   of the simulation   and   their   initial   default   values.
Note: The darting probability parameter is set to 0.0. This will be updated via a parameter provided by the user on the command line. 
Calving Interval 
3.1 
Darting Probability 
0.0 
Juvenile Age 
12 
Maximum Age 
60 
Calf Survival Probability 
0.85 
Adult Survival Probability 0.996 
Senior Survival Probability 
0.20 
Carrying Capacity 
7000 
Number of Years 
200 
L2. Create a list of parameters In order to   pass all of the   parameters at   once, we're going to   use   a list.   One   method   of   setting      up the   list   is to just   make a   list of   numbers. This   has the   benefit that we can   look   at   the variable   names   in the   list to tell   us the   meaning of each   position   in the   list.
Using the template below,   make a test function   in your elephant.py file that   creates   the   parameter list and then   prints   it to the   console.
Note: The order of the parameters must match that given in this document. Changing it will break the testing scripts.def test():# assign each parameter from the list above to a variable using thefollowing names:calvingInt = 3.1dartingProb = 0.0juvenileAge = 12maxAge = 60calfSurvivalProb = 0.85adultSurvivalProb = 0.996seniorSurvivalProb = 0.20carryingCap = 7000numYears = 200# create the parameters variable and assign it all the valuesparameters = [calvingInt, dartingProb,. . . ]# print the parameter listif __name__ == "__main__":test()First, verify that the   parameter list does   in fact contain all   the   parameters   and   that   they   are   in   the   correct order.   For now, we will   leave darting   probability at 0.0,   but   later on   we   will   add   the   ability      to get that parameter value from the   command   line.
Second,   notice that while working with the   parameters as a list   is an   ok   solution,   there   might   be   problems with this approach. Can you anticipate any   problems?   For example,   if we write a function that   needs to access a specific parameter, we will   have to remember that   parameter's      index   in the list. So, for example, the calving   interval   parameter will   be parameters[0] if you set   up the   parameter list with that value   in the first   position and parameters[5] will   be for the adult survival   probability. Then   realize that there are   nine   parameters   in this list and we   could   add more   in the future!
Using this arrangement   means   it   is easy to   make   mistakes when you   have to remember
whether a given value   is   in   position 4 or position 5.   It   also   makes   it   hard   to   modify   your   code   if   you   happen to change the order of the values   in the   parameter list or   even   add   new   ones.   If you   did   make changes,   it would   mean you would   have to go 代 写CS152 Lab Exercise 5: Representing Elephants as ListsR
代做程序编程语言through all of your code   and   change   all      the   indexes wherever you were accessing a parameter value. That's a   lot of   changes   and   it creates a lot of opportunities to   make   mistakes.Our solution will   be to create a system of indexes that   relates   the   position   to   the   item   in   the   parameter list using a mnemonic-like   naming strategy.   This   provides   flexibility   for   changes      without changing our code everywhere an   index   is used.   To   do   this   we   will   declare   a   set   of   variables with a specific naming   style. and assign   the   appropriate   index   number which corresponds to where   in the   parameter list the value   is located.   For example,   by   assigning to variable IDXCalvingInt the value 0 (the   index of the calving interval   in   the   parameter   list)   we   can access that value in   our   code   as follows: 
IDXCalvingInt =   0
probabilityPregnant = 1 /   parameters   [IDXCalvingInt]
In the elephant.py file, add variables for all the simulation   parameters   (after   module   import statements at the top of your file) and assign appropriate values for each   of the   parameters   in   the simulation (like   you did for IDXCalvingInt). When naming   index variables,   begin   each name with IDX to   indicate the value   is an   index, then use a   name that   indicates the   field.
L3. Representing an elephant as a list 
Because we will be representing individual elephants with   such   detail,   we   will   be   modeling   each elephant as a list with four features. We have   to   keep   track   of an   elephant's   sex   and   age.   For   females, we also have to keep track of whether an   adult female   is   pregnant,   and   whether   she   has   been   injected via contraceptive dart, and,   if so,   how   many   months are left   on   the contraception. The following table gives the attributes and their types.
Field 
Type 
Sex 
string 
Age integer 
Months pregnant integer 
Months contraceptive remaining integer 
Use the same IDX design as above. Create a separate set   of top-level variables   with   indexes   to   keep track of which entry   in the elephant list   is storing   information   about which field.   Write   the four assignment statements necessary to keep track   of   elephant   features.   Use   the   following   names: 
IDXSex = 0 
IDXAge = 1 
IDXMonthsPregnant = 2 
IDXMonthsContraceptiveRemaining = 3 
L4. Write a function to create and return a new elephant 
The function newElephant should create and return a   list with   all of the   necessary features   of   an   individual elephant. The newElephant function should have two   parameters: the   list   of simulation   parameters, and the age of the elephant to create.   It should   return   a   list   with   the   four   items above. 
def newElephant   ( parameters, age   ):
#Docstring for what this   function   does
elephant =   [0,0,0,0]
Add the values to the list   representing   a   new   elephant   using   the   algorithm below
return elephant
The newElephant function will need   to use the calving interval, juvenile age,   and maximum age parameters, so use the IDX names to access the   parameter list   in   your function.
a.      Assign to a variable elephant a list with four zeros   in   it.
b.       Then   use the   random   package to assign to elephant[IDXSex] either    'm   '   or    'f   '. Note: lookup random.choice() documentation or ask the   lab   TA.   This will   simplify   your   code and avoid another   if/elif statement.
c.       Then assign to elephant[IDXAge] the value of the age   parameter   (not   a   random   number,   but the value passed into   the   function).
d.       If the elephant   is female and if the elephant   is   of   breeding   age   (strictly   older than juvenile   age and less than or equal to the   maximum   age), test   if the   elephant   is   pregnant   (the probability the elephant   is   pregnant   is   1.0 / calvingInterval).   If the elephant   is   pregnant,   pick a   random   number between   1 and 22 (inclusive)   and   assign that   to   the
IDXMonthsPregnant position   in the elephant   list.
e.       No elephant starts out   on the   contraceptive,   so   the
IDXMonthsContraceptiveRemaining field of the elephant list will always be zero
when we create a   new elephant   because we   initialized that   index in the   elephant   list   with   0.
f.          Return the   elephant.
Finally, test the newElephant function by adding the following code   to your   test   function.Reduce the carrying capacity to around 5 elephants (so you can see the output on one line) and then print out the elephant population list. Just remember to change it back to 7000 later on. This code assumes you have a   variable   named parameters that   contains   the   parameters for the simulation and you have named   the   index variables   as   in   the   code.
# Code   inside test function:
population =   []
for i in   range   (parameters   [IDXCarryingCapacity):
population.append   ( newElephant   ( parameters, random.rand   int   (1,   parameters   [IDXMaximumAge]) ))
print   (pop)
Make sure that the data looks correct. There should be a spread of values. A mix of males and females. No males should be pregnant! (Don’t laugh, it has happened) Some females, within the correct age range, should be pregnant, but no female is on contraceptive. Run the test numerous times until you have convinced yourself that the newElephant function is working properly. If it doesn’t work correctly then debug until it does. This is a large 
project and if you start off incorrectly it will be very difficult to find the bugs later on. 
L5. Write an initPopulation function 
Write a function initPopulation (parameters) using the newElephant(parameters, age) function to create elephants. The init   Population function should take   in   the   parameter   list   and   return a   list of new elephants, where each   new elephant   is   a   list   itself.   The   number   of elephants to create is the carrying   capacity   parameter.
In the   last   project we   represented each   individual animal with a single letter   and   a   population   as   a   list such as   [‘f’   , ‘m’   , ‘m’   , ‘f’   , ‘f’   , ‘m’].   In this   project we will   be   representing each   individual   as a         list of four items: sex, age,   months pregnant, and   months   contraceptive   remaining.   This   means      that our population of elephants will be   represented as   a   list   of elephant   lists   such   as
[   [‘f’   ,22,12,0],   [‘m’   ,12,0,0],...]
The initPopulation function should   initialize a population   list to the   empty   list,   loop for   the   number of elephants to   create and append each   new elephant   (call newElephant with   a randomly chosen age   between   1   and the   maximum age   both   inclusive) to the   population   list   on   each   iteration.   It should then   return the   population list. Add code to your test function   that calls initPopulation and then   prints   out   the   population      list. Note: You may want to temporarily reduce the carrying capacity to 5 so that you can print out the population on one line and inspect it. Be sure to change it back to 7000. 
L6. Write a function to increment the age of the population 
Write a function incrementAge (population). This function   should take   in a   population   list   and   return a   population   list.   Inside   the function,   it should   increment each elephant's age   by   1         year accessing the age value by   using the IDXAge index.Add code to your test function that calls incrementAge. You will   be   passing   in   the   population list created by initPopulation and then assigning the   return value   from   the incrementAge function   back to the same variable.   Print out the new   population   list and   double-check   that   each   age was   incremented   by one and that   no other changes are   made to   each   elephant   list.
Congratulations! You have completed the lab portion of Project 5 and are ready to begin the project. 

         
加QQ：99515681  WX：codinghelp  Email: 99515681@qq.com
