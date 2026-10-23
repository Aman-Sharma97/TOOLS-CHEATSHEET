# Hashcat Cheat Sheet (Short)

> Use only on hashes/systems you own or have written permission to test.

## Basics

```
hashcat -m <hash-mode> -a <attack-mode> <hashfile> [wordlist/mask]
```

## Attack Modes (`-a`)

| Mode | Meaning |
|---|---|
| `0` | Straight (wordlist) |
| `1` | Combination (two wordlists) |
| `3` | Brute-force / mask |
| `6` | Hybrid: wordlist + mask |
| `7` | Hybrid: mask + wordlist |

## Common Hash Modes (`-m`)

| Mode | Hash type |
|---|---|
| `0` | MD5 |
| `100` | SHA1 |
| `1400` | SHA256 |
| `1700` | SHA512 |
| `1000` | NTLM |
| `3200` | bcrypt |
| `1800` | sha512crypt (Unix) |
| `22000` | WPA-PBKDF2 (WPA2 handshake) |

(Full list: `hashcat --help` or `hashcat -h | grep -i <name>`)

## Wordlist / Rules

| Option | Meaning |
|---|---|
| `-r <rule-file>` | Apply mangling rules (e.g. `best64.rule`) |
| `--stdout` | Preview generated candidates without cracking |
| `-1/-2/-3/-4 <charset>` | Define custom charsets for masks |
| `?l ?u ?d ?s` | Lower, upper, digit, special (mask placeholders) |

## Performance & Control

| Option | Meaning |
|---|---|
| `-O` | Optimized kernel (faster, length limits apply) |
| `-w 1-4` | Workload profile (1=low, 4=insane) |
| `--status` | Periodic status updates |
| `--force` | Ignore warnings (use with care) |
| `-o <file>` | Output cracked results to file |
| `--session=<name>` | Name session (for resume) |
| `--restore` | Resume a saved session |

## Common Workflow

```
hashcat -m 0 -a 0 hashes.txt rockyou.txt                     # wordlist attack (MD5)
hashcat -m 0 -a 0 hashes.txt rockyou.txt -r best64.rule        # + rule mangling
hashcat -m 0 -a 3 hashes.txt ?u?l?l?l?l?d?d                    # mask brute-force
hashcat -m 22000 -a 0 capture.hc22000 rockyou.txt              # WPA2 handshake
hashcat -m 0 hashes.txt --show                                 # show cracked results
```
