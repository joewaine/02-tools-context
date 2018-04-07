My Answers!

1. When this code is run in Node, e.g. node index.js, what are the two stages
of execution for this file called, and which order do they happen in?
  There are two stages happening here:

  1 - the compilation stage - the code is generated after being parsed.
 
  2 - the execution stage - the program is running or 'executes' the code


2. Write an explanation, using as much space as you need, relating to how the
first stage of execution for this file operates.
  -For example, identify the high level steps in a line by line overview and then
  define what each of those steps are accomplishing.

    Basically, the entire file will be read looking for where things should be defined/declared, this is essentially a stage for making the declarations. Places where mainly functions or variables or other considerations will need to be stored in the temporary memory. The scope is checked and then referred to determine where within the global spectrum they belong. For example, if a variable or a function happens to be declared within the global scope, it will get put at the very top or directly declared in the global "object". But of course there will also be the case where a variable or function will be nested within another scope or sub scope, so it will be considered within that range and not outside of it. There can also be an exception to this rule where variables that are set in a scope that is 'nested' but not declared with a convention such as "const", "let", or "var". These variables are then places directly in the global object. 

    After the entire file has been read/parsed - all functions and variables declared will be held strictly to their assigned scope.

    Here is a line by line assessment of the file: 

  ```
  0:    'use strict'
  1:    
  2:    var foo = 'bar';
  3:    
  4:    function bar() {
  5:      var foo = 'baz';
  6:
  7:      function baz(foo) {
  8:    
  9:        foo = 'bam';
  10:       bam = 'yay';
  11:     }
  12:     baz();
  13:   }
  14:     
  15:   bar();
  16:   foo;
  17:   bam;
  18:   baz();
  ```

line 2:
'foo' variable is created within the the global scope (it was place in the scope of the file, at the very top)

line 4:
the 'bar' function is globally declared.

line 5:
a local variable within the 'bar' function also named 'foo' is declared - so this reference of foo will be scoped within the bar function. If foo is referred to within the bar function, it will only refer to the foo that is declared within the bar function.

line 7:
in this line, another function is being declared (baz) - this will be scoped inside the 'bar' function. Additionally, the variable 'foo' is declared as a parameter argument for the baz() function (baz(foo))

line 9:
nothing is really happening here because foo is not a declaration. it is simply a consideration to be handled when the function runs and the parameter is passed.

line 10:
'bam' is not yet within the baz() or the bar() functions, it isn't even in the global scope, so it is treated as a new global variable known as 'bam',

line 12:
nothing happening - just an execution of bar which returns nothing.

line 15:
same as line 12 essential - just an execution that returns nothing.

line 16:
this simply references to foo but doesnt make any impact otherwise.

line 17:
this simply references to bam but doesnt make any impact otherwise.

line 18:
another execution, nothing happens.


3. Write an explanation, using as much space as you need, relating to how the second stage of execution for this file operates.
  -For example, identify the high level steps in a line by line overview and
  then define what each of those steps are accomplishing.  Write an explanation,
  using as much space as you need, relating to how the second stage of
  execution for this file operates.

  ```
  0:    'use strict'
  1:    
  2:    var foo = 'bar';
  3:    
  4:    function bar() {
  5:      var foo = 'baz';
  6:
  7:      function baz(foo) {
  8:    
  9:        foo = 'bam';
  10:       bam = 'yay';
  11:     }
  12:     baz();
  13:   }
  14:     
  15:   bar();
  16:   foo;
  17:   bam;
  18:   baz();
  ```


line 2:
this line executed in the second stage and the bar string is assigned to the 'foo' variable.

line 15:
'bar' function is executed.
line 15 being executed will cause the variable in line 5 to be executed, setting bas to the functional scope of the 'foo' variable.

line 12:
this line is executed next as it is a call to the function 'baz()', causing lines 9 and 10 to execute:
    -9: the string 'bam' is assigned to the functions scope 'foo' from line 5
    -10: the string 'yay' is assigned inside the 'bam' variable.

line 16:
it technically excutes but since its a just a string there will not be an outcome.

line 17:
bam will be executed which is simply a string, so there will not be an outcome in this case either.

line 18:
the baz function will be attempted to be executed but since it is scope inside of the bar functino and not globally scoped, a reference error will occur.



4. During the second stage of execution how many scopes have been registered
by the engine?

[answer]: There are 3 registered scopes.

  -Which segments of the code do they belong to?
 Identify the scopes/variables.

    -the global scope
      -'foo' from line 2
      -'bar()' from line 4
      -'bam' from line 10

    - the bar function scope
      -'foo' from line 5
      -'baz()' from line 7

    - the baz function scope
      -both variables used within 'baz()' aren't in its scope

5. When line 13 invokes the baz function, which foo will be assigned a value of
bam? More specifically, bam will be assigned to the foo in ??? scope. Give a
brief description in your own words to support your conclusion.


the foo that is declared within the 'bar' function's scope will be assigned because of 'lexical scoping'


6. Which scope, if any, will the variable bam on line 11 be registered to when the
first stage of execution occurs on this file? Provide a brief description in
your own words to support your conclusion.

case 1:
With 'use strict' being set, bam will get a referenceError.

case 2:
if 'use strict' is not used, bam will be part of the global scope.


7. For each line, 16 through 19, what is the return value for each?
 
    -'bar()' function returns undefined

    -'foo' call will just return the global foo contents: 'bar'

    -'bam' function will either return a reference error if 'use strict' is enabled as it is. Otherwise if 'use strict' is not enabled it would return 'yay'

    -the 'baz' function call will return a 'reference error' since that function is only accessible when it is in the scope of the 'bar()' function.