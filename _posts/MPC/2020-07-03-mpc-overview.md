---
author: 
category: MPC
layout: blogpost
article: Project Overview
summary: Overview of the FPGA accelrated Multi Party Computation project
---

Multi Party Computation (MPC) has been actively researched for the past 40 years because it offers the ability to use data held by several entities for calculations without needing to provide all the data to a single entity, and trusting that any provided information is not used for anything but the calculation. This lower trust requirement, as well as the ability for specific MPC protocols to protect against different quantities of passive or active opponents, is useful for healthcare, education, finance, technology, and government work. MPC implementations, typically done in software, have demonstrated these different guarantees and shown their effectiveness.

Despite the promise of MPC, there exist a number of limitations for MPC which must be addressed before it becomes practically viable enough for widespread adoption. The most important one is a large performance gap that exists between unsecured operations and equivalent software MPC implementations; in most cases, using MPC adds too much overhead to the computation for it to be practically viable. Moreover, since MPC is typically considered communication bound, there has been little motivation to advance algorithms in order to improve the computation performance of operations; this (apparently) means that scaling up technology will not provide significant performance improvements once the communication bound has been reached. Finally, the complexity of the process results in a steep learning curve and large deployment overhead; the time and effort needed to do MPC effectively acts as a barrier to entry for developers.  

This project aims to address the above limitations of MPC through a three pronged approach:

1. Bridging the MPC-unsecured performance gap by using hardware accelerators, specifically FPGAs, to offload existing protocols. This goes beyond just implementing basic MPC circuits, and instead takes a first principles approach towards exploring how hardware (as well as the enabling infrastructure) is built, deployed, instrumented, and optimized in the context of MPC.

2. Improving protocols so that FPGA-MPC to the point where it becomes a co-design problem, i.e., where communication and computation are equally bound, so that performance improves in tandem with increases in both network and compute capability. This involves: i) identifying different approaches used to implement MPC in hardware, ii) identifying the benefits and limitations of limitations of these approaches, iii) mapping protocols to application contexts where they are best suited, and iv) improving the computational performance of protocols.

3. Facilitate the use of MPC in real-world scenarios by abstracting the complexities such as selecting protocols, adapting these protocols based on the target application context, implementing circuits, scaling these circuits based on available technology, and integrating the FPGA into the application software flow.
