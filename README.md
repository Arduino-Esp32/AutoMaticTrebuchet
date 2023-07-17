#include<Servo.h>
int servoPin = 3;
int servoPos = 0;
Servo myServo;

#include <Stepper.h>
int stepsPerRevolution = 2048;

Stepper myStepper(stepsPerRevolution, 8, 10, 9, 11);

int motSpeed = 10;

int motDir = 460;
int motDir2 = 1558;


const int bPin = 2;
int bVal;

const int ledPin = 4;
int ledVal;

int counter = 0;

const int dt = 1000;
const int dt2 = 750;

void setup() {
  Serial.begin(9600);

  pinMode(bPin, INPUT_PULLUP);

  myStepper.setSpeed(motSpeed);

  pinMode(ledPin, OUTPUT);

  myServo.attach(servoPin);
  myServo.write(servoPos);

}

void loop() {
  bVal = digitalRead(bPin);
  Serial.println(bVal);

  if (bVal == 0 and counter == 0) {
    servoPos = servoPos = 180;
    myServo.write(servoPos);
    Serial.println("Ban");
    
    delay(dt);
    
    counter = 1;

    
    myStepper.step(230);
    
    delay(dt2);

    servoPos = servoPos = 0;
    myServo.write(servoPos);
    
    bVal = 1;
    
   
  }

  if (bVal == 0 and counter == 1) {
    Serial.println("Fan");
    
    
   
    myStepper.step(-230);
    
    delay(dt2);
    
    bVal = 1;
    counter = 0;
    
    
  }


}
