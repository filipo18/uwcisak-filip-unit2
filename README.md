Comunicating app
====================

A morse - binary code comunicating app based on Arduino kits

# Contents

  1. [Planning](#planning)
  1. [Design](#design)
  1. [Development](#development)
  1. [Evalution](#evaluation)


# Planning

**Definethe Problem:** 
It is year 2050, planet exploration is a thing, however comunication is still a problem. NASA is trying to establish comunication between Earth, Moon, and Mars. Earth can send messeges only in morse code and Mars can recive messeges only in binary code. Moon is between Earth and Mars so station on moon can comunicate in both binary and morse code. So we need to come up with the solution that will enable station on earth to enter messege in english and send it in morse code and vice versa. Station on mars need to be able to recive a messege in binary and translate it to english and vice versa. Moon station is most complicated one. Station on moon needs to send and recive in binary and morse and be able to translate everything to englsih. NASA is allowing us to use 100W lights and buzzers. We are limited on using only 2 buttons. My grupe is working on moon station.

**Solution proposed**
We were given Arduino kits to work with. With that we are able to meet all the requirements (2 buttons, lights and buzzers). In clas we are learning modern C and this is default language to program arduinos, that is why we are going to use it for our project. Use of two buttons to meet the reqirements will be explained down bellow.

**Succes criteria for moon station**
1. Messege from Earth can be recived in Morse and translated to english.
1. Messege can be translated from English to morse and be sent back to Earth.
1. Message can be translated from English to binary and be sent do Mars.
1. Messege can be recived in binary from Mars and translated to English.
1. Messege can be recived from earth in Morse and be sent to Mars translated to binary.
1. MEssege can be recived from Mars in binary and be sent to Earth translated to Morse.

# Design

### Design stage 1.0
![System diagram](systemdiagram.png)

**Fig. 1** System diagram 1.0

System diagram in Fig.1 is outlining our product, but it is not final since there are still few unclear things in our requirements. 

**Input**
Requirements for input are most clear, but there is still one question? I am considering 2 differend implementations of two buttons (look at "Two proposed solutions for english input with 2 buttons"). We enter messege in english and translate it to binary or Morse. 

But here is a problem we need to solve. If we use both buttons to enter english alphabet, how do we decide if we want to translate to bininary or to morse. To indicate which code is selected I would add more led lights. Depending on code selected according led light would turn on. To switch between Morse and binary I would add one more button but that is not accorind to requirements.

**Output** 
Morse code was created as simplest way to transfer messeges. We need one led ligh (we can also use 2), and we can send messege letter by letter using this table

![Morse](morse.png)

**Fig 2.** [Morse code table [2] ](#resources)

To change letters into binary code, there is standardized table already in place. It is called ASCII table. (American Standard Code for Information Interchange)

![ASCII](asciitable.png)

**Fig 3.** [ASCII table [1] ](#resources) 

To output messege according to this table we need 8 LED lights. If Morse needs 1 light and binary needs 8 lights, we will use 8 lights all together. **Everything described above is for sending messeges**. Now first thing I would add here is one more button to switch between sending and reciving mode (not accoring to requirements). *Another problem I need to solve* If we want to have english output of recived messege we need to enter a messege first. We can enter morse code with 2 buttons, to enter binary code we would need 8 buttons. And when we recive code and enter it we still to show english messege to the user. For that we would need a display.

There are a lot of unclear things about this project and its requirements, so I will contact NASA as soon as possible to sort these things out :)

### Two proposed solutions for english input with 2 buttons

**Solution 1** 
![Keyboard solution 1](keyboard1.png)

**Fig 4.** Fisrt proposed solution with just one line array and 2 buttons - Next and Select
In this solution we use button A to select and button B to move to next letter. This method is easy to code but not so time efficient. This is code I used

**Solution 2**
In this solution I am considering 2 possible verisions of program.
![Keyboard solution 2](keyboard2.png)

**Fig 5.** This picutre in propsing two differend solutions. 
1. First option is to move right and down with buttons and make selection just with waiting ceratin time period (1sec on the picture). 
1. Second option is slower. Program cycles through colums first and when we press button, colum is selected and rows start cycling. When we press button for the second time letter is chosen.

### Design stage 2.0
After talking to NASA, all the questions from **Design stage 1.0** were resolved. Here is **System diagram 2.0**

![System diagram 2.0](systemdiagram2.png)

**Fig 6.** System diagram 2.0

As shown in fig 6, input method for our sytem will be simple. Just 2 buttons. One to move on next argument in the menu, and one to confirm our choice. Menu will be organized in 4 (or 6 if we have time) main functions. Eng - Bin, Eng - Morse, Bin - Eng, Morse - Eng. 
If one of the first two options are selected, array of letters and numbers will shop up on LCD display. For now, we will use simple 1d array not matrix as metioned in design stage 1.0. User will enter the messege, program will convert it to chosen code and 100w light will transmit it. Because we don't need all the characters from ASCII table metntioned in Design stage 1.0, we will crate custm char to binary coverstaion table and implement it. By doing this we will reduce number of bits required to send one character.

If thrid or forth option is selected, arduino will enter recive mode.  User will be be able to enter coded messege in chosen code. Messege will be converted to english and shown on LCD display.

LED indicators are added to the system, to show user in which mode is now. Depending on function user will chose, one of four LEDs will turn on. 1 for Eng - Bin, 2 for Eng - Morse, 3 for Bin - Eng, 4 for Morse - Eng.


# Development


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


Traffic lights
--------
We crated traffic lights from arduino kit. I learned basics of programing arduino in modern C, its not hard to understand and I like functions functionality. Prgoraming in bash I repeated coding process for similar things to many times so fuctions are giving me option to have some basics library to make coding faster. I like this topic a lot because it combines some basic electro enginering with coding and when you code something you actually get phyisical touchable result, not just program running in you computer.

![trafficlights](trafficlights.gif)

**Fig 7.** First mini arduino project - traffic lights, getting familiar with arduino, getting familiar with concept of ports, learning some bascic coding

Counting in binary
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

Usign this we created arduino based circut with 4 differend colored LEDs, and programed it to count from 1 to 15 in [binary [3] ](#resources)  according to table above. 

This program work, but I would encounter problems if I had more inputs, which would result in very long if sentances.
It also demonstartes how to use button to trigger lights. ```c   if (digitalRead(butA) == LOW && digitalRead(butB) == LOW && digitalRead(butC) == LOW){
 		digitalWrite(out1, HIGH);
  		digitalWrite(out2, HIGH); }
      ```
      

Logic binary gates
--------

![binarygates](gates.png)

**Fig 8.** Types of binary gates, with tables of inputs and outputs [Source [4] ](#Resources)

A logic gates are building blocks of digital circuts or in our case program using binary inputs and outputs. Logic gates have two inputs and one output and are based on Boolean algebra. At any given moment every output is at one of the two binary conditions: true or false - [Source [5] ](#Resources). 4 basic gates we explored today are represented in the table above. In terms of matematcial decimal operators, AND is representing + (addition) and OR is representing x (multyplication). 
In modern C OR is represented with ```c | ``` AND is represented with ```c & ``` NOT is represented with ```c ! ``` and XOR is represented with ```c ^ ```

Code below shows how to implement this in program:
```c
  bool eqA = ( (!C) & (!A) ) | B | ( C & A );
 digitalWrite(ledA, eqA);
 ```
Segment counter
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

**Fig 9.** Seven segment counter

Using logical gates presented earlier, we convertet table (Fig 8.) to set of equations. One equation for each letter. And created a code that will count based on buttons pressed.

```c
// Defining variables as pins
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

// Defining pins as inputs ans outputs
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
//Defining buttons as variables I will use in equations
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
  
  **Fig 10.** Seven segment counter circut

Usability
--------
Usability is according to Wikpedia [ [6] ](#Resources) is the ease of use and learnability of a human-made object such as a tool or device.

Human-centered design **HCD** is based on Feedback and Discoverability. Accordning to Joe Posner everything should be intuative and easy to use. [ [7] ](#Resources).
 
Two proposed solutions for english input with 2 buttons
--------------------------------------------------------

**Solution 1** 

![Keyboard solution 1](keyboard1.png)

**Fig 11.** Fisrt proposed solution with just one line array and 2 buttons - Next and Select
In this solution we use button A to select and button B to move to next letter. This method is easy to code but not so time efficient. This is code I used
```.ino
//This program will allow user ener english

//Then we define array - matrix and buttons
int index = 0;
String text = "";
String keyboard[]={"SEND","DEL","_","a","b","c","d","e","f","g","h","i","j","k","l","m","n","o","p","q","r","s","t","u","v","w","x","y","z"};
int numOptions = 29;

void setup()
{
Serial.begin(9600);
attachInterrupt(0, changeLetter, RISING);
attachInterrupt(1, selected, RISING);
}

void loop()
{
  //This 2 fucntions will repeat infinitly. First one is  prinitng
  //Letter selected to the user and short quick instructions
  //Second prints total message with all selected letters to the user
  Serial.println("Option (Select: butB, Change: butA): " + 
                 keyboard[index]);
  Serial.println("Message: "+ text);
  delay(200);
 
}

//This function changes the letter in the keyboard
void changeLetter(){
  index++;
  //this if condition will reset index count when it reaches end of our alphabet
  if(index>numOptions){
    index=0; //back to begining
  }
}

//this function adds the letter to the text or sends the msg
void selected(){
  String key=keyboard[index];
    if(key=="DEL"){
    	int len= text.length();
      	text.remove(len-1);
  	}
	else if(key=="SEND"){
   		Serial.println("Message sent");
   		text = "";
    }
  	else {
    text+=key;
  }
  index=0;
   
 }
 ```
 This program works, the only problem I am encountering is blinking of serial monitor. I will resolve that when we move to LCD display. 

First key part used in this program is **array**. We use it to define arguments we will be using in the program. Type of variable we define if we are putting letters in the array is ``` String ```. After name we define for array we add ``` [n]``` . In bracets we specifiy number of arguments in array. If we don't specifiy it, program coutns arguments instead of us. We separate arguments with coma, each argument needs to be market with ``` ' ' ``` if specified type of variable is ```c int ``` and we are using numbers. If specified type of variable is ``` String ``` and we are using letters and other signs, each argument needs to be marked with ``` " " ```. So syntax all together looks like this ``` String arrayexample [5] = {"a", "b", "c", "d", "e"}

Second of the key parts of this program are **interuptions**. Instead of checking if button is pressed every milisecond, we can leave arduino runing other procces and then interupt this procces with input on pin 2 or 3. After interuption arduino goes back to procces runed before interuption.
1. First step is to set up interuption ports ``` attachInterrupt(0, changeLetter, RISING); ``` , first element in the brackets can only be 0 or 1. 0 is port 2, 1 is port 3 and this are only 2 ports on which interuption can be installed. Second element is function which will interupt main proccess when button on port 2 rises. That is defined in third element.
1. Second step is to write a function we want to interupt current process. Let's take our case as an exaple:
```.ino 
void changeLetter(){
  index++;
  //this if condition will reset index count when it reaches end of our alphabet
  if(index>numOptions){
    index=0; //back to begining
  }
}
```
So when button on port 2 will rise, this function will be performed.

**Solution 2**
In this solution I am considering 2 possible verisions of program.
![Keyboard solution 2](keyboard2.png)

**Fig 12.** This picutre in propsing two differend solutions. 
1. First option is to move right and down with buttons and make selection just with waiting ceratin time period (1sec on the picture). This was first plan, but I encounter some problmes coding it. Everything is compleatly based on interuptions, so I should figgure out where to add time check, to confirm selection. Also the problem I see with that is that serial monitor is blinking all the time due to looping our main functions.  I will try to solve it but I got another idea which I think its much easier to code. I will work on both and I will se which one works out better. Another imporant thing is to make keyboard vissible all the time. We could just add picture next to the syistem but if we can code it into program that is much better.

1. Second option is slower. Program cycles through colums first and when we press button, colum is selected and rows start cycling. When we press button for the second time letter is chosen. I have idea how to code that, and we also solve blinking problem since we can make cycle interval and delay interval on the loop the same. Problem with showing whole matrix remains the same also in this solution.

This is how far I come with coding matrix before I stuck:
```.ino
//This program will allow user ener english

//First we define pins as variables
int butA = 3;
int butB = 2;

//Then we define array - matrix and buttons
int row = 7;
int col = 6;
int indexRow = 0;
int indexCol = 0;
String text = "";
String keyboard[row][col] = {
  {"_", "DEL", "a", "s", "c", "w"},
  {"SENT", "t", "n", "d", "g", "s"},
  {"e", "i", "l", "p", "x", "z"},
  {"o", "h", "f", "k", "1", "6"},
  {"r", "m", "v", "0", "5", "9"},
  {"u", "b", "z", "4", "8", " "},
  {"y", "q", "3", "7", " "; " "},
}

int butA = 3;
int butB = 2;

void setup()
{
Serial.begin(9600);
attachInterrupt(0, changeRow, RISING);
attachInterrupt(1, changeCol, RISING);
//I need to add select function here, figre out how to do that, conect it to time

void loop()
{
  Serial.println("Option (Move Colum to the right: butA, Move Row down: butB, Select: Wait 1sec): 
	 +keyboard[indexRow][indexCol]);
  Serial.println("Message: " + text);
  delay(100);
}


  
//this function changes the row in the keybord
void changeRow () 
{
  indexRow++;
  //check for the max row numeber
  if(indexRow>row) 
  {
    indexRow=0;//loop back to first row
  }
}
//this function changes colum in the keybord
void changeCol()
{
  indexCol++;
  //check for the max col numeber
  if(indexcol>col)
  {
    indexCol=0; //loop back to first col
  }
}
  


//this funion adds the letter to the text or sends the msg
void selected(){
  string key = keyboard[row][col];
  if(key
  
  
}
```
From here on, I will try to code 2 differend solutions (option1 and option2). I will see which one works out better.

To crate 2D array or matrix we use same syntax as for array, only difference is that we use ```c [row][col] ``` at instead of ```c [] ```. First bracket defines rows and second colums. Type of variable we are using is string. So put this all together and we get ```c String matrixexample[][] = {   } ```. Example how we can create 2D array of symbols used for our purposes below:
```c
String keyboard[row][col] = {
  {"_", "DEL", "a", "s", "c", "w"},
  {"SENT", "t", "n", "d", "g", "s"},
  {"e", "i", "l", "p", "x", "z"},
  {"o", "h", "f", "k", "1", "6"},
  {"r", "m", "v", "0", "5", "9"},
  {"u", "b", "z", "4", "8", " "},
  {"y", "q", "3", "7", " "; " "},
  ```
  
English keyboad on LCD
-----------------------
We builded arduino LCD circut. Sketch from Thinkercad and actual build shown bellow:

![LCD Arduino sketch](lcdarduinosketch.png)

**Fig 13.** Arduino LCD Circuit sketch from Thinkercad

![LCD Arduino circuit](lcdarduino.jpg)

**Fig 14.** Arduino LCD circuit

Code below is working. It eneable user to enter englsih alphabet.

```.ino
// include the library code:
#include <LiquidCrystal.h>
int index = 0; 
// add all the letters and digits to the keyboard
String keyboard[]={" ", "A", "B", "C", "D", "E", "F", "G", "H", "I", "J", "K", "L", "M", "N", "O", "P", "Q", "R", "S", "T", "U", "V", "W", "X", "Y", "Z", "1", "2", "3", "4", "5", "6", "7", "8", "9", "0", "SENT", "DEL"};
String text = "";
int numOptions = 29;

// initialize the library with the numbers of the interface pins
LiquidCrystal lcd(12, 11, 7, 6, 5, 4);

void setup() {
  // set up the LCD's number of columns and rows:
  lcd.begin(16, 2);
  // Print a message to the LCD.
  attachInterrupt(0, changeLetter, RISING);//button A in port 2
  attachInterrupt(1, selected, RISING);//button B in port 3
}

void loop() {
  // set the cursor to column 0, line 1
  // (note: line 1 is the second row, since counting begins with 0):
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print(keyboard[index]);
  lcd.setCursor(0, 1);
  lcd.print(text);
  delay(100);
}

//This function changes the letter in the keyboard
void changeLetter(){
  static unsigned long last_interrupt_time = 0;
  unsigned long interrupt_time = millis();
  if (interrupt_time - last_interrupt_time > 200)
  {
  
    last_interrupt_time = interrupt_time;// If interrupts come faster than 200ms, assum
    index++;
      //check for the max row number
    if(index==numOptions){
      index=0; //loop back to first row
    } 
 }
}

//this function adds the letter to the text or send the msg
void selected(){
  static unsigned long last_interrupt_time = 0;
  unsigned long interrupt_time = millis();
  if (interrupt_time - last_interrupt_time > 200)
  {
  
    last_interrupt_time = interrupt_time;// If interrupts come faster than 200ms, assum
    
    String key = keyboard[index];
    if (key == "DEL")
    {
      int len = text.length();
      text.remove(len-1);
    }
    else if(key == "SENT")
    {
      text="";
    }else{
      text += key;
    }
    index = 0; //restart the index
  }
  
  
  //
}

```

![flowenglishkeyboard](flowenglishkeyboard.jpg)

**Fig 15.** This is flow diagram for English keyboard


Evaluation
-----------





Resources
----------
1. [1] **Fig 3.** Vivah, Linda. “Learn How to Read Binary in 5 Minutes.” Medium, Medium, 22 June 2018, https://medium.com/@LindaVivah/learn-how-to-read-binary-in-5-minutes-dac1feb991e.
1. [2] **Fig 2.** Åhlén, Johan. “Morse Code Translator, Decoder, Alphabet.” Boxentriq, https://www.boxentriq.com/code-breaking/morse-code.
1. [3] Stapel, Elizabeth. “Number Bases: Introduction & Binary Numbers.” Purplemath, https://www.purplemath.com/modules/numbbase.htm.
1. [4] **Fig 7.** Account Suspended, https://guidetofortnite.com/2-input-xor-truth-table.html.
1. [5] Account Suspended, https://guidetofortnite.com/2-input-xor-truth-table.html.
1. [6] “Usability.” Wikipedia, Wikimedia Foundation, 13 Nov. 2019, https://en.wikipedia.org/wiki/Usability.
1. [7] Posner J, Mars R. " It's not you, bad doors are everywhere" 2016. Retrived (25 Nov 2019)
