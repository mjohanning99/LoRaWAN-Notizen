```toc
```

# Konfiguration eines Anwendungsservers (GUI)
Um Geräte wie Gateways und Nodes mit dem Server zu verbinden muss auf die Weboberfläche des Anwendungsservers zugegriffen werden. Diese ist standardmäßig über `http://server_ip:8080` zu erreichen. Der Standardbenutzername ist `admin` mit selbigem Passwort. 

## Hinzufügen eines Netzwerkservers
Zu allererst sollte ein Netzwerkserver hinzugefügt werden. Dafür unter "Network-Servers" auf "+ Add" klicken.
![[Screenshot 2022-02-11 at 14.34.25.png]]
Hier muss dann einmal ein Name für den Netzwerkserver sowie auch die Adresse des Servers eingegeben werden. Sollte der Netzwerkserver auf demselben Server wie auch der Anwendungsserver laufen, so kann hier `localhost:8000` eingegeben werden.
Nach erfolgreicher Eingabe einfach auf "Add Network-Server" klicken und der Server wurde erfolgreich angelegt. 

## Hinzufügen eines Gateway-Profils
Auf "Gateway-profiles" klicken und daraufhin den "+ Create"-Knopf drücken.
![[Screenshot 2022-02-11 at 14.37.33.png]]
Auch hier muss wieder ein passender Name vergeben werden. Als "Stats interval (seconds)" kann hier einfach der vorgeschlagene Wert von "30" verwendet werden. Bei "Enabled channels" können alle drei Channels ("0, 1, 2") angegeben werden. Bei "Network-server" muss derjenige Netzwerkserver ausgewählt werden, der auch in der Gateway-Konfiguration hinterlegt wurde.

## Hinzufügen eines Service-Profils
Service-Profile dienen dazu, festzuhalten welche Features bestimmte User nutzen können (beispielsweise die Datenrate die über das Netzwerk gesendet werden darf). Hierzu muss in der entsprechenden Organisation der Menüpunk "Service-profiles" ausgewählt werden und dann oben rechts auf "+ Create". 
![[Screenshot 2022-02-11 at 15.04.31.png]]
- Service-profile name
	- Ein passender Name für das Profil
- Network-server
	- Der Netzwerkserver, der mit dem Profil verbunden sein soll
- Add gateway meta-data
	- Ob die Metadaten des Gateways (seine GPS-Position, Signalstärke usw.) mit in der JSON-Datei gespeichert werden sollen
- Enable network geolocation
	- Funktioniert nicht mit dem iC880A, deaktiviert lassen
- Device-status frequency
	- ?
- Minimum allowed data-rate
	- ?
- Maximum allowed data-rate
	- ?

## Hinzufügen eines Gateways
**Hinweis**: Gateways können nur von denjenigen Organisationen angelegt werden, denen dies auch explizit erlaubt wurde. Das Standard-Adminkonto mit der Standard-Organisation "ChirpStack" hat diese Befugnis. Gateways sind organisationsübergreifend verwendbar.

Zuerst muss die korrekte Organisation aus dem Dropdown-Menü ausgewählt werden und dann muss der Menüpunk "Gateways" angeklickt werden. Auf der Gateway-Seite dann oben rechts auf "+ Create".
![[Screenshot 2022-02-11 at 14.43.57.png]]
- Gateway name
	- Ein passender Name für den Gateway
- Gateway description
	- Eine genauere Beschreibung des Gateways (Raspberry Pi 3 Gateway HQ Lager, neben der Eingangstür rechts)
- Gateway ID
	- Siehe [[Einrichten eines LoRaWAN-Gateways]]
- Network-server
	- Der im Gateway hinterlegte Netzwerkserver
- Service-profile
	- Kann leergelassen werden
- Gateway-profile
	- Das vorhin erstellte Profil 
		
Die restlichen Einstellungen können so gelassen werden.

## Nodes einbinden
Um Nodes in das Netzwerk einbinden zu können ist zuallererst ein Geräteprofil vonnöten. Danach muss eine Application erstellt werden und die einzelnen Nodes in diese Application eingebunden werden.

