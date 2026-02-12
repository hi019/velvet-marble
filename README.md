Claude Code restores skills read by subagents when compacting. If the total number of skill tokens read by all subagents is > context limit, a compaction will result in >100% context utilization and further messages will error.

To reproduce (as of v2.1.39):

1. Start Claude Code in this repo
2. Run this prompt: `Spawn two subagents: one to read 100k-tok-a and another to read 100k-tok-b. Each subagent should return a random word after reading the skill.`
3. Run `/compact`
4. Try to send a message, and you should get "Context limit reached · /compact or /clear to continue" along with "Skills restored (100k-tok-b, 100k-tok-a)".

Each skill is 100k tokens. If you run `/context` after the error, you should see that the context is >100% full.
