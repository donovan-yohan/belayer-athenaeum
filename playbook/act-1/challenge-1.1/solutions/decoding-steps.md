# Challenge 1.1 Solution

## Decoding Steps

1. **Base64 decode** the main body to get the ROT13-encoded text
2. **ROT13 decode** to get the substitution cipher text
3. **Identify the substitution cipher key**: The "noise" metadata contains coordinate pairs (a,b) where b = a + 7. This reveals a Caesar cipher with shift +7.
4. **Caesar shift -7** (or +19) to recover the plaintext

## Plaintext

The Codex Machina awaits restoration. Five fragments lie scattered across the realms. Seek the Gateway at coordinates seven-three-nine. The path forward requires unity of mind and purpose.

## Key Insight
The metadata comment that looks like noise actually contains the cipher key pattern.
