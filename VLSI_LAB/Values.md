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

 - Differential Amplifier	

PMOS
	 
| Width | Length |
|--|--|
| 47.5 | 3.33 |
|  |  |

NMOS
| Width | Length |
|--|--|
| 541 | 3.33 |
|  |  |
 - Inverter
 
 PMOS
 
| Width | Length |
|--|--|
|  17| 84 |

NMOS
| Width | Length |
|--|--|
| 67 | 7 |
 - **Spice Code**

		vdd vdd 0 dc 1.8
		vss vss 0 dc -1.8
		vinp vinp 0 dc 1.8
		.dc vinp -1.8 1.8 0.1
		vinp vinp 0 ac sin(0.7 0.5m 1k)
		vinn vinn 0 dc 0.7
		.tran 0 5m
		vinp vinp 0 ac sin(0.7 0.5m 1k)
		vinn vinn 0 dc 0.7
		.ac dec 100 100 10g
		.include C:\Electric\C5_models.txt
# R2R Ladder
 - **PMOS Values**
		
|Width|Length  |
|--|--|
| 17 | 1 |
| 51 | 1 |

  **NMOS Values**

|Width|Length  |
|--|--|
| 7 | 1 |
| 17 | 1 |

 - **Spice Code**

		vdd vdd 0 dc 5
		vss vss 0 dc -5
		v1 d0 gnd pulse(5 0 0 1n 1n 1m 2m)
		v2 d1 gnd pulse(5 0 0 1n 1n 2m 4m)
		v3 d2 gnd pulse(5 0 0 1n 1n 4m 8m)
		v4 d3 gnd pulse(5 0 0 1n 1n 8m 16m)
	    .tran 32m
	    .include C:\Electric\C5_models.txt
