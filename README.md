# ENFITNIX Battery Converter

Bike lights by Enfitnix use the quite common 18650 form factor for their batteries. However, they require a very specific protection PCB that exposes both poles of the battery in two concentric circles on one side.

It's kinda hard to get these batteries (at least in Europe -> over 30€ for a single [battery](https://de.grandado.com/products/enfitnix-navi800-fahrrad-licht-lg-3350mah-akku-integrierte-hohe-prazision-batterie)!!!), so this custom PCB offers the option of converting almost any 18650 battery into one that fits your bike light for a BOM cost of just around 1€.

## Order

Any non-basic part has an LCSC part number attached so you can directly upload the files from _/fab_ to JLCPCB and order the fully assembled PCBs.

## Limitations

The current design is parametrised as follows

```
OVP: 4.2V
UVP: 2.5V
OCC: 18A
OCD: 40A
```

Before use, please confirm your cell's voltage range aligns with these limits (i.e. max cell operating voltage > OVP and min cell operating voltage < UVP). 

This will **not** work for LFP based cells!

## Usage

I recommend using heat shrink and a plastic base for the PCB as you get it from e.g. [AliExpress](https://de.aliexpress.com/item/32855964562.html)

With that the process is quite simple:
1. Solder one nickel strip each to the pads marked with + and -
2. Thread nickel strips through plastic base
3. Spot weld respective strips to their corresponding terminal of the cell
4. Wrap it all up in heat shrink
