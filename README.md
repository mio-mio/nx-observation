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
![Screenshot of vulnerable C program](CScreenshot2026-04-13122219.png)
  
### 3.1 Static vs. Dynamic Observation

After compiling the program with and without NX, the binaries were named wnx and non-nx.

I first examined both binaries using the `checksec` tool.

In the non-nx binary, the NX status was reported as "NX unknown - GNU_STACK missing".

![Screenshot of With NX checksec result](gazou.png

![Screenshot of Without NX checksec result](gazou.png

Next, I inspected the runtime memory layout using `info proc mappings` in GDB. The stack is mapped without execute permissions (no "x" flag) when inspecting the file with NX.
![Screenshot of With NX](WNXScreenshot2026-04-12093809.png)

The stack is mapped as executable (with the "x" flag) when inspecting the file without NX.

![Screenshot of Without NX](NONNXScreenshot2026-04-13114032.png)


Although the static analysis reported the NX status as unknown, runtime inspection showed that the stack was mapped as executable.

This indicates that actual memory permissions are determined at runtime and may not always be accurately reflected by static analysis alone.


### 3.2 Attempt to Execute Code on the Stack

To observe how NX actually works, I attempted to execute code on the stack by redirecting control flow to a region of user-controlled data.

Although the instruction pointer was successfully redirected to the stack, the instruction at that location (in this case, a ret instruction) could not be executed.

The program immediately terminated with a segmentation fault, indicating that execution from the stack is prohibited.

In this environment, it was not possible to observe successful execution with NX disabled, which reflects the behavior of modern systems where such protections are consistently enforced.

![Screenshot of sigsegv](sigsegvScreenshot2026-04-13121806.png)


## 4. Why the Attack Fails



## 5. What Comes Next: Bypassing NX



## 6. Key Insight

## 7. What I Learned
