#include <LiquidCrystal.h>

// LCD pins: RS, E, D4, D5, D6, D7
LiquidCrystal lcd(12, 11, A0, A1, A2, A3);

// LED pins: Green, Yellow, Red, Blue
int ledPins[4] = {2, 3, 4, 5};

// Button pins (with pull-down resistors)
int buttonPins[4] = {6, 7, 8, 9};

int buzzerPin = 10;

#define MAX_LEVEL 5
#define SEQ_LENGTH 10

int sequence[SEQ_LENGTH];
int level;
bool gameStarted = false;

void setup() {
  lcd.begin(16, 2);
  lcd.print("Simon Says");

  for (int i = 0; i < 4; i++) {
    pinMode(ledPins[i], OUTPUT);
    pinMode(buttonPins[i], INPUT);
  }

  pinMode(buzzerPin, OUTPUT);
  randomSeed(analogRead(A5));

  delay(1500);
  lcd.clear();
}

void loop() {
  if (!gameStarted) {
    generateSequence();
    playGame();
    gameStarted = true;
  }
}

// Generate random sequence
void generateSequence() {
  for (int i = 0; i < SEQ_LENGTH; i++) {
    sequence[i] = random(0, 4);
  }
}

// Main game logic
void playGame() {
  for (level = 1; level <= MAX_LEVEL; level++) {
    lcd.clear();
    lcd.print("Level: ");
    lcd.print(level);

    delay(1000);
    showSequence();

    if (!getUserInput()) {
      gameOver();
      return;
    }
  }
  winGame();
}

// Show Simon sequence
void showSequence() {
  for (int i = 0; i < level; i++) {
    digitalWrite(ledPins[sequence[i]], HIGH);
    tone(buzzerPin, 1000 + sequence[i] * 200, 200);
    delay(300);
    digitalWrite(ledPins[sequence[i]], LOW);
    delay(150);
  }
}

// Check user input
bool getUserInput() {
  for (int i = 0; i < level; i++) {
    int pressed = waitForButton();
    if (pressed != sequence[i]) {
      return false;
    }
  }
  return true;
}

// Wait for button press
int waitForButton() {
  int lastState[4] = {LOW, LOW, LOW, LOW};

  while (true) {
    for (int i = 0; i < 4; i++) {
      int currentState = digitalRead(buttonPins[i]);

      if (currentState == HIGH && lastState[i] == LOW) {
        digitalWrite(ledPins[i], HIGH);
        tone(buzzerPin, 800, 150);
        delay(150);
        digitalWrite(ledPins[i], LOW);
        delay(80); // debounce
        return i;
      }
      lastState[i] = currentState;
    }
  }
}

// Game over state
void gameOver() {
  lcd.clear();
  lcd.print("Game Over!");
  tone(buzzerPin, 300, 1000);
  delay(2000);
}

// Win state
void winGame() {
  lcd.clear();
  lcd.print("You Won!");

  for (int i = 0; i < 3; i++) {
    tone(buzzerPin, 1200, 200);
    delay(250);
    tone(buzzerPin, 1600, 200);
    delay(250);
  }
  delay(3000);
}
