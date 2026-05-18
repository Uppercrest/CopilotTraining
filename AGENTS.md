# AGENTS Guidelines for This Repository

This repository is for Learning git hub copilot and its features. Always verify copilot and copilor cli documentation before answering to user questions related to copilot features.

## Bash Redirection

RestrictionsTo prevent the creation of literal files named nul or . on Windows machines when using Git Bash or WSL, adhere to these rules:

1. NEVER use > nul: Git Bash treats nul as a literal filename.Instead use: > /dev/null for Git Bash/WSL or > $null for PowerShell.
2. Avoid Spaces in Redirection: Never put a space between the file descriptor and the redirector (e.g., avoid 2 > 1).Correct Syntax: 2>&1 (No spaces).
3. Cross-Platform Silence: When writing scripts intended for Windows users running Bash, always use the Unix-style "black hole":Correct: command > /dev/null 2>&1
4. No Naked Periods: Never redirect output to a period (e.g., > .). If the goal is to save to a file in the current directory, a specific filename must be provided.

When in doubt, use ask_user tool to resolve ambiguous quesries and questions, rather than self guessing the wrong answer.
