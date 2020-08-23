# Configuring xiaomi wifi repeater 2 without MiHome

The goal is to setup a xiaomi wifi repeater 2 without resorting to the official Xiaomi MiHome app.

Xiaomi devices are nice and cheap which make them interesting for diy projects, 
but they lack openness, and are bound to xiaomi Mihome application.

Not only, original app isn't very well made in my opinion but it implies installing it on you phone, creating an account and sharing your data with xiaomi servers. Which for whoever cares about privacy isn't very desirable.

I did not find any tutorial yet on how to configure this device without MI Home, so I decided to write one.

# Tools

Fortunately some people did a great job reverse engineering xiaomi protocol.

I found 2 tools able to talk directly with xiaomi devices: 
- [miio](https://github.com/aholstenson/miio)
- [python-miio](https://github.com/rytilahti/python-miio/)

Although `python-miio` is supposed to support xiaomi wifi repeater, I could not manage to to configure my device with it.
Instead I had to use the other nodejs based library called `miio` which did the job flawlessly.

## miio

You can install `miio` directly from npm tool. Choose global installation to directly access the tool from your command line typing:

	npm i -g miio
  
Once done you should be able to call it directly. If not check path where node js libraries are installed globally to include it in your path.

## python-miio

I just mention installtion it in case you need it, but as mentionned before I couldn't manage to configure my device with it.

This time library is writen in python. You can follow their [doc](python-miio.readthedocs.io/) to install it.
I advice you to use virtual env which makes usage of python tool cleaner.

Once installed you should have `mirobo` and `miiocli` python tools available from command line.

# Steps 
## Getting device IP

First we need to discover and retrieve device IP.

You can now plug your device to power it and it should blink, showing it cannot connect to any network yet. 
Once configuration done the light will switch to a permanent blue.

From now on you'll need to switch your computer wifi to the device network appearing under `xiaomi_wifi_reapeater...`
(this also means you'll loose your internet connection if your were connected in Wifi)

Once connected to the device's own network, use the following command:
	
	miio discover --sync

to get device's IP and token which in my case was reported under IP address 10.10.10.1.

Although this step worked flawlessly on linux, for some reason, on windows I couldn't manage to discover any device..
either using `miio` or `python-miio` `mirobo` tool.

Nevertheless I could still manage to do the further steps with windows, using device's IP address retrieved with linux.

So if you're on windows and it doesn't work, you can try to skip this step and use 10.10.10.1 as device's IP for next steps.

You can check it it works, using:
  
	miio inspect 10.10.10.1

which should return something similar to: 

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

If the configuration went well, the led of the device should turn blue, and a new network should appear under the same name of the router with suffix _PLUS

You can connect to this new network with the same password as your router wifi network.

I hope this tutorial was helpul and hopefully saved you precious time configuring this repeater.
