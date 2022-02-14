```toc
```
# Auslesen von Sensordaten
Um die Daten eines Sensors auszulesen und auch zu speichern muss zuallererst die Application, in dem sich der jeweilige Sensor befindet, geöffnet werden und der Sensor dessen Daten benötigt werden angeklickt werden. 
![[Screenshot 2022-02-14 at 13.03.44.png]]
Daraufhin sind über den Reiter "Device Data" die jeweiligen Daten abzulesen

## Erläuterungen
![[Screenshot 2022-02-14 at 13.04.19.png]]
Jede Zeile, die sich unter "Device Data" befindet entspricht einem LoRaWAN-Paket. Die Informationen die auf den jeweiligen Zeilen stehen haben folgende Bedeutungen: 

An erster Stelle steht das Datum und die Uhrzeit zu welcher das jeweilige Paket vom Gateway empfangen wurde. 

Danach kommt "up" oder "down" — bei "up" handelt es sich um ein Uplink-Paket, das der Sensor selbst geschickt hat; bei "down" würde es sich um ein Paket handeln, das der Gateway an den Sensor geschickt hat.

Die nächsten Informationen zeigen an, auf welcher Frequenz das Paket beim Gateway ankam. `SF` steht für den sogenannten _Spreading Factor_. `BW125` steht für die Bandbreite (125 kHz). `FCnt: num` steht für den _Frame-Count_, also das wievielte LoRaWAN-Paket vom Node geschickt wurde. `FPort` ist der Frame-Port. Als letztes steht die Art des Up- bzw. Downlink-Pakets: `Unconfirmed` bedeutet, dass der Sensor keine Antwort vom LoRaWAN-Gateway erwartet; `Confirmed` bedeutet, dass der Sensor auf eine Antwort wartet (passiert beispielsweise bei `JoinRequest`-Paketen).

## Öffnen eines LoRaWAN-Paketes
![[Screenshot 2022-02-14 at 13.28.48.png]]
Um ein bestimmtes LoRaWAN-Paket zu öffnen wird dieses einfach angeklickt. Es öffnet sich nun das Paket mit allerlei Daten. Eine Datei mit einer Handvoll Beispielpaketen liegt in dem Ordner `Dateien/lora_paket_beispiel.json` (enthält auch dekodierte Daten).

### JSON-Daten-Erläuterungen
- <ins>**General**</ins>
	- `applicationID`
		- Die ID der Application (wird automatisch angelegt vom Server)
	- `applicationName`
		- Der vom Anwender vergebene Application-Name
	- `deviceName`
		- Der vom Anwender vergebene Gerätename
	- `devEUI`
		- Die EUI der Node von welcher die Daten stammen
	- `adr`
		- ?
	- `dr`
		- ?
	- `fCnt`
		- Frame-Count (siehe auch oben)
	- `fPort`
		- Frame-Port (siehe auch oben)
	- `data`
		- Die tatsächlich vom Node geschickten Daten (in Base64)
	- `confirmedUplink`
		- Entweder `true` oder `false` (siehe auch oben)
	- `devAddr`
		- Die Geräte-Adresse (wird bei OTAA nach jedem Join zufällig generiert und zugewiesen)
	- `publishedAt`
		- Wann das Paket angekommen ist
	- `deviceProfileID`
		- Die vom LoRaWAN-Server generierte ID für das Geräte-Profil des Sensors
	- `deviceProfileName`
		- Der Name des obengenannten Profils

- <ins>**rxInfo**</ins>
	- `gatewayID`
		- Die Gateway-ID des Gateway, der die Daten der Node empfangen hat
	- `time`
		- ?
	- `timeSinceGPSEpoch`
		- ? 
	- `rssi`
		- Der "Received Signal Strength Indicator", quasi die Signalstärke
	- `loRaSNR`
		- Der Signal-To-Noise-Ratio
	- `channel`
		- Auf welchem Kanal das Paket empfangen wurde (0-7)
	- `rfChain`
		- ?
	- `board`
		- Falls mehrere Concentrator-Boards angeschlossen sein sollten
	- `antenna`
		- Falls mehrere Antennen an dem Concentrator-Board angeschlossen sein sollten
	- `location`
		- Falls in Gateway-Profil eine GPS-Position angegeben wurde wird diese hier angezeigt; dies ist auch der Fall wenn der Gateway GPS-fähig ist und dieses Feature aktiviert ist
	- `fineTimestampType`
		- ?
	- `context`
		- ?
	- `uplinkID`
		- Jeder Uplink hat eine eigene ID; diese wird hier angezeigt
	- `crcStatus`
		- ? 
	
- <ins>**txInfo**</ins>
	- `frequency`
		- Die Frequenz, auf welcher das Paket gesendet und empfangen wurde
	- `modulation`
		- Die Modulationsart; ist bei LoRaWAN eigentlich immer `LORA`
	- `bandwidth`
		- Bandbreite (siehe auch oben)
	- `spreadingFactor`	
		- Spreading-Factor (siehe auch oben)
	- `codeRate`
		- ?
	- `polarizationInversion`
		- ?
