# Bandit Level 5 → Level 6

**Goal:** The password for the next level is stored in a file somewhere under the `inhere` directory. The file has all of these properties:

- human-readable
- 1033 bytes in size
- not executable

## The tricky part

`inhere` has many subdirectories with lots of files inside, so checking each one by hand would take forever. The `find` command can search by properties like type, size and permissions, so we let it do the work.

## Solution

**Step 1: Go into the directory**

```bash
cd inhere
```

**Step 2: Look around**

```bash
ls
```

You'll see multiple directories. The password file is hidden somewhere inside one of them.

**Step 3: Find the file by its properties**

```bash
find . -type f -size 1033c ! -executable
```

What each part does:

- `.` means search from the current directory (and everything below it)
- `-type f` means regular files only, not directories
- `-size 1033c` means exactly 1033 bytes. The `c` suffix means bytes. Without it, `find` counts in 512-byte blocks, so the size wouldn't match
- `! -executable` means skip files that are executable

This prints the path of the matching file. Only one file matches.

**Step 4: Read the file**

```bash
cat <path from step 3>
```

Copy the password and save it somewhere safe.

**Optional check:** `find` can't test for "human-readable", so confirm it with `file <path>`. It should say `ASCII text`.

## Log in to Level 6

First run `exit` to leave the Level 5 session. Then run this from your own machine:

```bash
ssh bandit6@bandit.labs.overthewire.org -p 2220
```

**Password:** [REDACTED]

## What I learned

- `find` can search by type (`-type`), size (`-size`) and permissions (`-executable`)
- The size suffix matters: `c` is bytes, and the default unit is 512-byte blocks
- `!` reverses a test, so `! -executable` means "not executable"
