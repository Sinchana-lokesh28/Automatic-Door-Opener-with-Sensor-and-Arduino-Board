# Automatic-Door-Opener-with-Sensor-and-Arduino-Board
Designed a motion-activated door system , Integrated sensors with Arduino to control door motor.
WORKING PRINCIPLE:
The system uses an infrared (IR) sensor or ultrasonic sensor to detect the presence or motion of a person near the door. When the sensor detects an object within a specific range, it sends a signal to the Arduino microcontroller, which processes the input and activates a servo motor or motor driver to open the door. After a brief delay, the door automatically closes again.

CODE:
#include <Servo.h>
// Define pins for Ultrasonic Sensor
const int trigPin = 9;
const int echoPin = 10;
// Create Servo object
Servo doorServo;
// Define distance threshold in cm
const int distanceThreshold = 15; // adjust as needed
// Servo positions
const int openPosition = 90;
const int closePosition = 0;
void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  doorServo.attach(6); // Connect servo to pin 6
  doorServo.write(closePosition); // Initially closed
  Serial.begin(9600);
}
void loop() {
  long duration;
  int distance;
  // Send ultrasonic pulse
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  // Read echo
  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2; // Convert to cm
  Serial.print("Distance: ");
  Serial.println(distance);
  // Check if someone is near
  if (distance > 0 && distance < distanceThreshold) {
    doorServo.write(openPosition); // Open door
    delay(3000); // Keep open for 3 seconds
    doorServo.write(closePosition); // Close door
  }
  delay(500); // Check every 0.5 second
}

