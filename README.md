# my-first-project-SMART-OBSTACLE-MOTION-ALARM-SYSTEM-
"Smart Obstacle + Motion Alarm System using Arduino. Detects nearby obstacles with ultrasonic sensor and motion with PIR sensor, triggering buzzer and LED alerts. Ideal for security, automation, and embedded systems learning. Compact design, simple wiring, and easy-to-understand code."


// Smart Obstacle + Motion Alarm System
// Components: Ultrasonic, IR Sensor, Buzzer, LED

const int trigPin = 9;
const int echoPin = 10;
const int irPin = 8;
const int buzzer = 6;
const int led = 7;

long duration;
int distance;

void setup() {
  pinMode(trigPin, OUTPUT);
  pinMode(echoPin, INPUT);
  pinMode(irPin, INPUT);
  pinMode(buzzer, OUTPUT);
  pinMode(led, OUTPUT);
  Serial.begin(9600);
}

void loop() {
  // Measure distance with ultrasonic
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);

  duration = pulseIn(echoPin, HIGH);
  distance = duration * 0.034 / 2;

  // Read IR sensor
  int motion = digitalRead(irPin);

  // Show readings
  Serial.print("Distance: ");
  Serial.print(distance);
  Serial.print(" cm | IR: ");
  Serial.println(motion);

  // Alarm Condition
  // Some IR sensors give LOW = object detected, some HIGH = detected
  if (distance < 20 || motion == LOW) {   // change LOW→HIGH if needed
    digitalWrite(buzzer, HIGH);
    digitalWrite(led, HIGH);
    Serial.println("🚨 ALERT! Object or Motion Detected!");
  } 
  else {
    digitalWrite(buzzer, LOW);
    digitalWrite(led, LOW);
    Serial.println("✅ SAFE - No Obstacle or Motion");
  }

  delay(500);
}



