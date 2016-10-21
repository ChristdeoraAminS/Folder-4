# Folder-4
#include <Wire.h>
void setup(){
  Wire.begin();
}
void loop(){
  Wire.beginTransmission(4);
    unsigned dataADC = analogRead(A0);
    unsigned char dataI2C[2];
    dataI2C[0] = lowByte(dataADC);
    dataI2C[1] = highByte(dataADC);
    Wire.write(dataI2C[0]);
    Wire.write(dataI2C[1]);
    Wire.endTransmission();
    delay(500);
}
=========
#include <Wire.h>
void setup(){
  Wire.begin(500);
  Wire.onReceive(receiveEvent);
  Serial.begin(9600);
}
void loop(){
  delay(100);
}
void receiveEvent(int howMany)
{ while(Wire.available()){
  unsigned char dataI2C[2];
  dataI2C[0] = Wire.read();
  dataI2C[1] = Wire.read();
  unsigned int dataADC = word(dataI2C[1],dataI2C[0]);
  Serial.println(dataADC);
}
}
=========
#include <Wire.h>
void setup(){
  Wire.begin();
}
void loop(){
  Wire.beginTransmission(500);
    unsigned dataADC = analogRead(A0);
    unsigned char dataI2C[2];
    dataI2C[0] = lowByte(dataADC);
    dataI2C[1] = highByte(dataADC);
    Wire.write(dataI2C[0]);
    Wire.write(dataI2C[1]);
    Wire.endTransmission();
    delay(50);
}

========
#include <Wire.h>
void setup(){
  Wire.begin(500);
  Wire.onRequest(requestEvent);
  
}
void loop(){
  delay(100);
}
void requestEvent () 
{
  unsigned int dataADC = analogRead(A0);
  unsigned char dataI2C[2];
  dataI2C[0] = lowByte(dataADC);
  dataI2C[1] = highByte(dataADC);
  Wire.write(dataI2C,2);
}
