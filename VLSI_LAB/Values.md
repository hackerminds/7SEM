# Inverter 

 - **PMOS Values**

|Width|Length  |
|--|--|
| 10 | 2 |
 - **NMOS Values**

|Width|Length  |
|--|--|
| 10 | 2 |

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
 - **PMOS Values**

|Width|Length  |
|--|--|
| 67 | 14 |
 - **NMOS Values**

|Width|Length  |
|--|--|
| 20 | 20 |

 - **Spice Code**

		Vdd Vdd 0 dc 5
		Vb Vb 0 dc 0.8
		Vin Vin 0 dc 2
		.dc Vin 0 5 0.01 
		Vin Vin 0 sin(4 1 1K 0 0 0 50)
		.tran 0 5m
		Vin Vin 0 ac sin(4 1 1K 0 0 0 50)
		.ac dec 100 100 10G
		.include C:\Electric\C5_models.txt
# Common Source Amplifier
 - **PMOS Values**

|Width|Length  |
|--|--|
| 14 | 84 |
 - **NMOS Values**

|Width|Length  |
|--|--|
| 67 | 4 |

 - **Spice Code**

		Vdd Vdd 0 dc 5
		**DC ANALYSIS
		Vin Vin 0 DC 5
		.dc Vin 0 5 0.1
		**
		Vin Vin 0 sin(0.9 0.005 1K 0 0 50)
		.tran 0 5m
		Vin Vin 0 ac sin(0.9 0.005 1K 0 0 50)
		.ac DEC 100 100 10G
		.include C:\Electric\C5_models.txt
# Operation Amplifier
 - **PMOS Values**

|Width|Length  |
|--|--|
| 10 | 2 |
 - **NMOS Values**

|Width|Length  |
|--|--|
| 10 | 2 |

 - **Spice Code**

		Vdd Vdd 0 DC 5
		*DC Analysis
		Vin Vin 0 DC 5
		.dc Vin 0 5 1m
		*Transient Analysis
		Vin Vin 0 PULSE(0 5 0 1n 1n .5m 1m)
		.tran 2m
		.include C:\Electric\C5_models.txt
# R2R Ladder
 - **PMOS Values**

|Width|Length  |
|--|--|
| 10 | 2 |
 - **NMOS Values**

|Width|Length  |
|--|--|
| 10 | 2 |

 - **Spice Code**

		Vdd Vdd 0 DC 5
		*DC Analysis
		Vin Vin 0 DC 5
		.dc Vin 0 5 1m
		*Transient Analysis
		Vin Vin 0 PULSE(0 5 0 1n 1n .5m 1m)
		.tran 2m
		.include C:\Electric\C5_models.txt
