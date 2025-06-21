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









Attachments:
#include <ESP8266WiFi.h>
#include <ESP8266WebServer.h>
#include <Servo.h>
// Настройки Wi-Fi
const char* ssid = "Untrusted Network";
const char* password = "home_ctf_2{none}";
ESP8266WebServer server(80);
Servo myservo;
// Контакты подключения
int servoPin = D4; // Сервопривод
int greenLedPin = D1; // Зеленый светодиод (влево)
int redLedPin = D2; // Красный светодиод (вправо)
int currentAngle = 90; // Начальный угол
void setup() {
 Serial.begin(115200);
 delay(10);
 // Инициализация пинов
 pinMode(greenLedPin, OUTPUT);
 pinMode(redLedPin, OUTPUT);
 digitalWrite(greenLedPin, LOW);
 digitalWrite(redLedPin, LOW);

 myservo.attach(servoPin);
 myservo.write(currentAngle);
 // Подключение к Wi-Fi
 WiFi.begin(ssid, password);
 Serial.println("");
 while (WiFi.status() != WL_CONNECTED) {
 delay(500);
 Serial.print(".");
 }
 Serial.println("");
 Serial.print("Connected to ");
 Serial.println(ssid);
 Serial.print("IP address: ");
 Serial.println(WiFi.localIP());
 // Настройка сервера
 server.on("/", handleRoot);
 server.on("/left", handleLeft);
 server.on("/right", handleRight);
 server.begin();
 Serial.println("HTTP server started");
}
void loop() {
 server.handleClient();
}
void updateLeds() {
 // Выключаем оба светодиода
 digitalWrite(greenLedPin, LOW);
 digitalWrite(redLedPin, LOW);

 // Включаем соответствующий светодиод
 if (currentAngle < 90) {
 digitalWrite(greenLedPin, HIGH); // Влево - зеленый
 } else if (currentAngle > 90) {
 digitalWrite(redLedPin, HIGH); // Вправо - красный
 }
 // При 90° оба светодиода выключены
}
void handleRoot() {
 String html = "<!DOCTYPE html>";
 html += "<html>";
 html += "<head>";
 html += "<meta name=\"viewport\" content=\"width=device-width, initialscale=1\">";
 html += "<style>";
 html += "body { font-family: Arial, sans-serif; text-align: center; margin:
0; padding: 20px; }";
 html += "h1 { color: #444; }";
 html += ".button { background-color: #4CAF50; border: none; color: white;
padding: 15px 32px;";
 html += "text-align: center; text-decoration: none; display: inline-block;
font-size: 16px;";
 html += "margin: 10px 5px; cursor: pointer; border-radius: 5px; }";
 html += ".button:hover { background-color: #45a049; }";
 html += "#angle { font-size: 24px; font-weight: bold; margin: 20px; }";
 html += "</style>";
 html += "</head>";
 html += "<body>";
 html += "<h1>Servo Motor Control</h1>";
 html += "<div id=\"angle\">Current Angle: " + String(currentAngle) +
"°</div>";
 html += "<a href=\"/left\" class=\"button\">LEFT</a>";
 html += "<a href=\"/right\" class=\"button\">RIGHT</a>";
 html += "</body>";
 html += "</html>";
 server.send(200, "text/html", html);
}
void handleLeft() {
 if (currentAngle > 0) {
 currentAngle -= 180;
 if (currentAngle < 0) currentAngle = 0;
 myservo.write(currentAngle);
 updateLeds();
 }
 handleRoot();
}
void handleRight() {
 if (currentAngle < 180) {
 currentAngle += 180;
 if (currentAngle > 180) currentAngle = 180;
 myservo.write(currentAngle);
 updateLeds();
 }
 handleRoot();
}
Link YouTube:
https://youtu.be/qUjW5jo5LJg?si=yJB8bdeN1j7ZVizs
