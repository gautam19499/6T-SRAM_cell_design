# 1K-x-32-BIT-SRAM-CELL-DESIGN
In modern day VLSI system design memories are the vital blocks and they need to be thoroughly investigated with respect to area, power and performance before the fabrication. SRAM cell is an important candidate in the design of memories and a significant amount of attention is being paid to its design due to the ever increasing demand in data handling. The objective of the paper is to design a minimal size of SRAM cell which contain Multi-Ported Bit-cell Array, Address Decoders, Word line driver, column multiplexer, Bitline Precharge, Sense Amplifier and write driver using MOSIS 0.35um (SCN4M_SUBM) technology. The Bit cell Array consists of 1032 number of 6T-SRAM cells which can store 1032 number of bits. Using this 0.4um SCMOS technology we have to create a net-list for the 6T-SRAM cell to do both read and write operation and simulate it using NGSPICE simulator. By doing DC-Analysis and Transient analysis we will get the operating point of the transistors in 6T-SRAM cell.Using the Magic software we have to generate the layout of the cell. To simulate the 1K 32BIT SRAM cell we are using OpenRAM compiler. OpenRAM is an award winning open-source Python framework to create the layout, net-lists, timing and power models, placement and routing models, and other views necessary to use SRAMs in ASIC design. OpenRAM supports integration in both commercial and open-source flows with the both predictive and fabricable technologies.
