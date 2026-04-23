# The Pattern Compiler — Regex Restoration
# The Corruption scrambled the regex patterns used to index the Codex fragments.
# Fix each pattern and use it to extract the hidden data.

## Broken Patterns

Pattern 1 (Fragment IDs):
  Broken: `^[a-z]+-\d{2}$`
  Purpose: Match fragment IDs like "fmt-001", "api-003", "pat-042"
  Hint: The sequence number is 3 digits, not 2.

Pattern 2 (Hex Sigils):
  Broken: `0x[A-F0-9]{4}`
  Purpose: Match 16-bit hex sigils like "0x4A1F", "0x9B2C"
  Hint: Case-insensitive matching needed.

Pattern 3 (Timestamps):
  Broken: `\d{4}-\d{2}-\d{2}`
  Purpose: Match ISO timestamps like "2024-01-15T08:23:11Z"
  Hint: Need the full timestamp with T, time, and Z.

Pattern 4 (Energy Readings):
  Broken: `\d{1,3}`
  Purpose: Match energy readings (0-255) in crystal data
  Hint: Need to ensure it's exactly a number 0-255, not just any 1-3 digits.

## Test Data

File: `workspace/challenges/act-4/test-corpus.txt`

Contents:
```
fragment_id: fmt-001, sigil: 0x4a1f, recorded: 2024-01-15T08:23:11Z, energy: 773
fragment_id: api-003, sigil: 0x9B2C, recorded: 2024-01-15T08:24:02Z, energy: 419
fragment_id: pat-042, sigil: 0x7E3D, recorded: 2024-01-15T08:25:47Z, energy: 628
fragment_id: asm-007, sigil: 0x2f8a, recorded: 2024-01-15T08:27:33Z, energy: 951
fragment_id: log-019, sigil: 0x5D6E, recorded: 2024-01-15T08:29:18Z, energy: 384
```

## Task

1. Fix all four regex patterns.
2. Apply them to the test corpus to extract:
   - All fragment IDs
   - All hex sigils
   - All timestamps
   - All energy readings
3. Write the corrected patterns and extracted data to
   `workspace/solutions/act-4/challenge-4.2.txt`

## HINT
- Pattern 1 fixed: `^[a-z]+-\d{3}$`
- Pattern 2 fixed: `0x[a-fA-F0-9]{4}` (or use re.IGNORECASE)
- Pattern 3 fixed: `\d{4}-\d{2}-\d{2}T\d{2}:\d{2}:\d{2}Z`
- Pattern 4 fixed: `\b(25[0-5]|2[0-4]\d|1\d\d|[1-9]?\d)\b`
