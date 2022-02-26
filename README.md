# Design and Simulation of a 4-bit CLA adder using CMOS mirror logic
This repository presents a step-wise design and simulation guide to implement a 4-bit carry look-ahead (CLA) adder using CMOS mirror logic in 28nm PDK using Synopsy Custom Compiler and Primesim Tool.

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
To implement a 4 bit CLA adder using CMOS mirror logic, modular design approach is adopted. Modular design approach is a design principle that subdivides a system into smaller parts called modules/blocks, which can be independently created, modified, replaced, or exchanged with other modules/blocks or reused in other systems.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155846434-2f61e09a-5dd9-43d3-8304-7ce4a8028f57.png">
</p>
<p align="center">
Fig 5. Proposed Modular design of 4 bit CLA adder
</p>

Proposed modular design shown in Fig 5. subdivides 4 bit CLA adder IP block in smaller circuit blocks, i.e carry circuit, sum circuit, generate circuit, and propagate circuit blocks. Further, generate circuit block is divided into AND circuit block and propagate circuit block is divided into OR circuit block. Fig. 6 shows proposed 4 bit CLA adder design IP. 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155846835-cf319b46-a88a-4cf8-8d91-cc7ccbc78bc9.png">
</p> 
<p align="center">
Fig 6. 4 bit CLA adder IP
</p>

## AND2 circuit Schematic: 
We start our modular design approach by designing two input AND circuit block using static CMOS logic as shown in Fig. 7. First, an two input NAND gate is implemented using static CMOS design which is followed connecting a CMOS inverter to make it an AND2 circuit with two input pins In1 & In2, one output pin Out and supply pins VDD and VSS. The substrate/boby terminal of all NMOS transistors are connected to VSS and substrate/boby terminal of all PMOS transistors are connected to VDD.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155751142-81dd8d8a-763c-46be-b59d-cc604cf1114e.png">
</p> 
<p align="center">
Fig 7. AND2 circuit schematic 
</p>

## AND2 circuit symbol: 
Fig 8. shows AND2 circuit block symbol named 'isd_and2' which is the requirement for the modular design. The AND2 circuit block consists of two input pins In1 & In2, one output pin Out and supply pins VDD and VSS.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155751191-6667ac3f-97a2-42bf-ab1d-221102150a2f.png">
</p> 
<p align="center">
Fig 8. AND2 circuit symbol 
</p>

## OR2 circuit Schematic:
Next, we design a two input OR circuit block using static CMOS logic as shown in Fig. 9. First, an two input NOR gate is implemented using static CMOS design which is followed connecting a CMOS inverter to make it an OR2 circuit with two input pins In1 & In2, one output pin Out and supply pins VDD and VSS. The substrate/boby terminal of all NMOS transistors are connected to VSS and substrate/boby terminal of all PMOS transistors are connected to VDD.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155751255-2febc6bd-85d6-4849-9353-0f51b6bf404c.png">
</p> 
<p align="center">
Fig 9. OR2 circuit schematic 
</p>

## OR2 circuit symbol:
Fig 10. shows OR2 circuit block symbol named 'isd_or2_gate'. The OR2 circuit block consists of two input pins In1 & In2, one output pin Out and supply pins VDD and VSS.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155751304-24691eca-c306-4407-9b44-9f327aee8c1a.png">
</p> 
<p align="center">
Fig 10. OR2 circuit symbol 
</p>

## Propagate circuit Schematic: 
Next, we design the propagate circuit schematic using static CMOS logic as shown in Fig. 11. The propagate block is implemented as per design equation Pi = Ai+Bi. Using OR2 circuit block named 'isd_or2_gate' with two input pins In1 & In2, one output pin Out and supply pins VDD and VSS, propagate terms P0, P1, P2 and P3 are implemented utilizing modular design. Propagate circuit schematic consists of 24 transistors.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155748575-bc963bec-af7a-40e2-939e-6eea7e4c23d3.png">
</p> 
<p align="center">
Fig 11. Propagate circuit Schematic 
</p>

