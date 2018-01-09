# homebridge-rfoutlets-protocol

Homebridge plugin purpose-built for controlling 433MHz radio frequency outlets which can be purchased inexpensively. (i.e. [these](https://www.amazon.com/Etekcity-Wireless-Electrical-Household-Appliances/dp/B00DQELHBS "Etekcity Wireless Outlets")). Homebridge maintains state information, so you can always know if you left that lamp on.

This is a forg from homebridge-rfoutlets as it didn't feature different protocols. How ever there is no support for different GPIO pins anymore. I needed protocol 4 to get my [brennenstuhl RC-CE1-4001](https://www.brennenstuhl.com/en-DE/Comfort-Line-Remote-Control-Set-RC-CE1-4001)(same as LIDL Silvercrest RCR DP3 3711-A) working.

Homebridge-rfoutlets-protocol uses a compiled version of `codesend` from the [433Utils/RPi_utils](https://github.com/ninjablocks/433Utils) (by ninjablocks) which is based on [rc-switch](https://github.com/sui77/rc-switch/) (by sui77).

Tested on a Raspberry Zero W (armv6) Raspbian (Debian) Stretch and Node.js v8.9.1. This should work on most Raspberry Pi models, however YMMV. Possibly you need to compile `codesend` for your CPU architecture (using `make` and the [433Utils/RPi_utils](https://github.com/ninjablocks/433Utils)) and replace `.../node/lib/node_modules/homebridge-rfoutlets-protocol/codesend` with your self compiled version.

Supports *lights*, *switches*, *outlets* and *fans*

## Installation

- Install homebridge  
`sudo npm install -g homebridge`

- Install homebridge-rfoutlets-protocol
`sudo npm install -g homebridge-rfoutlets-protocol`

- Update your homebridge configuration (see `sample-config.json`)

## Notes

- The user which homebridge is run from does **not** have to be a *sudoer* as like in the original homebridge-rfoutlets
- The 433MHz transmitter must be connected to pin 0 (GPIO17, physical 11)
- A great guide on how to record RF signals and set up your Pi to transmit can be found [here](https://www.samkear.com/hardware/control-power-outlets-wirelessly-raspberry-pi "Pi 433Mhz Transmitter Guide"). Note: the web portion of the guide is not required
- A better but german guide is [here](https://tutorials-raspberrypi.de/raspberry-pi-funksteckdosen-433-mhz-steuern/)
- A more specific information on how to record RF signals can be found [here](https://github.com/sui77/rc-switch/issues/103). This was the most valuable hint to get my outlets working as they use protocol 4 and 5 but only 4 is important
- My german guide how to record the codes for Silvercrest/brennenstuhl outlets can be found [here](https://forum.pimatic.org/topic/3337/433-mhz-funksteckdosen-lidl-silvercrest-rcr-dp3-3711-a-brennenstuhl-mit-homeduino/19)

## Configuration

- `name`: Name of your device
- `type`: `Light`, `Switch`, `Outlet` or `Fan` (**required**, if  `Outlet` selected 'outlet in use' will always be 'No')
- `manufacturer`: manufacturer of the device plugged into the outlet (*optional*, defaults to *blank*)
- `model`: model of the device plugged into the outlet (*optional*, defaults to *blank*)
- `serial`: serial number of the device plugged into the outlet (*optional*, defaults to *blank*)
- `rf_on`: RF signal to turn the outlet on (**required**)
- `rf_off`: RF signal to turn the outlet off (**required**)
- `pulselength`: RF transmission pulse length (*optional*, defaults to 189)
- `protocol`: protocol for the transmitter (*optional*, defaults to 1)
- `pin`: can **NOT** be configured as in homebridge-rfoutlets, it's always 0

See `sample-config.json`
