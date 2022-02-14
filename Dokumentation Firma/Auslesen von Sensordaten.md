```toc
```
# Auslesen von Sensordaten
Um die Daten eines Sensors auszulesen und auch zu speichern muss zuallererst die Application, in dem sich der jeweilige Sensor befindet, geöffnet werden und der Sensor dessen Daten benötigt werden angeklickt werden. 
![[Screenshot 2022-02-14 at 13.03.44.png]]
Daraufhin sind über den Reiter "Device Data" die jeweiligen Daten abzulesen.
![[Screenshot 2022-02-14 at 13.04.19.png]]
Jede Zeile, die sich unter "Device Data" befindet entspricht einem LoRaWAN-Paket. Die Informationen die auf den jeweiligen Zeilen stehen haben folgende Bedeutungen: 

An erster Stelle steht das Datum und die Uhrzeit zu welcher das jeweilige Paket vom Gateway empfangen wurde. 

Danach kommt "up" oder "down" — bei "up" handelt es sich um ein Uplink-Paket, das der Sensor selbst geschickt hat; bei "down" würde es sich um ein Paket handeln, das der Gateway an den Sensor geschickt hat.

Die nächsten Informationen zeigen an, auf welcher Frequenz das Paket beim Gateway ankam. `SF` steht für den sogenannten _Spreading Factor_. `BW125` steht für die Bandbreite (125 kHz). `FCnt: num` steht für den _Frame-Count_, also das wievielte LoRaWAN-Paket vom Node geschickt wurde. `FPort` ist der Frame-Port. Als letztes steht die Art des Up- bzw. Downlink-Pakets: `Unconfirmed` bedeutet, dass der Sensor keine Antwort vom LoRaWAN-Gateway erwartet; `Confirmed` bedeutet, dass der Sensor auf eine Antwort wartet (passiert beispielsweise bei `JoinRequest`-Paketen).
