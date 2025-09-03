# Dorfstatus control panel (2025 edition)
The "Dorfstatus" is a virtual state in our Home Assistant, representing if the Hackspace is open to the public or not. The state is written to the public [Space API](https://spaceapi.io/), and can be seen in various locations around our main website, wiki, and chats.
Additionally, the panel controls the startup and shutdown sequences to turn many lights and power sockets around the space on or off sequentially when the first person arrives or the last person leaves. The sequences are just button triggers for scripts in Home Assistant.
You can read more about the Dorfstatus in German in [our wiki](https://wiki.chaosdorf.de/Dorfstatus).

## why do we want a new one?
The current setup utilizes an [Ikea E2201 Zigbee dimmer switch](https://www.zigbee2mqtt.io/devices/E2201.html) as a physical control interface. Short press to set the status, long press for startup and shutdown (you really don't want to press these accidentally during peak hours in the space).
In our experience, these switches are just not up to the task and break frequently, losing their "click" and, because of that, a good electrical connection. This means that sometimes the space doesn't properly switch to "closed" when the last person is leaving, or that stuff turns on again after turning off everything because the button bounces.
The Dorfstatus is represented by the color of the lights in the hallway. No one understands this. We wanna do it better. :3

## pics

(currently WIP. pics will be added later when we're actually building the thing)

## hardware
The base for the project is a Siemens industrial control unit case with 4 sockets, with the following components:

- solid red and green buttons with "O" and "I" labels for starting up and shutting down the hackspace
- transparent red and green buttons to read and set the Dorfstatus.
- LEDs for the latter to show the current status, or a failure state for the ESP

They'll be connected to an ESP32 for attaching everything to our Home Assistant, with ESPHome at its core.

A 4-button-panel eliminates the need for long- and short-press button combinations, simplifying the usage of setting the status vs starting up or shutting down the space. The status LEDs will show a clear and easily-understandable state. Because the buttons are recessed and industrial grade, they can't be pressed accidentally. The buttons are rated for ten million (!!) switching cycles. They'll probably outlast our civilization.

The LEDs are industrial-grade modules that attach to the back of the switches and need 24V AC or DC. We still need to figure out if we wanna step up from 5V to 24V, down from 24V to 5V, or if we even need the 24V rail at all (maybe the LEDs are bright enough at 5V? We'll see!). If we need 24V for the LEDs, we also need two relais or transistors to control them.
A BOM will follow.

## software
The ESP runs ESPHome. You can find the config in `/config`.
