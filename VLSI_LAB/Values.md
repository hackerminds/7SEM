# Inverter 

 - P**MOS Values**

|Width|Length  |
|--|--|
|  |  |
 - **NMOS Values**

|Width|Length  |
|--|--|
|  |  |

 - **Spice Code**

		Vdd Vdd 0 DC 5
		*DC Analysis
		Vin Vin 0 DC 5
		.dc Vin 0 5 1m
		*Transient Analysis
		Vin Vin 0 PULSE(0 5 0 1n 1n .5m 1m)
		.tran 2m
		.include C:\Electric\C5_models.txt

# Common Drain Amplifier
# Common Source Amplifier
# Operation Amplifier
# R2R Ladder
