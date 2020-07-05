---
author: 
category: Morpheus
layout: blogpost
article: Project Overview
summary: Overview of Project Morpheus
---
A hardware Operating System is FPGA logic that supports application execution on the FPGA, similar to the role played by software OSes running on CPUs. It is implemented on a dedicated part of the FPGA fabric, assigned during floorplanning, and linked to application logic during compilation. Since this linking takes into account the location and interfaces of the hardware OS, any changes to the OS may require a recompilation of all applications running on it. As a result, updates to the hardware OS should be infrequent with respect to application updates; this again is similar to the update frequency for OS vs applications in software. "Shell" and "Board Support Package (BSP)" are two common alternative names used for a hardware OS. 

Hardware OSes are responsible for supporting external interfaces (memory, host, network etc), partitioning device fabric between multiple entities, data flow management,  resource multiplexing, and hardware modifications. They also define a number of specifications such as APIs, protocols, bus widths, clock domains, FIFO depths etc. For elastic and shared FPGAs in particular, hardware OSes support simultaneous deployment of code from multiple independent users/tenants, as well as code from system administrators. System administrator logic in FPGAs enables implementation of important, often performance and security critical, services and functions. This includes crypto, firewalls/isolation, packet processing, control/management planes, event logs/counters, firmware attestation services etc. A hardware OS also enables modification of deployed logic in a number of forms with varying overhead, including i) hotfixes (run-time parameter updates that do not modify FPGA configuration memory), and ii) partial reconfiguration (modifications to a predefined region of the FPGA).

While there have been numerous efforts towards building hardware OSs, these efforts have typically been ad hoc. This results in a number of limitations, such as:

1. Limited Support:  Most designs only support the limited set of applications or infrastructure configurations that are of interest to the developer.

2. Incompatibility: Even if two hardware OSs share the same functionality and provide the same amount of resources to application logic, the application logic may still need to be recompiled. One binary may not be compatible for both OSs due to differences in APIs and floorplanning. In the worst case, this could require modifications to the source code which could require building a large number of wrappers that consume the already limited resources, especially if the application logic consists of IP blocks and cannot be directly modified

3. Development Overhead: A new hardware OS may need to be written for each application if the existing options are insufficient. While different building blocks for this OS may be available as vendor IP, understanding how the different IP blocks work and how they should be connected is still a challenge. As a result, the application developer has to spend a significant amount of time on building the OS, in addition to the time taken to build the actual application. 
  
4. Performance Overhead: If the application developer does not have sufficient expertise in the design and/or operation of a hardware OS component, it can have a negative impact on performance since the OS is in the critical path of virtually all data movement in and out of the application logic. Moreover, inefficiently designed OS components can use up more chip resources than what was actually needed, resulting in less resources being made available to the application itself, which in turn could also translate to lower performance. 


The goal of Project Morpheus is to build a framework to first formalize and generalize hardware OSs, and then automate the process of generating them for different functionality requirements. The project aims to achieve this goal through the following explorations: 

1. Generation of a taxonomy of the different infrastructure configurations in which FPGAs are deployed in the data center and the edge. While an exhaustive list is not possible, analysis of FPGA use cases and previous efforts in hardware OS design will help generate a partial hardware OS taxonomy that covers some of the most common methods of FPGA deployment. 

2. Identification and categorization of the different components of a hardware OS. This will help formalize what functionality should be supported in a hardware OS, what can be varied across different configurations, and how those changes can be made. 

3. Standardization of APIs to ensure application source code does not need to be modified if changes to the OS are made, and that the application is compatible with any OS running in any FPGA. 

4. Implementation of a library of high performance and open source components, such as interface controllers, reconfiguration controllers, schedulers, monitors etc. This will support modifications to components, which in turn will help minimize resource usage and optimize performance based on a particular configuration. Moreover, it will also ensure that the design is portable across different FPGA chips and vendors. 

5. Implementation of a hardware OS generator for automatically floor planning the target chip and stitching together different components from a hardware library based on provided specifications. 
