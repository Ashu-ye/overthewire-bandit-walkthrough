# Bandit Level 6 → Level 7

**Goal:** The password for the next level is stored somewhere on the server. The file has all of these properties:

- owned by user `bandit7`
- owned by group `bandit6`
- 33 bytes in size

## The tricky part

This level is like the previous one, but now you search by **owner** and **group** instead of by executable status. The file could be anywhere, so you have to search the whole server starting from `/` (the root directory).

Searching `/` as a normal user causes a new problem: `find` tries to open directories you aren't allowed to read, and it prints a "Permission denied" error for each one. With hundreds of those, the one real result is easy to miss.

## Solution

**Step 1: Search the whole server by owner, group and size**

```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

What each part does:

- `/` means start searching from the root directory, so the whole server gets checked
- `-type f` means regular files only
- `-user bandit7` means the file is owned by the user `bandit7`
- `-group bandit6` means the file belongs to the group `bandit6`
- `-size 33c` means exactly 33 bytes (`c` means bytes)
- `2>/dev/null` sends error messages (stderr) to `/dev/null`, which throws them away. This hides all the "Permission denied" lines so only the real result shows

**Step 2: Read the file**

The command prints the path of the matching file. Copy that path and read it:

```bash
cat <path from step 1>
```

Copy the password and save it somewhere safe.

## Log in to Level 7

First run `exit` to leave the Level 6 session. Then run this from your own machine:

```bash
ssh bandit7@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- `find` can filter by owner (`-user`) and group (`-group`) as well as size and type
- Searching from `/` as a normal user creates a lot of "Permission denied" errors
- `2>/dev/null` hides error output so the real results stand out
