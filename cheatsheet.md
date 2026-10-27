# Bandit Command Cheatsheet

Commands and ideas I've used so far, grouped by topic. Updated as I go.

## Logging in

```bash
ssh bandit0@bandit.labs.overthewire.org -p 2220
```

- `-p 2220` is required. Without it, SSH tries the default port 22.
- The server blocks SSH from inside itself. Run `exit` first, then log in from your own machine.

## Looking around

| Command | What it does |
|---------|--------------|
| `pwd` | show the current directory |
| `ls` | list files |
| `ls -la` | list all files, including hidden ones, with details |
| `cat file` | print a file |
| `file name` | show what type of data a file contains |

## Tricky filenames

| Problem | Fix |
|---------|-----|
| Name starts with `-` | `cat ./-name` or `cat -- -name` |
| Name is just `-` | `cat ./-` or `cat < -` (`cat -` waits for stdin) |
| Name has spaces | `cat "my file"` or `cat my\ file` (or use Tab completion) |
| Many files starting with `-` | `file ./*` |

## Searching with `find`

```bash
find . -type f -size 1033c ! -executable
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

- `-type f`: regular files only
- `-size 33c`: exactly 33 bytes (`c` means bytes; the default unit is 512-byte blocks)
- `-user`, `-group`: filter by owner and group
- `! -executable`: not executable
- `2>/dev/null`: hide error messages such as "Permission denied"

## Text processing

| Command | What it does |
|---------|--------------|
| `grep "word" file` | print lines that contain the word |
| `sort file` | sort lines alphabetically |
| `sort file \| uniq -u` | print lines that appear only once |
| `uniq -d` / `uniq -c` | print repeated lines / count each line |
| `strings file` | pull readable text out of a binary file |
| `strings file \| grep '=='` | find readable lines with a pattern |

## Encoding

```bash
base64 -d data.txt                          # decode Base64
tr 'A-Za-z' 'N-ZA-Mn-za-m' < data.txt       # ROT13 (encodes and decodes)
```

## Hexdump and compression

```bash
mktemp -d                 # make a private working folder under /tmp
xxd -r data.txt > data    # turn a hexdump back into binary
file data                 # check the type before every step
```

| `file` says | Run |
|-------------|-----|
| gzip compressed data | `mv data data.gz` then `gzip -d data.gz` |
| bzip2 compressed data | `mv data data.bz2` then `bzip2 -d data.bz2` |
| POSIX tar archive | `tar -xvf data` (creates a new file with a different name) |
| ASCII text | `cat` it |

If binary output garbles your terminal, type `reset`.
