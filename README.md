# Damir
Web-Server-Controller-for-Servo-Motor esp 32 github


Equipment and Components
ESP8266 (NodeMCU or similar)
SG90 Servo Motor (or equivalent)
2 LEDs (Green and Red)
2 220Ω Resistors (for current limiting)
Breadboard and jumper wires
5V Power Supply (for the servo, if required)



Working Principle
When the servo turns left (angle < 90°), the green LED lights up.
When the servo turns right (angle > 90°), the red LED lights up.
At neutral position (90°), both LEDs remain off.
Software Implementation
Libraries used:
ESP8266WiFi – For Wi-Fi connectivity.
ESP8266WebServer – For hosting a web server.
Servo – For servo motor control.
Results
Servo motor successfully controlled via the web interface.
LEDs correctly indicate the direction of rotation.
The system operates stably on a local network.





Conclusion:
This project demonstrates a simple and effective way to control a servo motor and LEDs
through a web interface using the ESP8266 microcontroller. The system allows the user
to rotate the servo motor to the left or right via Wi-Fi, while visually indicating the
direction with LEDs. When the servo is at the center position (90°), both LEDs are turned
off, providing a clear and intuitive user experience.
The project serves as a useful learning example for working with servos, implementing
network-based control, building web interfaces on ESP8266, and understanding basic
interactions between hardware and software in IoT systems.
It is important to consider the power requirements of all components, especially the
servo motor, to ensure stable operation and avoid damaging the microcontroller. Using
an external power source for the servo and proper resistors for the LEDs is strongly
recommended for safe and reliable performance.
This project can be easily extended with additional features, such as advanced control
logic or integration into more complex automation systems.






