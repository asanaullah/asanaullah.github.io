---
author: 
category: MemRe
layout: blogpost
article: Project Overview
summary: Overview of Project Mem-Re
---
Memory controllers for SDRAMs, proprietary and open source, have traditionally had a number of limitations that have affected their performance, functionality, reliability, portability and accessibility. 

Proprietary IP blocks only allow a limited number of parameters to be tuned. As a result, the controller is typically not application specific. To get something that is tuned to a particular application, we either build a custom controller from scratch, or build wrappers for the vendor IP block - neither of which is an efficient approach. Moreover, even when a use case is not application specific, such as system level research into memory controllers, we hit the same roadblocks since low level access to the data and control paths is typically not possible. Finally, there is the cost of these IP blocks. 

On the other hand, open source memory controllers have one or more of the following limitations: i) can be difficult to read and understand, ii) are built with a large number of source files and complex hierarchies that substantially increase any effort to modify and/or debug the design, iii) have only been tested in simulation, iv) lack one or more core features, v) have poor out of box performance and/or resource usage, vi) are not vendor agnostic, and vii) are accompanied with little or no documentation, making them difficult to use and/or modify.


The goal of Project Mem-Re is to develop HDL based SDRAM memory controllers that are, to the greatest extent possible, i) open source, ii) FPGA vendor agnostic, iii) simple to modify, and iv) able to easily close timing after controller modifications. This project aims to achieve this goal through:
1. Using as much basic HDL as possible. Anything that doesn't deal with clock generation or a high frequency DDR data path will likely be HDL code.

2. Providing loose circuit coupling, appropriate interfaces and compilation flags for facilitating users in replacing primitives in the default design with equivalent circuits.

3. Minimizing, but not completely eliminating, code reuse. Striking the right balance between redundancy and lines-of-code is important for ensuring a design is both readable and easy to modify - High code reuse can sometimes make modifications difficult since a change affects all instantiations of the circuit, and not just the target part of the controller.

4. Providing low level constraints for mapping designs to physical hardware, provided that these not only help reduce the effort of closing timing, but are also applicable, with little or no modifications, to most FPGA chips.



The design is likely to have some primitives, which are typically proprietary ASIC chips embedded within the FPGA fabric. Examples of these primitives include PLLs, SERDES units, DDR signalling, global clock buffers, phasers and tristate logic. These primitives are chip architecture specific, and can even differ across FPGA chips from the same vendor. Use of the primitives is important for a number of reasons such as:

1. High speed interfaces typically require the FPGA to operate at frequencies significantly higher than what the fabric can easily close timing for. While FPGA technologies have continued to improve and support faster internal clocks, so have the speeds of external interfaces since we consistently target higher performance to keep pace with growing requirements/constraints of workloads. As a result, this disparity between frequencies was, is and will likely continue to be a problem for FPGAs. By using ASICs embedded within the FPGA fabric, we can offload the high frequency data path to the dedicated circuit and close timing.

2. While HDL is a low level assembly-like language, it is still an abstraction of a physical circuit. And as with almost all abstractions, they trade off expressibility for programmability. As a result, there are certain circuits which cannot be effectively expressed within HDL; a shortcoming addressed through use of primitives.

3. Even if a circuit is expresable and can be built in a stable manner within the FPGA fabric, if the primitive is common enough across FPGAs, it is usually a good idea to provide the option of using either the primitive or its HDL equivalent. This is because the HDL equivalent would i) consume the already limited reconfigurable fabric (making it difficult to place and route designs), ii) unlikely achieve the same levels of performance, and iii) have a relatively higher energy cost.


Note: Project Mem-Re is part of Project Morpheus, which is an effort to build an open source reconfigurable hardware operating system (analogous to Linux in the software world).
