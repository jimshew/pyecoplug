# ECO Plug Switches for Home Assistant

[![MIT license](http://img.shields.io/badge/license-MIT-brightgreen.svg)](http://opensource.org/licenses/MIT)

# UNSUPPORTED

NOTE: This integration is unsupported. I have modified it from the original to keep it going for my own
installation, but no guarantees the repo https://github.com/rsnodgrass/pyecoplug will continue to exist.
I may delete this at any time.

The Home Assistant EcoPlug support forum can be found here:
https://community.home-assistant.io/t/ecoplug-integration/83854/64


# Original from @philburr

While evaluating Home Assistant, I ran across this repository.
I was looking for support available for my existing devices to
determine the viability of moving from openHAB. One type of device
I have is Workchoice outlets (same as Woods/WiOn, KAB, etc.)
that I use with openHAB, but no offical addon exists. I currently use the 
homebridge-ecoplug npm package to control them.

When a search revealed this repository, I found no mention of it in
the Home Assistant Community. I did find some requests for support with
little response.  The primary method of use seemed to be firmware mods,
not an option I was interested in. I decided to test this with my evaluation 
system.  The author, philburr, had published the requirements
on PyPi, so all I had to do was determine the (undocumented) installation steps
and test.

I was successful in installing, testing and operating my plugs, 
but I did have to fix errors in the homeassistant support module. 
Discovery detected all devices on my network, and as I add devices via the
Eco Plug apk, they were discovered and included w/o addtional interaction.
Once the plugs are setup, the Eco Plug apk is no longer required.
Alexa/Google Assistant discovery and control using the homeassistant/hass.io
skills work.

Note: No support for the energy monitoring capability of selected outlets.

# Installation

### Installation with HACS

The easist solution for installing, and keeping up-to-date, this Home Assistant integration is to install using the [Home Assistant Community Store (HACS)](https://github.com/custom-components/hacs). Make sure you have installed [HACS](https://github.com/custom-components/hacs), then through the Store panel in Home Assistant, add the "Integration" repository: `gbealmer/pyecoplug`.

### Manual Home Assistant installation

1. Plugs must be setup on the same network as your homeassistant system via the Eco Plug apk.
2. Copy folder/files from custom_components/ecoplug to "your homeassistant dir"/custom_components/ecoplug
3. Edit your configuration.yaml and add the following lines

```yaml
switch:
   - platform: ecoplug
     scan_interval: 10
```  

4. Restart homeassistant. The requirements will be loaded successfully by homeassistant.
5. Plugs on the same network will be discovered and switches added in the ui.
6. If you have set up Alexa and/or Google Assistant integration, devices can be discovered
and controlled.
(tested with 4 Workchoice RC-032W Outlets)

Note: Updated to add scan_interval entry. Required to detect status when manual switch on/off occurs




## Original README from philburr

Python library interface to EcoPlug wifi outlet.

Until proper documentation...

    >>> from pyecoplug import *
    >>> plugs = {}
    >>> def add(s):
    ...     plugs[s.name] = s
    ... 
    >>> def remove(s):
    ...     del(plugs[s.name])
    ... 
    >>> e = EcoDiscovery(add, remove)
    >>> e.start()
    >>> plugs
    {'test': ('## EcoPlug ##', b'test')}
    >>> plugs['test'].is_on()
    False
    >>> plugs['test'].turn_on()
    >>> plugs['test'].is_on()
    True
    >>> plugs['test'].turn_off()
    >>> plugs['test'].is_on()
    False
    >>> plugs['test'].turn_on()
    >>> plugs['test'].turn_off()
    >>> e.stop()
