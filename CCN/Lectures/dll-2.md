# Types of Errors

1. **Single-bit Error:**
   - A single-bit error occurs when one bit of data changes. It can either change from `0` to `1` or from `1` to `0`.
   - **Example:** 
     - Original: `1101`
     - Error: `1001` (1st bit changed)

2. **Burst Error:**
   - A burst error happens when two or more bits in a sequence change at once.
   - **Example:** 
     - Original: `1101101`
     - Error: `1110101` (2nd and 4th bits changed)

---

# Redundancy and Coding Techniques

1. **Redundancy:**
   - Extra bits are added to the data for error detection or correction. These bits are added at the sender's side and removed at the receiver's side.
   - This extra data helps the receiver detect or correct errors during transmission.

2. **Coding Schemes:**
   - Two main types of coding schemes:
     - **Block Coding**: Divides data into fixed-size blocks.
     - **Convolutional Coding**: More complex, involves continuous transmission.

---

# Block Coding

1. **Block Coding Explanation:**
   - The message is divided into blocks. Each block contains `k` data bits and `r` redundant bits, giving a total length of `n = k + r`.
   - **Example:** If `k = 4` and `n = 5`, the total number of possible codewords is `2^5 = 32`, but only `2^4 = 16` datawords are used. The other 16 codewords are invalid.

2. **Error Detection in Block Coding:**
   - When the receiver gets a codeword, it checks if it's valid by comparing it with a list of valid codewords. If it's not valid, it's discarded.
   - **Example:**
     - Original dataword `01` is encoded as `011`.
     - If the receiver gets `011`, it's valid, and `01` is extracted.
     - If the receiver gets `111`, it's invalid and discarded.

---

# Hamming Distance

1. **Hamming Distance:**
   - Hamming distance measures the number of differing bits between two codewords.
   - **Example:** 
     - Codeword 1: `00000`
     - Codeword 2: `01101`
     - Hamming Distance = 3 (because 3 bits differ)

2. **Minimum Hamming Distance:**
   - It's the smallest Hamming distance between any two valid codewords in a set.
   - To detect up to `s` errors, the minimum Hamming distance should be `d_min = s + 1`.
   - **Example:** If `d_min = 4`, it can detect up to 3 errors.

---

# Parity Check Code

1. **Explanation:**
   - A parity bit is added to make the number of 1s in the codeword even or odd.
   - **Example:**
     - Dataword: `1011`
     - Parity bit added: `10111` (to make the number of 1s even)

2. **Error Detection:**
   - **Receiver's Role:** The receiver checks the parity. If the number of 1s is even (or odd, depending on the parity chosen), the code is correct. Otherwise, it's discarded.
   - **Example of Error Detection:**
     - If one bit is flipped during transmission, the syndrome (error check) will signal an error.

---

# Two-Dimensional Parity Check

1. **Explanation:**
   - Data is organized in a table (rows and columns) and parity checks are done for both rows and columns.
   - **Example:** 
     - 4 datawords of 7 bits each.
     - A parity check is done for each row and column.
   
2. **Error Detection:**
   - Can detect up to 3 errors in the table, but not all 4-bit errors.

---

# Cyclic Redundancy Check (CRC)

1. **Explanation:**
   - CRC is a type of cyclic code where, if a codeword is cyclically shifted (rotated), the result is still a valid codeword.
   - **Example:** 
     - Codeword `1011000`, if cyclically shifted left, becomes `0110001`.

2. **Error Detection:**
   - CRC is widely used in LANs and WANs for error detection.
