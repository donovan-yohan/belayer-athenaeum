# The Algorithm Scroll — Pattern of the Resonant Array
# From the Realm of Patterns. Implement this algorithm to align the fragment energies.

## Problem: Resonant Frequency Alignment

You are given an array of crystal energies. Some crystals resonate harmonically,
others create dissonance. Your task is to find the longest contiguous subarray
where the energy levels form a "resonant sequence."

### Definition: Resonant Sequence
A sequence is resonant if for every element at position i (where i >= 2):
  energy[i] = (energy[i-1] + energy[i-2]) % 256

That is, each element is the sum of the two previous elements, modulo 256.

### Input
File: `workspace/challenges/act-4/crystal-energies.txt`
Format: One integer per line (0-255)
Count: 500 energy readings

### Task
1. Find the LONGEST contiguous subarray that is a resonant sequence.
2. Report: start index (0-based), length, and the sequence itself.
3. Compute the "alignment checksum": XOR of all elements in the resonant subarray.
4. Write results to `workspace/solutions/act-4/challenge-4.1.txt`

### Pseudocode

```
function find_resonant_subarray(energies):
    max_length = 0
    max_start = 0
    
    for start from 0 to len(energies) - 1:
        if len(energies) - start <= max_length:
            break  # Can't beat current best
        
        for end from start + 2 to len(energies):
            valid = true
            for i from start + 2 to end - 1:
                expected = (energies[i-1] + energies[i-2]) % 256
                if energies[i] != expected:
                    valid = false
                    break
            
            if valid and (end - start) > max_length:
                max_length = end - start
                max_start = start
    
    return max_start, max_length

function alignment_checksum(energies, start, length):
    checksum = 0
    for i from start to start + length - 1:
        checksum = checksum XOR energies[i]
    return checksum
```

### HINT
The brute-force approach works but is O(n^3). A dynamic programming approach
reduces this to O(n^2). For 500 elements, either should complete quickly in Python.
