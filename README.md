Roland VH to Yamaha adapter
================

This KiCad project represents a simple adapter which allows you to connect Roland Virtual Hi-Hat controllers (like VH-11, VH-12, VH-13) to Yamaha drum modules (DTX series).

## Tested configurations:

|         |DTX Multi 12|DTX 400|DTX 500|DTX 700|DTX 900|
|---------|:----------:|:-----:|:-----:|:-----:|:-----:|
|**VH-11**|            |       |       |       |       |
|**VH-12**|            |       |       |       |       |
|**VH-13**|      OK    |       |       |       |       |

Note: I haven't produced a PCB which is inculded here yet. So I can't say if it is OK for production.

## Operation principles

This adapter emulates Yamaha HH65 Hi-hat controller. So it should probably work with every drum module that accepts HH65.

HH65 sequentially connects drum modules's input to the ground via the set of resistances depending on the pressure:

1. Pedal is depressed: module's input floats
2. Pressure level 1: 100k between ground and input
3. Pressure level 2: 100k + 47k in parallel
4. Pressure level 3: 100k + 47k + 10k in parallel
5. Pedal is fully pressed: input is shorted to ground

Drum module supplies power to the scheme via the TIP terminal. It appears that the supplied voltage varies depending on the module. Adapter should work with both +3.3V and +5V power levels.

## Tuning
Adapter was designed to be flexible. Four potentiometers RV1, RV2, RV3, RV4 adjust reference voltage levels which allows the comparator to gradually connect R3, R4, R5 and finally short the module's input to ground.

To tune the adapter one simply need to adjust the potentiometers so the voltage levels on a debug pins are like this: V5 > V4 > V3 > V2 > V1 > V5low. Where V5 is the voltage on the pin P5 when the hi-hat controller is fully depressed, and V5low is the voltage on P5 when the controller is fully pressed. Each interval (e.g. between V5 and V4, V4 and V3, etc.) should be roughly the same. In most cases this should be enough. 

It is possible to adjust reference voltages in a different proportions to get other response curves.

