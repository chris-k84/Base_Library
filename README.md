# Base Library

## Contents

1. [Motivation](#motivation)
2. [The Goal](#the-goal)
3. [Background](#background)
4. [Description](#description)
3. [Repository Design](#repository-design)
4. [Tests](#Tests)
5. [Support](#Support)
6. [Requirements](#Requirements)
7. [Documents](#Document-List)

## Motivation

This started out as an XTS library, then became something else, a huge crawling repo with too much stuff doing too many things. So it's been broken up into numerous libraries which will break out the elements into modules which align in function and intent. Basically the motivation is to have a clue whats going on :-) 

## The Goal

The Goal of this repo is to define a set of base behaviour of any module created for PLC use. The objects within this library will force a particular behaviour for handling cyclic behaviour, task calls and initialisation. All objects used in a PLC program will be built on these basic building blocks.

## Background

The background to this repo is essentially my leanring journey in PLC programming. Initially i had no strong view on how to construct a PLC program. As time has gone on I have learned OOP provides the best soltuion for architecting code.
This doesnt mean you must use full OOP, design patterns, testing etc, I believe you should, but its not required. Instead it means you simply divide the code into function, repeatable blocks, calling them classes or FBs doesnt matter.
The important part is you break up code into block and call those blocks cyclically, rather than in the structured programming paradigm.
Once you go donw this path, libraries like this start to make more sense. 
This library forms the basis of how i think those blocks of code should be constructed and operated.

## Description

The repo is effectively formed of three sections, Cyclic_Base, Task_Base and Initialise. 

The Cyclic_Base is the most basic element of these, it is used in all objects in the code created using this library. Every class/fb you create should extend this class.
This will enforce a cyclic behaviour of calling the cycle method of the object you create. Thats it, thats the big impact, but by doing so you shift the cyclic behaviour of the objectinto that method.
This means you no longer call the body of the FB yo make. This sounds pointless, but it creates some amazing and interesting possibilities later on.

The Task_Base is a second level of this, the task class again exits to be extended by the function blocks you create.
The task enforces an interface that includes a Busy, Done, Error, Abort operation. You can see how the cyclic code would be writtena round these.
As the module is triggered you set the error, done flags false and the busy true, once the operation is complete the busy flag drops and the error/done can be set.
This allows you to break the cyclic operation of code, you can command an operation, then there is no need to observe the process, simply wait for the outputs to be set.

Finally the Initialise, sometimes it is useful to have a pre cyclic operation, assigning pointers for example.
This was implemented as an interface, it simply gets implemented in your function block to enfire the method requirement.
It has no code implementation requirement itself so an interface was enough. This is unlike the cyclic and task base which are both abstract types.

## Repository Design

The repo is split into 2 projects, the base library and the testing project, the library is referenced in the test project. The test project can be run in the UmRT.

## Tests

There is a unit testing project created, the library is referenced in the test project. 

## Support

LOL, little old me now, all by myself :-)


## Requirements: 

Please include important requirements in the local readme files.

Currently nothing more than:

TwinCAT 4026


## Document List





