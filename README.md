#  Design and Simulation of 6T- SRAM cell design. 
## Table Of Contents :
 - [Overview](#Overview)
 - [Block Diagram](#Block_Diagram)
 - [Sizing](#Sizing)
 - [DC Analysis](#DC_Analysis)
 - [SNM](#SNM)
     - [Hold SNM](#Hold_SNM)
     - [Read SNM](#Read_SNM)
     - [Write SNM](#Write_SNM)
 - [Transient Analysis](#Transient_Analysis)
 - [Sense Amplifier](#Sense_Amplifier)
 - [Write Driver](#Write_Driver)
 - [Acknowledgments](#Acknowledgements)
 - [Contact Information](#Contact_Information)
 
---
## Overview
This project mainly focuses on the design of 1K * 32 bit 6T-SRAM memory design.

Specifications:
 - Memory size - 1K * 32 bit
 - Supply Voltage - 5V
 - Technology - 0.5um SCMOS Technology
---
## Block_Diagram

![SRAM Block Diagram](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/SRAM%20Block%20Diagram2.jpg)

---
## Sizing
Typical MOS Parameters:
-   Vdd = 5V
-   Lmin = 0.4um
-   Wmin = 0.6um
-   Vtn = 0.49V (NMOS threshold voltage)
-   Vtp = -0.66V (PMOS threshold voltage)
-   un = 445 cm^2/Vs (NMOS mobility)
-   up = 151 cm^2/Vs (PMOS mobility)

A schematic diagram of a standard 6-T SRAM cell is given below:
![6-T SRAM cell](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/images/6-T%20SRAM%20cell.jpg)

### Read Operation:
Assuming logic 0 is stored in the cell i.e, V1=0V & V2=5V.
WL is connected to Vdd.
Transistor Region of Operation:

-   M1  Linear Region  
-   M2  Cutoff Region
-   M3  Saturation Region
-   M4  Cutoff Region
-   M5  Cutoff Region
-   M6  Linear Region

The data read operation should not destroy the stored information.

The key design issue for the data-read operation is to guarantee that the voltage V1, does not exceed the threshold voltage of M2 so that the transistor M2 remains turned off during the read phase, i.e., V1 ≤ Vtn.
Now to maintain the stored data and considering the design constraint we can say that M1 should be stronger than M3.

After solving the Id equation for M1 and M3 we get (Eq 1):
![Eq-1](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/images/Eq-1.jpeg)

### Write Operation:
Assuming logic 1 is stored in the cell i.e, V1=5V & V2=0.
WL is connected to Vdd.
BL = 0V & BLB = 5V. (Means we are trying to write logic 0 in the cell.)

Transistor Region of Operation:

-   M1  Cutoff Region
-   M2  Linear Region
-   M3  Saturation Region
-   M4  Saturation Region
-   M5  Linear Region
-   M6  Cutoff Region

The cell should allow modification of the stored information.
To change the stored information, i.e., to force V1 to 0 V, and V2 to Vdd, the
node voltage V1, must be reduced below  the threshold voltage of M2 so that M2 turns off first.
Now to modify the stored data and considering the design constraint we can say that M3 should be stronger than M5.
After solving the Id equation for M3 and M5 we get (Eq-2):
![Eq-2](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/images/Eq-2.jpeg)

Note: When circuit starts operating, and V1 node reaches to Vtn voltage then M3 will be in linear and M5 will be in saturation region.
Now using typical MOS parameters as given above and taking V1=Vtn=0.49V and L=0.4um (for all MOS).

From Eq -2 we get:

![Eq-3](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/images/Eq-3.jpeg)

From Eq - 1 we get:

![Eq-4](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/images/Eq-4.jpeg)

Taking **W₅ = 0.6um** (since from above analysis we get strength of **M1 > M3 > M5**).

Then **W₃ = 1um** and **W₁ = 3.9um**.

---
## DC_Analysis
Voltage Transfer Characteristic (VTC) of Inverter:

![Eq-4](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/images/VTC_inverter.jpeg)

Here the supply voltage = 5V.
And we get the switching threshold (Vth) of the inverter = 1.09V.

---
## SNM
The stability and writability of the cell is addressed by the:
 - Hold Margin
 - Read Margin
 - Write Margin
 
 which are determined by Static Noise Margin (SNM) of the cell in its various modes of operation (i.e. Hold, Read & Write).
 The SNM measures how much noise can be applied to the inputs of the two cross coupled inverters before a stable state is lost.
 It is the least noise voltage needed to change the cell state.
 
[SNM Reference paper ](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/docs/SNM.pdf).

### Hold_SNM

![HSNM](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/images/HSNM.jpeg)

### Read_SNM

![RSNM](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/images/RSNM.jpeg)

### Write_SNM

![WSNM](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/images/WSNM.jpeg)

---
## Transient_Analysis

![6T-cell with all parasitics](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/6T-cell_parasitics.jpeg)

The above circuit consists of 6T-cell with all its parasitics and precharge circuit. Since the memory size is 1k * 32 bit  (i.e., 32000 cells), so there will be 128 number of wordlines and 256 columns.
Here for M12 and M13  m=255. 
For M10 and M11 m=127.


![Transient simulation with all parasitics.](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/tran_with_parasitics.jpeg)   


---
## Sense_Amplifier

![sense_amplifier](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/sense_amp.jpeg)

It is a differential amplifier used to sense the voltage difference between the bit-lines of a memory cell while a read operation is performed. It is needed in the circuit because the 6T-cell as being small sized not able to drive the large load capacitance appearing at the bit lines.


![tran_sense_amp](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/tran_sense_amp.jpeg)


---
## Write_Driver

![Write Driver](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/write_driver.jpeg)


The write drivers send the input data signals onto the bit-lines for a write operation.


![Transient analysis with sense amplifier and write driver.](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/tran_write_driver.jpeg)


---
## Acknowledgements

 -   Dr.Saroj Rout,Associate Professor,Silicon Institute Of Technology,Bhubaneswar
-   Mr.Santunu Sarangi,Assistant Professor,Silicon Institute Of Technology,Bhubaneswar

---
## Contact_Information

 - Gautam Kumar, Design Engineer, [Sevya Multimedia Technologies Pvt. Ltd.](https://sevyamultimedia.com/)
 - gautamkumar99342@gmail.com



