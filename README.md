# VESM-Lokaverkefni
lokaverkefni i vesm

# Myndband af Snúrustýrður bíll með fjarstýringu
https://www.youtube.com/watch?v=pYsarbQF3kQ&feature=youtu.be
# Tinkercad link
https://www.tinkercad.com/things/0HbZ9zkIMRe-lokaverkefni-vesm/editel?sharecode=BJIkOjMOXkG2-XQpFAz2repSeiCsLwcHQSO4gvbR3RQ
# Myndband af bílnum
https://www.youtube.com/watch?v=LG6TwuXU8lM&feature=youtu.be
# Bíll link
https://www.tinkercad.com/things/6gxLfOOpupN-exquisite-hillar-jaiks/edit?sharecode=fcBBseQwUTYz901wTldScv5vyZ9CPIAbr_icdoSUAqk
# Dagbók
Ég klúðraði soldið mikið á verkefninu. Ég búinn að gefast upp en Stefán bauðst til að hjálpa mér, ég er honum mjög þakklátur að hafa hjálpað mér með þetta. Ég var nefnilega svona hrikalega seinn að byrja á þessu, mér finnst svo erfitt að ekki vera í skólanum og gleymi mér oft heima, og þegar skilafresturinn kláraðist reif ég mig í gang og stútaði verkefninu. Ég byrjaði á að henda saman cuircit dótinu og kóða það tók mig soldna stund að koma öllu saman þótt fyrir mikla hjálp. Þegar ég var búinn með það þá var það bara gera bílinn sem ég hafði betri á. Skilaði þessu svo á github og uppfyllti það sem var óskast af mér.

# Kóðarnir
## fjarstýringin

```
#include <Servo.h>

Servo serv1, serv2;
const int trigPin = 1;
const int echoPin = 2;
long duration;
int CM;
int pos = 0;

int forward = 0;
int backward = 0;
int right = 0;
int left = 0;
void setup()
{
  pinMode(echoPin, INPUT);
  pinMode(7, INPUT);
  pinMode(8, INPUT);
  pinMode(12, INPUT);
  pinMode(11, INPUT);
  pinMode(trigPin, OUTPUT);
  pinMode(3, OUTPUT);
  pinMode(5, OUTPUT);
  pinMode(6, OUTPUT);
  pinMode(9, OUTPUT);
  digitalWrite(7, HIGH);
  digitalWrite(8,HIGH);
  digitalWrite(12,HIGH);
  digitalWrite(11, HIGH);
  digitalWrite(3,LOW);
  digitalWrite(5,LOW);
  digitalWrite(6,LOW);
  digitalWrite(9,LOW);
  serv1.write(0);
  serv2.write(0);
  serv1.attach(11);
  serv2.attach(7);
  

}

void loop()
{
  
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  
  duration = pulseIn(echoPin, HIGH);
  CM = duration*0.034/2;
  
  forward = digitalRead(12);
  backward = digitalRead(8);
  right = digitalRead(7);
  left = digitalRead(11);
  
  digitalWrite(3,LOW);
  digitalWrite(5,LOW);
  digitalWrite(6,LOW);
  digitalWrite(9,LOW);

  if(backward == 0)
  {
  if(CM <= 50){
  digitalWrite(3,LOW);
  digitalWrite(5,LOW);
  digitalWrite(6,LOW);
  digitalWrite(9,LOW);
  }
    else{
    digitalWrite(6,HIGH);
    digitalWrite(9,HIGH);
    }
  }

  if(forward == 0)
  {
  if(CM <= 50){
  digitalWrite(3,LOW);
  digitalWrite(5,LOW);
  digitalWrite(6,LOW);
  digitalWrite(9,LOW);
  }
    else{
    digitalWrite(3,HIGH);
    digitalWrite(5,HIGH);
    }
  }
  
  if(right == HIGH){
  for (pos = 0; pos <= 150; pos += 1) { 
    serv1, serv2.write(pos); 
    
  }
  }
 
  if(left == HIGH){
  for (pos = 150; pos >= 0; pos -= 1) { 
   serv1, serv2.write(pos); 
                       
  }
  }

}
```
## Bíllinn
```
#include <Wire.h>
#include <LiquidCrystal.h>
LiquidCrystal Skjar(6 , 7, 5, 4, 3, 2);
const int trigPin = 11;
const int echoPin = 10;
long duration;
int CM;

bool forward , backward , right , left =0;
void setup()
{
  Skjar.begin(16,2);
  pinMode(echoPin, INPUT);
  pinMode(trigPin, OUTPUT);


}

void loop()
{
 
  digitalWrite(trigPin, LOW);
  delayMicroseconds(2);
  digitalWrite(trigPin, HIGH);
  delayMicroseconds(10);
  digitalWrite(trigPin, LOW);
  
  duration = pulseIn(echoPin, HIGH);
  CM = duration*0.034/2;
  
  Skjar.setCursor(0,0); // Sets the location at which subsequent text written to the LCD will be displayed
  Skjar.print("Fjarlaegd:"); // Prints string "Distance" on the LCD
  Skjar.print(CM); // Prints the distance value from the sensor
  Skjar.print("cm");

  if (CM > 100){ 
    Skjar.setCursor(0,1);
    Skjar.print("Metrar: ");
    Skjar.print(CM/100);
    Skjar.print("     ");
  	delay(2);
  }
 
  if (CM >51 and CM < 79){
  	Skjar.setCursor(0,1);
    Skjar.print("Varlega.");
  }
  if (CM <= 50){
	Skjar.setCursor(0,0);
    Skjar.print("Heyrdu!        ");
    Skjar.setCursor(0,1);
    Skjar.print("Alltof nalaegt");
    delay(500);
  }
  if (CM < 100 and CM > 80){
  Skjar.setCursor(0,1);
  Skjar.print("Metrar: 0");
  Skjar.print("         ");
  }
}

```
