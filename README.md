# 4bit_CLA_adder_IITH_Hackathon
This repository presents step-wise design and simulation guide for implementing 4-bit carry look-ahead (CLA) adder using CMOS mirror logic in 28nm PDK using Synopsy Custom Compiler and Primesim Tool.
# Abstract:
This report presents a transistor-level implementation of a 4-bit carry look-ahead (CLA) adder using CMOS mirror logic. CLA adder design overcomes the delay issue in 
conventional RCA adder by eliminating the cascading effect of the carry bits. The sum and carry terms are processed at once in the CLA adder. CMOS mirror logic results in reduced transistor count compared to Static CMOS logic. Further, it uses the same transistor topology for NMOS and PMOS networks which leads to a symmetric layout. Simulations are carried out in 28nm PDK using Synopsy Custom Compiler and PrimeWave tool. 
# Reference circuit details: 
Proposed 4-Bit Carry Look-Ahead Adder is implemented using CMOS Mirror Logic. CLA first calculates the values of generate Gi and propagate Pi terms [1]. 

For every bit i,

Gi = AiBi               

Pi = Ai+Bi               

Then, they are used to calculate carry bits 

Ci+1 = Gi + PiCi              

This means every carry bit can be found from generate and propagate terms.

Next, sum bits are evaluated using 

Si = AiBiCi xor (Ci+1)_bar (Ai+Bi+Ci)       

This avoids the need to ripple the carry bits serially down the chain [2]. Carry and sum terms are implemented using CMOS mirror logic, whereas generate and propagate terms are implemented using Static CMOS logic.


The proposed circuit add two 4-bit binary numbers and generate a carry out bit if the sum exceeds 15

# Reference circuit Design:
## 1. Generate and Propagate circuit of 4 bit CLA adder:
![4_bit_CLA_reference_circuit_generate_propogate_circuit](https://user-images.githubusercontent.com/99788755/155375356-f33f86ed-de48-4c54-8fc0-4a05b6a2e078.jpg)
## 2. Carry circuit of 4 bit CLA adder:
![4_bit_CLA_reference_circuit_Carry_circuit](https://user-images.githubusercontent.com/99788755/155376043-11b716f8-78fb-4533-ab44-7f2f3ff8dd24.jpg)
## 3.  Sum circuit of 4 bit CLA adder:
![4_bit_CLA_reference_circuit_Sum_circuit](https://user-images.githubusercontent.com/99788755/155376689-c864cc61-00f6-4f49-b065-4de74ad08c48.jpg)
# Reference Circuit Waveforms:
![4_bit_CLA_waveforms](https://user-images.githubusercontent.com/99788755/155377136-407b194a-2aa5-4313-ab8c-9d99af45bfe2.jpg)


# Tools Used:
## 1. Synopsys Custom Compiler:
 The Synopsys Custom Compiler™ design environment is a modern solution for full-custom analog, custom digital, and mixed-signal IC design. As the heart of the Synopsys Custom Design Platform, Custom Compiler provides design entry, simulation management and analysis, and custom layout editing features. This tool was used to design the circuit on a transistor level.

## 2. Synopsys Primewave:
 PrimeWave™ Design Environment is a comprehensive and flexible environment for simulation setup and analysis of analog, RF, mixed-signal design, custom-digital and memory designs within the Synopsys Custom Design Platform. This tool helped in various types of simulations of the above designed circuit.

## 3. Synopsys 28nm PDK:
 The Synopsys 28nm Process Design Kit(PDK) was used in creation and simulation of the above designed circuit.

# Pre-Layout Schematics and Simulations:






# Simulations: 

## Transient analysis

1. After creating and saving the 4 bit CLA adder schematic testbench, go to 'Tools' and open 'Primewave' to start the simulation. 
2. In the Primewave select the 'model file' i.e the '28nm PDK's .lib file present in the HSPICE folder. 
3. After this click on the analyses and select the 'tran' (Transient) analysis in the analysis window and give the 'Start Time', 'Stop Time', and 'Time step' parameters and save it. 
4. In this design, start time is 0, stop time is 6ns and  time step is 0.5ns 
5. Then add the outputs which needs to be plotted by writing the expression which select the input and output nets/labels on the testbench schematic.
6. Next, from Simulation tab, click on Netlist and Run to view the input and output waveforms w.r.t time 


# References: 
[1] M. S. Hossain and F. Arifin, "A Proposed Design of Conventional 4-Bit Carry Look-Ahead Adder Improving Performance," 2020 Advanced Computing and Communication Technologies for High Performance Applications (ACCTHPA), 2020, pp. 89-93, doi:10.1109/ACCTHPA49271.2020.9213227.

[2] Uyemura, J., 2002. Introduction to VLSI circuits and systems. 1st ed. New York: Wiley
