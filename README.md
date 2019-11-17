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





Evaluation
-----------
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
```c
int A = 12;
int B = 9;
int C = 7;
int D = 4;
int i = 0;
//We define our variables 

void setup()
{
  pinMode(A, OUTPUT);
  pinMode(B, OUTPUT);
  pinMode(C, OUTPUT);
  pinMode(D, OUTPUT);
}

void loop()
{
  for (i = 0; i <= 15; i += 1)
  {
    if (i%2 == 1)
    {
      digitalWrite (D, HIGH);
    } 
    if (i%4 > 1)
    {
      digitalWrite (C, HIGH);
    }
    if (i%8 > 3) 
    {
      digitalWrite (B, HIGH);
    }
    if (i%16 > 7)
    {
      digitalWrite (A, HIGH);
    }
    delay (300);
    digitalWrite (D, LOW);
    digitalWrite (C, LOW);
    digitalWrite (B, LOW);
    digitalWrite (A, LOW);
    
  }
}  
```

![binarycounter](binarycouner.gif)

**Fig 2.** Second mini project - we created Arduino based binary counter that counts from 1 to 15








Resources
----------
Stapel, Elizabeth. “Number Bases: Introduction & Binary Numbers.” Purplemath, https://www.purplemath.com/modules/numbbase.htm.

