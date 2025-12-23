# 🎮 Simon Says Game with Arduino

A classic **Simon Says memory game** implemented using **Arduino**, LEDs, push buttons, buzzer, and a 16x2 LCD.

---

## 🧠 How the Game Works
- The system generates a random sequence of LEDs.
- Each LED represents a specific color.
- The player must repeat the sequence using the corresponding buttons.
- With each successful level, the sequence becomes longer.
- A wrong input ends the game.

---

## 🔧 Hardware Components
- Arduino Uno
- Breadboard
- 4 LEDs (Green, Yellow, Red, Blue)
- 4 Push Buttons
- Active Buzzer
- 16x2 LCD
- 4 × 220Ω resistors (LEDs)
- 4 × 1kΩ resistors (pull-down for buttons)
- Jumper wires

---


## 🖼️ Circuit Schematic

The following image shows the complete circuit schematic of the project:

<img width="300" height="300" alt="SimonSays-Schematic" src="https://github.com/user-attachments/assets/b1db9898-91e7-4fb6-949d-5ba0c5ebdafc" />


---


## 🔌 Pin Configuration

| Component | Arduino Pins |
|---------|--------------|
| LEDs | 2, 3, 4, 5 |
| Buttons | 6, 7, 8, 9 |
| Buzzer | 10 |
| LCD | 12, 11, A0–A3 |

---

## ✨ Features
- Random sequence generation
- Increasing difficulty levels
- Visual and audio feedback
- LCD messages for game status
- Simple and readable Arduino code

---

## 🚀 Getting Started
1. Connect the components according to the pin configuration.
2. Upload `simon_says.ino` to your Arduino board.
3. Power the board via USB.
4. Enjoy the game!

---

## 📚 Notes
- Buttons are connected using **pull-down resistors**.
- The buzzer is used for both feedback and game sounds.
- Code is written for educational purposes and clarity.

---

⭐ If you like this project, feel free to star the repository!
