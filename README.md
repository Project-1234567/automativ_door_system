Automatic Door System for Metro Trains and Elevators
Overview:
This project aims to create an automatic door system for metro trains and elevators using a combination of Arduino Uno, servo motors, ESP32-CAM, and Python. The system automatically opens and closes doors based on proximity and other smart sensors, improving user experience, efficiency, and safety.

Components Used:
Arduino Uno: Main controller for the system that manages door operations.
Servo Motors: Used to control the movement of the doors.
ESP32-CAM: For visual recognition and surveillance purposes, enabling additional security measures.
IR Sensors: For detecting people or objects near the doors to trigger opening and closing.
Push Buttons: Manual override to open and close doors.
Jumper Wires: For connecting the components together.
Python: For controlling the ESP32-CAM via a computer for monitoring or image capture.
Arduino IDE: For programming the Arduino Uno.

Features:
Automatic Opening/Closing: Doors open and close automatically based on proximity sensors.
Manual Override: A button allows users to manually open or close doors.
Surveillance: ESP32-CAM captures images when motion is detected near the door.
Security: The system includes visual surveillance, which can be connected to a central monitoring system.

Circuit Diagram:
A detailed schematic will be uploaded soon. The connections are as follows:
Servo Motor: Connected to a PWM pin on the Arduino (e.g., pin 9).
IR Proximity Sensors: Connected to digital input pins (e.g., pin 2 and pin 3).
Push Button: Connected to a digital pin for manual control (e.g., pin 4).
ESP32-CAM: Connected via serial communication to a computer for capturing images or videos.

Software Requirements:
Arduino IDE: For uploading the code to the Arduino.
Python: For controlling the ESP32-CAM or additional monitoring software.
Libraries:
Servo library (for controlling servo motors).
ESP32 library (for programming the ESP32-CAM).
OpenCV (for processing images, if using the ESP32-CAM for visual recognition).

Code Explanation:
Arduino Code:
This code is designed to control the automatic opening and closing of the doors based on the proximity of people and manual inputs. The system uses IR sensors to detect nearby objects, and the servo motor is used to open and close the door.

#include <Servo.h>

const int irSensorPin1 = 2;  // IR sensor 1
const int irSensorPin2 = 3;  // IR sensor 2
const int buttonPin = 4;     // Manual override button
Servo doorServo;            // Servo motor object

void setup() {
  pinMode(irSensorPin1, INPUT);
  pinMode(irSensorPin2, INPUT);
  pinMode(buttonPin, INPUT);
  doorServo.attach(9);  // Attach the servo to pin 9
  doorServo.write(0);   // Close the door initially
}

void loop() {
  int sensor1 = digitalRead(irSensorPin1);
  int sensor2 = digitalRead(irSensorPin2);
  int buttonState = digitalRead(buttonPin);

  // Open the door if an object is detected near either sensor
  if (sensor1 == HIGH || sensor2 == HIGH || buttonState == HIGH) {
    doorServo.write(90);  // Open the door
  } else {
    doorServo.write(0);   // Close the door
  }
  delay(100);  // Delay to prevent rapid triggering
}
Python Code (for ESP32-CAM):
This Python code connects to the ESP32-CAM to capture images and store them locally or upload them to a server.

import cv2
import requests

# Initialize ESP32-CAM URL (modify this according to your setup)
esp32_cam_url = "http://<ESP32_CAM_IP>/capture"

while True:
    # Capture image from ESP32-CAM
    response = requests.get(esp32_cam_url)
    
    # Save the image locally or perform any action
    with open("image.jpg", "wb") as file:
        file.write(response.content)
    
    # Add your processing logic here, like image recognition or upload to server
    
Setup Instructions:
Hardware Setup:
Connect the Servo Motor to the Arduino board. The control pin should be connected to the PWM-capable pin (e.g., pin 9).
Connect the IR Sensors to digital input pins on the Arduino (e.g., pin 2 and pin 3).
Connect the Push Button to a digital input pin (e.g., pin 4) for manual control.
ESP32-CAM should be connected to a computer via serial communication to allow image capture or surveillance.
Software Setup:
Arduino IDE:

Open the Arduino IDE and load the provided code.
Select your Arduino board (Arduino Uno) and the correct COM port.
Upload the code to the Arduino.
Python:

Install Python and required libraries (requests, opencv-python).
Update the ESP32-CAM IP address in the Python script.
Run the Python script to start capturing images.
Future Improvements:
Face Recognition: Implement face recognition for advanced security features using OpenCV.
Smart Integration: Integrate with IoT systems or cloud platforms for remote monitoring.
Energy Efficiency: Optimize the system for low-power usage in the field.
License:
This project is open-source and available under the MIT License.

Conclusion
This automatic door system provides an effective solution for metro trains and elevators, leveraging a combination of hardware and software to automate door control, enhance safety, and integrate modern technology. The code is easily customizable to suit various use cases, and the system can be expanded to include additional sensors or features.

You can find the full code and hardware setup files in the repository.

Demo Videos:
System Overview: https://drive.google.com/file/d/1cv11SD1C6ddDe7YMS_gcJER8qZsnPh3G/view?usp=drive_link
Door Operation in Action: https://drive.google.com/file/d/1LjWl5bKxZ4_RmxABtMPDmPIP2TBzt5y5/view?usp=drive_link
