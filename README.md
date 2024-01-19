# Práctica ESP32 con LCD y ultrasonico
## Introducción
En este práctica se muestra como podemos programar una ESP32 con el sensor ULTRASONICO y un display LCD.
## Material a utilizar
WOKWI
Tarjeta ESP32
Sensor HC-SR04
Display LCD16x2(I2C)
## Intrucciones
### Requisitos previos
Para esta práctica utilizaremos el simulador WOKWI.
### Instrucciones de preparación de entorno
1. Escribir el siguiente código:
```
#include "DHTesp.h"
#include <LiquidCrystal_I2C.h>
#define I2C_ADDR    0x27
#define LCD_COLUMNS 20
#define LCD_LINES   4

const int Trigger = 4;   //Pin digital 2 para el Trigger del sensor
const int Echo = 15;   //Pin digital 3 para el Echo del sensor
LiquidCrystal_I2C lcd(I2C_ADDR, LCD_COLUMNS, LCD_LINES);
void setup() {
  Serial.begin(9600);//iniciailzamos la comunicación
  pinMode(Trigger, OUTPUT); //pin como salida
  pinMode(Echo, INPUT);  //pin como entrada
  digitalWrite(Trigger, LOW);//Inicializamos el pin con 0
  lcd.init();
  lcd.backlight();
}

void loop()
{

  long t; //timepo que demora en llegar el eco
  long d; //distancia en centimetros

  digitalWrite(Trigger, HIGH);
  delayMicroseconds(10);          //Enviamos un pulso de 10us
  digitalWrite(Trigger, LOW);
  
  t = pulseIn(Echo, HIGH); //obtenemos el ancho del pulso
  d = t/59;             //escalamos el tiempo a una distancia en cm
  
  Serial.print("Distancia: ");
  Serial.print(d);      //Enviamos serialmente el valor de la distancia
  Serial.print("cm");
  Serial.println();
  delay(1000);          //Hacemos una pausa de 100ms
  
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Distancia: " + String(d) +"cm  ");
  delay(1000);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Ing. ALejandro");
  lcd.setCursor(0, 1);
  lcd.print("Ing. Industrial");
  delay(2000);

}
```
2. Instalar la libreria de DHT sensor library for ESPx como se muestra en la siguente imagen.
   
![](https://github.com/AlejandroBarreraU/Practica-4-Ultrasonico/blob/main/instalar%20librerias.png?raw=true)
3.Instalar la libreria de LiquidCrystal I2C como se muestra en la siguente imagen.

![](https://github.com/AlejandroBarreraU/Practica-4-Ultrasonico/blob/main/instalar%20librerias%202.png?raw=true)
4. Agregamos LCD y HC-SR04.

![](https://github.com/AlejandroBarreraU/Practica-4-Ultrasonico/blob/main/agrear%20lcd.png?raw=true)

![](https://github.com/AlejandroBarreraU/Practica-4-Ultrasonico/blob/main/a%C3%B1adimos%20ultra.png?raw=true)
## Conexiones
Se realizan las siguientes conexiones.

![](https://github.com/AlejandroBarreraU/Practica-4-Ultrasonico/blob/main/conexiones%20ultra.png?raw=true)

## Instrucciones de operación
1. Iniciar simulador.
2. Visualizar los datos en el monitor serial.
3. Colocar la distancia dando doble click al sensor HC-SR04
## Resultados
Cuando haya funcionado, verás los valores dentro del monitor serial y el display como se muestra en la siguente imagen.

![](https://github.com/AlejandroBarreraU/Practica-4-Ultrasonico/blob/main/resultados%20ultra%202.png?raw=true)

![](https://github.com/AlejandroBarreraU/Practica-4-Ultrasonico/blob/main/resultados%20ultra%201.png?raw=true)
## Créditos
Desarrollado por el Ing. Alejandro Barrera
