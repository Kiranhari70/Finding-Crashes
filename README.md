# CSE 543 – Finding Crashes Assignment

## Overview

This README explains the methodology used to break different levels in the *Finding Crashes* assignment by identifying and exploiting memory corruption vulnerabilities. While specific input files like `lvl0.txt`, `lvl2.txt`, and `lvl3.txt` were used for testing, they serve as examples of techniques rather than final deliverables. Each level required reasoning about how a program handles input—either from source code or decompiled binary—and then crafting input that causes a crash or hijacks control flow.

---

## General Strategy for Crashing a Level

1. **Understand the Input Format:**  
   Determine what kind of input the program expects—strings, integers, structured input, etc. This can be inferred from the source code or decompiled binary.

2. **Identify Vulnerability Type:**  
   Common crash types include:
   - **Buffer Overflows**
   - **Integer Overflows**
   - **Improper Format Parsing**
   - **Out-of-Bounds Access**

3. **Craft Input to Trigger the Bug:**  
   Once the vulnerability is identified, design the input to exploit it. Use very large or malformed values, or overflow a buffer to corrupt memory.

4. **Verify the Crash:**  
   Use `/challenge/run input.txt` or `/challenge/verify.py` in the pwn.college environment to confirm the program crashes or prints "Great Job" and exits cleanly.

---

## Examples

### 🔹 **Buffer Overflow (Level 4 Example)**
- **Exploit Strategy:**  
  Use padding to fill the buffer, then overwrite the return address.
- **Sample Code:**
  ```python
  with open("exploit.txt", "wb") as f:
      f.write(b"A" * 56 + b"\x66\x11\x40\x00")
