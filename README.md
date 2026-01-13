# Battery-SOC-thermal-Models
Electro thermal model of a single cell 18650 battery 

This repositary contains thermal model  of a 2RC single cell battery. This model exhibits thermal behaviour of the battery due to the effect of reversible and irreversible heat generated in a battery. The process employed in this model involves the following steps

1. Create a 2RC model of a battery
2. Add a ohmic power dissipation to the 2RC model
3. Add a entropic power dissipation block to the 2RC model
4. Add a thermal block to the model
5. Add a dashboard block to add inputs and verify outputs

## Pre requisites
1. Simulink
2. Simscape Electrical

## System
<img width="1537" height="648" alt="image" src="https://github.com/user-attachments/assets/51f4ebf0-6b6d-407b-9a69-25d9676edc4a" />

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
Nominal internal resistance of the cell = 50 mohms ( Rtotal): Rtotal = R0 + R1 + R2
Ohmic resistance = 50% of total resistance = 25 mohms
R1 (Electrochemical charge transfer resistance) = 8 mohms
R2 ( Diffusion polarization resistance ) = 17 mohms





