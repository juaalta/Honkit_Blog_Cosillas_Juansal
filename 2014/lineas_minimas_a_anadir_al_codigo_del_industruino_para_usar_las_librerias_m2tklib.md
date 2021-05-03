# Líneas mínimas a añadir al código del Industruino para usar las librerías m2tklib

 Según mi experiencia creando menús y formularios dentro del Industruino usando las librerías m2tklib, el código mínimo a añadir a un fichero de código es el siguiente:

### Includes mínimos

``` c++
#include <U8glib.h>
#include <M2tk.h>
#include <utility/m2ghu8g.h>
```


### Declaración del tipo de pantalla

Esta declaración se ha de descomentar, si ya está o añadir al código.

``` c++
U8GLIB_MINI12864 u8g(21, 20, 19, 22);
```

### Gestión de botones

``` c++
uint8_t uiKeyUpPin = 7;
uint8_t uiKeyDownPin = 3;
uint8_t uiKeySelectPin = 2;
uint8_t uiKeyExitPin = 0;

int adc_key_in = 0;

int read_LCD_buttons_original() //routine to check button inputs and pass the correct button event to GUI
{

  adc_key_in = analogRead(A5);  // read the value from the sensor
  delay(5); //switch debounce delay. Increase this delay if incorrect switch selections are returned.
  if (adc_key_in < 100) return M2_KEY_NONE; // We make this the 1st option for speed reasons since it will be the most likely result
  if (adc_key_in > 300 && adc_key_in < 315)  return M2_KEY_PREV;
  if (adc_key_in > 600 && adc_key_in < 630)  return M2_KEY_SELECT;
  if (adc_key_in > 700 && adc_key_in < 930)  return M2_KEY_NEXT;

}

uint8_t m2_es_arduino_analog_input(m2_p ep, uint8_t msg)
{
  switch (msg)
  {
case M2_ES_MSG_GET_KEY:
  return read_LCD_buttons_original();
case M2_ES_MSG_INIT:
  return 0;
  }
  return 0;
}
```

### A incluir dentro del método setup()

``` c++
void industruino_Menu_setup(void) {

  //flip the screen 180°
  u8g.setRot180();
  // Connect u8glib with m2tklib
  m2_SetU8g(u8g.getU8g(), m2_u8g_box_icon);

  // Assign u8g font to index 0
  m2.setFont(0, u8g_font_6x13r);

  // Assign icon font to index 3
  m2.setFont(3, u8g_font_m2icon_7);

}
```

### Método loop()

``` c++
void industruino_Menu_loop() {
  // menu management
  m2.checkKey();
  if ( m2.handleKey() != 0 ) {
u8g.firstPage();
do {
  m2.checkKey();
  draw();
} while ( u8g.nextPage() );
  }
}
```

### Métodos adicionales a añadir

``` c++
Método draw:

void draw(void) {
  m2.draw();
}
```

