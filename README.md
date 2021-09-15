# Ultrasonic-Verticle-Pinball
 
## Table of Contents 
* [Basic Onshape Design](#BasicOnshapeDesign)
* [Candy Despenser](#CandyDespenser)
* [Scoring Code](#ScoringCode)

---
## Important Links
Our google doc:

https://docs.google.com/document/d/1TA_9WrA0F9Z6xXhp9BvIn8aGqwSHfH74XpkMvyFv2LM/edit

Our onshape document:

https://cvilleschools.onshape.com/documents/721ab8d6fc612b3ebe288890/w/96b0925b53077712cb29c698/e/4148ccb3f22a86a659c6ac1a?aa=true

Our jamboard/Sketches:

https://jamboard.google.com/d/13NjuDtLQfgviIAU7torhaJOaqLBc8eHyzzhvuv4Cx6M/viewer?f=1

Scoring Code:

https://create.arduino.cc/editor/benwyattwright/2b13edd5-2c66-4b77-807c-37921331ae3a/preview

## Basic Onshape Design 

### Description 

Just a rough draft of what we wanted the machine to look like. 

### Process

This was first on our to do list when we first planned out this project. We wanted to get some basic outlines and dementions in onshape so that we could start working on the specifics of other parts like the candy despensor. We made some intial drawings in a Jambord document and then moved on to Github where we designed the basic outline for our parts. Just dropping in a few blank slabs of acrilic with the right dimensions and pulling some more complicated parts from the parts library to make sure everything would fit. 

### Diagrams 

* [Basic Design, and spring diagram](Photos/Screenshot%202021-02-11%20at%203.44.58%20PM.png)
* [Spring design](Photos/Screenshot%202021-02-11%20at%203.46.49%20PM.png)
* [Candy Dispenser Design](Photos/Screenshot%202021-02-11%20at%203.46.57%20PM.png)
* [Main Vertical Pinball Design](Photos/Screenshot%202021-02-11%20at%203.47.06%20PM.png)
* [Dimensions](Photos/Screenshot%202021-02-11%20at%203.47.17%20PM.png)

### Images 

---
## Spring

### Desciption

We learned how to make a dummy spring on onshape to be a placeholder during virtual assembly. 

## Candy Dispenser 

### Description 

The candy functions as a prize for winning the game. Your score determines the amount of candy you get, or how long the servo operated trapdoor will remain open. 

### Process

We first sketched out a quick diagram to get an idea for the plan and demensions of the dispenser. 

### Diagrams 

Our sketches :
[Candy Dispenser Design](Photos/Screenshot%202021-02-11%20at%203.46.57%20PM.png)


### Images 

---

## Scoring Code 

### Description 

The Code that opens the candy despensor latch when the ball passes through a scoring zone 

### Process

Originally we were going to use three sensors and each one triggers the latch separately, but we changed the code to only use one sensor that triggers the latch at different distances. This code is basically just recycled Hello_Functions code with a few variables changed 

### Diagrams 

(This is not the final code)

```C++

#include <Servo.h>
#define echoPin 2
#define trigPin 3

Servo myServo;

int servoPin = 12;
int loopDistance = 0;

void setup() {
  Serial.begin(9600);
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  Serial.println("Ultrasonic Sensor HC-SR04 Test");
  myServo.attach(servoPin);
}

void loop() {
  loopDistance = getdis();
  Serial.print("Distance: ");
  Serial.print(loopDistance);
  Serial.println(" cm");

  if ((loopDistance <= 4)) {
    scoreOne();
  }
  else if ((loopDistance >= 5) && (loopDistance <= 9)) {
    scoreTwo();
  }
  else if ((loopDistance >= 10) && (loopDistance <= 20)) {
    scoreOne();
  }
  else {
    stopServo();
  }
}
int getdis() {
  long duration;
  int distance;

  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);

  distance = duration * 0.034 / 2; // Speed of sound wave divided by 2 (go and back)
  return distance;
}
void stopServo() {
  myServo.write(89);
}
void scoreOne() {
  myServo.write(40);
}
void scoreTwo() {
  myServo.write(99);
}
```

### Images 


---
