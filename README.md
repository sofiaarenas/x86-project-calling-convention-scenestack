# Scene Stack — Visualizing Calling Conventions

This project is a **visual simulation of how function calls work in a computer**.

Instead of just reading about it, you can:
* Push values
* Call functions
* Return from functions
* Watch how memory (the stack) changes

I used a **movie set analogy** to make it easier to understand.

---

## 🎥 The Analogy

Think of your program like filming a movie.

* A **function** = a scene
* The **call stack** = a stack of scenes
* Each **stack frame** = everything needed to film one scene
* **Arguments / variables** = props used in the scene
* The **stack** = backstage table holding props

---

## What happens when you press buttons

### ➕ Push

Adds a “prop” to the current scene.

In real life:

* This is like adding a variable or argument to the stack

---

### ➖ Pop

Removes the most recent prop.

In real life:

* Stacks are **Last-In-First-Out (LIFO)**
* The last thing added is the first thing removed

---

### 📞 Call 

Starts a new scene (function call)

Behind the scenes, this happens:

1. The program saves **where to come back to**
   → called the **return address**

2. It saves the current setup
   → called the **base pointer (RBP/EBP)**

3. A **new stack frame** is created for the new function

So the stack grows.

---

### 🔙 Return

Ends the current scene and goes back to the previous one.

What happens:

1. Current stack frame is removed
2. Old base pointer is restored
3. Program jumps back to the saved return address

So the stack shrinks.

---

## What is a Stack Frame?

A **stack frame** is just a section of memory for one function call.

It contains:

* Arguments
* Local variables
* Saved base pointer
* Return address

Each function gets its own frame.

---

## What is “RIP”?

You’ll see a label like:

```
RIP: scene_A
```

This represents the **instruction pointer**:

* It tells you **what function is currently running**

---

## 32-bit vs 64-bit 

This is where calling conventions come in.

### 32-bit (older style)

Everything goes on the stack.

So:

* All arguments = pushed onto stack
* Function reads them from memory

Think:

> “Put every prop on the table and grab them from there”

#### Downsides:

* Slower (memory access)
* More stack usage

---

### 64-bit (modern style)

First few arguments go into **registers** (CPU’s hands).

Typical registers:

* RCX
* RDX
* R8
* R9

Only extra arguments go on the stack.

Think:

> “Director holds the first few props in their hands, only uses the table if needed”

#### Benefits:

* Faster (registers are very fast)
* Less stack usage

---

## Who cleans the stack?

This is called a **calling convention**

Two common ones:

### cdecl

* Caller cleans up the stack

Think:

> “Producer cleans the set after filming”

---

### stdcall

* Callee (function) cleans the stack

Think:

> “Director cleans up before leaving”

---

## Why this matters

This is how:

* Programs run functions
* Memory is managed
* Bugs like stack overflows happen
* Reverse engineering works

This concept is used in:

* Compilers
* Operating systems
* Security (exploits use the stack!)

---

## Final takeaway

If you remember one thing, remember this:

> A function call is just adding a new layer to the stack, and returning is removing it.
