// Load in the libraries
#include <SPI.h>
#include <nRF24L01.h>
#include <RF24.h>

// include the library code:
#include <LiquidCrystal.h>
int x=0;
// initialize the library by associating any needed LCD interface pin
// with the arduino pin number it is connected to
const int rs = 2, en = 3, d4 = 4, d5 = 5, d6 = 6, d7 = 7;
LiquidCrystal lcd(rs, en, d4, d5, d6, d7);

// Set the CE & CSN pins
#define CE_PIN   9
#define CSN_PIN 10
int bilgi[1];

// This is the address used to send/receive
const byte rxAddr[6] = "00002";

// Create a Radio
RF24 radio(CE_PIN, CSN_PIN); 
int sem=0, sem1=0;
void setup(void) {
 
 pinMode(A0,INPUT);
 

  pinMode(A1,INPUT);
  

  pinMode(A2,INPUT);





  
  // Start up the Serial connection
  while (!Serial);
  Serial.begin(9600);
  
  // Start the Radio!
  radio.begin();
  
  // Power setting. Due to likelihood of close proximity of the devices, set as RF24_PA_MIN (RF24_PA_MAX is default)
  radio.setPALevel(RF24_PA_MIN); // RF24_PA_MIN, RF24_PA_LOW, RF24_PA_HIGH, RF24_PA_MAX
  
  // Slower data rate for better range
  radio.setDataRate( RF24_250KBPS ); // RF24_250KBPS, RF24_1MBPS, RF24_2MBPS
  
  // Number of retries and set tx/rx address
  radio.setRetries(15, 15);
  radio.openWritingPipe(rxAddr);

  // Stop listening, so we can send!
  radio.stopListening();
}

void loop() {
//1
//Serial.println(analogRead(A0));
int x = analogRead(A0);
     int y = analogRead(A1);
int b=analogRead(A2);
int a=analogRead(A3);
int c=analogRead(A4);
int d=analogRead(A5);
Serial.print(" ");
Serial.print(a);
Serial.print(" ");
Serial.print(b);
Serial.print(" ");
  Serial.print(c); 
  Serial.print(" ");  
Serial.print(d);
Serial.println(" ");

      if(analogRead(A0) <320 )
  {
  bilgi[0] = 1;
   radio.write(bilgi, 1);
  Serial.print("L");
          
    
}
 
 else if(analogRead(A0) >380 )
  {
  bilgi[0] = 2;
   radio.write(bilgi, 1);
  Serial.print("R");

  
}

else{
  bilgi[0] = 5;
   radio.write(bilgi, 1);
  Serial.print("s");

 
    
}
if(a>=305){
  bilgi[0] = 6;
   radio.write(bilgi, 1);
  Serial.print("a1 ");
          
    
}
if(a<305){
  bilgi[0] = 7;
   radio.write(bilgi, 1);
  Serial.print("a2 ");
          
    
}
if(b>=340){
  bilgi[0] = 8;
   radio.write(bilgi, 1);
  Serial.print("b1 ");
          
    
}
if(b<340){
  bilgi[0] = 9;
   radio.write(bilgi, 1);
  Serial.print("b2 ");
          
    
}
   if(c>=290){
  bilgi[0] = 10;
   radio.write(bilgi, 1);
  Serial.print("c1 ");
          
    
}
if(c<290){
  bilgi[0] = 11;
   radio.write(bilgi, 1);
  Serial.print("c2 ");
          
    
}
if(d>=302){
  bilgi[0] = 12;
   radio.write(bilgi, 1);
  Serial.print("d1 ");
          
    
}
if(d<302){
  bilgi[0] = 13;
   radio.write(bilgi, 1);
  Serial.print("d2 ");
          
    
}
 delay(500);
 

}
