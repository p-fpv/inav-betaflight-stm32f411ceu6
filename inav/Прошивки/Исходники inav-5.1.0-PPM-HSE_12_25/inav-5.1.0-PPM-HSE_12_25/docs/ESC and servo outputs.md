# ESC and servo outputs

## ESC protocols

INAV support the following ESC protocols:

* "standard" PWM with 50-400Hz update rate
* OneShot125
* OneShot42
* Multishot
* Brushed motors
* DSHOT150, DSHOT300, DSHOT600

ESC protocol can be selected in Configurator. No special configuration is required.

Check ESC documentation of the list of protocols that it is supporting.

## Servo outputs

By default, INAV uses 50Hz servo update rate. If you want to increase it, make sure that servos support
higher update rates. Only high end digital servos are capable of handling 200Hz and above!

## Servo output mapping

Not all outputs on a flight controller can be used for servo outputs. It is a hardware thing. Always check flight controller documentation. 

While motors are usually ordered sequentially, here is no standard output layout for servos! Some boards might not be supporting servos in _Multirotor_ configuration at all!

## Modifying output mapping

INAV 5 allows the limited output type mapping by allowing to change the function of *ALL* outputs at the same time. It can be done with the `output_mode` CLI setting. Allowed values:

* `AUTO` assigns outputs according to the default mapping
* `SERVOS` assigns all outputs to servos
* `MOTORS` assigns all outputs to motors