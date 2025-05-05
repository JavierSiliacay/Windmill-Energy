# Windmill Energy Control System

This project simulates a windmill energy control system, where the speed and direction of a motor are controlled by a button. The system uses an LCD to display the current gear and PWM value. The motor's speed is adjusted based on the gear selected, and LEDs indicate varying brightness levels corresponding to the motor's PWM value.

## Components Used

- **Arduino Board (e.g., Uno, Nano)**
- **Motor Driver (H-Bridge, e.g., L298N)**
- **DC Motor**
- **5x LEDs (PWM capable)**
- **1x Button**
- **16x2 LCD with I2C**
- **Wires and Breadboard**

## Circuit Diagram

- **IN1** and **IN2** are connected to pins 9 and 10 on the Arduino, respectively. These control the motor's direction.
- **Motor PWM** is controlled using PWM signals on the H-Bridge.
- **Button** is connected to pin 2 to cycle through the gears (1–5).
- **LEDs** are connected to pins 3, 5, 6, 10, and 11 for displaying PWM values.
- **LCD** is connected via I2C at address `0x27`.

## Functionality

- The motor's speed is controlled by the **gear** (1–5) selected via the button.
- The motor direction alternates between forward and reverse based on the gear (odd gears reverse, even gears forward).
- The motor's speed is controlled using PWM values that correspond to the gear.
- The system displays the current gear and PWM value on an LCD screen.
- The brightness of the LEDs gradually increases based on the PWM value.

## Code

```cpp
#include <Wire.h>
#include <LiquidCrystal_I2C.h>

LiquidCrystal_I2C lcd(0x27, 16, 2);

const int buttonPin = 2;
const int IN1 = 9; // Motor direction pin 1
const int IN2 = 10; // Motor direction pin 2

// PWM LED pins
const int ledPins[5] = {3, 5, 6, 10, 11}; // Use PWM-capable pins only

int gear = 0;
bool lastButtonState = HIGH;

void setup() {
  pinMode(buttonPin, INPUT_PULLUP);
  pinMode(IN1, OUTPUT);
  pinMode(IN2, OUTPUT);

  for (int i = 0; i < 5; i++) {
    pinMode(ledPins[i], OUTPUT);
  }

  lcd.init();
  lcd.backlight();
  lcd.setCursor(0, 0);
  lcd.print("Windmill Energy");
}

void loop() {
  bool currentButtonState = digitalRead(buttonPin);

  if (lastButtonState == HIGH && currentButtonState == LOW) {
    gear++;
    if (gear > 5) gear = 0;

    int pwmValue = gear * 51;

    // Control motor direction and speed
    if (gear % 2 == 0) { // Forward direction for even gears
      digitalWrite(IN1, HIGH);
      digitalWrite(IN2, LOW);
    } else { // Reverse direction for odd gears
      digitalWrite(IN1, LOW);
      digitalWrite(IN2, HIGH);
    }

    // Set motor speed using PWM
    analogWrite(IN1, pwmValue);
    analogWrite(IN2, pwmValue);

    lcd.setCursor(0, 1);
    lcd.print("Gear: ");
    lcd.print(gear + 1);
    lcd.print(" PWM: ");
    lcd.print(pwmValue);
    lcd.print("   ");

    // Distribute brightness across 5 LEDs
    for (int i = 0; i < 5; i++) {
      int brightness = map(pwmValue, 0, 255, 0, (i + 1) * 51);  // Gradual fade effect
      brightness = constrain(brightness, 0, 255);
      analogWrite(ledPins[i], brightness);
    }

    delay(200);
  }

  lastButtonState = currentButtonState;
}
