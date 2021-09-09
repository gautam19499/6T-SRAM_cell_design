
#  Design and Simulation of 6T- SRAM cell design. 
## Table Of Contents :
 - [Overview](#Overview)
 - [Design of 6T cell](#Design_of_6T_Cell)
 - [DC Analysis 6T cell](#DC_Analysis_of_6T_Cell)
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


![SRAM Block Diagram](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/block_diagram_new2.png)


This project mainly focuses on the design and simulation of 6T SRAM cell.
The total memory size for the design is 1K x 32 bit, and the technology used is 0.5um SCMOS Technology. 
Here according to the row and column address one of the wordline and one of the column will get selected, which will give access to one of the 6T cell in the respective column. For thid 6T cell we did the simulation for read, write operation, checked the noise margin in Hold, Read and Write states.

---
## Design_of_6T_Cell
6T cell consists of two back to back connected inverters and two access transistors. For the design of 6T cell first we need to understand the operation and behaviour of the 6 transistors involved in the design. 
 1. Read Operation
 2. Write Operation

### Read Operation:

![read_operation](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/read_operation-Page-1.jpg)

Assuming logic 0 is stored in the cell i.e, V1=0V & V2=5V.
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

![enter image description here](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/write_operation-Page-2.jpg)

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

For sizing data [click here](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/docs/6T_sizing.pdf).

---
## DC_Analysis_of_6T_Cell
The stability and writability of the cell is addressed by the:
 - Hold Margin
 - Read Margin
 - Write Margin
 
 which are determined by **Static Noise Margin (SNM)** of the cell in its various modes of operation (i.e. Hold, Read & Write).
 The SNM measures how much noise can be applied to the inputs of the two cross coupled inverters before a stable state is lost.
 It is the least noise voltage needed to change the cell state.
 
[SNM Reference paper ](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/docs/SNM.pdf).

### Hold_SNM

![schematic for HSNM](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/HSNM_new2.jpeg)


### Read_SNM

![Schematic for RSNM](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/Schematic_RSNM.jpeg)

The Schematic for determining Static Noise Margin in Read Mode.

![RSNM](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/images/RSNM.jpeg)

SNM curve for 6T in Read mode.

### Write_SNM

![Schematic for WSNM](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/Schematic_WSNM.jpeg)

The Schematic for determining Static Noise Margin in Write Mode.

![WSNM](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/images/WSNM.jpeg)

SNM curve for 6T in Write mode.

---
## Transient_Analysis

![6T-cell with all parasitics](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/6T-cell_parasitics_new.jpeg)

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



