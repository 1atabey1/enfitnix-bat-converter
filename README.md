# ENFITNIX Battery Converter

**NOTE: The released boards (1.0.0 / 1.1.0) are not functional without workarounds: the CTR pin of the BMS IC is left floating, which the BQ298218 reads as an over-temperature fault. See [issues](https://github.com/1atabey1/enfitnix-bat-converter/issues) for more info. The design on `master` fixes this and routes the load current through the sense resistor so overcurrent/short-circuit protection actually works. It has not been ordered and tested yet.**

Bike lights by Enfitnix use the quite common 18650 form factor for their batteries. However, they require a very specific protection PCB that exposes both poles of the battery in two concentric circles on one side.

It's kinda hard to get these batteries (at least in Europe -> over 30€ for a single [battery](https://de.grandado.com/products/enfitnix-navi800-fahrrad-licht-lg-3350mah-akku-integrierte-hohe-prazision-batterie)!!!), so this custom PCB offers the option of converting almost any 18650 battery into one that fits your bike light for a BOM cost of just around 1€.

## Order

Any non-basic part has an LCSC part number attached so you can directly upload the files from the latest [release](https://github.com/1atabey1/enfitnix-bat-converter/releases) to JLCPCB and order the fully assembled PCBs.

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
5. **Activate the protection IC** by briefly applying a current-limited charger voltage (e.g. 5V from USB, or a bench supply set to ~4.5-5V) between the outer (-) and inner (+) ring

The last step is required. The BQ2982 powers up in SHUTDOWN mode when the cell is attached: both FETs stay off, the output reads 0V and the IC draws <0.1uA. It only switches the FETs on once it detects a charger, i.e. the pack voltage is >~0.7V above the cell voltage (datasheet SLUSCS3M, section 7.4.1.1). The same applies after an undervoltage shutdown. Charging the battery in the light may also wake it up, but that depends on whether the light's charger starts with 0V at the battery terminals.
