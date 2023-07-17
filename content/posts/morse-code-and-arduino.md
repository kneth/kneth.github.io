---
title: "Morse Code and Arduino"
date: 2012-02-07T18:06:14+02:00
draft: false
---

## Morse codes and Arduino

My son [Svante](http://www.supersejemig.dk/) came home Friday and told me that he had been working on Morse codes in science class. We talked a bit on how to translate sentences to Morse code. Yesterday evening I had to construct a translator using my [Arduino](http://www.arduino.cc/) board, a LED and a LCD display. The program is pretty simple. It processes the message - letter by letter - and shows the current letter in capital and the Morse code on the second line. Moreover, it blinks the Morse code using the LED. You find my program below.

```C
#include <stdio.h>
#include <stdlib.h>
#include <LiquidCrystal.h>

int LED  = 9;
LiquidCrystal lcd(10, 11, 12, 13, 14, 15, 16);
char msg[] = "super seje mig";
char m[16];
char *morse[] = {
  "*-",       // A
  "-***",     // B
  "-*-*",     // C 
  "*--",      // D
  "*",        // E
  "**-*",     // F
  "--*",      // G
  "****",     // H
  "**",       // I
  "*---",     // J
  "-*-",      // K
  "*-**",     // L
  "--",       // M
  "-*",       // N
  "---",      // O
  "*--*",     // P
  "--*-",     // Q
  "*-*",      // R
  "***",      // S
  "-",        // T
  "**-",      // U
  "***-",     // V
  "*--",      // W
  "-**-",     // X
  "-*--",     // Y
  "--**"      // Z
};
void setup() {
  lcd.begin(16, 2);
  lcd.clear();
  lcd.setCursor(0, 0);
  lcd.print("Booting");
  for(int i=0; i<16; i++) {
    lcd.setCursor(i, 1);
    lcd.write('.');
    delay(100);
  } 
  lcd.clear(); 
  lcd.setCursor(0, 0);
  lcd.print("K. Geisshirt");
  lcd.setCursor(0, 1);
  lcd.print("Copyright 2012");
  delay(1000);
  pinMode(LED, OUTPUT);
}
void loop() {
  for(int i=0; i<strlen(msg); i++) {
    for(int j=0; j<strlen(msg); j++) m[j] = msg[j];
    m[strlen(msg)] ='\0'; 
    if (m[i] != ' ') m[i] = m[i]+('A'-'a'); 
    lcd.clear();
    lcd.setCursor(0, 0);
    lcd.print(m);
    lcd.setCursor(0, 1);
    if (m[i] != ' ') {
      lcd.print(morse[m[i]-'A']);
      for(int j=0; j<strlen(morse[m[i]-'A']); j++) {
        digitalWrite(LED, HIGH);
        if (morse[m[i]-'A'][j] == '*') {
          delay(500);
        } else {
          delay(1000);
        }
        digitalWrite(LED, LOW);
        delay(250);
      }
    }
    if (m[i] != ' ') {   
      delay(1000);
    } else {
      delay(100);
    }
  }
}
```

If you haven't tried an Arduino board, it is highly recommended. With an electronic brick and a few components, it is much like LEGO for adults.

{{< youtube KBK3YLvwbwg >}}