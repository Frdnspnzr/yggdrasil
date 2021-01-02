# Yggdrasil Home Automation

[![Last commit](https://img.shields.io/github/last-commit/Friedenspanzer/yggdrasil?style=for-the-badge)](https://github.com/Friedenspanzer/yggdrasil/commits/master)
[![Commit activity](https://img.shields.io/github/commit-activity/y/Friedenspanzer/yggdrasil?style=for-the-badge)](https://github.com/Friedenspanzer/yggdrasil/commits/master)
[![Homeassistant version](https://img.shields.io/github/pipenv/locked/dependency-version/Friedenspanzer/yggdrasil/dev/homeassistant?style=for-the-badge)](https://www.home-assistant.io/blog/2020/07/22/release-113/)
[![Travis status](https://img.shields.io/travis/Friedenspanzer/yggdrasil?style=for-the-badge)](https://travis-ci.org/github/Friedenspanzer/yggdrasil)
[![GitHub issues](https://img.shields.io/github/issues/Friedenspanzer/yggdrasil?style=for-the-badge)](https://github.com/Friedenspanzer/yggdrasil/issues)
[![MIT License](https://img.shields.io/github/license/Friedenspanzer/yggdrasil?style=for-the-badge)](https://github.com/Friedenspanzer/yggdrasil/blob/master/LICENSE)

## Concept

The basic concept is to strongly discouple assessment of states from consequences.
To achieve that most rooms have a state that determine what's going on in there.
States can be things like "On" when somebody flipped the light on, "Occupied" when somebody is there or "Off" when nothing of those two did happen.

Sensors and events now feed into these states.
When the motion sensors detect motion we turn a room to "Occupied".
When somebody presses down on a switch we turn a room to "Dimmed".
Devices are only controlled through these states, not directly through sensors or real world events.
That way I can have as much inputs and outputs as I want without big lists that get exponentially harder to maintain as I add more devices and automations.

There are however some exceptions to this rule.
The light under the bed for example is directly controlled by the motion sensors.

## Devices

### Infrastructure

| Device | Quantity | Connectivity | Integration | Notes |
| -------| :------: | ------------ | ----------- | ----- |
| Raspberry Pi 4 32 GB | 1 | - | - | Cheap and easy to set up so this was the most straight-forward way to get into home automation. Installed the default image formerly known as Hass.io, now Home Assistant. It works for now so I don't see a reason to change things around. |
| Dresden Electronic Conbee II | 1 | USB | [deCONZ](https://www.home-assistant.io/integrations/deconz/) | My main way to connect ZigBee devices. Connected directly to the Raspberry and working with the deCONZ integration. This thing works great. It was very easy to install, getting new devices set up is a breeze and it has a very generous range. Just look at how often I wrote "deCONZ" as the integration for devices.
| FRITZ!Box 6490 Cable | 1 | LAN | [AVM FRITZ!Box](https://www.home-assistant.io/integrations/fritz/) | I had this anyway because I like to have advanced routers instead of the things your cable provider sends you. AVM offering smart home solutions with easy integration into Home Assistant is something I discovered later. I kind of don't like that I have to use an actual user for the FRITZ!Box to connect to it instead of, say, just an API token. I set it up to use a dedicated technical user with minimal rights to make the integration work.

### Lighting

| Device | Quantity | Connectivity | Integration | Notes |
| -------| :------: | ------------ | ----------- | ----- |
| Müller Licht Tint Bulbs | 3 | ZigBee | [deCONZ](https://www.home-assistant.io/integrations/deconz/) | Great, cheap, easy to use ZigBee light bulbs. I hear they are hard to get outside of Germany but here they are literally placed at the Aldi checkout between candy bars and cheap liquor. I must admit I have not tried *that* many light bulbs but these are so great I can't think of anything more expensive ones could do better.
| IKEA Trådfri Bulbs | 4 | ZigBee | [deCONZ](https://www.home-assistant.io/integrations/deconz/) | I get those because they are even cheaper than the Tint bulbs for non-colored bulbs. They are a bit finnicky to use with the Conbee but do a great job overall.
| IKEA Floalt | 1 | ZigBee | [deCONZ](https://www.home-assistant.io/integrations/deconz/) | Used as the main ceiling lamp in the kitchen (we have the biggest model). It was easy to install and is easy to extend with additional Floalts. Great range of color temperatures and brighter than I could ever ask for.
| OSRAM Smart+ ZigBee LED Strips | 1 | ZigBee | [deCONZ](https://www.home-assistant.io/integrations/deconz/) | I got these on sale and they are pretty nice actually. I'm currently using two sets stitched together to make a longer strip. |
| Gledopto RGB+CCT LED Controller | 1 | ZigBee | [deCONZ](https://www.home-assistant.io/integrations/deconz/) | Compared to the OSRAM strips this is bad. I'm using the controller with a cheap bulk LED strip so I don't now *why* this is bad but I have not heard good things about Gledopto so maybe it really is the controller. The LEDs take a hell of a long time to turn on and switch colors, the warmer whites are not nice to look at (I'm using a orangey red instead) and the light just goes out completely when going below 30% brightness. |

### Presence Detection

| Device | Quantity | Connectivity | Integration | Notes |
| -------| :------: | ------------ | ----------- | ----- |
| Aqara Human Motion Sensor | 8 | ZigBee | [deCONZ](https://www.home-assistant.io/integrations/deconz/) | These are pretty great. I order them exclusively from Hong Kong so they are also cheap. The motion and brightness detection work like a charm but the temperature sensors on all my devices register values slightly off. Best thing is how small and unobstrusive they are.
| IKEA Trådfri Motion Sensor | 3 | ZigBee | [deCONZ](https://www.home-assistant.io/integrations/deconz/) | With things like the Aqara motion sensor I get to choose between them beeing cheap or easily available. With the Trådfri motion sensors I can get a dozen in the next twenty minutes if I really want to. I can drop five of those in a single room and still not break the bank. For being cheap and easy to aquire they get a free pass of not being *that* great after all. They take a few seconds to trigger after walking past them and have a very long reset time to trigger again after they stopped detecting motion.

### Security

| Device | Quantity | Connectivity | Integration | Notes |
| -------| :------: | ------------ | ----------- | ----- |
| Aqara Door and Window Sensor | 2 | ZigBee | [deCONZ](https://www.home-assistant.io/integrations/deconz/) | I was surprised by how fast and reliable these were. I sometimes literally open and close the balcony door just to see the lights change in real time like a small child.

### Switches

| Device | Quantity | Connectivity | Integration | Notes |
| -------| :------: | ------------ | ----------- | ----- |
| IKEA Trådfri Remote Control | 5 | ZigBee | [deCONZ](https://www.home-assistant.io/integrations/deconz/) | They are nice. I like them. I'll plaster all the walls with them. |

### Outlets

| Device | Quantity | Connectivity | Integration | Notes |
| -------| :------: | ------------ | ----------- | ----- |
| FRITZ!DECT 200 | 3 | DECT | [AVM FRITZ!Box](https://www.home-assistant.io/integrations/fritz/) | Smart Plugs by AVM made to be used with a FRITZ!Box. They are very clunky and take up much more space than other plugs I've seen but they double down as easy to use temperature sensors for the AVM thermostats. As with the thermostats I don't like that these are pretty much useless without a FRITZ!Box because I have never seen DECT used anywhere else. But at the same time I hope my FRITZ!Box is around for at least a few years so that shouldn't be an issue.
| OSRAM Smart+ Plug | 4 | ZigBee | [deCONZ](https://www.home-assistant.io/integrations/deconz/) | Got them pretty cheap in a sale. I'd like them a bit less bulky but overall they're pretty nice even though they don't support output readings. One is solely used as a ZigBee range extension right now.

### Climate

| Device | Quantity | Connectivity | Integration | Notes |
| -------| :------: | ------------ | ----------- | ----- |
| FRITZ!DECT 301 | 3 | DECT | [AVM FRITZ!Box](https://www.home-assistant.io/integrations/fritz/) | Very easy to install and use and I'm a big fan of the screen. I can see the target temperature with a quick glance at all times. As with the Smart Plugs I kind of dislike the fact that those are DECT because it's not exactly a widespread standard for home automation. |

### Media

| Device | Quantity | Connectivity | Integration | Notes |
| -------| :------: | ------------ | ----------- | ----- |
| LG 55UJ6309 | 1 | LAN | [LG webOS Smart TV](https://www.home-assistant.io/integrations/webostv/) | The TV was older than my home automation ambitions so I was pleasently surprised to see how much I can actually do with it. Sadly the status does not properly update when using apps such as Netflix which seems to be a known and not easily fixable issue with the integration. |
| Sonos One SL | 2 | LAN | [Sonos](https://www.home-assistant.io/integrations/sonos/) | I've gone with Sonos because they are easy to use with Home Assistant. For me that was worth the slightly higher price compared to similiar products. I probably could have built Smart Speakers myself but pulling off small, nice looking and good sounding all at once seems pretty hard. I decided on the SL models for now because I do not feel emotionally ready to talk with Amazon just yet. |

## FAQ

### Why is this thing called Yggdrasil?

I just like having names for things and having a clear concept for names.
Everything in my local network is named after something from nordic mythology.
I find Yggdrasil fitting, being that thing that keeps all of existence kind of together.

There's one thing I want to make clear right here and now:
I'm not a right-wing asshole claiming nordic mythology AS mY HerITagE or whatever they call it.
I just think it's pretty cool.
Punch nazis.

### Don't you think you're going a bit overboard to solve simple problems?

Absolutely!
This thing is a hobby and I just *like* to build a lighting switch so complicated I [need a diagram](https://blog.frdnspnzr.de/2020/04/was-hat-zwei-daumen-und-einen-irrational-komplexen-lichtschalter-gebaut/) to understand it. I can't recommend using this as a template for a "It just works" style of solution.

### Why didn't you go with packages

I just don't see how they can be useful for me.
I tried converting my setup to packages but it kind of just turned the config files inside out: What's been a folder before has been a file and vice versa.
Nothing got easier to find or maintain, just different.
I still think it's a nice concept and I will totally use packages as soon as they make my life easier.

### Why don't you go with smart switches instead of light bulbs?

Great question I don't have great answers to!
I started with this thing when I lived in a flat where I couldn't change the switches around as I liked.
Now I could, but it still would be a hassle to make the switch (pun absolutely intended) without *great* pay-off.

I also like having an easy to use fallback when the complete home automation system burns down.
Smart bulbs are stupid bulbs when not connected after all.

### Did somebody really ask you any of these questions?

The going overboard question, yes.
Everything else, no.
But that's basically how all FAQs work.

I was asked if my living room is haunted when the lights turned on for no reason, though.