## Propagate circuit Symbol: 
Fig 12. shows propagate circuit block symbol named 'isd_propagate_block'. It consists of eight input pins A0_pg to A3_pg, B0_pg to B3_pg, four output pins P0-P3 and supply pins Vdd and VSS.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155748620-b7292100-0fbb-4952-b5a2-7afe6166a9ae.png">
</p> 
<p align="center">
Fig 12. Propagate circuit Symbol
</p>

## Generate circuit Schematic:
Next, we design the generate circuit schematic using static CMOS logic as shown in Fig. 13. The generate block is implemented as per design equation Gi = AiBi. Using AND2 circuit block named 'isd_and2' with two input pins, one output pin and supply pins, generate terms G0, G1, G2 and G3 are implemented utilizing modular design. Generate circuit schematic consists of 24 transistors.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155747583-ca3f2362-9c70-4f7d-894d-f2b26cc10d84.png">
</p> 
<p align="center">
Fig 13. Generate circuit schematic
</p>

## Generate circuit Symbol:
Fig 14. shows generate circuit block symbol named 'isd_generate_block'. It consists of eight input pins A0_gen to A3_gen, B0_gen to B3_gen, four output pins G0-G3 and supply pins Vdd and VSS.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155747630-9816041f-b89a-43d5-9266-a276b0ca8535.png">
</p> 
<p align="center">
Fig 14. Generate circuit symbol
</p>

## Carry 1 circuit Schematic: 
Carry 1 circuit schematic using CMOS mirror logic is shown in Fig. 15. The circuit 1 block is implemented as per design equation C1 = G0 + P0C0. The substrate/boby terminal of all NMOS transistors are connected to vss and substrate/boby terminal of all PMOS transistors are connected to vdd. Carry 1 circuit schematic consists of 8 transistors. 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155743857-3bdb0ec0-1d3d-40a3-8099-0ecbbd3b91a4.png">
</p> 
<p align="center">
Fig 15. Carry 1 circuit schematic
</p>

## Carry 1 circuit symbol:
Fig 16. shows carry 1 circuit block symbol named 'isd_carry1_block'. It consists of three input pins C0, G0 & P0, two output pins C1 & C1bar and supply pins vdd & vss.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155743913-338ba3a0-8cfd-4aa2-8317-ad67dc92f28c.png">
</p> 
<p align="center">
Fig 16. Carry 1 circuit symbol
</p>

## Carry 2 circuit Schematic: 
Carry 2 circuit schematic using CMOS mirror logic is shown in Fig. 17. The circuit 2 block is implemented as per design equation C2 = G1 + P1(G0 + P0C0). The substrate/boby terminal of all NMOS transistors are connected to vss and substrate/boby terminal of all PMOS transistors are connected to vdd. Carry 2 circuit schematic consists of 12 transistors. 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155743985-c4f662d4-1fe3-403d-83b8-3a3d0eae7201.png">
</p> 
<p align="center">
Fig 17. Carry 2 circuit schematic
</p>

## Carry 2 circuit symbol:
Fig 18. shows carry 2 circuit block symbol named 'isd_carry2_block'. It consists of five input pins C0, P0, P1, G0 & G1, two output pins C2 & C2bar and supply pins vdd & vss.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155744094-c65b6ef7-1f4f-42cc-918e-3101c7b0b279.png">
</p> 
<p align="center">
Fig 18. Carry 2 circuit symbol
</p>

## Carry 3 circuit schematic:
Carry 3 circuit schematic using CMOS mirror logic is shown in Fig. 19. The circuit 3 block is implemented as per design equation C3 = G2 + P2(G1 + P1(G0 + P0C0)). The substrate/boby terminal of all NMOS transistors are connected to vss and substrate/boby terminal of all PMOS transistors are connected to vdd. Carry 3 circuit schematic consists of 16 transistors. 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155744165-af2013c4-6fdd-4ba0-a6d0-01e74142ffaf.png">
</p> 
<p align="center">
Fig 19. Carry 3 circuit schematic
</p>

