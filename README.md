#include <Servo.h> //here we add the servo pre-made functions

Servo myservo;  // create servo object to control a servo
const int buttonPin1 = 13;//introduction of the button connected to port 13
const int ledPinR =  5;  //red LED connected to port 5

const int buttonPin2 = 12; //introduction of the button connected to port 12
const int ledPinB = 3 ;   //blue LED connected to port 3

const int buttonPin3 = 11; //introduction of the button connected to port 11
const int ledPinG = 6 ; //green LED connected to port 6

const int buttonPin4 = 10;//introduction of the button connected to port 11

int buttonState1 = 0; // variable for reading the pushbutton status
int buttonState2 = 0; // variable for reading the pushbutton status
int buttonState3 = 0; // variable for reading the pushbutton status
int buttonState4 = 0; // variable for reading the pushbutton status
int val;    // variable to read the value from the analog pin

//int brightness = 0;    // how bright the LED is
//int fadeAmount = 5;    // how many points to fade the LED by


void setup() {
  myservo.attach(9);  // attaches the servo on pin 9 to the servo object
  // initialize the LED pins as an output:
  pinMode(ledPinR, OUTPUT); 
  pinMode(ledPinB, OUTPUT);
  pinMode(ledPinG, OUTPUT);
  // initialize the pushbutton pins as an input:
  pinMode(buttonPin1, INPUT);
  pinMode(buttonPin2, INPUT);
  pinMode(buttonPin3, INPUT);
  pinMode(buttonPin4, INPUT);
}

void loop() { // the code established into the void loop will be run repetedly
  // each button has a state related so, depending on which action we declare, the buttons will make one thing or another.
  buttonState1 = digitalRead(buttonPin1); // whatever we declare in buttonState1 will happen in buttonPin1
  buttonState2 = digitalRead(buttonPin2); // whatever we declare in buttonState2 will happen in buttonPin2
  buttonState3 = digitalRead(buttonPin3); // whatever we declare in buttonState3 will happen in buttonPin3
  buttonState4 = digitalRead(buttonPin4); // whatever we declare in buttonState4 will happen in buttonPin4

  // analogWrite(ledPinR, 255 - brightness);
  // analogWrite(ledPinB,0);
  // analogWrite(ledPinG,100 - brightness);


  //SERVO
  if (buttonState1 == HIGH && buttonState2 == HIGH && buttonState3 == HIGH) {//if any button is pressed, the servo will not move.
    myservo.write(0);
  }

  if (buttonState1 == LOW && buttonState2 == HIGH && buttonState3 == HIGH) {//if buttonPin1 is pressed, the servo will move 90 degrees.
    myservo.write(90);

  }
  if (buttonState1 == HIGH && buttonState2 == LOW && buttonState3 == HIGH) {//if buttonPin2 is pressed, the servo will move 150 degrees.
    myservo.write(150);

  }
  if (buttonState1 == HIGH && buttonState2 == HIGH && buttonState3 == LOW) {//if buttonPin3 is pressed, the servo will move 30 degrees.
    myservo.write(30);
  }
  if (buttonState1 == LOW && buttonState2 == LOW && buttonState3 == LOW) {//if all three buttonPins are pressed, the servo will move 180 degrees.
    myservo.write(180);
  }


//if two buttonPins are pressed, the servo will not move.
  
  //   if (buttonState1 == LOW && buttonState2 == LOW && buttonState3 == HIGH) {
    //myservo.write(0);
  //}

   //   if (buttonState1 == LOW && buttonState2 == HIGH && buttonState3 == LOW) {//
    //myservo.write(0);
   //}

  //if (buttonState1 == HIGH && buttonState2 == LOW && buttonState3 == LOW) {//
    //myservo.write(0);
  //}


    

  // LEDS
  if (buttonState1 == LOW) { // if buttonPin1 is pressed...
 
    digitalWrite(ledPinR, LOW); // ...red ledPin turns on.
  } else if (buttonState4 == HIGH) {// if buttonPin1 and buttonPin4 are not pressed the red LED turns off.
    
    digitalWrite(ledPinR, HIGH);
  }
  if (buttonState2 == LOW) {// if buttonPin2 is pressed...

    digitalWrite(ledPinB, LOW);// ...blue ledPin turns on.
  } else if (buttonState4 == HIGH) {// if buttonPin2 and buttonPin4 are not pressed the blue LED turns off.
    digitalWrite(ledPinB, HIGH);
  }

  if (buttonState3 == LOW) {// if buttonPin3 is pressed...

    digitalWrite(ledPinG, LOW);//...green ledPin turns on.
  } else if (buttonState4 == HIGH) {// if buttonPin3 and buttonPin4 are not pressed the green LED turns off.
    digitalWrite(ledPinG, HIGH);
  }



  if (buttonState4 == LOW ) {//if buttonPin4 is pressed...
    delay(150); // intern timer used to declare the time in milliseconds for each pin to 'shine'
   // analogWrite shows the random byte between 0 and 255 that is equivalent to random (256).
    analogWrite( ledPinR , random(256) ); 
    analogWrite( ledPinG , random(256) );
    analogWrite( ledPinB , random(256) );

  }
  else {
    // if buttonState4 is HIGH (not pressed) each LED will turn off.
    analogWrite( ledPinR , 255 );
    analogWrite( ledPinG, 255 );
    analogWrite( ledPinB , 255 );
  }
}

//change the brightness for next time through the loop:
// brightness = brightness + fadeAmount;
//
//// reverse the direction of the fading at the ends of the fade:
//if (brightness <= 0 || brightness >= 255) {
// fadeAmount = -fadeAmount;
//}
// //wait for 30 milliseconds to see the dimming effect
//delay(30);



//
//  val = map(val, 0, 1023, 0, 180);     // scale it to use it with the servo (value between 0 and 180)
//  myservo.write(val);                  // sets the servo position according to the scaled value
//  delay(15);                           // waits for the servo to get there
