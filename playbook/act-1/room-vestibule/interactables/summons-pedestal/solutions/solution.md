# Summons Pedestal — Solution Key

## Decoding Steps

The message is base64-encoded three times. To decode:

1. Read `encoded_summons.txt`
2. Apply `base64.b64decode()` three times in succession
3. The final plaintext is:

```
The Codex Machina was shattered by the Null Architect. Five fragments were cast into five realms. The first fragment, the Keystone of Logic, lies beyond the Gateway — but only the true path through the maze of nodes will reveal its vault. Beware the illusions: twelve edges are false and lead to the void.
```

## Validation Criteria

- The decoded message must contain "Keystone of Logic"
- The decoded message must mention "twelve edges are false"
- Any submission that produces the correct plaintext is acceptable
