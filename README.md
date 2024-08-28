A universal thermostat that can be used to alternately control a cooling unit and a heat source, for example, a refrigerator and a heating plate.

## Details
Regularly send temperature measurements to this node, and it will instruct you on when to turn on/off your cooling and heating unit to reach the target temperature.

### Target temperature (°C)
This is your wanted temperature.

Default value is `18`°C but you really need to define this yourself.

### Temperature difference (°C)
* Cooling is triggered when the temperature measurement is greater than or equal to your target temperature + temperature difference.
* Heating is triggered when the temperature measurement is less than or equal to your target temperature - temperature difference.

A lower value of the temperature difference means this thermostat reacts quicker but could also lead to more starts and stops.

Default value is `2`°C.

### Compressor delay (minutes)
The node has built-in support for compressor protection. As soon as cooling is stopped, it will not allow cooling again until at least this delay has elapsed, to avoid damaging the compressor.
You can turn compressor protection of by setting this value to 0.

Default value is `3` minutes.

### Status object
The node will show its current state throught the status object. It will tell you when the thermostat is idling, heating, cooling or in a compressor delay state.
It also shows the most recent measurement received as well as the target temperature.

## Inputs
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
The first output represents the cooler, and the second output represents the heater. Messages are sent with topic `cooler-controller` and `heater-controller` respectively so you could merge
them in your flow and use topic to distinguish.

