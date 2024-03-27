# non-invasive-glucose-measurement
int sensorValue = 0;
int numReadings = 100;
int glucose = 0;
double volts = 0;
double totalV = 0;
double averageV = 0;
double concentration = 0;
const int sensorPin = A0;

int Mode = 0;
bool Active = false;

void setup() {
  Serial.begin(9600);
  pinMode(sensorPin, INPUT);
}

void loop() {
  Active = true;

  Serial.println("Select Mode (0, 1, 2):");
  while (!Serial.available()) {
    // Wait for input from the Serial Monitor
  }

  Mode = Serial.parseInt();
  while (Serial.available()) {
    Serial.read(); // Clear buffer
  }

  if (Mode == 0) {
    numReadings = 100;
    Serial.println("Eaten 1 Hour or Before");
    delay(2000);
  } else if (Mode == 1) {
    numReadings = 150;
    Serial.println("Eaten 2 Hour To 3 Hour");
    delay(2000);
  } else if (Mode == 2) {
    numReadings = 200;
    Serial.println("Eaten 5 Hour or More");
    delay(2000);
  }

  concentration = 0;
  averageV = 0;
  Serial.println("Place finger");
  delay(2000);

  for (int j = 0; j < 5; j++) {
    totalV = 0;
    sensorValue = analogRead(sensorPin);
    volts = double(sensorValue) * (5.0 / 1023.0);
    totalV += volts;
    averageV = totalV / numReadings;

    if (j == 1)
      concentration += 4;
    else if (j > 1)
      concentration += 2;

    delay(1000);
  }

  Serial.print("GLUCOSE LEVEL IS: ");

  if (Mode == 0) {
    glucose = (3.95 - averageV) / 0.009;
  } else if (Mode == 1) {
    glucose = (3.25 - averageV) / 0.009;
  } else if (Mode == 2) {
    glucose = (3 - averageV) / 0.009;
  }

  Serial.println(glucose);
  delay(5000);
}int sensorValue = 0;
int numReadings = 100;
int glucose = 0;
double volts = 0;
double totalV = 0;
double averageV = 0;
double concentration = 0;
const int sensorPin = A0;

int Mode = 0;
bool Active = false;

void setup() {
  Serial.begin(9600);
  pinMode(sensorPin, INPUT);
}

void loop() {
  Active = true;

  Serial.println("Select Mode (0, 1, 2):");
  while (!Serial.available()) {
    // Wait for input from the Serial Monitor
  }

  Mode = Serial.parseInt();
  while (Serial.available()) {
    Serial.read(); // Clear buffer
  }

  if (Mode == 0) {
    numReadings = 100;
    Serial.println("Eaten 1 Hour or Before");
    delay(2000);
  } else if (Mode == 1) {
    numReadings = 150;
    Serial.println("Eaten 2 Hour To 3 Hour");
    delay(2000);
  } else if (Mode == 2) {
    numReadings = 200;
    Serial.println("Eaten 5 Hour or More");
    delay(2000);
  }

  concentration = 0;
  averageV = 0;
  Serial.println("Place finger");
  delay(2000);

  for (int j = 0; j < 5; j++) {
    totalV = 0;
    sensorValue = analogRead(sensorPin);
    volts = double(sensorValue) * (5.0 / 1023.0);
    totalV += volts;
    averageV = totalV / numReadings;

    if (j == 1)
      concentration += 4;
    else if (j > 1)
      concentration += 2;

    delay(1000);
  }

  Serial.print("GLUCOSE LEVEL IS: ");

  if (Mode == 0) {
    glucose = (3.95 - averageV) / 0.009;
  } else if (Mode == 1) {
    glucose = (3.25 - averageV) / 0.009;
  } else if (Mode == 2) {
    glucose = (3 - averageV) / 0.009;
  }

  Serial.println(glucose);
  delay(5000);
}