### Erstellung eines Geräteprofils
In der jeweiligen Organisation muss der Menüpunkt "Device-profiles" ausgewählt werden. Für jede Art von Node sollte idealerweise ein eigenes Profil erstellt werden. Dann wieder oben rechts auf "+ Create".

#### General
Unter dem Tab "General" müssen nun folgende Dinge eingegeben werden:
![[Screenshot 2022-02-11 at 15.14.33.png]]
- Device-profile name
	- Ein passender Name für das Profil (rauchmelder_marke_xy)
- Network-server
	- Der Netzwerkserver, an den die Gateways die Pakete schicken
- LoRaWAN MAC version
	- Die MAC-Version; siehe Dokumentation der jeweiligen Node
- LoRaWAN Regional Parameters revision
	- Regionalparameterversion; siehe Dokumentation, sonst "A"
- ADR algorithm
	- Hier einfach "Default ADR algorithm" auswählen
- Max EIRP
	- ? 
- Uplink interval (seconds)
	- Die Häufigkeit der Uplink-Pakete in Sekunden; wie oft schickt das Gerät ein Paket? -> Siehe Dokumentation der jeweiligen Node

#### Join
Unter dem Reiter "Join" muss nun angegeben werden, ob das Gerät OTAA oder nur ABP unterstützt. Da die meisten modernen Geräte OTAA unterstützen (und dies auch die sicherere Variante ist), wird in der folgenden Anleitung nur OTAA beschrieben.
Hierzu einfach den Haken bei "Device support OTAA" setzen.![[Screenshot 2022-02-11 at 15.20.51.png]]

#### Codec
Die Daten der Nodes kommen als Base64 kodiert beim Netzwerkserver und somit auch bei dem Anwendungsserver an. Wenn man diese Daten in einer für Menschen lesbaren Form haben möchte, so ist ein Dekodierer nötig. Für viele Nodes gibt es bereits passende Dekodierer. Ein Beispieldekodierer ist in dem Order `Dateien` zu finden. Dekodierer müssen in JavaScript geschrieben werden.

### Erstellen einer Application
Nachdem ein Profil für die Nodes angelegt wurde muss in der jeweiligen Organisation unter "Applications" auch noch eine Application erstellt werden. Als Application kann beispielsweise ein Gebäude angesehen werden. Es werden somit also alle Nodes innerhalb eines bestimmten Gebäudes zusammengefasst. Hier muss auch wieder auf "+ Create" gedrückt werden.
![[Screenshot 2022-02-11 at 15.33.56.png]]
- Application name
	- Passender Name für die Application (herforder_strasse_155a_33609_bielefeld)
- Application description
	- Passende Beschreibung (Alle Warmwasserzähler in der Herforder Str. 155a)
- Service-profile
	- Ein passendes Service-Profil

### Hinzufügen von Nodes zu einer Application
Nachdem eine Application angelegt wurde muss diese mit einem Klick auf dessen Namen geöffnet werden. Auf der Konfigurationsseite der Application unter dem Reiter "Devices" muss auf "+ Create" geklickt werden.
![[Screenshot 2022-02-14 at 10.20.21.png]]
Auf der Seite die sich dann öffnet müssen folgende Daten eingegeben werden:
![[Screenshot 2022-02-14 at 10.24.36.png]]
- Device name
	- Ein passender Gerätename (temp_sensor_whg_10)
- Device description
	- Eine Gerätebeschreibung (Temperatursensor in Wohnung 10, 2. OG rechts)
- Device EUI
	- Die Geräte-EUI (befindet sich in der Anleitung des Gerätes oder direkt auf dem Gerät)
- Device-profile
	- Das korrekte Geräteprofil, das vorhin angelegt wurde

Nach Eingabe aller Daten wird auf "Create Device" geklickt. Man wird daraufhin dazu aufgefordert, den "Application key" einzugeben (bei OTAA). Auch dieser
 ![[Screenshot 2022-02-14 at 10.28.11.png]]
 Nach Eingabe des Keys muss auf "Set Device-Keys" geklickt werden — der Node wurde nun erfolgreich hinzugefügt.