
## **Cryptography Challenges**

### **colors**
- **Input**:
  ```
  MzAgMzEgMzAgMzAgMzAgMzAgMzEgMzEgMjAgMzAgMzEgMzAgMzEgMzEgMzAgMzAgMzEgMjAgMzAgMzEgMzAgMzAgMzAgMzAgMzEgMzAgMjAgMzAgMzEgMzAgMzAgMzEgMzEgMzEgMzEgMjAgMzAgMzEgMzAgMzEgMzAgMzAgMzEgMzAgMjAgMzAgMzEgMzAgMzAgMzAgMzEgMzEgMzEgMjAgMzAgMzEgMzEgMzEgMzEgMzAgMzEgMzEgMjAgMzAgMzEgMzEgMzEgMzAgMzEgMzAgMzAgMjAgMzAgMzEgMzAgMzEgMzAgMzAgMzEgMzAgMjAgMzAgMzAgMzEgMzEgMzAgMzAgMzAgMzAgMjAgMzAgMzEgMzEgMzAgMzEgMzAgMzEgMzAgMjAgMzAgMzEgMzEgMzAgMzAgMzAgMzAgMzEgMjAgMzAgMzEgMzEgMzAgMzEgMzEgMzEgMzAgMjAgMzAgMzEgMzEgMzEgMzAgMzAgMzEgMzEgMjAgMzAgMzEgMzAgMzEgMzEgMzEgMzEgMzEgMjAgMzAgMzEgMzEgMzAgMzEgMzEgMzAgMzAgMjAgMzAgMzEgMzEgMzAgMzEgMzEgMzEgMzEgMzAgMzE=
  ```
- **Solution**:
  - I used **CyberChef** to decode this cipher. The process began with Base64 decoding, followed by converting the result to hex, and finally to binary.
  - After following the appropriate steps in CyberChef, I obtained the flag:
    ```
    CYBORG{tR0jans_love_C4rdinal_@nd_G0ld}
    ```

---

### **decipherium**
- **Input**:
  ```
  TeSbILaTeSnTeNoISnTeCsCsDyICdTeIISnTeLaSbCdTeTeTeLaTeSbINoTeSbSbInICdTeBaSbSbISnIYbSbCdTeXeINoSbSbTeHoTeITeFmTeITeMdITeSbICsEr
  ```
- **Solution**:
  - Initially, I searched on **CyberChef** and **Dcode** for any straightforward results but found no hits.
  - After some consideration, I recognized that the entire string consisted of symbols from the periodic table, which led me to treat it as such.
  - I converted the string into atomic numbers based on the periodic table.
  
  The code to map the elements to atomic numbers was:
  ```python
  periodic_string = "TeSbILaTeSnTeNoISnTeCsCsDyICdTeIISnTeLaSbCdTeTeTeLaTeSbINoTeSbSbInICdTeBaSbSbISnIYbSbCdTeXeINoSbSbTeHoTeITeFmTeITeMdITeSbICsEr"
  
  element_to_atomic_number = {
      'Te': 52, 'Sb': 51, 'La': 57, 'Sn': 50, 'No': 102, 'I': 53, 'Cs': 55,
      'Dy': 66, 'Cd': 48, 'Ba': 56, 'Xe': 54, 'Ho': 67, 'Fm': 100, 'Md': 101,
      'Er': 68, 'Yb': 70, 'In': 49
  }
  
  atomic_numbers = []
  i = 0
  while i < len(periodic_string):
      if i + 1 < len(periodic_string):
          symbol = periodic_string[i:i + 2]  # Check for two-letter symbols
          if symbol in element_to_atomic_number:
              atomic_numbers.append(element_to_atomic_number[symbol])
              i += 2  
              continue

      symbol = periodic_string[i]
      if symbol in element_to_atomic_number:
          atomic_numbers.append(element_to_atomic_number[symbol])

      i += 1
  atomic_numbers_str = ' '.join(map(str, atomic_numbers))
  print(atomic_numbers_str)
  ```
  - After converting the atomic numbers to ASCII characters, I got a hex string:
    ```
    4359424f52477B50455249304449435f4331504833525F30465f334C454d454e54357D
    ```
  - Finally, I used **CyberChef** to decode the hex string and revealed the flag:
    ```
    CYBORG{PERI0DIC_C1PH3R_0F_3LEMENT5}
    ```

---

This solution demonstrates how cryptographic challenges can be tackled using both algorithmic techniques and practical tools like **CyberChef** for decoding ciphers, making it an informative example for those learning cryptography.
