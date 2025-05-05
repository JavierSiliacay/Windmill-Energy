# Windmill Energy Simulation

This project simulates a windmill energy system with adjustable gears and PWM motor control. The system allows the user to cycle through 5 gears using a button, which adjusts the motor's speed and simulates energy levels through LED brightness.

## 🛠️ Hardware Components
- Arduino Board (Uno, Nano, or compatible)
- 1 x Push Button
- 1 x Motor (DC motor or similar)
- 5 x PWM-capable LEDs
- 1 x LCD 16x2 with I2C (LiquidCrystal_I2C)
- Jumper Wires
- Breadboard

## 📦 Libraries Installed
- `Wire.h` (for I2C communication)
- `LiquidCrystal_I2C.h` (for controlling the LCD display)

## ⚙️ Pin Configuration
| Component          | Pin       |
|--------------------|-----------|
| Button             | Pin 2     |
| Motor              | Pin 9     |
| LED 1 (PWM)        | Pin 3     |
| LED 2 (PWM)        | Pin 5     |
| LED 3 (PWM)        | Pin 6     |
| LED 4 (PWM)        | Pin 10    |
| LED 5 (PWM)        | Pin 11    |

## 🧠 How It Works
- The system starts with gear 1, and you can cycle through the gears (1-5) using the push button.
- Each gear has a corresponding PWM value that controls the speed of the motor.
- The 5 LEDs simulate energy levels, with brightness distributed gradually based on the current PWM value.
- The LCD displays the current gear and PWM value in real-time.

## 🖥️ LCD Output
- **Line 1:** Displays "Windmill Energy"
- **Line 2:** Displays the current gear and the associated PWM value.

## 💡 LED Behavior
- Each of the 5 LEDs corresponds to a portion of the PWM range and gradually increases brightness as the gear increases.

## 📋 Setup Instructions
1. Connect the hardware components based on the pin configuration above.
2. Upload the Arduino sketch to your Arduino board.
3. Use the push button to cycle through gears and adjust the motor's PWM speed.
4. Observe the gear and PWM values displayed on the LCD.
5. Watch the LEDs gradually increase their brightness to simulate energy levels.

## 📝 License
This project is open-source and free to use under the MIT License.

---

Made with ❤️ by Javier Siliacay | USTP 🇵🇭
