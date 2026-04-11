# Understanding NX Through Exploitation: Why ret2win Stops Working

## 1. From ret2win to Its Limitations

Ret2win works in simple environments, but it does not work reliably in real systems where basic defenses are enabled.

One of the most fundamental protections is NX (No-eXecute), which prevents certain memory regions from being executed as code.

## 2. What NX Actually Does

NX (No-eXecute), also known as Data Execution Prevention (DEP), is a memory protection mechanism that prevents execution of code from non-executable regions such as the stack.

This means that even if an attacker successfully overwrites memory and injects shellcode, the CPU will refuse to execute it.

NX is typically enabled at compile time and enforced at runtime, and its effect can be observed through memory permissions.

## 3. Experiment: With and Without NX

To understand how NX affects exploitation, I prepared a simple vulnerable C program and observed its behavior under different configurations.

The goal is to compare what happens when execution from the stack is allowed versus when it is blocked.

This experiment highlights a key limitation of classic stack-based exploitation techniques.

Below is the test program:

<Screenshot of C program>
### Case 1: NX Disabled — Code Execution Succeeds
### Case 2: NX Enabled — Execution Blocked

## 4. Why the Attack Fails



## 5. What Comes Next: Bypassing NX

## 6. Key Insight

## 7. What I Learned