## Carry 3 circuit symbol:
Fig 20. shows carry 3 circuit block symbol named 'isd_carry3_block'. It consists of seven input pins C0, P0, P1, P2, G0, G1 & G2, two output pins C3 & C3bar and supply pins vdd & vss.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155744230-84080e67-df73-4cbf-b816-b34bac05ca1a.png">
</p> 
<p align="center">
Fig 20. Carry 3 circuit symbol
</p>

## Carry 4 circuit schematic:
Carry 4 circuit schematic using CMOS mirror logic is shown in Fig. 21. The circuit 4 block is implemented as per design equation C4 = G3 + P3(G2 + P2(G1 + P1(G0 + P0C0))). The substrate/boby terminal of all NMOS transistors are connected to vss and substrate/boby terminal of all PMOS transistors are connected to vdd. Carry 4 circuit schematic consists of 20 transistors. 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155745409-677f496b-51dd-4fff-b1b2-afd6c67be62f.png">
</p> 
<p align="center">
Fig 21. Carry 4 circuit schematic
</p>

## Carry 4 circuit symbol:
Fig 22. shows carry 4 circuit block symbol named 'isd_carry4_block'. It consists of seven input pins C0, P0, P1, P2, P3,G0, G1, G2 & G3, two output pins C4 & C4bar and supply pins vdd & vss.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155745457-4d885b0e-e872-42c3-8531-5ac5c96dc68f.png">
</p> 
<p align="center">
Fig 22. Carry 4 circuit symbol
</p>

## Sum circuit Schematic:
Sum circuit schematic using CMOS mirror logic is shown in Fig. 23. The sum circuit block is implemented as per design equation Si = GiCi + (Ci+1)bar (Pi+Ci). The substrate/boby terminal of all NMOS transistors are connected to vss and substrate/boby terminal of all PMOS transistors are connected to vdd. Sum circuit schematic consists of 12 transistors. 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155740407-7775bf1e-116f-4afb-9e3d-9d771080c4a2.png">
</p> 
<p align="center">
Fig 23. Sum circuit symbol
</p>

## Sum circuit Symbol:
Fig 24. shows sum circuit block symbol named 'isd_sum_block'. It consists of four input pins Ci, Ci1, Gi, & Pi, one output pin Si and supply pins vdd & vss.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155740537-aa450801-15aa-4faf-af15-dd625e789964.png">
</p> 
<p align="center">
Fig 24. Sum circuit symbol
</p>

## 4 bit CLA adder Schematic:

Finally, integrating the various block together, we achieve final schematic of 4 bit CLA adder modular design as shown in Fig 25. All 8 inputs A0-A3 and B0-B3 are applied to generate and propagate blocks. The outputs from generate and propgate blocks are G0-G3 and P0-P3. 
With the help of propagate and generate terms, sum and carry bits are evaluated in a faster way. Four sum circuit blocks and carry 1 to carry 4 circuit blocks are interconnected together to achieve a 4 bit CLA adder. Total transistor count for the 4 bit CLA adder design is 152. 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155745365-f6fb3a18-5d39-4a5d-937b-1b7739b775e1.png">
</p> 
<p align="center">
Fig 25. 4 bit CLA adder schematic
</p>


## 4 bit CLA adder Symbol:
Fig 26. shows 4 bit CLA adder symbol named 'isd_final_circuit_test'. It consists of nine input pins C0, A0-A3, & B0-B3, five output pins C4, S0, S1, S2 & S3 and supply pins vdd & vss. This final 4 bit CLA adder IP is same as the proposed IP shown in Fig. 6. 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155745152-545eb361-e295-4ffb-a3af-eacaef5fbcc9.png">
</p> 
<p align="center">
Fig 26. 4 bit CLA adder symbol
</p>

## Testbench Set up: 
Finally, to test a 4 bit CLA adder operation, a testbench is created. Here, input pulse definition include parameters setting of the rise time, fall time, delay time, high and low voltage levels, pulse width and period as shown in Fig 27 & 28. 

### 1. Input pulse Voltage Source definitions: 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155772780-779cf528-3641-4667-a70f-0fcc7b3c1cfe.png">
</p> 
<p align="center">
Fig 27. Parameters set for Voltage Source for Input C0
</p>

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155772743-436913a4-7f7e-4601-a446-55e0f875de36.png">
</p> 
<p align="center">
Fig 28. Input pulse definitions 
</p>

