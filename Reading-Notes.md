## Reading 1

static-type: check at compile time  
dynamic-type: check at runtime  
gradual typing: add static type into a language that is dynamic type  

catch bugs in static checking is the easiest  
mutable is always devil  
document must contain assumption that the programming language doesn't provide  

goal of programs: communicating with other computer / other people  
primary goal: <b>safe from bugs, easy to understand, ready for change</b>  

a good programmer must be multilingual  

## Reading 2

verification: constructs a formal proof that the software is correct  
systematic testing  
module: part of software, specification: describe the behavior of a module  
test first programming: write testbench before write code  

systematic testing: <b>correct, thorough, small</b>  
test is goal to make it fail  
input -> subdomains -> partition  
subdomains: <b>disjoint, complete, nonempty</b>  

boundary is often where bug happens  

unit-test: document boundaries & subdomains in the test  

glass-box testing may include a new boundary  
statement coverage, branch coverage, path coverage  

integration test: a set of tests to cover the whole software  
trace the failure separately in functions, especially dependence  

regression testing: run tests after any small changes  
when meet a bug, add the bug-caused imput immediately into the testcase  
iterate: best way to use of time when problem is difficult or the space is unknown  

## Reading 3

Code review: read the code by the person who is not the author  
purpose: improve the code, improve the programmers  

Don't repeat yourself  

Comment where you need: write input, output, even source of the program  
never translate code into English directly  
divide code into paragraphs, describe them  

fail fast: if a problem/bug appears quickly, it's easiest to fix  
numbers are less readable than names  
constants may need to change  
constants may be dependent on other constants  

don't reuse parameters and variables  
name variables properly  
use abbreviation less as reviewer may not English-native  

never put tab characters into code as tab may diff in different settings  
never use global variables but use global constant  

consider the lifetime of variables  

only highest layer of a software should interact with users  
when writing a special case, stop, and think about the common case  

each function should only has a length of a page  
finally, keep each line short  
refactoring: make small steps, comment old code when rewriting, 
use static checking for changes, run tests after every changes, 
delete old code and commit to the version control  

## Reading 4

Specification act as a contract  
How to define `same behavior`?  
contract acts as a firewall  
specification: function, require, effect  
consider the implementation is far from reader  

null will cause bug if the object is used soon  
empty is always allowed as a parameter  
test case shouldn't include specific behavior  
all test must follow the spec  
mutation should never be allowed except for special case  
exception: signaling bugs, signal anticipated source of failure  

return as a union type instead of using a exception  
if a bug is indicated, assert it  
in TS, KeyError or IndexOutOfBound will return `undefined` value instead of exception  

## Reading 5

comparing specs: detereministic, decalarative, strong  

deterministic: presented with a state satisfying the condition  
underdetermined: the code may have different bahavior as time goes  

decalarative: never give detailed steps, just give the relation of I/R  
when operational, use commands  

compare the condition is a subset of the previous one or not  
strengthen the postcondition, weaken the precondition  

immutable: if modify, create a new one  
mutable: if modify, change at the origin one  

pass mutable value to a function is risky  
bug will stealth if a mutable value is returned, especially when it is passed into 
another function  
do defense copy always  

develop the snapshot of program, visualize the behavior  
specification should be coherent  
incoherent: do several things in one function  
specification should be strong enough, and beware of mutation  

## Reading 6

abstract data types has similar advantage with function  
creater, producer, observer, mutator  
ADT is defined by its operations  
coherent behavior  

use enumerations, use constant object  

test other three method by calling observer  

## Reading 7

a good abstract data type is that it preserves its own intervals  
representation exposure: class can modify the representation directly  
readonly, const: unreassignable  

patch rep exposure by defensive copying  
return a reference to a mutable rep object causes rep exposure  

abstraction function: maps rep values to the abstract values they represent  
rep invariant & abstraction function should documented into docs  
write assumptions of the rep into docs  
benevolent side-effect: the change of a rep value is invisible to client  

write a rep exposure safety argument  
establish invariant  
write a implementation, write an ADT, write the program lastly  

## Reading 8

interface: a list of method signatures without method bodies  
subtype: a subset of supertype  
structural subtyping: needn't mention the supertype, but be careful about immutability!  

Interface: doc for human & compiler, allowing performance trade-off,
method with intentionally undetermined specification, multiple views, 
more/less trustworthy  

inherit, override  
subclass inherits class's rep  
dynamic dispatch  

generic type: a type whose specification is in terms of a 
placeholder type to be filled in later  

put a helper function without assert.fail everytime should use a 
generic function  
enumerate: a small set of immutable value  

## Reading 9

functions in TypeScript is First-Class  
iterator: an object that steps through a sequence of elements  
use iterable types, not iterator itself  
Mutating a list that is currently being iterated over is simply not safe in general  
pure function: create a new output instead of modifying inputs  

higher function: take a function as an argument/return a function back  
write a iterator instead of using loops  

fp makes programmers focus on the heart of computation  

## Reading 10

discuss equality without mutation is easier  
define a equivalence relation between data  
if and only if AF(a) = AF(b)  

reference / value equality: whether objects is in same memory / value  

call a mutator; create a observable difference  
observational equality: cannot be distinguished now  
behavioral equality: cannot be distinguished even in the future  

TS/JS is lack of deep equality judging  
but deep equality operations should be use with care, especially, not use with ADT  

Always implement hashing consistent with equality  
Always use behavioral equality for hashing, so that hash values do not change over time.  
interning: reuse the instance  

# Reading 11

recursive data type: eg: immutable list  
implementation empty using the factory function without passing arguments  
put parameters into rep could be powerful and dangerous  

the immutable list is from a natural abstraction, ans is a generic type  
declaring ; implementing  
rewrite reverse using accumulate helper is more efficient  
a state change that doesn't change the abstract value represented by the object  
Any time you write an ADT, its specs must not talk about the rep.  

use a common design of wrapper  
do not use `instanceof`  

extract set of variables  
try all possible assignments  
evaluate the formula for each environment  

backtrack a map is just throwing the map away!!  

## Reading 12

grammar: used to distinguish whether a string is legal  
terminals: literal strings  
nonterminal: a variable to change into terminal / nonterminal  
use repitition operator to write recursion into iteration into (non-)terminal  
parser generator: input a grammar, output a parser  

import ParserLib library, define enum type contains nonterminals  
write a recursive function to visit nodes in parsetree  

left recursion may have fault in parsing  

## Reading 13

MUST read the API docs before programming, bugs could appear as 
the usage is described by yourself  
`const` only means the address of memory is unreassignable!!!  

let program fail fast is a good practice  
do a runtime check is a way to fail fast  

assertions could be expensive to performance  
assume the precondition of input and postcondition of return value  
If an assertion is obvious from its local context, leave it out  

internal failure: assertion; external failure: exception  

incremental development: develop a bit and test a bit at a time  

modularity and encapsulation is good for find out bugs  
modularity: divide a system into modules  
encapsulation: build walls between walls around modules  

minimizing the scope of variables  
always declare a loop variable in the for-loop initializer  
declare a variable only when needs, and in the innermost block that you can  

reproduce a bug reported by user may be very hard  

decrease input into a controllable range and produce a simmilar bug is easy to 
debug  
debug use a scientific method  
study the data, hypothesize, delta debugging, prioritize hypothesis  
debug one bug at a time  

