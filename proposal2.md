# Arduino Wireless Drone

This project is a controllable tank drone built with Arduino and able to control by a remote.

## Summary

This drone is able to move with two motors and users are able to control it with a remote. The project is focusing on utilizing the IR remote and motor driver to wirelessly control the tank drone.

## Component Parts

Arduino board, tank chassis, remote, IR remote, motor driver, 18650 batteries * 2

## When your project is completed, you will then add the following sections:

## Timeline

What did you do in each of the past four weeks?

- Week 0: Write Proposal
- Week 1: Material preparation, purchase from Amazon
- Week 2: Testing component parts to make sure they are functionable, weld the arudino extension board, building the electric circuit.
- Week 3: Finishing building the electri circuit by changing the motor driver to make it work. Testing the IR remote and collect the hex number of remote controller
- Week 4: Present!

## Challenges

The challenge of this project is the arduino kits are reletively new to us. Therefore, we need to learn everything about the kit and how to make it work. We spent most of the time on building the circuit, it didn't work for day until we realize it was the problem with the motor driver. We also faced some problem with uploading codes in to the arudino board, we were not able to upload on one of the laptop but able to upload on the other one, which took us some time to target what the problem was.

## Completed Work

// include library //
#include <IRremote.h>

// define IR sensor pin //
int IRsensorPin = 13;

// define the some functions used by the library //
IRrecv irrecv(IRsensorPin);
decode_results results;

// define motor drive control pins //
int RightMotorForward = 8;    // IN1
int RightMotorBackward = 9;   // IN2
int LeftMotorForward = 10;     // IN3
int LeftMotorBackward = 11;    // IN4


void setup(){
  
  // initialize motor control pins as output //
  pinMode(LeftMotorForward,OUTPUT);
  pinMode(RightMotorForward,OUTPUT);
  pinMode(LeftMotorBackward,OUTPUT);
  pinMode(RightMotorBackward,OUTPUT);

  // start serial communication to see hex codes //
  Serial.begin(9600);
  irrecv.enableIRIn();
}

void loop(){
  
  // if the sensor is receive any signal //
  if (irrecv.decode(&results)){
 
  }
  
  // hex codes//
  if(results.value == 16730805) MotorForward();
  if(results.value == 16718055) MotorBackward();
  if(results.value == 16716015) TurnRight();
  if(results.value == 16734885) TurnLeft();
  if(results.value == 16726215) MotorStop();
  
}

// FORWARD //
void MotorForward(){
  digitalWrite(LeftMotorForward,HIGH);
  digitalWrite(RightMotorForward,HIGH);
  digitalWrite(LeftMotorBackward,LOW);
  digitalWrite(RightMotorBackward,LOW); 
}

// BACKWARD //
void MotorBackward(){
  digitalWrite(LeftMotorBackward,HIGH);
  digitalWrite(RightMotorBackward,HIGH);
  digitalWrite(LeftMotorForward,LOW);
  digitalWrite(RightMotorForward,LOW);
}

/* TURN RIGHT */
void TurnRight(){
  digitalWrite(LeftMotorForward,HIGH); 
  digitalWrite(RightMotorForward,LOW);
  digitalWrite(LeftMotorBackward,LOW);
  digitalWrite(RightMotorBackward,HIGH);
}

// TURN LEFT //
void TurnLeft(){
  digitalWrite(RightMotorForward,HIGH);  
  digitalWrite(LeftMotorForward,LOW);
  digitalWrite(LeftMotorBackward,HIGH);
  digitalWrite(RightMotorBackward,LOW);
}

// STOP //
void MotorStop(){
  digitalWrite(LeftMotorBackward,LOW);
  digitalWrite(RightMotorBackward,LOW);
  digitalWrite(LeftMotorForward,LOW);
  digitalWrite(RightMotorForward,LOW);
}


## References and links

https://www.youtube.com/watch?v=8E3ltjnbV0c&t=576s
https://www.youtube.com/watch?v=JQrP7MDZdIo&t=202s
https://www.youtube.com/watch?v=by5qH-Xzeag
