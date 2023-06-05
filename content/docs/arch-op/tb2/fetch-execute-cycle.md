---
title: "3. Fetch Execute Cycle"
weight: 1
# bookFlatSection: false
# bookToc: true
# bookHidden: false
# bookCollapseSection: false
# bookComments: false
# bookSearchExclude: false
---

# 3. Fetch Execute Cycle

[🔒 Recording](https://github.com/ryanbester/uni-resources/tree/main/arch-op/y1/tb2/3-fetch-execute-cycle)

![Top-Level View of a Computer](/img/arch-op/y1/computer-top-level.png)

Instruction processing consists of two steps: fetch and execute.

## Instruction Fetch and Execute

![Program Execution Example](/img/arch-op/y1/program-execution-example.png)

In this example: 

1. The PC contains 300, the address of the first instruction. The instruction is loaded into the IR, and the PC is incremented.
2. The first 4 bits in the IR indicate that the AC is to be loaded. The remaining 12 bits specifiy the address from which data are to be loaded.
3. The next isntruction is fetched from address 301, PC is incremented.
4. Old contents of AC and the contents of address 941 are added, and result stored in AC.
5. The next instruction is fetched from address 302, PC is incremented.
6. The contents of the AC are stored in address 941.
