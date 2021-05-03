# Sistema de detección de paso por un camino con Arduino

## Descripción

La finalidad del proyecto es detectar el paso de coches y personas a la entrada de un huerto y avisar con una señal sonora dentro de la casa de este.
Por esto este proyecto está compuesto por 2 módulos:

- Módulo de detección de paso, ya sea de personas o de coches.
- Módulo de aviso de paso.

Los requerimientos son los siguientes:

- El módulo de detección de paso, al estar en el huerto, ha de tener una fuente de alimentación independiente, en este caso le hemos puesto una placa solar y una batería.
- El módulo de aviso ha de sonar cuando el módulo de detección le avise.
- El módulo de detección está a la entrada del huerto.
- El módulo de aviso está dentro de la casa.

![Módulo de detección con placa solar](../imagenes/detector_paso_coches/Descripcion_01.jpg "Módulo de detección con placa solar")

## Instrucciones

### Componentes usados

Los componentes usados han sido, por módulo:

- Módulo de detección
 - [Arduino Nano](https://www.wish.com/c/549bc514b9cb921840d9ecc5)
 - [PCB 5x7 cm](http://www.ebay.es/itm/20x-Double-Side-Prototype-PCB-Universal-Circuit-Board-2x8-3x7-4x6-5x7CM-DIY-124-/170989228488?hash=item27cfc091c8:g:ZtEAAMXQkN1RyZV7)
 - [Placa solar 3W 138x160](http://www.seeedstudio.com/depot/3W-Solar-Panel-138X160-p-954.html)
 - [Batería 3.7 v 6600 mAh](http://es.aliexpress.com/store/product/Solar-Street-Light-battery-3-7v-6600mAh-made-by-Chinese-manufacturer/1894067_32447790091.html#extend)
 - [LiPo Rider Pro](http://www.seeedstudio.com/depot/LiPo-Rider-Pro-p-992.html)
 - [Módulo subida de 3.3v a 5v](http://www.aliexpress.com/item/BL8530-BL8531-DC-DC-Step-Up-Power-Converter-Module-DC-Boost-Converter-Board-5V-3-3V/32296844878.html)
 - [Sensor ultrasonidos mojable JSN-SR04T](http://www.ebay.es/itm/272041782549?_trksid=p2060353.m2749.l2649&ssPageName=STRK%3AMEBIDX%3AIT)
 - [Módulos inalámbricos RF APC220](http://tienda.tuelectronica.es/index.php?route=product/product&product_id=57&search=SKU156095)
- Módulo de aviso
 - [Arduino Nano](https://www.wish.com/c/549bc514b9cb921840d9ecc5)
 - [PCB 5x7 cm](http://www.ebay.es/itm/20x-Double-Side-Prototype-PCB-Universal-Circuit-Board-2x8-3x7-4x6-5x7CM-DIY-124-/170989228488?hash=item27cfc091c8:g:ZtEAAMXQkN1RyZV7)
 - [Módulos inalámbricos RF APC220](http://tienda.tuelectronica.es/index.php?route=product/product&product_id=57&search=SKU156095)
 - Buzzer pasivo / relé.



### Montaje del circuito

El esquema en Fritzing es el siguiente:

- Módulo de detección

![Módulo de detección](../imagenes/detector_paso_coches/DetectorCoches_bb.png "Módulo de detección")

En este esquema no se ha añadido la parte de conexión al Lipo Rider Pro, la batería y la placa solar, por no tener los diseños para el Fritzing.

- Módulo de aviso

![Módulo de aviso](../imagenes/detector_paso_coches/Alarma_bb.png "Módulo de aviso")

Imágenes del sistema montado dentro del laboratorio:

- Módulo de detección

![Placa solar con Lipo Rider Pro y batería lipo conectados](../imagenes/detector_paso_coches/DetectorCoches_01.jpg "Placa solar con Lipo Rider Pro y batería lipo conectados")

![Módulo de detección montado sobre una breadboard con detector de ultrasonidos inicial](../imagenes/detector_paso_coches/DetectorCoches_02.jpg "Módulo de detección montado sobre una breadboard con detector de ultrasonidos inicial")

![Módulo de detección montado sobre una breadboard con detector de ultrasonidos final](../imagenes/detector_paso_coches/DetectorCoches_03.jpg "Módulo de detección montado sobre una breadboard con detector de ultrasonidos final")

![Parte superior de la PCB del módulo de detección sin componentes conectados](../imagenes/detector_paso_coches/DetectorCoches_04.jpg "Parte superior de la PCB del módulo de detección sin componentes conectados")

![Parte superior de la PCB del módulo de detección con componentes conectados](../imagenes/detector_paso_coches/DetectorCoches_05.jpg "Parte superior de la PCB del módulo de detección con componentes conectados")

![Módulo de detección dentro de su caja estanca](../imagenes/detector_paso_coches/DetectorCoches_06.jpg "Módulo de detección dentro de su caja estanca")

- Módulo de aviso

![Módulo de aviso montado sobre una breadboard](../imagenes/detector_paso_coches/Alarma_01.jpg "Módulo de aviso montado sobre una breadboard")

![Parte superior de la PCB del módulo de aviso sin componentes conectados](../imagenes/detector_paso_coches/Alarma_02.jpg "Parte superior de la PCB del módulo de aviso sin componentes conectados")

![Parte superior de la PCB del módulo de aviso con componentes conectados](../imagenes/detector_paso_coches/Alarma_03.jpg "Parte superior de la PCB del módulo de aviso con componentes conectados")

![Módulo de aviso dentro de su caja estanca](../imagenes/detector_paso_coches/Alarma_04.jpg "Módulo de aviso dentro de su caja estanca")

### Software

Las librerías usadas han sido:

- [HCSR04Ultrasonic](http://freecode.com/projects/hc-sr04-ultrasonic-arduino-library)

El código del arduino es el siguiente:

- Módulo de detección

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

- Módulo de aviso

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
