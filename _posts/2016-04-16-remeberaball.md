---
layout: post_page
title: Magic Item
description: The Rememberaball
assignment_number: 6
---

This Week's assignment was: Pick a spell from the AD&D Player's Handbook (any edition), other fantasy role playing game, or from fantasy literature or mythology, and make it real.

I've decided to make a Harry Potter Remembeall  

***'It's a Remembrall!' he [Neville] explained. 'Gran knows I forget things – this tells you if there's something you've forgotten to do. Look, you hold it tight like this and if it turns red – oh…' His face fell, because the Remembrall had suddenly glowed scarlet, '... you've forgotten something...'***  

(From Harry Potter and the Philosopher’s Stone, Chapter Nine)
  

A Remembrall is a tennis ball-sized glass ball that contains smoke that turns red when its owner has forgotten something. It turns clear once whatever was forgotten is remembered.

<div align="center">
<video width="100%" controls>
  <source src="{{site.baseurl}}/img/rememberaball/Rememberaball.mov" type="video/mov">
  <source src="{{site.baseurl}}/img/rememberaball/Rememberaball.mp4" type="video/mp4">
Your browser does not support the video tag.
</video>
</div>
  
  

### How It's Done:  


With Tal's advice, I got a [Light Blue Bean](https://punchthrough.com/bean), it's a tiny size BLE dev board. 30$ worth.
![the Light Blue Bean]({{site.baseurl}}/img/rememberaball/light_blue_bean.png)

I cut the board, to fit it into a small clear ornament ball.
And soldered a strip of 5 Neopixels(https://www.adafruit.com/category/168) to it.

![preparing the board]({{site.baseurl}}/img/rememberaball/bean_cut.jpg)  ![preparing the board]({{site.baseurl}}/img/rememberaball/bean_neopixels.jpg)

Then, I programed the board to only blink the Neopixels when there is no Bluetooth connection. which means, whenever it is far enough from a chosen device to be connected, it will blink.

```
#include <Adafruit_NeoPixel.h>
#ifdef __AVR__
  #include <avr/power.h>
#endif

#define PIN            0

#define NUMPIXELS      5

Adafruit_NeoPixel pixels = Adafruit_NeoPixel(NUMPIXELS, PIN, NEO_GRB + NEO_KHZ800);

bool connected = false;
void setup() 
{
  Bean.setLed(0, 0, 0);
    // This is for Trinket 5V 16MHz, you can remove these three lines if you are not using a Trinket
  #if defined (__AVR_ATtiny85__)
    if (F_CPU == 16000000) clock_prescale_set(clock_div_1);
  #endif
  // End of trinket special code

  pixels.begin(); // This initializes the NeoPixel library.
}

// the loop routine runs over and over again forever:
void loop() 
{
  connected = Bean.getConnectionState();
  if (connected) {
  for(int i=0;i<NUMPIXELS;i++){
    pixels.setPixelColor(i, pixels.Color(0,0,0)); // Moderately bright green color.
    pixels.show(); // This sends the updated pixel color to the hardware. 

  }
  }
  else{
      for(int i=0;i<NUMPIXELS;i++){
       pixels.setPixelColor(i, pixels.Color(160, 0, 160)); // Moderately bright green color.
       pixels.show(); // This sends the updated pixel color to the hardware.
       Bean.sleep(25);
       pixels.setPixelColor(i, pixels.Color(0,0,0)); // Moderately bright green color.
       pixels.show(); // This sends the updated pixel color to the hardware. 
     }
    
  }
   Bean.sleep(100);  
}
```

I then just covered the Light blue bean with a plastic bag, to give it a smoke effect, and put it inside the clear ball.

![rememberaball]({{site.baseurl}}/img/rememberaball/ball.jpg)
  
  

![rememberaball]({{site.baseurl}}/img/rememberaball/rememberaball.jpg)
