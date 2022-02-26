# Design and Simulation of a 4-bit CLA adder using CMOS mirror logic
This repository presents step-wise design and simulation guide for implementing 4-bit carry look-ahead (CLA) adder using CMOS mirror logic in 28nm PDK using Synopsy Custom Compiler and Primesim Tool.

# Table of Contents: 
1. [Introduction](#introduction)
2. [Reference circuit details](#reference-circuit-details)
3. [Pre Layout Circuit Design](#pre-layout-circuit-design)
4. [Simulation Results](#simulation-results)
5. [Conclusion](#conclusion)
6. [Author](#author)
7. [Acknowledgements](#acknowledgements)
8. [References](#references)

# Introduction:
This repository presents a transistor-level implementation of a 4-bit carry look-ahead (CLA) adder using CMOS mirror logic. CLA adder design overcomes the delay issue in 
conventional RCA adder by eliminating the cascading effect of the carry bits. The sum and carry terms are processed at once in the CLA adder. CMOS mirror logic results in reduced transistor count compared to Static CMOS logic. Further, it uses the same transistor topology for NMOS and PMOS networks which leads to a symmetric layout. The design has been created on Synopsis [Custom Compiler ](https://www.synopsys.com/implementation-and-signoff/custom-design-platform/custom-compiler.html) software and simulated using [PrimeWave](https://www.synopsys.com/implementation-and-signoff/ams-simulation/primewave.html) environment.

# Reference circuit details: 


## Reference circuit Design:

<p align="left">
<img src="https://user-images.githubusercontent.com/99788755/155841865-4cd1c547-75fe-4bcf-a575-fd1c0024d506.png">
</p>

### 1. Generate and Propagate circuit of 4 bit CLA adder:
Fig 1 shows generate and propgate circuit blocks implemented using static CMOS logic. Generate circuit block emulates AND operation i.e Gi = AiBi, thus requiring 6x4= 24 transistors. Propagate circuit block emulates OR operation i.e Pi = Ai+Bi, thus requiring 6x4= 24 transistors. Note i goes from 0 to 3. 


<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155375356-f33f86ed-de48-4c54-8fc0-4a05b6a2e078.jpg">
</p>
<p align="center">
Fig 1. Generate and Propagate circuit
</p>
 
### 2. Carry circuit of 4 bit CLA adder:
Fig 2. shows carry circuit block implemented using CMOS mirror logic for 4 bit CLA adder. The carry circuit is implemented based on the following equation

Ci+1 = Gi + PiCi

This means every carry bit can be found from generate and propagate terms.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155376043-11b716f8-78fb-4533-ab44-7f2f3ff8dd24.jpg">
</p>
<p align="center">
Fig 2. Carry circuit
</p>

### 3.  Sum circuit of 4 bit CLA adder:
Fig 3. shows sum circuit block implemented using CMOS mirror logic for 4 bit CLA adder. The sum circuit is implemented based on the following equation

Si = GiCi + (Ci+1)bar (Pi+Ci)

This means every sum bit can be found from generate, propagate terms and carry terms. 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155376689-c864cc61-00f6-4f49-b065-4de74ad08c48.jpg">
</p>
<p align="center">
Fig 3. Sum circuit
</p>

## Reference Circuit Waveforms:
Fig 4. shows reference circuit waveforms which demonstrates the addition of two 4 bit binary numbers. The plots includes carry-in bit(C0), carry-out bit(C4), two 4 bit binary numbers (A0-A3 and B0-B3) and 4 bit sum bits (S0-S3). 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155377136-407b194a-2aa5-4313-ab8c-9d99af45bfe2.jpg">
</p>
<p align="center">
Fig 4. Reference circuit waveforms
</p>

# Pre-Layout Circuit Design: 

## Proposed Modular Design of 4 bit CLA adder using Synopsys Custom Compiler tool:
To implement 4 bit CLA adder using CMOS mirror logic, modular design apporach is adopted. Modular design approach is a design principle that subdivides a system into smaller parts called modules/blocks, which can be independently created, modified, replaced, or exchanged with other modules/blocks or reused in other systems.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155846434-2f61e09a-5dd9-43d3-8304-7ce4a8028f57.png">
</p>
<p align="center">
Fig 5. Proposed Modular design of 4 bit CLA adder
</p>

Proposed modular design shown in Fig 5. subdivides 4 bit CLA adder IP block in smaller circuit blocks, i.e carry circuit, sum circuit, generate circuit, and propagate circuit blocks. Further, generate circuit block is divided into AND circuit block and propagate circuit block is divided into OR circuit block. Fig. 6 shows proposed 4 bit CLAD adder design IP. 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155846835-cf319b46-a88a-4cf8-8d91-cc7ccbc78bc9.png">
</p> 
<p align="center">
Fig 6. 4 bit CLA adder IP
</p>

## AND2 circuit Schematic: 
We start our modular design approach by designing two input AND circuit block using static CMOS logic as shown in Fig. 7. First, an two input NAND gate is implemented using static CMOS design followed connecting a CMOS inverter to make it an AND2 circuit with two input pins In1 & In2, one output pin Out and supply pins VDD and VSS. The substrate/boby terminal of all NMOS transistors are connected to VSS and substrate/boby terminal of all PMOS transistors are connected to VDD.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155751142-81dd8d8a-763c-46be-b59d-cc604cf1114e.png">
</p> 
<p align="center">
Fig 7. AND2 circuit schematic 
</p>

## AND2 circuit symbol: 
Fig 8. shows AND2 circuit block symbol which is the requirement for the modular design. The AND2 circuit block clearly shows two input pins In1 & In2, one output pin Out and supply pins VDD and VSS.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155751191-6667ac3f-97a2-42bf-ab1d-221102150a2f.png">
</p> 
<p align="center">
Fig 8. AND2 circuit symbol 
</p>

## OR2 circuit Schematic:
![OR circuit schematic](https://user-images.githubusercontent.com/99788755/155751255-2febc6bd-85d6-4849-9353-0f51b6bf404c.png)

## OR2 circuit symbol:
![OR circuit symbol](https://user-images.githubusercontent.com/99788755/155751304-24691eca-c306-4407-9b44-9f327aee8c1a.png)


## Propagate circuit Schematic: 
![Propagate circuit schematic](https://user-images.githubusercontent.com/99788755/155748575-bc963bec-af7a-40e2-939e-6eea7e4c23d3.png)

## Propagate circuit Symbol: 
![Propagate circuit symbol](https://user-images.githubusercontent.com/99788755/155748620-b7292100-0fbb-4952-b5a2-7afe6166a9ae.png)


## Generate circuit Schematic:
![Generate circuit Schematic](https://user-images.githubusercontent.com/99788755/155747583-ca3f2362-9c70-4f7d-894d-f2b26cc10d84.png)

## Generate circuit Symbol:
![Generate circuit symbol](https://user-images.githubusercontent.com/99788755/155747630-9816041f-b89a-43d5-9266-a276b0ca8535.png)

## Carry 1 circuit Schematic: 
![Carry_1_circuit_schematic](https://user-images.githubusercontent.com/99788755/155743857-3bdb0ec0-1d3d-40a3-8099-0ecbbd3b91a4.png)

## Carry 1 circuit symbol:
![Carry_1_circuit_symbol](https://user-images.githubusercontent.com/99788755/155743913-338ba3a0-8cfd-4aa2-8317-ad67dc92f28c.png)

## Carry 2 circuit Schematic: 
![Carry_2_circuit_schematic](https://user-images.githubusercontent.com/99788755/155743985-c4f662d4-1fe3-403d-83b8-3a3d0eae7201.png)

## Carry 2 circuit symbol:
![Carry_2_circuit_symbol](https://user-images.githubusercontent.com/99788755/155744094-c65b6ef7-1f4f-42cc-918e-3101c7b0b279.png)

## Carry 3 circuit schematic:
![Carry_3_circuit_schematic](https://user-images.githubusercontent.com/99788755/155744165-af2013c4-6fdd-4ba0-a6d0-01e74142ffaf.png)

## Carry 3 circuit symbol:
![Carry_3_circuit_symbol](https://user-images.githubusercontent.com/99788755/155744230-84080e67-df73-4cbf-b816-b34bac05ca1a.png)

## Carry 4 circuit schematic:

![Carry_4_circuit_schematic](https://user-images.githubusercontent.com/99788755/155745409-677f496b-51dd-4fff-b1b2-afd6c67be62f.png)

## Carry 4 circuit symbol:
![Carry_4_circuit_symbol](https://user-images.githubusercontent.com/99788755/155745457-4d885b0e-e872-42c3-8531-5ac5c96dc68f.png)


## Sum circuit Schematic:
![Sum_circuit_schematic](https://user-images.githubusercontent.com/99788755/155740407-7775bf1e-116f-4afb-9e3d-9d771080c4a2.png)

## Sum circuit Symbol:
![Sum_circuit_symbol](https://user-images.githubusercontent.com/99788755/155740537-aa450801-15aa-4faf-af15-dd625e789964.png)

## 4 bit CLA adder Schematic:
![4_bit_CLA_adder_schematic](https://user-images.githubusercontent.com/99788755/155745365-f6fb3a18-5d39-4a5d-937b-1b7739b775e1.png)



## 4 bit CLA adder Symbol:
![4_bit_CLA_adder_symbol](https://user-images.githubusercontent.com/99788755/155745152-545eb361-e295-4ffb-a3af-eacaef5fbcc9.png)

## Testbench Set up: 

### 1. Input pulse Voltage Source definitions: 
![Parameters set for Voltage Source for Input C0](https://user-images.githubusercontent.com/99788755/155772780-779cf528-3641-4667-a70f-0fcc7b3c1cfe.png)

![input pulse definitions](https://user-images.githubusercontent.com/99788755/155772743-436913a4-7f7e-4601-a446-55e0f875de36.png)

### 2. Supply voltage definitions: 
![supply voltage definitions](https://user-images.githubusercontent.com/99788755/155772838-cbbe88bd-a0f4-4a6f-aac8-eb623ec3bb71.png)

### 3. Transient settings: 

![transient settings](https://user-images.githubusercontent.com/99788755/155772878-930dc8e3-ccc0-4728-8288-482ee9523611.png)

## 4 Bit CLA adder Testbench: 
![4_bit_CLA_adder_testbench](https://user-images.githubusercontent.com/99788755/155745282-eec4019b-3b30-46b3-84a8-7a3c10c3a816.png)

# Simulation Results: 

## Transient analysis:
1. After creating and saving the 4 bit CLA adder schematic testbench, go to 'Tools' and open 'Primewave' to start the simulation. 
2. In the Primewave select the 'model file' i.e the '28nm PDK's .lib file present in the HSPICE folder. 
3. After this click on the analyses and select the 'tran' (Transient) analysis in the analysis window and give the 'Start Time', 'Stop Time', and 'Time step' parameters and save it. 
4. In this design, start time is 0, stop time is 6ns and  time step is 0.5ns 
5. Then add the outputs which needs to be plotted by writing the expression which select the input and output nets/labels on the testbench schematic.
6. Next, from Simulation tab, click on Netlist and Run to view the input and output waveforms w.r.t time 

## Actual Waveforms: 
![Input_output transient waveforms](https://user-images.githubusercontent.com/99788755/155678368-cf9de85e-0627-4c42-9e8d-7cfa2dc6957a.png)
Fig : Addition of of two 4 bit binary numbers with carry in bit  
![Input_output transient waveforms 1](https://user-images.githubusercontent.com/99788755/155678611-b27b1184-7e91-48b5-b047-88d227e03e8a.png)
Fig : Expanded view of Addition of of two 4 bit binary numbers with carry in bit 

## Verification of binary addition from waveforms: 

The input-output waveforms showcases the addition of of two 4 bit binary numbers with carry in and carry out bits.

![4 bit binary addition process](https://user-images.githubusercontent.com/99788755/155765427-34a6630e-5bd2-456c-af0b-a355a709b83c.png)

![binary addition time 1](https://user-images.githubusercontent.com/99788755/155766852-681f6b51-3fdd-41c8-9a77-9a5d719cbe30.png)


![binary addition time 2](https://user-images.githubusercontent.com/99788755/155765480-63098648-c5fa-483f-acf4-18ded424e411.png)

![binary addition time 3](https://user-images.githubusercontent.com/99788755/155765490-ccfc6c31-928e-4db0-b695-8e669bc3e195.png)

# Conclusion:

# Author:
Inderjit Singh Dhanjal, Assistant Professor, K.J Somaiya College of Engineering, Mumbai

# Acknowledgements:
1. [Cloud Based Analog IC Design Hackathon](https://www.iith.ac.in/events/2022/02/15/Cloud-Based-Analog-IC-Design-Hackathon/)
2. [Synopsys India](https://www.synopsys.com/)
3. [Kunal Ghosh, Co-founder, VSD Corp. Pvt Ltd.](https://www.linkedin.com/in/kunal-ghosh-vlsisystemdesign-com-28084836?lipi=urn%3Ali%3Apage%3Ad_flagship3_profile_view_base_contact_details%3B0xcWjpLDThSEo6S9UPO9Tw%3D%3D)
4. Chinmay panda, IIT Hyderabad
5. Sameer Durgoji, NIT Karnataka
                                  
# References: 
[1] M. S. Hossain and F. Arifin, "A Proposed Design of Conventional 4-Bit Carry Look-Ahead Adder Improving Performance," 2020 Advanced Computing and Communication Technologies for High Performance Applications (ACCTHPA), 2020, pp. 89-93, doi: 10.1109/ACCTHPA49271.2020.9213227.

[2] Uyemura, J., 2002. Introduction to VLSI circuits and systems. 1st ed. New York: Wiley
