Here’s a well-structured solution for your **Reversing** category on GitHub:

---

## **Reverse Engineering Challenges**

### **concoction**
- **Challenge**: An executable file (.exe) was provided, and the task involved reversing the code to obtain the flag. When executed, the program prompted for specific numbers.
- **Solution**:
  - I began by analyzing the executable in **Binary Ninja**, examining the code’s structure and conditions.
  - During my analysis, I found multiple `if` conditions scattered across the code, which were linked to the input prompts shown at runtime.
  - Tracing the code, I identified a section where the flag was constructed as a concatenation of several specific variables, each tied to the initial input prompts.
  - I noted a condition `rax_71 != 0` that pointed back to an earlier code segment. This part involved several variables, which aligned with the numbers prompted during execution.
  - Converting the hex values of the variables to integers and using "decompiler" as the answer for the final prompt allowed me to satisfy the conditions needed to reach the print flag function.
  - The final flag was revealed as:
    ```
    CYBORG{RECIPE=7914–111100–2310–51337–42154142–9111-decompiler}
    ```

---
