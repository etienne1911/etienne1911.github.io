# Configuring xiaomi wifi repeater 2 without MiHome

This tutorial is about setting up xiaomi wifi repeater 2 without resorting to the official Xiaomi MiHome app.

Xiaomi devices are nice and cheap which make them interesting for diy projects, 
but they lack openness, and are bound to xiaomi Mihome application.

Not only, original app isn't very well made in my opinion but it implies you install it on you phone and create an account which implies you share your data with xiaomi servers
which for whoever cares about privacy isn't desirable.

I did not find any tutorial yet on how to configure this device without MI Home, so I decided to write this tutorial.

# Tools

Fortunately some people did a great job reverse engineering xiaomi closed protocol.
I found 2 tools able to talk directly with xiaomi objects: 
- https://github.com/rytilahti/python-miio/
- https://github.com/aholstenson/miio

Although the first one, python-miio is supposed to support the xiaomi wifi repeater, I could not directly configure it using this tool.
On the contrary the other nodejs based library `miio` did the job very well.

## miio

You can install `miio` directly from npm tool. Choose global installation to directly access miio tool from your command line typing:

	npm i -g miio
  
Once done you can call directly call miio. If not check path where node js libraries are installed globally to include it in your path.

## python-miio

I just mention setup of this other tool in case you need it, but as I said before I couldn't manage to configure device using it.

This time library is writen in python. You can follow their doc to install it.
I advice you to use virtual env which makes usage of python tool cleaner.

Install python 3 + pip + pipenv.

# Steps 
## Getting device IP

First step will be to discover device and get its IP.

You'll need to plug your device to power it and it should blink, showing it cannot connect to any network yet. 
Once configuration done light will switch to always blue.

From now you'll need to switch your computer wifi to self device network which should appear under name xiaomi_wifi_reapeater...
(which means you'll also loose your internet connection if your were connected using Wifi)

Once connected to the device's own network, you can use the command:
	
	miio discover --sync

to get device's IP and token which in my case was reported under IP address 10.10.10.1.

For some reason this step worked flawlessly on linux, whereas on windows, I couldn't manage to discover device..
either using `miio` or `python-miio` `mirobo` tool.

Nevertheless I could still manage to do the further steps also on windows, using device's IP address retrieved with linux.

So if you're on windows and it doesn't work, you can try to skip this step and use 10.10.10.1 as device's IP for next steps.

You should see it it works, typing:
  
	miio inspect 10.10.10.1

which should return: 

	INFO  Attempting to inspect 10.10.10.1
	
	Device ID: 258406439
	Model info: xiaomi.repeater.v2
	Address: 10.10.10.1
	Token: <device_token> via auto-token
	Support: At least generic
	
	Type info: miio
	Capabilities:
	
	Firmware version: 2.0.35
	Hardware version: R02
	MCU firmware version: 1000
	
	WiFi:  () RSSI: 0
	WiFi firmware version: 1.0.0
	
	Remote access (Mi Home App): Maybe


# wifi router configuration

Initially your device isn't configured so unable to connect to your home wifi network. 
So we need to provide wifi connexion information so it can extend the range of your router

Optionnaly, if you installed python-miio, you can check current device configuration with:

	miiocli.exe wifirepeater --ip <device_IP> --token <device_token> info
	
replacing <device_IP> and <device_token> by the ones you obtained in previous step

which should return somthing similar to this, if your device has never been configured:

	Model: xiaomi.repeater.v2
	Hardware version: R02
	Firmware version: 2.0.35
	Network: {}
	AP: {'rssi': 0, 'ssid': '', 'bssid': '', 'rx': 0, 'tx': 0}


Now, device configuration is done by typing this command:

	$ miio configure 10.10.10.1 --ssid <router_ssid> --passwd <router_wifi_password>

replacing <router_ssid> by the SSID of the router you want to extend the range of, and the associated wifi password.


	INFO  Attempting to configure 10.10.10.1
	Updated wireless configuration

From now if the configuration worked well, the led of your device should turn blue, 
and you should see a new network appearing under the same name as your router with suffix _PLUS

You can now connect to this network with the same password as your router.

I hope this tutorial will be helpul and hopefully save you time.
