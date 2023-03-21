# ferm-pressure-sensor
A sensor to monitor beer fermentation progress

In addition to a camera monitoring the airlock in the fridge, I have used a pressure sensor for two years now to see how things are going. The sensor (MPX5010DP) is meant for low pressures, and cannot be used in a closed and pressurized vessel.

Parts I have used, are:
* 1x MPX5010DP. 0.2-4.7V output measures 0-10kPa
* 1x ADS1115 A/D converter
* 1x 4x 5V/3V3 Voltage Level Converter
* 1x Wemos D1 mini
* Filter cap's for MPX5010: 1x1uF, 1x10nF and 1x470pF
* Arduino connection cables
* 5mm ID Silicone hose connected to Positive Pressure on the MPX5010
* 1x Box. My favourite for such projects is a 82x57x32mm. If you are situated in Norway or Sweden, it is available at Kjell&Co (#89043). The box is also found as Velleman #G1019 or CamdenBoss #400-019.

The schematic (fermpress-sensor-d1.pdf) should be self-explanatory in how to connect the parts.

ESPEasy is used as firmware on the D1 mini. 

I created two devices: One collecting raw data from the ADS1115 every 2s and Gain set to 2/3x. The second one is a Dummy Device collecting average data from every 10th measurement every 15s via Rules (beer-ferm-rules1.txt).

Measurements are sent to Home Assistant via MQTT. This is how it could look like in the beginning of a brew:
![fermpress-20230313](https://user-images.githubusercontent.com/52971840/226713482-214738cd-4bbb-4ea8-8b6b-ff72ec519b5a.png)
The only Formula I have used, is "%value%-1200" for the raw device, only for getting numbers down to human levels. The interesting part is the curve itself.
When fermentation "stops", i.e.: no more plops, you would see from the curve there might still be pressure, and maybe a "plop" every 2 - 3hrs.

This is how it looks like inside the box:
![P1010701](https://user-images.githubusercontent.com/52971840/226715680-365029eb-1f24-44b8-9973-c47f08e1d189.JPG)

The box is placed as high up above the fermentor as possible (MPX5010 does not like humidity):
![P1010702](https://user-images.githubusercontent.com/52971840/226716124-d4aa5cbe-a793-4b9a-a840-19e842b387df.JPG)

The other end of the hose ends up in a T with quick disconnects on top of the fermentor:
![P1010703](https://user-images.githubusercontent.com/52971840/226716799-4bb3b98b-8779-4b0c-a1ef-36451f1f2262.JPG)

Being bored of cleaning up the mess of fermenting virile beers, I use a blow-off tube ending up in a 3L Erlenmeyer:
![P1010704](https://user-images.githubusercontent.com/52971840/226717673-a78e3b5e-1dad-4e89-ba48-b904dfb4d2de.JPG)


