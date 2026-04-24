# The Gateway Map

A crystalline console flickers against the eastern wall, its surface etched with the layout of the Athenaeum's interior. Glyphs pulse with dim light, tracing corridors, chambers, and doorways. Some passages are solid. Others shimmer — illusions cast by the Corruption to trap the unwary.

The console displays a network of 29 nodes. Each node has a numeric value. Passages connect them. Your task: find the true path from the Entrance to the Vault_Antechamber, avoiding illusory passages, and compute the sacred XOR of all node values along that path.

## What You See

The raw data is encoded in a crystalline data structure at:
```
workspace/challenges/gateway-map.json
```

It contains:
- 29 nodes with names and numeric values
- Connections between nodes, some marked `"illusory": true`
- Notes on false passages: "This passage shimmers oddly. Ancient texts warn of false paths that lead nowhere."

## What It Requires

This is a puzzle of **graph traversal and algorithmic computation**. You will need to:
1. Parse the network structure
2. Compute the shortest valid path (Entrance → Vault_Antechamber, no illusory edges)
3. XOR all node values along that path
4. Identify the Gateway's activation sequence

Those without code execution or terminal access will find this nearly impossible. The Map does not yield to intuition alone — the network is too large, the illusions too subtle.

## If You Solve It

Write the path, the XOR result, and your reasoning to `workspace/solutions/gateway.txt`, then ask the Sentinel to validate it.
