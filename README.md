#include <AFMotor.h>
// motor pins
AF_DCMotor motor1(1, MOTOR12_1KHZ);
AF_DCMotor motor2(2, MOTOR12_1KHZ);
AF_DCMotor motor3(3, MOTOR34_1KHZ);
AF_DCMotor motor4(4, MOTOR34_1KHZ);
// speed limit
const int MAX_SPEED = 500;
const int REDUCED_SPEED = 500 / 3.1;
const int BAUD_RATE = 9600;
// Variables
int val;
void setup() {
  Serial.begin(BAUD_RATE);  // Sets baud rate to the Bluetooth module
}
void loop() {
  if (Serial.available() > 0) {
    val = Serial.read();
    Stop();  // Initialize with motors stopped
    switch (val) {
      case 'F':
        forward();
        break;
      case 'B':
        back();
        break;
      case 'L':
        left();
        break;
      case 'R':
        right();
        break;
      case 'I':
        topright();
        break;
      case 'J':
        topleft();
        break;
      case 'K':
        bottomright();
        break;
      case 'M':
        bottomleft();
        break;
      case 'T':
        Stop();
        break;
    }
  }
}
void forward() {
  setMotorsSpeed(MAX_SPEED, FORWARD);
}
void back() {
  setMotorsSpeed(MAX_SPEED, BACKWARD);
}
void left() {
  motor1.setSpeed(MAX_SPEED);
  motor1.run(BACKWARD);
  motor2.setSpeed(MAX_SPEED);
  motor2.run(BACKWARD);
  motor3.setSpeed(MAX_SPEED);
  motor3.run(FORWARD);
  motor4.setSpeed(MAX_SPEED);
  motor4.run(FORWARD);
}
void right() {
  motor1.setSpeed(MAX_SPEED);
  motor1.run(FORWARD);
  motor2.setSpeed(MAX_SPEED);
  motor2.run(FORWARD);
  motor3.setSpeed(MAX_SPEED);
  motor3.run(BACKWARD);
  motor4.setSpeed(MAX_SPEED);
  motor4.run(BACKWARD);
}
void topleft() {
  motor1.setSpeed(MAX_SPEED);
  motor1.run(FORWARD);
  motor2.setSpeed(MAX_SPEED);
  motor2.run(FORWARD);
  motor3.setSpeed(REDUCED_SPEED);
  motor3.run(FORWARD);
  motor4.setSpeed(REDUCED_SPEED);
  motor4.run(FORWARD);
}
void topright() {
  motor1.setSpeed(REDUCED_SPEED);
  motor1.run(FORWARD);
  motor2.setSpeed(REDUCED_SPEED);
  motor2.run(FORWARD);
  motor3.setSpeed(MAX_SPEED);
  motor3.run(FORWARD);
  motor4.setSpeed(MAX_SPEED);
  motor4.run(FORWARD);
}
void bottomleft() {
  motor1.setSpeed(MAX_SPEED);
  motor1.run(BACKWARD);
  motor2.setSpeed(MAX_SPEED);
  motor2.run(BACKWARD);
  motor3.setSpeed(REDUCED_SPEED);
  motor3.run(BACKWARD);
  motor4.setSpeed(REDUCED_SPEED);
  motor4.run(BACKWARD);
}
void bottomright() {
  motor1.setSpeed(REDUCED_SPEED);
  motor1.run(BACKWARD);
  motor2.setSpeed(REDUCED_SPEED);
  motor2.run(BACKWARD);
  motor3.setSpeed(MAX_SPEED);
  motor3.run(BACKWARD);
  motor4.setSpeed(MAX_SPEED);
  motor4.run(BACKWARD);
}
void Stop() {
  setMotorsSpeed(0, RELEASE);
}
void setMotorsSpeed(int speed, int direction) {
  motor1.setSpeed(speed);
  motor1.run(direction);
  motor2.setSpeed(speed);
  motor2.run(direction);
  motor3.setSpeed(speed);
  motor3.run(direction);
  motor4.setSpeed(speed);
  motor4.run(direction);
}
