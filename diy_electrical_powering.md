# DIY Electric Power System

You'll find insightful resources about creating your own power system and produce your own electricity.

This will like trip toward electrical autonomy with various topics being discussed such as storage, production, delivery,

Each stage will try to reach a specific goal always more ambitious:
- powering ultra low consumption device: arduino, rapsberry pi
- power small electronic devices (tablet, external screen) up-to 18W using power bank
- build 12V power supply from custom battery pack and solar panels
- charge cordless battery tool (up to 24V)
- 100W devices powering using USB-C PD norm
- AC

## Must have equipment
Before starting, you'll need to get some indispensable tools to work properly and efficiently.

### measuring equipment and devices
- multimeter: for everything
- usb power measuring tool: check your current consumption/production
- usb PD trigger: take benefit of latest Power Delivery USB standard to power devices requiring up to 20V and 5A which means 100W!

### Misc materials
- connectors: Jack, XT60, wago
- wires

## Safety

### Common mistakes
Be careful about mistake, this happens much more often than we think, and will result in burning wire, 
smoke, damage on equipment/devices/cells and even more serious consequences depending on it.

This is really annoying seeing things broken due to small inattention.

Among my "favorites":
- short circuit: bad design, lack of connectors, tinkering
- wrong polarity: contrary to AC, DC cares about polarity and many devices aren't protected against it. 
So better be careful before plugin things such as car charger which suppose polarity to be correct. 
I allready burnt 2 small car charger.. fortunately this isn't big things but still annoying to stupidily brake devices€ 
- deep discharge: this happened me twice. Once with 18650 cell custom battery (which was even protected with BMS) 
and 4 Ah cordless battery tool. Both were connected to a car charger to power device on USB.
I was quite surprised when I saw my battery voltage droped because I would have thought the battery would be protected as well as
my custom battery through BMS but this was obviously not the case.
Li-ion hate deep discharge, you can drastically reduce lifetime of your batteries by letting them completetly discharge.
I was upset when it happened on a brand new 30€ 4AH battery and on my custom batteries...

As a conclusion protection has to be taken seriously.

### Advice
- use fuses
- use BMS to protect 18650 packs
- use safe connectors, not ones you made yourself 
- always think twice before doing something. Check polarities.
- use as much as possible as possible commercial batteries (powerbanks, cordless tool batteries) and not tinkered ones. 
Cost isn't so much higher when you think about all the additional things: descent case, secured battery welding, protection circuit, professional build
I saw this was really not worth the investment of time needed to secure battery. 
Some powerbank I bought were same price as buying corresponding 18650 cells, so why waste time to do something that will be far less safer?


## Storage

Storage is an important part of the system. You have different option. Here I'll talk mainly about li-ion based ones.

You have several choices:
- building your own pack based on 18650 cells which I do not recommand at least at the beginning given the poor benefit compared to commercial solutions and the risks involved.
- powerbanks: good for powering small devices up to 18W. Very cheap ( some time same price as custom build) and secured compared to other solutions
- cordless tool batteries: more powerful than powerbanks. Able to deliver important power able to power tools. 
I noticed it was arount twice the price as what I could do myself with 18650 cells but it is can be worth the investment given the build quality and security. 
Furthermore if you use cordless tools they will be useful.

At the beginning my advice is to opt for premade solution before trying to build yourself. 
In my case I started building my own pack before switching quickly toward pre-made batteries, due to unnattended recurrent issues.

