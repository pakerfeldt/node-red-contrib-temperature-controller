# Temperature controller
A universal thermostat with both cooling and heating capabilities for Node-RED. Hook up temperature readings as input and connect output to whatever controls your cooler and/or heater.
This node was built as a substitute for STC-1000, commonly used for controlling temperature in a fermenter cabinet. Combine this node with hardware, e.g. Shelly Plus 2PM and Shelly Plus Addon and you have a connected thermostat that you can monitor and control remotely.

![image](https://github.com/user-attachments/assets/393fe62c-05c6-4a53-9a21-6f0703625a80) ![image](https://github.com/user-attachments/assets/83f0c3d3-df86-44b6-a69a-7ce42db737cc)

The following documentation can also be found under the help section of this node inside Node-RED.

---

A universal thermostat that can be used to alternately control a cooling unit and a heat source, for example, a refrigerator and a heating plate.

## Details
You should regularly send temperature measurements to this node's input, and it will instruct you on when to turn on/off your cooling and heating unit to reach the target temperature.

### Target temperature (°C)
This is your wanted temperature.

Decimals allowed.

Default value is `18`°C but you really need to define this yourself.

### Temperature difference (°C)
* Cooling is triggered when the temperature measurement is greater than or equal to your target temperature + temperature difference.
* Heating is triggered when the temperature measurement is less than or equal to your target temperature - temperature difference.

A lower value of the temperature difference means this thermostat reacts quicker but could also lead to more starts and stops.

Decimals allowed.

Default value is `2`°C.

### Compressor delay (minutes)
The node has built-in support for compressor protection. As soon as cooling is stopped, it will not allow cooling again until at least this delay has elapsed, to avoid damaging the compressor.
You can turn compressor protection of by setting this value to 0.

Default value is `3` minutes.

### Status object
The node will show its current state throught the status object. It will tell you when the thermostat is idling, heating, cooling or in a compressor delay state.
It also shows the most recent measurement received as well as the target temperature.

## Inputs
Please note that any override of properties does not automatically trigger a change in cooling/heating until next measurement is sent.

### payload
Give temperature measurements in the payload as a number.

### target
You may override the target temperature defined in the configuration of this node by passing in a new value in `msg.target`.
Value must be a number. See documentation above for more details.

### difference
You may override the temperature difference defined in the configuration of this node by passing in a new value in `msg.difference`.
Value must be a number. See documentation above for more details.

### compressor
You may override the compressor delay defined in the configuration of this node by passing in a new value in `msg.compressor`. 
Value must be a number. See documentation above for more details.

## Outputs
This node has two outputs for controlling your cooler and heater. Both outputs emits a boolean to determine if your appliance should be turned on (`true`) or turned off (`false`).
The first output represents the cooler, and the second output represents the heater. Messages are sent with topic `cooling-controller` and `heating-controller` respectively so you could merge
them in your flow and use topic to distinguish.
