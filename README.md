# Line-follower-robot-
My first year project :line follower robot using Arduino and IR sensor .
Over View:
This is a basic Line Follower Robot built using an Arduino Uno, IR sensors, and L2N89 Motor. The robot detects and follows a black line on a white surface by using IR sensors to differentiate between black and white colors.
Components used:
-Arduino Uno
-IR sensor
-L2N89 Motor driver 
-BO Motor
-lithium ion battery
-Jumper cables
Working of line follower robot :
The line follower robot concept is all about light. In this, we implement the characteristics of light on the black-and-white surface. The white color reflects all the light falling on it, and the black color absorbs the light.
In this line-follower robot, we employ IR transmitters and receivers (photodiodes). They are employed to transmit and receive the lights. When IR rays hit a white surface, they get reflected in the direction of the IR receiver, producing some voltage variations. 
Black surfaces emit infrared radiation and do not reflect any of the rays incident on them; hence, no photons arrive at the infrared receiver.
In this project, when the IR sensor detects a white surface, an Arduino receives 1 (high) as input, and when it detects a black line, an Arduino receives 0 (low) as input. From these inputs, an Arduino Uno gives the correct output to operate the bot.
Code:
int mot1 = 9;
int mot2 = 6;
int mot3 = 5;
int mot4 = 3;
int left = 13;
int right = 12;
int Left = 0;
int Right = 0;
void LEFT(void);
void RIGHT(void);
void STOP(void);
void setup() {
pinMode(mot1, OUTPUT);
pinMode(mot2, OUTPUT);
pinMode(mot3, OUTPUT);
pinMode(mot4, OUTPUT);
pinMode(left, INPUT);
pinMode(right, INPUT);
digitalWrite(left, HIGH);
digitalWrite(right, HIGH);
}void loop() {
analogWrite(mot1, 255);
analogWrite(mot2, 0);
analogWrite(mot3, 255);
analogWrite(mot4, 0);
Left = digitalRead(left);
Right = digitalRead(right);
if ((Left == 0) && (Right == 1)) {
LEFT();
}
else if ((Right == 0) && (Left == 1)) {
RIGHT();
}
}
void LEFT(void) {
analogWrite(mot3, 0);
analogWrite(mot4, 30);
while (Left == 0) {
Left = digitalRead(left);
Right = digitalRead(right);
if (Right == 0) {
int lprev = Left;
int rprev = Right;
STOP();
while ((lprev == Left) && (rprev == Right)) {
Left = digitalRead(left);
Right = digitalRead(right);
}
analogWrite(mot1, 255);
analogWrite(mot2, 0);
}
}
analogWrite(mot1, 255);
analogWrite(mot2, 0);
analogWrite(mot3, 255);
analogWrite(mot4, 0);
}
void RIGHT(void) {
analogWrite(mot1, 0);
analogWrite(mot2, 30);
while (Right == 0) {
Left = digitalRead(left);
Right = digitalRead(right);
if (Left == 0) {
int lprev = Left;
int rprev = Right;
STOP();
while ((lprev == Left) && (rprev == Right)) {
Left = digitalRead(left);
Right = digitalRead(right);
}
analogWrite(mot3, 255);
analogWrite(mot4, 0);
}
}
analogWrite(mot1, 255);
analogWrite(mot2, 0);
analogWrite(mot3, 255);
analogWrite(mot4, 0);
}
void STOP(void) {
analogWrite(mot1, 0);
analogWrite(mot2, 0);
analogWrite(mot3, 0);
analogWrite(mot4, 0);
}
Circuit diagram
![WhatsApp Image 2025-07-11 at 22 34 35](https://github.com/user-attachments/assets/72c7e224-0a2a-4e86-9836-02816182f427)
Future improvements
-Use PID control for smoother movement
-add obstacle detection using ultrasonic sensor
