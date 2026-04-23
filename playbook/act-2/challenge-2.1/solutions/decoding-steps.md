# Challenge 2.1 Solution

## Decoding Steps

1. **Identify the cipher**: JSON segment specifies Vigenere cipher
2. **Derive the key**: JSON hint says "Alpha before Omega" → key is **ALPHA**
   - Alternative: CSV column 4 runes at prime positions, first letters → A,B,G,M,A (first 5 = ABGMA, doesn't work)
   - The direct hint is the correct path
3. **Decode the ciphertext**: Apply Vigenere decode with key ALPHA

Ciphertext: Tst zeczck frlvtene glstd xu thp pychtkl of eghnsqdymeo shta
Key: ALPHA
Plaintext: The second fragment rests in the archive of transformed data
