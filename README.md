Comunicating app
====================

A morse - binary code comunicating app based on Arduino kits

Contents
---------
  1. [Planning](#planning)
  1. [Design](#design)
  1. [Development](#development)
  1. [Evalution](#evaluation)


Planning
-----------



Design
-------


Development
------------

**Bash and Modern C evaluation**

Modern C

| Proos       | Cons          | 
| :-----------: |:-------------:| 
| Syntax is more forgiving     | Is not pre installed  | 
| More resources online      | By default can't run on every computer withaut any aditional work      |   
|  We can work with decimal numbers | \      |    

Bash

| Proos       | Cons          | 
| :-----------: |:-------------:| 
| Is pre installed   | Syntax is not forgiving  | 
| By default can run on every computer with terminal      | Less resources online  |   
|  \                          | We can't work with decimal numbers      |    

**Types of variables in Modern C**
1. Boolean - can hold only two values, 0 or 1. It uses only 1 byte
1. Float - varaible with decimal point
1. Word - stores an unsigned number from 0 to 65,535
1. Long - extened numberical variable -2,147,483,648 to 2,147,483,647
1. Char - stores a single character as a value
1. unsigned char encodes numbers from 0 to 255
1. int stores an integer from  -32,768 to 32,767
1. usnigned int stores values from 0 to 65,535.


Nov 11
--------
We crated traffic lights from arduino kit. I learned basics of programing arduino in modern C, its not hard to understand and I like functions functionality. Prgoraming in bash I repeated coding process for similar things to many times so fuctions are giving me option to have some basics library to make coding faster. I like this topic a lot because it combines some basic electro enginering with coding and when you code something you actually get phyisical touchable result, not just program running in you computer.

![trafficlights](trafficlights.gif)

**Fig 1.** First mini arduino project - traffic lights, getting familiar with arduino, getting familiar with concept of ports, learning some bascic coding

Nov 13
-------
How to count from 0 to 15 in binary:

0 0
1. 1
1. 10
1. 11
1. 100
1. 101
1. 110
1. 111
1. 1000
1. 1001
1. 1010
1. 1011
1. 1100
1. 1101
1. 1110
1. 1111

Usign this we created arduino based circut with 4 differend colored LEDs, and programed it to count from 1 to 15 in [binary](#resources)  according to table above. 

This program work, but I would encounter problems if I had more inputs, which would result in very long if sentances.
It also demonstartes how to use button to trigger lights. ```c   if (digitalRead(butA) == LOW && digitalRead(butB) == LOW && digitalRead(butC) == LOW){
 		digitalWrite(out1, HIGH);
  		digitalWrite(out2, HIGH); }
      ```
      

Nov 18
--------

![binarygates](gates.png)

**Fig 4.** Types of binary gates, with tables of inputs and outputs [Source](#Resources)

A logic gates are building blocks of digital circuts or in our case program using binary inputs and outputs. Logic gates have two inputs and one output and are based on Boolean algebra. At any given moment every output is at one of the two binary conditions: true or false - [Source](#Resources). 4 basic gates we explored today are represented in the table above. In terms of matematcial decimal operators, AND is representing + (addition) and OR is representing x (multyplication). 
In modern C OR is represented with ```c | ``` AND is represented with ```c & ``` NOT is represented with ```c ! ``` and XOR is represented with ```c ^ ```

Code below shows how to implement this in program:
```c
  bool eqA = ( (!C) & (!A) ) | B | ( C & A );
 digitalWrite(ledA, eqA);
 ```
Nov 20
-------
We crated seven segment counter using 3 buttons. First step was to create a table of inputs and outputs:

| Button A  | Button B    | Button C     | Decimal Number | A | B | C | D | E | F | G |
| :----: |:----:| :----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|:----:|
| 0 | 0 | 0 | 0 | 1 | 1 | 1 | 1 | 1 | 1 | 0 |
| 0 | 0 | 1 | 1 | 0 | 0 | 0 | 0 | 1 | 1 | 0 |
| 0 | 1 | 0 | 2 | 1 | 0 | 1 | 1 | 0 | 1 | 1 |
| 0 | 1 | 1 | 3 | 1 | 0 | 0 | 1 | 1 | 1 | 1 |
| 1 | 0 | 0 | 4 | 0 | 1 | 0 | 1 | 1 | 1 | 1 |
| 1 | 0 | 1 | 5 | 1 | 1 | 0 | 1 | 1 | 0 | 1 |
| 1 | 1 | 0 | 6 | 1 | 1 | 1 | 1 | 1 | 0 | 1 |
| 1 | 1 | 1 | 7 | 1 | 0 | 0 | 0 | 0 | 1 | 1 |

Each letter at the top of the colums represents one segment of our counter

![Sevensegmentcounter](segmentcouter.png)

**Fig 5.** Seven segment counter

Using logical gates presented earlier, we convertet table (Fig 5.) to set of equations. One equation for each letter. And created a code that will count based on buttons pressed.

```c
int butA = 13;
int butB = 12;
int butC = 11;
int ledA = 7;
int ledB = 6;
int ledC = 5;
int ledD = 4;
int ledE = 3;
int ledF = 2;
int ledG = 1;

void setup()
{
  pinMode(butA, INPUT);
  pinMode(butB, INPUT);
  pinMode(butC, INPUT);
  pinMode(ledA, OUTPUT);
  pinMode(ledB, OUTPUT);
  pinMode(ledC, OUTPUT);
  pinMode(ledD, OUTPUT);
  pinMode(ledE, OUTPUT);
  pinMode(ledF, OUTPUT);
  pinMode(ledG, OUTPUT);
}

void loop()
{
  bool A = digitalRead(butA);
  bool B = digitalRead(butB);
  bool C = digitalRead(butC);

  bool eqA = ( (!C) & (!A) ) | B | ( C & A );
  bool eqB =  ( A & C ) | ( (!B) & (!C) );
  bool eqC = ( (!C) & (!A) ) | ((!C) & B);
  bool eqD = (!C & !A) | (!A & B) | (!C & B) | (A & !B & C);
  bool eqE = C | (!A & !B) | A;
  bool eqF = !B | ( !A & !C ) | ( A & C);
  bool eqG = B | (A & !B);
 
  digitalWrite(ledA, eqA);
  digitalWrite(ledB, eqB);
  digitalWrite(ledC, eqC);
  digitalWrite(ledD, eqD);
  digitalWrite(ledE, eqE);
  digitalWrite(ledF, eqF);
  digitalWrite(ledG, eqG);
}

```
  
  This is circut we used:
  
  ![Counter circut](sevensegmentcounterarduino.png)
  
  **Fig 6.** Seven segment counter circut

Nov 25
--------
Usability is according to Wikpedia [ [4] ](#Resources) is the ease of use and learnability of a human-made object such as a tool or device.

Human-centered design **HCD** is based on Feedback and Discoverability. Accordning to Joe Posner everything should be intuative and easy to use. [ [5] ](#Resources)


Evaluation
-----------





Resources
----------
1. [1] Stapel, Elizabeth. “Number Bases: Introduction & Binary Numbers.” Purplemath, https://www.purplemath.com/modules/numbbase.htm.
1. [2] **Fig 4.** Account Suspended, https://guidetofortnite.com/2-input-xor-truth-table.html.
1. [3] Account Suspended, https://guidetofortnite.com/2-input-xor-truth-table.html.
1. [4] “Usability.” Wikipedia, Wikimedia Foundation, 13 Nov. 2019, https://en.wikipedia.org/wiki/Usability.
1. [5] Posner J, Mars R. " It's not you, bad doors are everywhere" 2016. Retrived (25 Nov 2019)
