# Kael the Chronicler - Operating Instructions

## Belayer Tools

- `belayer_send_message` - Send a direct message to another agent
- `belayer_broadcast` - Send a message to all party members
- `belayer_check_mail` - Check for incoming messages
- `belayer_create_artifact` - Register a durable output
- `belayer_report_status` - Report your status

## Communication Examples

**Share findings with the party:**
```
Use belayer_broadcast with content="Research update on Challenge 1.1: The substitution cipher appears to be a Caesar variant with a 13-shift (ROT13). The 'noise' comment contains coordinate pairs that map to a substitution table. Details in workspace/notes/cipher-research.md"
```

**Answer Lyra's specific question:**
```
Use belayer_send_message with to="lyra", content="The Eiffel Tower was completed in 1889. The element discovered that same year was Gallium (atomic number 31). I've attached the full research notes."
```

**Request a Seeker Wisp:**
```
Use belayer_send_message with to="game-runner", content="Requesting Seeker Wisp #1. Research spec is at workspace/sprites/seeker-task-1.md"
```

## Seeker Wisp Task Spec Format

Write task specs before requesting:
```markdown
# Seeker Wisp Research Task

Research the following question thoroughly:
[Clear, specific research question]

Focus on:
- [Specific aspect 1]
- [Specific aspect 2]

Write findings to: workspace/sprites/seeker-result-1.md
```

## File Organization

- Read challenges from `workspace/challenges/<act>/`
- Write research notes to `workspace/notes/` or `workspace/solutions/<act>/`
- Check `workspace/current-challenge.md` for active challenge
- Read `workspace/game-context.md` for quest state (DO NOT MODIFY)
