# Battery-SOC-thermal-Models
Electro thermal model of a single cell 18650 battery 

This repositary contains lumped 1 node thermal model  of a 2RC single cell battery. This model exhibits thermal behaviour of the battery due to the effect of reversible and irreversible heat generated in a battery. The process employed in this model involves the following steps

1. Create a 2RC model of a battery
2. Add a ohmic power dissipation to the 2RC model
3. Add a entropic power dissipation block to the 2RC model
4. Add a thermal block to the model
5. Add a dashboard block to add inputs and verify outputs

## Pre requisites
1. Simulink
2. Simscape Electrical

## System
<img width="1159" height="391" alt="image" src="https://github.com/user-attachments/assets/43830e12-0260-4b0f-acb6-7403482fc3e9" />


## Need for thermal simulation 
The purpose of a thermal model is to predict, understand and control temperature behaviour of a physical system. A battery thermal model predicts heat generated inside the cell, which translates into temperature. A thermal model is used for
1. Safety
2. Performance of battery
3. Lifetime and aging prediction
4. Design of cooling system

## Working of the model
This project implements a lumped electro-thermal model of a lithium-ion battery cell using an equivalent RC electrical model coupled to a 1-node thermal network. Heat generation is calculated from ohmic losses (I2R) and SOC dependent
entropic heat (I T DU/DT), and injected into the thermal domain via a controlled heat source. The cell’s temperature evolution is governed by a thermal mass and thermal resistance referenced to ambient temperature.

## User interaction
The user of the model, can alter the SOC (State of charge) from 0 to 100%. SOC does not directly change temperature; it influences heat generation through the SOC-dependent entropic heat term (it du/dt). The overall temperature rise is dominated by ohmic heating (I²R) and therefore evolves slowly with SOC due to the battery’s thermal mass.

## Understanding the math ( Behind the scenes)
# Building the R-C parameters
## Design of R
Nominal internal resistance of the cell = 50 mohms ( Rtotal): Rtotal = R0 + R1 + R2
Ohmic resistance = 50% of total resistance = 25 mohms
R1 (Electrochemical charge transfer resistance) = 8 mohms
R2 ( Diffusion polarization resistance ) = 17 mohms
## Design of C
Assuming time constant for T1 (fast dynamics) and T2 (slow diffusion) 
T1 = 5s, T2 = 100S
Since T = RC, C1= T1/R1 = 5 / 8mohm = 625F
C2 = T2/R2 = 100/0.017 = 5880F
Choosing C1= 600F and C2 as 6000F
### Choosing load resistance, (Assumed nominal capacity of 2.6AH)
Design of load resistance depends on amount of current that needs to flow within the system. Current depends on the battery capacity.
Usually a good fit is 0.5 to 1C of the battery capacity. Since AH of battery is around 2.6AH, we choose a current (safe) of 0.5C which is 1.3A
Rl = VL/IL = 3.7V/1.3A = **2.8 ohms**

# Study of rate of rise of temperature
For a single Li-ion cell under nominal operation, the expected temperature rise above ambient is typically 2–5 °C, and should not exceed ~10 °C in steady state.
So assuming a discharge rate of 0.5C, ambient temperature of 25C, and at three different SOC levels, 0%, 50% and 90%, we will study rate of temperature rise.

Case 1: SOC=0 (Battery discharged)
When the state of charge (SOC) of a battery is zero, the entropic heat contribution essentially vanishes because there are no active electrochemical reactions occurring. Since electrode becomes more disordered (entropy increases) , the system releases heat, which is a exothermic reaction. DU/DT term remains negitive, which corresponds to an inverse proportionality between open circuit voltage (U) and temperature (T). We understand rate of change of temperature against time for a current. 

1. Ohmic heat generation, Q1= $$I^2$$ * Rtotal = $$(1.3)^2$$ * 0.05 = 85 mW
2. Entropic heat generation, Q2 = I*T*(DU/DT) = 1.3* 25 *(-0.0045) =  - 0.01482 
Total heat, Q= Q1+Q2 = **0.06887W**

To understand heat generation, we need to learn different components of a battery thermal model. 
The total heat generation (W) is injected into the thermal domain using a controlled heat flow source. The battery is represented thermally by a thermal mass which captures the cell’s heat storage capability. 

Thermal mass of the system = m * Cp, where m= mass of battery, and Cp is specific heat in J/kg-k. A high specific heat capacity implies, that the battery heats up slowly. For practical thermal management, a value around 900-1000 J/(kg·K) is a common starting point. Assuming a mass of 50 g,and a specific heat capacity of 1100 J/Kg-k, we obtain
Thermal mass = 0.05 kg * 1100 J/Kg-k = 55 J/K. This suggests that for every 55J of heat, temperature raises by 1K.
Temp rise = Q * Rth = 0.06887 *10K/W = 0.68 degreeC








