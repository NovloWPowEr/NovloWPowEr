// Motor A pins (enableA = enable motor, pinA1 = forward, pinA2 = backward) A = ซ้าย
int enableA = 3;
int pinA1 = 6;
int pinA2 = 7;

//Motor B pins (enabledB = enable motor, pinB1 = forward, pinB2 = backward) b = ขวา
int enableB = 5;
int pinB1 = 8;
int pinB2 = 9;

int sensor[5] = {0, 0, 0, 0, 0};

void setup()
{
  pinMode(enableA, OUTPUT);
  pinMode(pinA1, OUTPUT);
  pinMode(pinA2, OUTPUT);

  pinMode(enableB, OUTPUT);
  pinMode(pinB1, OUTPUT);
  pinMode(pinB2, OUTPUT);
}

void loop()
{

  enableMotors();
  analogWrite(enableA, 70);  // ปรับค่าความเร็วของหุ่นยนต์
  analogWrite(enableB, 70);  // ปรับค่าความเร็วของหุ่นยนต์

  sensor[0] = digitalRead(A1);
  sensor[1] = digitalRead(A2);
  sensor[2] = digitalRead(A3);
  sensor[3] = digitalRead(A4);
  sensor[4] = digitalRead(A5);

  if ((sensor[0] == 1) && (sensor[1] == 0) && (sensor[2] == 0) && (sensor[3] == 0) && (sensor[4] == 1))
    forward(2);
  else if ((sensor[0] == 1) && (sensor[1] == 1) && (sensor[2] == 0) && (sensor[3] == 0) && (sensor[4] == 0))
    turnRight(1);
  else if ((sensor[0] == 1) && (sensor[1] == 1) && (sensor[2] == 0) && (sensor[3] == 0) && (sensor[4] == 1))
    turnRight(1);
  else if ((sensor[0] == 1) && (sensor[1] == 0) && (sensor[2] == 1) && (sensor[3] == 1) && (sensor[4] == 1))
    turnLeft(1);
  else if ((sensor[0] == 1) && (sensor[1] == 0) && (sensor[2] == 0) && (sensor[3] == 1) && (sensor[4] == 1))
    turnLeft(1);
  else if ((sensor[0] == 0) && (sensor[1] == 0) && (sensor[2] == 0) && (sensor[3] == 1) && (sensor[4] == 1))  //
    turnLeft(470);
      analogWrite(enableA, 255);  // ปรับค่าความเร็วของหุ่นยนต์
      analogWrite(enableB, 120);  // ปรับค่าความเร็วของหุ่นยนต์
  else if ((sensor[0] == 0) && (sensor[1] == 0) && (sensor[2] == 1) && (sensor[3] == 1) && (sensor[4] == 1))  //
    turnLeft(470);
      analogWrite(enableA, 255);  // ปรับค่าความเร็วของหุ่นยนต์
      analogWrite(enableB, 120);  // ปรับค่าความเร็วของหุ่นยนต์
  else if ((sensor[0] == 1) && (sensor[1] == 1) && (sensor[2] == 0) && (sensor[3] == 0) && (sensor[4] == 0))  //
    turnRight(470);
      analogWrite(enableA, 120);  // ปรับค่าความเร็วของหุ่นยนต์
      analogWrite(enableB, 255);  // ปรับค่าความเร็วของหุ่นยนต์
  else if ((sensor[0] == 1) && (sensor[1] == 1) && (sensor[2] == 1) && (sensor[3] == 0) && (sensor[4] == 0))  // 
    turnRight(470);
     analogWrite(enableA, 120);  // ปรับค่าความเร็วของหุ่นยนต์
     analogWrite(enableB, 255);  // ปรับค่าความเร็วของหุ่นยนต์
  else
    forward(1);
}

//Define high-level H-bridge commands

void enableMotors()
{
  motorAOn();
  motorBOn();
}

void disableMotors()
{
  motorAOff();
  motorBOff();
}

void forward(int time)
{
  motorAForward();
  motorBForward();
  delay(time);
}

void backward(int time)
{
  motorABackward();
  motorBBackward();
  delay(time);
}

void turnLeft(int time)
{
  motorABackward();
  motorBForward();
  delay(time);
}

void turnRight(int time)
{
  motorAForward();
  motorBBackward();
  delay(time);
}

void coast(int time)
{
  motorACoast();
  motorBCoast();
  delay(time);
}

void brake(int time)
{
  motorABrake();
  motorBBrake();
  delay(time);
}
//Define low-level H-bridge commands

//enable motors
void motorAOn()
{
  digitalWrite(enableA, HIGH);
}

void motorBOn()
{
  digitalWrite(enableB, HIGH);
}

//disable motors
void motorAOff()
{
  digitalWrite(enableB, LOW);
}

void motorBOff()
{
  digitalWrite(enableA, LOW);
}

//motor A controls
void motorAForward()
{
  digitalWrite(pinA1, HIGH);
  digitalWrite(pinA2, LOW);
}

void motorABackward()
{
  digitalWrite(pinA1, LOW);
  digitalWrite(pinA2, HIGH);
}

//motor B controls
void motorBForward()
{
  digitalWrite(pinB1, HIGH);
  digitalWrite(pinB2, LOW);
}

void motorBBackward()
{
  digitalWrite(pinB1, LOW);
  digitalWrite(pinB2, HIGH);
}

//coasting and braking
void motorACoast()
{
  digitalWrite(pinA1, LOW);
  digitalWrite(pinA2, LOW);
}

void motorABrake()
{
  digitalWrite(pinA1, HIGH);
  digitalWrite(pinA2, HIGH);
}

void motorBCoast()
{
  digitalWrite(pinB1, LOW);
  digitalWrite(pinB2, LOW);
}

void motorBBrake()
{
  digitalWrite(pinB1, HIGH);
  digitalWrite(pinB2, HIGH);
}
