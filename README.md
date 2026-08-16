# Smart Gate Entry System (Arduino) 🚧🚗

This project is a simulation of an automated smart parking gate system. Built using **Arduino** and simulated on the **Wokwi** platform, this system detects an approaching vehicle, simulates scanning its license plate, issues a ticket, and automatically opens the gate for entry.

## 🧠 Circuit Design & Simulation (Wokwi)

The circuit was designed to integrate multiple actuators and sensors to mimic a real-world toll booth or parking gate:

1. **Distance Sensing:** An **HC-SR04 Ultrasonic Sensor** (Pins 5 & 6) acts as the vehicle detector, constantly measuring the distance to trigger the system when a car is within 50 cm.
2. **Camera Simulation:** A **Stepper Motor** (Pins 8, 9, 10, 11) is used to simulate a security camera panning left and right to "scan" the vehicle's license plate.
3. **Ticket Dispenser:** A simple **Red LED** (Pin 3) lights up to simulate the printing and issuing of a parking ticket.
4. **Gate Mechanism:** A **Micro Servo Motor** (Pin 4) acts as the physical gate barrier, rotating from 0 degrees (closed) to 90 degrees (open).

<img width="100%" alt="Smart Gate Entry Wokwi Simulation" src="image_d9cc95.png" />

---

## 📁 Repository Structure
* `smart_gate.ino`: The main Arduino C++ script containing the logic for the sensors, motors, and sequence timing.
* `image_d9cc95.png`: The visual schematic showing the wiring connections in the Wokwi simulator.

## 🛠 Prerequisites
To build or simulate this project, you will need:

**Hardware (If building physically):**
* 1x Arduino Uno
* 1x HC-SR04 Ultrasonic Sensor
* 1x Stepper Motor (e.g., 28BYJ-48 with ULN2003 driver)
* 1x Micro Servo Motor (e.g., SG90)
* 1x LED & 220Ω Resistor
* Breadboard & Jumper Wires

**Software:**
* [Arduino IDE](https://www.arduino.cc/en/software) or the [Wokwi Online Simulator](https://wokwi.com/).
* The standard `<Servo.h>` and `<Stepper.h>` libraries (included by default).

## 🚀 How to Run
1. Recreate the circuit in the Wokwi simulator or wire the physical components according to the schematic.
2. Open the **Arduino IDE** (or the Wokwi code editor) and paste the provided C++ code.
3. If using physical hardware, connect your Arduino Uno via USB, select the correct Board and Port from the **Tools** menu, and click **Upload**.
4. Open the **Serial Monitor** (set to 9600 baud rate) to view the system's live status messages.

## 📊 Expected Behavior (Results)
Once the system is powered on, it enters a standby loop and operates according to the following automated sequence:

* **Standby:** The Serial Monitor displays `"System Ready. Waiting for a car..."`
* **Detection:** If a car (or object) comes within **50 cm** of the ultrasonic sensor, the entry sequence begins.
* **Step 1 (Scan):** The stepper motor pans 45 degrees, sweeps back 90 degrees, and returns to the center to simulate license plate scanning.
* **Step 2 (Ticket):** The LED turns on for 2 seconds to simulate dispensing a ticket.
* **Step 3 (Open Gate):** The servo motor rotates to 90 degrees, opening the gate. 
* **Passage & Close:** The gate remains open for **5 seconds** to allow the car to pass, then automatically returns to 0 degrees (closed).
* **Cooldown:** The system pauses for 3 seconds to prevent double-triggering before returning to Standby mode.
