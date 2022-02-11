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
		- Das vorhin erstellte Profil
		
Die restlichen Einstellungen können so gelassen werden