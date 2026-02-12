# STM32-Pomodoro-Timer
An event-driven Pomodoro timer built for STM32, featuring an RTC-backed Finite State Machine (FSM), SSD1306 OLED display, and clean, decoupled C architecture.
 # 🍅 STM32 Pomodoro Timer (FSM & Event-Driven)
![IMG_20260212_092822430](https://github.com/user-attachments/assets/b8b870b8-a64b-4cb4-9fa8-bb2e41fa361f)

## ✨ Key Features
* **Custom FSM Logic:** The core timer logic is completely hardware-independent, making it highly testable and portable.
* **Event-Driven Architecture:** Button inputs are translated into logical events (`START`, `PAUSE`, `INC`, `DEC`) rather than directly manipulating hardware variables.
* **RTC-Backed Timing:** Uses the STM32 Real-Time Clock (RTC) and Unix timestamps (`<time.h>`) for flawless timekeeping, immune to blocking delays and midnight rollovers.
* **OLED User Interface:** Real-time updates on an SSD1306 OLED display via I2C.
* **Two Modes:** Dedicated "Work" and "Relax" phases with customizable durations.
* **Edit Mode:** Adjust timer settings on the fly using intuitive button holds and clicks.

## 🛠️ Hardware Requirements
* **Microcontroller:** STM32 (e.g., STM32F411 "Black Pill" or Nucleo board)
* **Display:** SSD1306 OLED display (I2C)
* **Inputs:** 3x Push Buttons (Top, Middle, Bottom)
* **Outputs:** 1x LED or Buzzer (for Alarm notification)

## 🧠 Software Architecture
1. **Hardware Layer (`main.c`, `Button.c`, `SSD1306.c`):** Handles physical button debouncing, reading the RTC, and pushing pixels to the OLED.
2. **Bridge / Event Dispatcher:** Translates physical button presses (e.g., "Middle Button Short Press") into logical FSM events (e.g., `POMO_EVENT_ACTION`).
3. **Business Logic (`PomodoroFSM.c`):** A pure C library that receives events, calculates Unix timestamps, updates states, and raises a `NeedsRedraw` flag. It has zero knowledge of the STM32 HAL.

### State Machine Overview
The timer operates in the following states:
* `IDLE` - Waiting to start.
* `RUNNING` - Active countdown (Work or Relax phase).
* `PAUSED` - Timer temporarily halted; remaining time is saved.
* `ALARM` - Countdown finished, awaiting user confirmation.
* `EDIT` - Adjusting configured Work/Relax times.

## 🚀 How to Build and Run
1. Clone this repository.
2. Open the project in **STM32CubeIDE**.
3. Compile and flash to your STM32 board.
4. *Controls:*
   * **Middle Button:** Start / Pause / Resume / Confirm Alarm
   * **Middle Hold:** Enter / Exit Edit Mode
   * **Top Button:** Increase Time
   * **Bottom Button:** Decrease Time

## 📝 License
This project is open-source and available under the [MIT License](LICENSE).
