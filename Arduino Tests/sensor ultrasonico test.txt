//    Arduino  sensor ultrasonico HC-SR04
//    primer sensor------ arduino
//      echo           S3
//      tigger         S2
//    segundo sensor------ arduino
//     echo            S4
//     tigger          S5


#define echoPin1 2 // Echo Pin del primer sensor
#define trigPin1 3 // Trigger Pin del primer sensor

#define echoPin2 4 // Echo Pin del segundo sensor
#define trigPin2 5 // Trigger Pin del segundo sensor

#define MAX_DISTANCE 7.5 // Distancia máxima para detectar un objeto (en cm)

void setup() {
  Serial.begin (9600);
  pinMode(trigPin1, OUTPUT);
  pinMode(echoPin1, INPUT);
  pinMode(trigPin2, OUTPUT);
  pinMode(echoPin2, INPUT);
}

void loop() {
  if (detectObject(trigPin1, echoPin1)) {
    Serial.println("Objeto detectado por el primer sensor!");
  }
  if (detectObject(trigPin2, echoPin2)) {
    Serial.println("Objeto detectado por el segundo sensor!");
  }
  delay(1000); // Espera 1 segundo antes de la próxima detección
}

bool detectObject(int trigPin, int echoPin) {
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  float distance = pulseIn(echoPin, HIGH) / 58.2; // Calcula la distancia en cm
  return (distance <= MAX_DISTANCE);
}

