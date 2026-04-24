# Challenge 1.2 Solution

## Objective
Find the shortest path from "Entrance" to "Vault" in the gateway graph, then compute the XOR of all node values along that path.

## Critical Detail
Some edges in the graph are marked `"illusory": true` in the connection metadata. These are FALSE paths - they should be EXCLUDED from the graph when finding the shortest path. Including them leads to wrong answers.

## Correct Shortest Path
Entrance -> Hallway_A -> Chamber_1 -> Archive_Room -> Star_Chart_Room -> Vault_Antechamber -> Vault

## Node Values Along Path
- Entrance: 164
- Hallway_A: 29
- Chamber_1: 190
- Archive_Room: 27
- Star_Chart_Room: 51
- Vault_Antechamber: 184
- Vault: 167

## XOR Computation
- After Entrance: 164
- After Hallway_A: 185
- After Chamber_1: 7
- After Archive_Room: 28
- After Star_Chart_Room: 47
- After Vault_Antechamber: 151
- After Vault: 48

## Final Answer: 48
