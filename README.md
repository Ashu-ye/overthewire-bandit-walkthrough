# OverTheWire Bandit Walkthrough

My walkthroughs for the [OverTheWire Bandit](https://overthewire.org/wargames/bandit/) wargame.

Bandit is a beginner-friendly wargame that teaches Linux command-line fundamentals, file handling, networking, encoding, SSH, cron, and basic privilege escalation. I'm working through it as part of my path toward a SOC Analyst / Blue Team role, so each writeup focuses on *how I solved the level and what I learned*, not just the answer.

> ⚠️ **Passwords are intentionally not included.** OverTheWire asks players not to spoil levels. Every writeup shows the method and commands, and the password is shown as `[REDACTED]`. If you're stuck, use the writeups as a nudge, but try it yourself first.

---

## Repository Structure

```
overthewire-bandit-walkthrough/
├── README.md          # this file
├── cheatsheet.md      # commands and concepts collected so far
└── levels/
    ├── level_00.md        # Level 0 (login)
    ├── level_00-01.md     # Level 0 → 1
    ├── level_01-02.md     # Level 1 → 2
    └── ...
```

Level 0 is just the login. After that, each file covers the step from level **N** to level **N+1**. Most writeups follow the same format:

- **Goal**: what the level asks for
- **The tricky part / concepts**: the idea or command you need to understand
- **Solution**: the steps and commands, one at a time
- **Log in to the next level**: the SSH command, with the password left out
- **What I learned**: key takeaways

---

## Progress

Legend: ✅ Done | ⬜ Not started

| Level | Topic | Status |
|-------|-------|--------|
| [0](levels/level_00.md) | Logging in with SSH on port 2220 | ✅ |
| [0 → 1](levels/level_00-01.md) | Reading a file (`cat`) | ✅ |
| [1 → 2](levels/level_01-02.md) | Files with a dash in the name | ✅ |
| [2 → 3](levels/level_02-03.md) | Filenames with spaces and dashes | ✅ |
| [3 → 4](levels/level_03-04.md) | Hidden files | ✅ |
| [4 → 5](levels/level_04-05.md) | Identifying human-readable files (`file`) | ✅ |
| [5 → 6](levels/level_05-06.md) | `find` by size and properties | ✅ |
| [6 → 7](levels/level_06-07.md) | `find` by owner and group | ✅ |
| [7 → 8](levels/level_07-08.md) | `grep` in a large file | ✅ |
| [8 → 9](levels/level_08-09.md) | Finding the unique line (`sort`, `uniq`) | ✅ |
| [9 → 10](levels/level_09-10.md) | `strings` on a binary file | ✅ |
| [10 → 11](levels/level_10-11.md) | Base64 decoding | ✅ |
| [11 → 12](levels/level_11-12.md) | ROT13 with `tr` | ✅ |
| [12 → 13](levels/level_12-13.md) | Hexdump reversal and repeated decompression | ✅ |
| 13 → 14 | SSH private key login | ⬜ |
| 14 → 15 | Talking to a port with `nc` | ⬜ |
| 15 → 16 | SSL/TLS with `openssl s_client` | ⬜ |
| 16 → 17 | Port scanning with `nmap` | ⬜ |
| 17 → 18 | Comparing files with `diff` | ⬜ |
| 18 → 19 | Modified `.bashrc` and SSH commands | ⬜ |
| 19 → 20 | Setuid binaries | ⬜ |
| 20 → 21 | Setuid binary with a network listener | ⬜ |
| 21 → 22 | Cron jobs | ⬜ |
| 22 → 23 | Reading and understanding cron scripts | ⬜ |
| 23 → 24 | Cron job that runs scripts | ⬜ |
| 24 → 25 | Brute-forcing a 4-digit PIN | ⬜ |
| 25 → 26 | Escaping a restricted shell | ⬜ |
| 26 → 27 | Using a setuid binary | ⬜ |
| 27 → 28 | Git: cloning a repository | ⬜ |
| 28 → 29 | Git: commit history | ⬜ |
| 29 → 30 | Git: branches | ⬜ |
| 30 → 31 | Git: tags | ⬜ |
| 31 → 32 | Git: pushing files | ⬜ |
| 32 → 33 | Escaping the uppercase shell | ⬜ |
| 33 → 34 | Wrap-up | ⬜ |

---

## Skills Covered So Far

| Theme | Levels | Tools and concepts |
|-------|--------|--------------------|
| SSH basics | 0 | `ssh`, non-default ports |
| File handling and tricky filenames | 0 → 1 to 4 → 5 | `ls -a`, `cat`, `file`, quotes, `./`, `--` |
| Searching the filesystem | 5 → 6 to 6 → 7 | `find` by type, size, owner and group, `2>/dev/null` |
| Text processing | 7 → 8 to 9 → 10 | `grep`, `sort`, `uniq`, `strings`, pipes |
| Encoding | 10 → 11 to 11 → 12 | `base64`, ROT13 with `tr` |
| Compression and archives | 12 → 13 | `xxd -r`, `gzip`, `bzip2`, `tar`, `mktemp` |

---

## How to Use This Repo

1. Try the level yourself first.
2. If you're stuck, read the explanation and the first steps of the matching writeup for a hint.
3. Check the full commands only after you've tried.
4. Read **What I learned** to connect the skill to real-world work.

See [`cheatsheet.md`](cheatsheet.md) for a quick reference of the commands used so far.

---

## About

**Author:** Ashu
**Goal:** Entry-level SOC Analyst / Blue Team role

---

## Disclaimer

This repository is for educational purposes. All writeups cover the legal, intentionally vulnerable Bandit wargame provided by [OverTheWire](https://overthewire.org). Passwords are omitted to respect the spirit of the game. Techniques shown here should only be used on systems you own or have explicit permission to test.
