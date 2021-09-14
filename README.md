
#  Design and Simulation of 6T- SRAM cell design. 
## Table Of Contents :
 - [Overview](#Overview)
 - [SRAM Array and Peripheral circuits](#SRAM-Array-and-Peripheral-Circuits)
 - [Design of 6T cell](#Design-of-6T-Cell)
 - [DC Analysis 6T cell](#6T-SRAM-Stability)
     - [Hold SNM](#Hold-SNM)
     - [Read SNM](#Read-SNM)
     - [Write SNM](#Write-SNM)
 - [SRAM Timing  Analysis](#SRAM-Timing-Analysis)
 - [Timing Analysis with Sense Amplifier](#Timing-Analysis-with-Sense-Amplifier)
 - [Timing Analysis with Write Driver](#Timing-Analysis-with-Write-Driver)
 - [Acknowledgments](#Acknowledgements)
 - [Contact Information](#Contact-Information)
 
---
## Overview
This project mainly focuses on the design and simulation of 6T SRAM cell.

 Specifications:
 - Memory size - 1K * 32 bit
 - Supply Voltage - 5V
 - Technology - 0.5um SCMOS Technology



---
## SRAM Array and Peripheral Circuits

<p align="center">
  <img width="700" height="500" src="https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/block_diagram_new2.png">
</p>


At a very basic level SRAM Architecture consists of Bit Cell Array, Precharge circuit, Sense amplifier, Column Decoder, Write Driver, Wordline Driver and Row Decoder. The Row and Column addresses will be feed into the Row and Column Decoders respectively. Then according to the address feed, one of the Wordline and one of the Bitline will get selected, means one of the 6T cell in the Bit Cell Array will get selected. There after according to the signal in the Read Enable (REN) and Write Enable (WEN) we can access data from the cell or feed data into the cell.


---
## Design of 6T Cell
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
Now to maintain the stored data and considering the design constraint we can say that **M1 should be stronger than M3**.

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
Now to modify the stored data and considering the design constraint we can say that **M3 should be stronger than M5**.
After solving the Id equation for M3 and M5 we get (Eq-2):
![Eq-2](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/images/Eq-2.jpeg)

For sizing data [click here](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/docs/6T_sizing.pdf).

---
## 6T SRAM Stability
The stability and writability of the cell is addressed by the:
 - Hold Margin
 - Read Margin
 - Write Margin
 
 which are determined by **Static Noise Margin (SNM)** of the cell in its various modes of operation (i.e. Hold, Read & Write).
 The SNM measures how much noise can be applied to the inputs of the two cross coupled inverters before a stable state is lost.
 It is the least noise voltage needed to change the cell state.
 
[SNM Reference paper ](https://github.com/gautam19499/6-T-SRAM-cell-design/blob/main/docs/SNM.pdf).

### Hold SNM

![schematic for HSNM](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/HSNM_new2.jpeg)

The above diagram contains the schematic and plot of the SRAM cell in Hold Mode.

Hold SNM is the side of the largest square nested inside the butterfly curve.

### Read SNM

![Schematic for RSNM](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/RSNM_new.jpeg)


The above diagram contains the schematic and plot of the SRAM cell in Read Mode. 

Read SNM is the side of the largest square nested inside the butterfly curve. 

Read SNM is smaller than the Hold SNM because low level is raised by the access transistors.

### Write SNM

![Schematic for WSNM](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/WSNM_new.jpeg)

The above diagram contains the schematic and plot of the SRAM cell in Write Mode. 
Write SNM is side of the square that can fit between two curves as shown above.

---
## SRAM Timing Analysis

![6T-cell with all parasitics](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/tran.jpeg)

The above circuit diagram consists of 6T-cell with all its parasitics and precharge circuit. Since the memory size is 1k * 32 bit  (i.e., 32000 cells), so there will be 128 number of wordlines and 256 columns.
Here for M12 and M13  m=255. 
For M10 and M11 m=127.



---
## Timing Analysis with Sense Amplifier

![sense_amplifier](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/tran_sense.jpeg)

The above diagram contains the schematic and plot of the SRAM cell with [sense amplifier circuit](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/sense_amp.jpeg). 

Sense Amplifier is a differential amplifier used to sense the voltage difference between the bit-lines of a memory cell while a read operation is performed. It is needed in the circuit because the 6T-cell as being small sized not able to drive the large load capacitance appearing at the bit lines.


---
## Timing Analysis with Write Driver

![Write Driver](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/tran_write.jpeg)


The above diagram contains the schematic and plot of the SRAM cell with sense amplifier and [write driver circuit](https://github.com/gautam19499/6T-SRAM_cell_design/blob/main/images/write_driver.jpeg).
The write drivers send the input data signals onto the bit-lines for a write operation.


---
## Acknowledgements

 -   Dr.Saroj Rout,Associate Professor,Silicon Institute Of Technology,Bhubaneswar
-   Mr.Santunu Sarangi,Assistant Professor,Silicon Institute Of Technology,Bhubaneswar

---
## Contact Information

 - Gautam Kumar, Design Engineer, [Sevya Multimedia Technologies Pvt. Ltd.](https://sevyamultimedia.com/)
 - gautamkumar99342@gmail.com



