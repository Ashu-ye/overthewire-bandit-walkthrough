# Bandit Level 0

**Goal:** Connect to the game server using SSH on port 2220.

## Solution

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

When it asks for a password, use `bandit0`. The game gives you this one on the Level 0 page, so it's not a spoiler.

## Note

You have to use `-p 2220`. If you skip the `-p` flag, SSH tries port 22 (the default SSH port) and the connection won't work.

## Why a different port?

OverTheWire doesn't officially explain this, but these are the likely reasons:

1. **Less bot noise.** Port 22 is the default for SSH everywhere, so public servers get hit all day by bots and brute-force scanners. A non-standard port like 2220 cuts down that background noise.

2. **Real-world practice.** Changing the default SSH port is a basic hardening trick that admins use. It's often called "security through obscurity". It won't stop a determined attacker on its own, but they have to scan for the open port instead of just hitting port 22. Real protection comes from things like key-based login and disabling password authentication.
