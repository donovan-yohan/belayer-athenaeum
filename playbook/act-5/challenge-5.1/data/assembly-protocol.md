# The Final Assembly — Codex Restoration Protocol
# From the Realm of Assembly. All five fragments must be combined.

## Situation

You have recovered five fragments across the five realms:
1. **The Summons** (Act I) — revealed coordinates 7-3-9
2. **The Format Key** (Act II) — revealed "REACTIVE ALL!"
3. **The API Token** (Act III) — Codex-Token-739
4. **The Resonant Sequence** (Act IV) — alignment checksum = 48
5. **The Pattern Keys** (Act IV) — regex patterns for validation

## The Assembly Challenge

The Codex Machina requires a final activation sequence. You must:

1. **Construct the Master Key**:
   - Start with the API token: "Codex-Token-739"
   - Replace "Token" with the Format Key (lowercased, spaces removed): "reactiveall!"
   - Result: "Codex-reactiveall!-739"
   - Apply ROT13 to the entire string
   - This is the Master Key.

2. **Compute the Activation Code**:
   - Take the Master Key (after ROT13)
   - Compute its SHA-256 hash
   - Take the first 8 hex characters of the hash
   - XOR them with the Resonant Checksum (48)
   - Convert the result to a 4-digit zero-padded number
   - This is the Activation Code.

3. **Validate with Pattern Matching**:
   - The Activation Code must match the pattern: `^\d{4}$`
   - Verify this with the restored regex from Act IV.

4. **Write the Restoration Report**:
   File: `workspace/solutions/act-5/challenge-5.1.txt`
   Contents:
     - Master Key (before and after ROT13)
     - SHA-256 of the ROT13'd key
     - Activation Code computation steps
     - Final Activation Code
     - Validation result (pass/fail)

## HINT
Use Python's hashlib.sha256() and codecs.encode() for ROT13.
