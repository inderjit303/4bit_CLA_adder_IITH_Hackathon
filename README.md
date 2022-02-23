# 4bit_CLA_IITH_Hackathon
This report is step-wise design and simulation guide for implementing 4-bit carry look-ahead (CLA) adder using CMOS mirror logic in 28nm PDK using Synopsy Custom Compiler tool.
# Abstract:
This report presents a transistor-level implementation of a 4-bit carry look-ahead (CLA) adder using CMOS mirror logic. CLA adder design overcomes the delay issue in 
conventional RCA adder by eliminating the cascading effect of the carry bits. The sum and carry terms are processed at once in the CLA adder. CMOS mirror logic results in reduced transistor count compared to Static CMOS logic. Further, it uses the same transistor topology for NMOS and PMOS networks which leads to a symmetric layout. Simulations are carried out in 28nm PDK using Synopsy Custom Compiler and PrimeSim tool. 
# Reference circuit details: 
Proposed 4-Bit Carry Look-Ahead Adder is implemented using CMOS Mirror Logic. CLA first calculates the values of generate Gi and propagate Pi terms [1]. Then, they are used to calculate carry bits 

Ci+1 = Gi + PiCi             ...for every bit i

This means every carry bit can be found from generate and propagate terms. Next, sum bits are evaluated using 

Si = Pi xor Ci               ...for every bit i

This avoids the need to ripple the carry bits serially down the chain [2]. Carry and sum terms are implemented using CMOS mirror logic, whereas generate and propagate terms are implemented using Static CMOS logic.
# Reference circuit Design:
## 1. Generate and Propagate circuit of 4 bit CLA adder:
![4_bit_CLA_reference_circuit_generate_propogate_circuit](https://user-images.githubusercontent.com/99788755/155375356-f33f86ed-de48-4c54-8fc0-4a05b6a2e078.jpg)
## 2. Carry circuit of 4 bit CLA adder:
![4_bit_CLA_reference_circuit_Carry_circuit](https://user-images.githubusercontent.com/99788755/155376043-11b716f8-78fb-4533-ab44-7f2f3ff8dd24.jpg)
## 3.  Sum circuit of 4 bit CLA adder:
![4_bit_CLA_reference_circuit_Sum_circuit](https://user-images.githubusercontent.com/99788755/155376689-c864cc61-00f6-4f49-b065-4de74ad08c48.jpg)
# Reference Circuit Waveforms:
![4_bit_CLA_waveforms](https://user-images.githubusercontent.com/99788755/155377136-407b194a-2aa5-4313-ab8c-9d99af45bfe2.jpg)
