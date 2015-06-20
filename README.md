#include <Wire.h>
#include <LiquidCrystal_I2C.h>
LiquidCrystal_I2C lcd(0x27,16,2);

int Ana1 = A0;                      //Entrada analogica de LM35
int Temp = 0;
char Grados = 'º';

int Ana11 = A1;                      //Entrada analogica de LM352
int Temp1 = 0;

void setup(){
  Serial.begin(9600);      
  lcd.backlight();
  lcd.init();
  pinMode(13,OUTPUT);
  digitalWrite(13, HIGH);          //Activamos la retroiluminacion
}

void loop(){
  Temp = analogRead(Ana1);         //Leemos el valor de la entrada analogica
  Temp = (Temp*500)/1023;
//  Temp = (5.0*Temp*100)/1023;
//  Temp = map(Temp,0,1024, 55,150);  //Escalamos la señal a grados centigrados
  Temp1 = analogRead(Ana11);         //Leemos el valor de la entrada analogica
  Temp1 = (Temp1*500)/1023;
  
  //Mostramos los grados en el serial
  Serial.print("Grados: ");
  Serial.print(Temp);
  Serial.print(Grados);
  Serial.println("C");
  
  
  //Mostramos los grados en la pantalla LCD
  lcd.setCursor(0,0);            //Con este comando decimos en que linea queremos escribir
  lcd.print("T1 = ");
  lcd.print(Temp);
  lcd.print((char)223); 
  lcd.print("C"); 
  lcd.setCursor(0,1); 
  lcd.print("T0 = ");  
  lcd.print(Temp1); 
  lcd.print((char)223); 
  lcd.print("C"); 
  
  delay(1000);                  //Al ser temperatura no hace falta leerlo tan seguido
}
