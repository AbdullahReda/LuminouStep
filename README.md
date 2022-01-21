# LuminouStep
int ledPin = 13;
int G_LED = 3; // Green LED pin
int R_LED = 2; // Red LED pin
int LM35_OUT = A1;  // Input pin
int sensorPin = A0;

float VOLTAGE, TEMP ; // Variables for calculations

void setup() 
{
  Serial.begin(9600);
  pinMode(sensorPin, INPUT);
  pinMode(ledPin, OUTPUT);
   pinMode(G_LED, OUTPUT);
  pinMode(R_LED, OUTPUT); 
}
void loop() 
{
  int sensorValue = analogRead(sensorPin);

    // Read The Voltage From The LM35_OUT Pin
  VOLTAGE = analogRead(LM35_OUT);

  // Convert The Value From 0-1023 To 0-5 Volt
  VOLTAGE = VOLTAGE * 5.0 / 1024;

  // Convert The Voltage From Volt To Milli Volt
  VOLTAGE = VOLTAGE * 1000;

  // Convert The Voltage To Temperture : 1 Celsius = 10mV
  TEMP = VOLTAGE / 10;

  //Printing On Serial Monitor
  Serial.print("Temp = ");
  Serial.print(TEMP);
  Serial.println("Celsius ");
  delay(500);

  if( sensorValue <= 200 )  // Change the value as per your requirement
  {
    digitalWrite(ledPin, HIGH);
    Serial.print("LED ON ");
    Serial.println(sensorValue);
    delay(100);
  }

  else
  {
    digitalWrite(ledPin, LOW);
    Serial.println("LED OFF");
  }
 if (TEMP > 25) {
    digitalWrite(G_LED, LOW);
    digitalWrite(R_LED, HIGH);
  }
  else
  {
    digitalWrite(G_LED, HIGH);
    digitalWrite(R_LED, LOW);
  }
  
}