### 2. Supply voltage definitions: 
In modular design, all the modules/blocks require a steady DC source, since a 28nm PDK Technology node of Synopsys was adopted, a 1.8V supply is considered for the design.

vdc = 1.8V 

vss = 0V 

## 4 Bit CLA adder Testbench: 
Fig. 29 shows the testbench set-up for the final 4-bit CLA adder block, with appropriate input pulses acting as inputs for the CLA adder, and supply voltages. Further steps after creation and executing testbench results are elaborated in simulation results.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155745282-eec4019b-3b30-46b3-84a8-7a3c10c3a816.png">
</p> 
<p align="center">
Fig 29. 4 bit CLA adder testbench
</p>

# Simulation Results: 

## Transient analysis:
1. After creating and saving the 4 bit CLA adder schematic testbench, go to 'Tools' and open 'Primewave' to start the simulation. 
2. In the Primewave select the 'model file' i.e the '28nm PDK's .lib file present in the HSPICE folder. 
3. After this click on the analyses and select the 'tran' (Transient) analysis in the analysis window and give the 'Start Time', 'Stop Time', and 'Time step' parameters and save it. 
4. In this design, start time is 0, stop time is 6ns and  time step is 0.5ns 
5. Then add the outputs which needs to be plotted by writing the expression which select the input and output nets/labels on the testbench schematic.
6. Next, from Simulation tab, click on Netlist and Run to view the input and output waveforms w.r.t time 

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155772878-930dc8e3-ccc0-4728-8288-482ee9523611.png">
</p> 
<p align="center">
Fig 30. Transient setting 
</p>

## Actual Waveforms: 
Fig. 31 shows the 4 bit CLA adder input and output waveforms. Among the inputs, C0 is carry in bit, A0-A3 is 4 bit binary number, B0-B3 is 4 bit binary number and among the outputs is S0-S3, a 4 bit Sum and C4 is carry out bit. Fig 32 shows expanded view of the 4 bit CLA adder input output waveforms.

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155856332-719a775e-305b-4a17-9f26-e8df451ef699.png">
</p> 
<p align="center">
Fig 31. 4 bit CLA adder input output waveforms 
</p>

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155678611-b27b1184-7e91-48b5-b047-88d227e03e8a.png">
</p> 
<p align="center">
Fig 32. Expanded view of 4 bit CLA adder input output waveforms 
</p>

## Verification of binary addition from waveforms: 
From the simulated input-output waveforms, the addition of two 4 bit binary numbers with carry in and carry out bits is verified. Fig. 33 shows the binary addition process of two 4 bit numbers. The proposed design adds two 4-bit binary numbers and generate a carry out bit if the sum exceeds 15 which clearly visible from timing waveforms shown in Fig. 34

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155765427-34a6630e-5bd2-456c-af0b-a355a709b83c.png">
</p> 
<p align="center">
Fig 33. Binary addition process of 4 bit numbers 
</p>

![binary addition time 1](https://user-images.githubusercontent.com/99788755/155766852-681f6b51-3fdd-41c8-9a77-9a5d719cbe30.png)

![binary addition time 2](https://user-images.githubusercontent.com/99788755/155765480-63098648-c5fa-483f-acf4-18ded424e411.png)

<p align="center">
<img src="https://user-images.githubusercontent.com/99788755/155765490-ccfc6c31-928e-4db0-b695-8e669bc3e195.png">
</p> 
<p align="center">
Fig 34. Binary addition of 4 bit numbers by time frame
</p>

# Conclusion:
1. The repository presents the design and simulation of 4 bit CLA adder using CMOS mirror logic on 28nm technology node of Synopsys.
2. Modular design adopted was successful and 4 bit binary addition is verified from output waveforms. The proposed circuit add two 4-bit binary numbers and generates a carry out bit if the sum exceeds 15
3. Adopting CMOS Mirror logic for 4 bit CLA adder have reduced the transistor count from 178 to 152 in comparison with static CMOS logic. 

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
