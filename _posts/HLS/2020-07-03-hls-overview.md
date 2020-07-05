---
author: 
category: HLS
layout: blogpost
article: Project Overview
summary: Overview of the High Level Synthesis project 
---

Programmability is one of the biggest challenges for specialized hardware, faced by software and hardware developers alike. Writing code for high quality hardware using a Hardware Description Language (HDL) requires both time and expertise due to limited abstractions, akin to assembly languages in CPUs and GPUs.

High Level Synthesis (HLS) provides an alternative to HDL programming by enabling designs to be expressed with (familiar) high level languages, such as 'C', which is then compiled to HDL code. This is similar to the front-end of compilers for software languages, in that HLS compilers parse high level language code, generate IR code, and do a number of optimization passes on this IR code. Developers can guide the optimization passes by annotating the source code to indicate where, how and to what degree parallelism can be exploited.


Despite the advantages of HLS and the advances made in recent years in this field, we are still far from the same levels of productivity as with compilers for software languages. This is because of two major challenges.

The first challenge stems from the optimization passes done by HLS compilers, and is referred to as the Performance-Portability problem. In a nutshell, the Performance-Portability problem means it is possible to write high level language code that performs well for either FPGAs or CPUs/GPUs as long as we tailor the code to target a specific platform - in general so far, it is not possible to have high-level code which executes well on all platforms. This is because of the limitations of the semantics of high level languages. Even with annotations, it is not possible for HLS compilers to reliably derive sufficient information about the target circuit from CPU/GPU source code in an acceptable time frame. To achieve good results, the source code must be manually restructured to help the compiler detect design patterns that map well to hardware, i.e. losing portability to get performance. "Unified" languages and APIs for heterogeneous compute environments can help overcome the semantic limitations of traditional languages, but it may not  be practical to port over decades worth of existing code.


The second challenge deals with the HDL generation passes of HLS compiler, which are responsible for converting the compiler's internal IR format, typically a form of Single Static Assignment (SSA), to HDL code. These passes match code fragments to libraries of vendor IP blocks in order to construct HDL, an approach which has three major drawbacks:

1. To meet the required design space coverage for building arbitrary circuits, a large library of IP blocks is typically needed. Such libraries consume a substantial amount of CPU memory, have high-overhead non-trivial lookup operations, and provide limited opportunities for optimization since they are proprietary.

2. Vendor IP libraries tend to be chip specific, which means that the generated HDL code is no longer generic; rather, it is a chip specific low level abstraction of a circuit. Therefore a given design has to be recompiled for each unique target chip architecture separately.

3. Traditional HLS compilers translate entire functions (and even programs) directly into HDL, often simply by doing a "1-to-1" IR to HDL translation. They do not support more complex analysis techniques that can tap into a number of potential optimizations; optimizations which not only reduce the overhead of HLS compilation, but also the subsequent hardware generation steps. An example of this is breaking up a large kernel into smaller ones and individually considering them for acceleration. Since the complexity of P&R does not grow linearly, the reduction in circuit size will lead to drastically lower analysis requirements - to the point that it becomes feasible to leverage quite exhaustive searches for exploring solutions. Another example is mapping part of the kernel code which is not in the critical path (e.g. the control plane) to a softcore. This can drastically lower the amount of hardware that needs to be generated, further reducing the analysis requirements and hardware generation overhead.



In this project, we will explore the design of a HLS compiler that addresses both the challenges outlined above: i) how do we bridge the performance-portability gap? and ii) how and to what degree can we generate HDL code that is generic and compiles faster than traditional HLS generated HDL? Addressing (i) will enable us to compile designs to a single fat binary, capable of targeting any combination of the three common backends (CPU, GPU and FPGA). Addressing (ii) will enable HLS compilers to be both vendor/chip agnostic and have significantly lower turnaround times for the full hardware generation process- It will also enable HLS compilers to be compatible with most back-end compilers i.e.  Synthesis and Place & Route tools. 
