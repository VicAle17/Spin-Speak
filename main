#include <Wire.h>
#include <LiquidCrystal_I2C.h>
#include <Stepper.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

// Stepper settings
const int stepsPerRevolution = 2048;
Stepper stepper(stepsPerRevolution, 8, 10, 9, 11); // IN1 IN3 IN2 IN4

const int button1Pin = 2;
const int button2Pin = 3;

const int led1 = 4;
const int led2 = 5;
const int led3 = 6;
const int led4 = 7;

void setup() {
  lcd.begin();
  lcd.backlight();

  pinMode(button1Pin, INPUT_PULLUP);
  pinMode(button2Pin, INPUT_PULLUP);

  pinMode(led1, OUTPUT);
  pinMode(led2, OUTPUT);
  pinMode(led3, OUTPUT);
  pinMode(led4, OUTPUT);

  lcd.setCursor(0, 0);
  lcd.print("1: Scientifico");
  lcd.setCursor(0, 1);
  lcd.print("2: Linguistico");

  stepper.setSpeed(10);
  randomSeed(analogRead(0));
}

void loop() {
  if (digitalRead(button1Pin) == LOW) {
    handleScientific();
    delay(500);
  }

  if (digitalRead(button2Pin) == LOW) {
    handleLinguistic();
    delay(500);
  }
}

void handleScientific() {
  int angles[] = {30, 60, 90, 120, 180};
  int angle = angles[random(0, 5)];
  rotateTo(angle);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Scientifico");

  switch (angle) {
    case 30:
      lcd.setCursor(0, 1);
      lcd.print("Domanda: A1");
      digitalWrite(led1, HIGH);
      break;
    case 60:
      lcd.setCursor(0, 1);
      lcd.print("Domanda: A2");
      digitalWrite(led2, HIGH);
      break;
    case 90:
      lcd.setCursor(0, 1);
      lcd.print("Domanda: A3");
      digitalWrite(led1, HIGH);
      break;
    case 120:
      lcd.setCursor(0, 1);
      lcd.print("Domanda: A4");
      digitalWrite(led1, HIGH);
      break;
    case 180:
      lcd.setCursor(0, 1);
      lcd.print("Domanda: A5");
      digitalWrite(led2, HIGH);
      break;
  }
  delay(4000);
  resetLeds();
  resetDisplay();
}

void handleLinguistic() {
  int angles[] = {45, 75, 135, 225, 270};
  int angle = angles[random(0, 5)];
  rotateTo(angle);

  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Linguistico");

  switch (angle) {
    case 45:
      lcd.setCursor(0, 1);
      lcd.print("Inizia con 'c'");
      digitalWrite(led3, HIGH); // es. inglese
      break;
    case 75:
      lcd.setCursor(0, 1);
      lcd.print("Verbo al passato");
      digitalWrite(led4, HIGH); // es. francese
      break;
    case 135:
      lcd.setCursor(0, 1);
      lcd.print("Frase lunga");
      digitalWrite(led3, HIGH); // es. tedesco
      break;
    case 225:
      lcd.setCursor(0, 1);
      lcd.print("Domanda strana");
      digitalWrite(led4, HIGH); // es. spagnolo
      break;
    case 270:
      lcd.setCursor(0, 1);
      lcd.print("Sinonimi/Contrari");
      digitalWrite(led4, HIGH); // es. francese
      break;
  }
  delay(4000);
  resetLeds();
  resetDisplay();
}

void rotateTo(int angle) {
  // 2048 passi = 360°, quindi 1° ≈ 5.688 passi
  int steps = angle * 2048 / 360;
  stepper.step(steps);
}

void resetLeds() {
  digitalWrite(led1, LOW);
  digitalWrite(led2, LOW);
  digitalWrite(led3, LOW);
  digitalWrite(led4, LOW);
}

void resetDisplay() {
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("1: Scientifico");
  lcd.setCursor(0, 1);
  lcd.print("2: Linguistico");
}
