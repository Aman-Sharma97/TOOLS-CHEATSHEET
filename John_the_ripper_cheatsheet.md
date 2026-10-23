# John the Ripper Cheat Sheet (Short)

> Use only on hashes/systems you own or have written permission to test.

## Basics

```
john [options] <hashfile>
```

## Preparing Hashes

| Tool | Meaning |
|---|---|
| `unshadow passwd shadow > combined.txt` | Merge Linux passwd + shadow |
| `zip2john file.zip > hash.txt` | Extract hash from zip |
| `rar2john file.rar > hash.txt` | Extract hash from rar |
| `ssh2john id_rsa > hash.txt` | Extract hash from SSH key |
| `pdf2john file.pdf > hash.txt` | Extract hash from PDF |
| `office2john file.docx > hash.txt` | Extract hash from Office doc |

## Attack Modes

| Option | Meaning |
|---|---|
| `--single` | Single crack mode (uses GECOS/login info) |
| `--wordlist=<file>` | Dictionary attack |
| `--rules` | Apply mangling rules with wordlist |
| `--incremental` | Brute-force mode |
| `--mask=<mask>` | Mask-based attack (e.g. `?u?l?l?l?d?d`) |

## Format & Scope

| Option | Meaning |
|---|---|
| `--format=<type>` | Specify hash format (e.g. `raw-md5`, `nt`, `sha512crypt`) |
| `--list=formats` | List all supported formats |
| `--users=<user>` | Restrict to specific user(s) |
| `--fork=<n>` | Parallelize across n processes |

## Viewing / Managing Results

| Option | Meaning |
|---|---|
| `--show <hashfile>` | Show cracked passwords |
| `--status` | Show progress of running session |
| `--session=<name>` | Name the session |
| `--restore=<name>` | Resume a saved session |
| `--pot=<file>` | Use specific pot file (cracked cache) |

## Common Workflow

```
unshadow /etc/passwd /etc/shadow > combined.txt
john combined.txt                                   # auto-detect + crack
john --wordlist=rockyou.txt --rules combined.txt      # dictionary + rules
john --format=nt --wordlist=rockyou.txt hash.txt       # crack NTLM hashes
john --show combined.txt                               # view cracked creds
```
