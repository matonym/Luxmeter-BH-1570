# Luxmeter-BH-1570
A simple Luxmeter using BH-1570 using Tibbo EM2000 (I2C)
### Introduction
A simple I2C example using the BH-1750 Luxmeter

It has only been tested on the EM2000 but there's no reason it shouldn't work on other devices.

### Usage example

Add the BH1750.tbs and BH1750.tbh to your project
Include BH1750.tbh in your global.tbh

```
'DEFINES-------------------------------------------------------------

'INCLUDES------------------------------------------------------------

include "BH1750.tbh"

'DECLARATIONS--------------------------------------------------------

```

In the on_sys_init() system event, initialize the BH1750 "object"
```
sub on_sys_init()
  ...
  BH1750_Init(0, PL_IO_NUM_43, PL_IO_NUM_42, AddrL)
  ...
end sub
```
In the above example it uses SSI channel 0, PL_IO_NUM_43 as Clock pin, PL_IO_NUM_42 as Data pin and the BH1750 address 0x23

Add the Powerup function and set a mode
```
sub on_sys_init()
  ...
  BH1750_Init(0, PL_IO_NUM_43, PL_IO_NUM_42, AddrL)
  BH1750_Powerup()
  BH1750_SetMode(ContHighRes)
  ...
end sub
```

In the on_sys_timer system event add

```
sub on_sys_timer()
  ...
  sys.debugprint("Light: "+str(BH1750_GetLux())+ " lx"+chr(10))
  ...
end sub
```
