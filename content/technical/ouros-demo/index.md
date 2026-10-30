---
title: "Specialised Haskell Processor on FPGA"
date: 2026-10-30
---

*I follow Lennart Augustsson's approach when he was presenting [MicroHs](https://github.com/augustss/MicroHs) --- give the demo first.*

*This is a Haskell program running on a specialised processor, which is hosted on an FPGA and talks through UART port:*

![fig1](demo.gif)

*There is no software runtime or "kernel trap" underneath, everything is handled by the hardware processor.*

*A more detailed demo video can be found [here](https://youtu.be/cafTcH-DuZM).* *If you want to reproduce this demo, either by running it on your FPGA or using our simulator, see the [guidance](#guidance).*

## Introduction

My PhD study topic is about specialised hardware design for non-strict functional languages. This post talks about my recent work on adding IO into our Haskell processor and putting it on an FPGA, with a goal of convincing people that a Haskell processor is a cute idea.


## Architecture Overview

The processor is called **Ouros**.

Many design details, including representation of combinators, thread management (Ouros can do automatic multithreading!) and garbage collection, can be found in our paper[^1]. 

![fig2](full-arch.svg)

## Handling IO in Ouros

Adding IO allows the Ouros processor to become a standalone computer.

```haskell
type World = Int
newtype IO a = IO (World -> (a, World))

runIO :: IO a -> World -> (a, World)
runIO (IO f) = f

instance Monad IO where
  return a = IO (\w -> (a, w))

  (IO m) >>= k = IO (\w ->
    case m w of
      (a, w') -> runIO (k a) w')
```



## Some FPGA Implementation Results

The FPGA board I am using is [AUP-ZU3](https://www.realdigital.org/hardware/aup-zu3), which was kindly donated by people from AMD.

## Limitation

- **Limited primitives:** currently Ouros doesn't support `Float` or `Double`; its ALU also doesn't support division on `Int` yet. Apart from `Double`, the other two can be added without too much effort.
- **Missing Haskell features:** I am totally relying on the MicroHs frontend to handle Haskell source, and haven't done any serious testd to check what language features are missing --- my experience suggests that basic stuffs like ADT and type class can work (but I am not a decent Haskell programmer).
- **No memory hierarchy:** a heap memory of 8K 288-bit words and a code memory of 4K 288-bit words seems to fit on the AUP-ZU3 board. A Haskell program with 1-2k lines can likely be hosted in the code memory --- but a more serious deisgn to utilise the big off-chip memories for programs with bigger heap footprint and code size might need considerable engineering effort to build.
- **No interrupt in hardware:** We only have poll-based IO; how to properly add interrupt to the system can be an interesting question, but currently I don't have an answer to it.

## Guidance on Reproducing the Demo {#guidance}

There are several related repo for Ouros:
- A fork on MicroHs:  https://github.com/bathtub-01/MicroHs (go to branch `real-world`).
- Hardware implementation of Ouros: https://github.com/bathtub-01/ouros-chisel (go to branch `real-world`).
- A cycle-accurate simulator of Ouros: https://github.com/bathtub-01/ouros-simulator (go to branch `real-world`).

## Reference
[^1]: Y. Xie, C. Ramsay, R. Stewart and H. -W. Loidl. "Ouros: A Dataflow-Driven Processor for Lazy Functional Programming Languages." 2026 IEEE 37th International Conference on Application-specific Systems, Architectures and Processors (ASAP). doi: [10.1109/ASAP71856.2026.00023](https://doi.org/10.1109/ASAP71856.2026.00023).