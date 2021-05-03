# Step detection system by a way with Arduino

## Description

The purpose of the project is to detect the passing of cars and people at the entrance to an orchard and a warning beep inside this house.  
For this project it consists of 2 modules:

- Module detection step, either of people or cars.
- Module warning step.

The requirements are:

- The step detection module, being in the garden, must have a separate power supply, in this case we have put a solar panel and a battery.
- The module must sound warning when the detection module warn you.
- The detection module is at the entrance of the garden.
- The warning module is inside the house.

![Detection module with solar panel](../imagenes/detector_paso_coches/Descripcion_01.jpg "Detection module with solar panel")

## Instructions

### Components used

The components used have been:

- Detection module
 - [Arduino Nano](https://www.wish.com/c/549bc514b9cb921840d9ecc5)
 - [PCB 5x7 cm](http://www.ebay.es/itm/20x-Double-Side-Prototype-PCB-Universal-Circuit-Board-2x8-3x7-4x6-5x7CM-DIY-124-/170989228488?hash=item27cfc091c8:g:ZtEAAMXQkN1RyZV7)
 - [3W Solar Panel 138x160](http://www.seeedstudio.com/depot/3W-Solar-Panel-138X160-p-954.html)
 - [Battery 3.7 v 6600 mAh](http://es.aliexpress.com/store/product/Solar-Street-Light-battery-3-7v-6600mAh-made-by-Chinese-manufacturer/1894067_32447790091.html#extend)
 - [LiPo Rider Pro](http://www.seeedstudio.com/depot/LiPo-Rider-Pro-p-992.html)
 - [Step up power converter module 3.3v to 5v](http://www.aliexpress.com/item/BL8530-BL8531-DC-DC-Step-Up-Power-Converter-Module-DC-Boost-Converter-Board-5V-3-3V/32296844878.html)
 - [Ultrasonic Module Distance Measuring Transducer Sensor Waterproof JSN-SR04T](http://www.ebay.es/itm/272041782549?_trksid=p2060353.m2749.l2649&ssPageName=STRK%3AMEBIDX%3AIT)
 - [APC220 RF wireless modules](http://tienda.tuelectronica.es/index.php?route=product/product&product_id=57&search=SKU156095)
- Warning module
 - [Arduino Nano](https://www.wish.com/c/549bc514b9cb921840d9ecc5)
 - [PCB 5x7 cm](http://www.ebay.es/itm/20x-Double-Side-Prototype-PCB-Universal-Circuit-Board-2x8-3x7-4x6-5x7CM-DIY-124-/170989228488?hash=item27cfc091c8:g:ZtEAAMXQkN1RyZV7)
 - [Ultrasonic Module Distance Measuring Transducer Sensor Waterproof JSN-SR04T](http://www.ebay.es/itm/272041782549?_trksid=p2060353.m2749.l2649&ssPageName=STRK%3AMEBIDX%3AIT)
 - Passive buzzer / relay.

### Assembly of the circuit

The Fritzing scheme is as follows:

- Detection module

![Detection module](../imagenes/detector_paso_coches/DetectorCoches_bb.png "Detection module")

In this scheme has not been added to the connection part of the Lipo Rider Pro, battery and solar panel, I not to have the designs for Fritzing.

- Warning module

![Warning module](../imagenes/detector_paso_coches/Alarma_bb.png "Warning module")

Images of the system mounted inside the laboratory:

- Detection module

![Solar panel with Lipo Rider Pro and battery](../imagenes/detector_paso_coches/DetectorCoches_01.jpg "Solar panel with Lipo Rider Pro and battery")

![Detection module mounted on a breadboard with initial ultrasound detector](../imagenes/detector_paso_coches/DetectorCoches_02.jpg "Detection module mounted on a breadboard with initial ultrasound detector")

![Detection module mounted on a breadboard with final ultrasound detector](../imagenes/detector_paso_coches/DetectorCoches_03.jpg "Detection module mounted on a breadboard with final ultrasound detector")

![Top of the PCB detection module without connected components](../imagenes/detector_paso_coches/DetectorCoches_04.jpg "Top of the PCB detection module without connected components")

![Top of the PCB detection module with connected components](../imagenes/detector_paso_coches/DetectorCoches_05.jpg "Top of the PCB detection module with connected components")

![Detection module inside his waterproof case](../imagenes/detector_paso_coches/DetectorCoches_06.jpg "Detection module inside his waterproof case")

- Warning module

![Warning module mounted on a breadboard](../imagenes/detector_paso_coches/Alarma_01.jpg "Warning module mounted on a breadboard")

![Top of the PCB warning module without connected components](../imagenes/detector_paso_coches/Alarma_02.jpg "Top of the PCB warning module without connected components")

![Top of the PCB warning module with connected components](../imagenes/detector_paso_coches/Alarma_03.jpg "Top of the PCB warning module with connected components")

![Warning module inside his waterproof case](../imagenes/detector_paso_coches/Alarma_04.jpg "Warning module inside his waterproof case")

### Software

The libraries used have been:

- [HCSR04Ultrasonic](http://freecode.com/projects/hc-sr04-ultrasonic-arduino-library)

The code of the Arduino is the following:

- Detection module

``` cpp
/*
  Título: Modulo_RF_APC220 --> Puerto serie
*/

#include <Ultrasonic.h>

//Pins ultrasonido
const int TRIG_PIN = 12;
const int ECHO_PIN = 13;

Ultrasonic ultrasonic(TRIG_PIN, ECHO_PIN);

void setup()
{
  Serial.begin(9600); // Establecemos la velocidad del puerto serie (Igual que APC220)
}

void loop()
{

  float cmMsec;
  long microsec = ultrasonic.timing();
  cmMsec = ultrasonic.convert(microsec, Ultrasonic::CM);

  Serial.print(int(cmMsec));
  Serial.println("=");

  delay(1000);

}
```

- Warning module

``` cpp

// create notes for our song
int C = 131;
int D = 147;
int E = 165;
int F = 175;
int G = 196;

// create an array to hold note values
int songNotes[] = {E, E, E, E, E, E, E, G, C, D, E, F, F, F, F, F, E, E, E, G, G, F, D, C};
// create another array to hold note lengths
int noteDurations[] = {4, 4, 2, 4, 4, 2, 4, 4, 4, 4, 1, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 4, 1};

byte byteRead;  //Datos leídos por el puerto serie
long longitud;  //Longitud recibida por el puerto serie

long longitudMaxima = 100;

String inString = "";                          //This string is used to store the incoming data
unsigned int pitch;                            //This is the variable we will use to store the buzzers p

void setup()
{
  Serial.begin(9600);

  longitud = 0;
}


void loop()
{

  while (Serial.available() > 0)
  {
    byteRead = Serial.read();

    //listen for numbers between 0-9
    if (byteRead > 47 && byteRead < 58) {
      //number found
      longitud = (longitud * 10) + (byteRead - 48);
    }

    if (byteRead == 61)
    {
      Serial.println(longitud);

      if (longitud <= longitudMaxima)
      {
        melodia();
      }

      longitud = 0;
    }

  }


}


void melodia()
{
  // iterate through arrays to play each note for its duration
  // plays our jingle once
  for (int i = 0; i < 24; i ++)
  {
    // calculate note duration
    // 1 second divided by note length
    // adjusting value of 1000 can change tempo
    int noteDuration = 1000 / noteDurations[i];
    // sends tone to pin 8
    tone(8, songNotes[i], noteDuration);

    // pause between notes a little to hear them better
    // this can also be used to adjust tempo
    int pauseBetweenNotes = noteDuration * 1.3;
    delay(pauseBetweenNotes);
    // once note is done, stop playing it
    noTone(8);
  }
}
```
