# Understanding NX (No-execute) through gdb

## Overview
NX (No-execute) is a memory protection feature that prevents execution of code in certain memory regions such as the stack.

In this short experiment, I used gdb to observe how NX affects a simple buffer overflow attempt.


## Setup
- OS: Linux (WSL / Kali)
- Tool: gdb
- Target: simple vulnerable C program


## Experiment

I compiled a basic vulnerable program and attempted to execute injected shellcode from the stack.
