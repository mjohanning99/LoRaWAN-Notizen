# From zero to LoRaWAN in a weekend

So you want to extend the coverage of [The Things Network](http://thethingsnetwork.org) in your neighborhood but missed the kickstarter to buy a gateway?

*Worry not!* It's really easy to build one yourself that is on par with most other gateways when it comes to specs, but is significantly cheaper.

## Ordering the parts

Our gateway will be based on the [IMST iC880a board](http://www.wireless-solutions.de/products/radiomodules/ic880a). This is the most important piece, the rest are components you might even have already lying around.

Here's our shopping list:

|Part|Price|Order/link|
|----|-----|----------|
|iC880A-SPI concentrator board|EUR 119.- (excl. tax)|[IMST Webshop](http://shop.imst.de/wireless-modules/lora-products/8/ic880a-spi-lorawan-concentrator-868-mhz)|
|Pigtail for antenna <sup>1</sup>|EUR 6.5 (excl. tax)|[IMST Webshop](https://shop.imst.de/wireless-modules/accessories/20/u.fl-to-sma-pigtail-cable-for-ic880a-spi)|
|Raspberry Pi <sup>2</sup>|EUR 32.-|RPi2: [Farnell](http://de.farnell.com/raspberry-pi/rpi2-modb-v1-2/sbc-raspberry-pi-2-model-b-v1/dp/2612474) and RPi3: [Farnell](http://de.farnell.com/raspberry-pi/raspberrypi-modb-1gb/raspberry-pi-3-model-b/dp/2525225)|
|Antenna <sup>3</sup>|EUR 3.50 - EUR 8|3dBi: [Farnell](http://de.farnell.com/rf-solutions/ant-8whip3h-sma/ant-868mhz-peitsche-gelenk-sma/dp/2305899), 5dBi: [Aliexpress](http://www.aliexpress.com/item/Free-shipping-customized-best-performance-High-Gain-5dBi-GSM-868mhz-900-1800mhz-magnetic-base-antenna/32592017287.html), 7dBi: [Aliexpress](http://www.aliexpress.com/store/product/868MHZ-915MHZ-GSM-3G-antenna-small-sucker-7dbi-aerial-3meters-SMA-male-2/1859567_32512220307.html), 7.5dBi [Aliexpress](http://www.aliexpress.com/item/868MHz-Antenna-7-5dBi-Gain/1870152812.html)|
|Power Supply 2.5A with micro USB|EUR 7.79|[Farnell](https://de.farnell.com/raspberry-pi/t5875dv/psu-raspberry-pi-5v-2-5a-multi/dp/2520785)|
|MicroSD Card (4Gb or more)|~ EUR 8||
|RPi to iC880a interface|~ EUR 5-40|Four options: <ul><li>simple backplane: [Tindie](https://www.tindie.com/products/gnz/imst-ic880a-lorawan-backplane/)</li><li>ch2i backplane: [pcbs.io](https://pcbs.io/share/zvoQ4)</li><li>coredump.ch backplane: [coredump.ch](https://shop.coredump.ch/product/ic880a-lorawan-gateway-backplane-prototype/)</li><li>7x Dual female jumper wires <sup>4</sup></li></ul>|
|WiFi dongle <sup>5</sup>|||

<sup>\[1\]</sup> Normally, the [pigtail](http://webshop.imst.de/pigtail-for-ic880a-spi-and-ic880a-usb.html) is SMA, but on some orders IMST shipped one with a [RP-SMA Female connector](https://en.wikipedia.org/wiki/SMA_connector#Reverse_polarity_SMA). Since the linked antennas are SMA Male, you need an [RP-SMA Male to SMA Female adapter](http://www.aliexpress.com/item/Brass-Adapter-RP-SMA-Male-Jack-To-SMA-Female-Jack-Screw-Thread-Connector-90-Degrees-Right/32637688405.html) in this case.

<sup>\[2\]</sup> It works with RPI 3, RPi 2 B, RPi B+ and even RPi Zero; but avoid the original revisions because the polyfuse might cause problems.

<sup>\[3\]</sup> The choice of antenna is huge, pick any of your liking, as long as it is 1/2 wavelength and has 3dBi or higher.

<sup>\[4\]</sup> Using any of the backplane boards listed instead of jumper wires is **strongly** recommended. Jumper wires can cause interference, and even thou the software will handle it, the performance of your gateway will be sub-optimal.

<sup>\[5\]</sup> e.g. Edimax EW-7811UN. Only required if you connect via WiFi instead of Ethernet and not using the Raspberry Pi 3, which already comes with built in WiFi. The alternative is to power the device via the Ethernet cable using a PoE splitter/injector.

That will get you a functional gateway, but you most likely want to have it in a box. There are plenty of options, here's just one suggestion:

* IP67 Enclosure (we got ours from [decentlab.com](http://www.decentlab.com/). you have to send an email to them to shop it. The Enclosure is not on the products page. Price is 85CHF + shipping 40CHF)
* Mounting plate, screws and spacers

Now sit and wait for the postman to make you happy.

## Choosing the backhaul

What is a **backhaul**? Backhaul refers to how the Raspberry Pi will be connected to the Internet.

This guide focuses on using Wifi as backhaul, but you could also use Ethernet or 3G/4G.

If you do have Ethernet available near the gateway, then prefer it over WiFi or 3G/4G. This is because having an additional radio signal inside the enclosure will cause noise. The software can handle the noisy environment, so it's not a big issue, but the less noisy, the better. You can combine this choice with Power-over-Ethernet to minimize the cabling going all the way up to the gateway.

On the other hand, if you choose WiFi instead of Ethernet, then try to use a dongle with external antenna and move the antenna outside the enclosure to have less noise inside the box.

## Putting it all together

And now comes the fun part!

First, let's prepare the SD card so that we can insert it on the RPi and be ready to boot:

* Download [Raspbian Stretch Lite](https://www.raspberrypi.org/downloads/)
* Follow the [installation instructions](https://www.raspberrypi.org/documentation/installation/installing-images/README.md) to create the SD card
* Create a new empty file named `ssh` (without extension) onto the `boot` partition of the SD card. This enables ssh on the RPi upon startup.

Some things won't be easily accessible once we mount the boards, so better connect them before hand:

* Install the SD card in the RPi
* Connect the WiFi dongle to RPi
* Connect ethernet cable to RPi
* Connect the pigtail to iC880a

The stage is set! We can start mounting our gateway:

* Drill the mount holes for both boards on the mounting plate
* Mount both boards on the mounting plate (add spacers between board and mounting plate for ventilation)
* Mount the mounting plate in the enclosure
* Install the antenna (**WARNING**: never power up without the antenna!)
* Connect the jumper wires between the two boards using the following table:

|iC880a pin|Description|RPi physical pin|
|----------|-----------|----------------|
|21|Supply 5V|2|
|22|GND|6|
|13|Reset|22|
|14|SPI CLK|23|
|15|MISO|21|
|16|MOSI|19|
|17|NSS|24|

*alt=Pinout*
*alt=Mounted boards*

We're now ready to power up and start configuring our gateway!

## Setting up the software

* Plug the power supply of the RPi which will also power the concentrator board

* From a computer in the same LAN, `ssh` into the RPi using the default hostname:
  
  ````
    local $ ssh pi@raspberrypi.local
  ````

* Default password of a plain-vanilla RASPBIAN install for user `pi` is `raspberry`.

* Use `raspi-config` utility to **enable SPI** (`[5] Interfacing options -> P4 SPI`) and also expand the filesystem (`[7] Advanced options -> A1 Expand filesystem`):
  
  ````
    $ sudo raspi-config
  ````

* Reboot (it will ask on exit, but you can do it manually with `sudo reboot`)

* Configure locales and time zone:
  
  ````
    $ sudo dpkg-reconfigure locales
    $ sudo dpkg-reconfigure tzdata
  ````

* Make sure you have an updated installation and install `git`:
  
  ````
    $ sudo apt-get update
    $ sudo apt-get upgrade
    $ sudo apt-get install git
  ````

* Create new user for TTN and add it to sudoers
  
  ````
    $ sudo adduser ttn
    $ sudo adduser ttn sudo
  ````

* To prevent the system asking root password regularly, add TTN user in sudoers file
  
  ````
    $ sudo visudo
  ````

Add the line `ttn ALL=(ALL) NOPASSWD: ALL`

:warning: Beware this allows a connected console with the ttn user to issue any commands on your system, without any password control.
This step is completely optional and remains your decision.

* Logout and login as `ttn` and remove the default `pi` user
  
  ````
    $ sudo userdel -rf pi
  ````

* Configure the wifi credentials (check [here for additional details](https://www.raspberrypi.org/documentation/configuration/wireless/wireless-cli.md))
  
  ````
    $ sudo nano /etc/wpa_supplicant/wpa_supplicant.conf 
  ````

And add the following block at the end of the file, replacing SSID and password to match your network:

````
	network={
	    ssid="The_SSID_of_your_wifi"
	    psk="Your_wifi_password"
	}
````

* Clone [the installer](https://github.com/ttn-zh/ic880a-gateway/tree/spi) and start the installation
  
  ````
    $ git clone -b spi https://github.com/ttn-zh/ic880a-gateway.git ~/ic880a-gateway
    $ cd ~/ic880a-gateway
    $ sudo ./install.sh spi
  ````

* If you want to use the remote configuration option, please make sure you have created a JSON file named as your gateway EUI (e.g. `B827EBFFFE7B80CD.json`) in the [Gateway Remote Config repository](https://github.com/ttn-zh/gateway-remote-config).

* By default, the installer changes the hostname of your Raspeberry Pi to `ttn-gateway` (to prevent collisions with other Raspberry Pis in your network). You can override this in non-remote configuration mode.

* Unplug the Ethernet cable and close the enclosure

* **Big Success!** You should now have a running gateway in front of you!

*alt=Gateway ready*

## Checking connection to TTN

The best way to check if the gateway is working is registering it on the TTN Console.

* Login to thethingsnetwork.org `Console`
* Click on `Gateways -> register gateway`
* Enable checkbox `I'm using the legacy packet forwarder`
* Enter your Gateway EUI (if is printed on start and end of the installer)
* Enter any description 
* Select `Europe 868Mhz` as frequency plan
* Select the correct antenna placement according to your plans
* Confirm clicking `Register gateway`

Now you can see the status (which at this point should be `connected` if we did everything right) and traffic of your gateway!

## Wrapping up

Depending on the kind of enclosure you selected, you might still need to do one more thing: put the power cable through the weather-proof cable holes.

For this purpose, we will cut the micro USB end of the power supply, pass it through the hole, solder the wires to jumper wires, and finally connect 5v and GND to the Raspberry Pi:

|Micro USB|RPi physical pin|
|---------|----------------|
|Supply 5V|4|
|GND|9|

In the following image, I used a tiny, generic breakout board with pin header to connect the wires. That is not really required, it's only to keep the cabling neatly arranged inside the box.

*alt=Gateway powered via RPi GPIOs*

And now we're really done!

**Here's our final product!**
*https://github.com/ttn-zh/ic880a-gateway/blob/spi/images/closed-gateway.jpg*

Now go install the gateway in a nice location to give your neighborhood the joy of IoT!
