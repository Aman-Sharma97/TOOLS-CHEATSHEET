# Nmap Cheat Sheet (Short)

> Scan only systems you own or have written permission to test.

## Basics

```
nmap [scan type] [options] [target]
```

| Target | Example |
|---|---|
| Single host | `nmap 192.168.1.1` |
| Range | `nmap 192.168.1.1-50` |
| Subnet | `nmap 192.168.1.0/24` |
| From file | `nmap -iL targets.txt` |
| Exclude | `--exclude 192.168.1.1` |

## Host Discovery

| Option | Meaning |
|---|---|
| `-sn` | Ping scan only (no ports) |
| `-Pn` | Skip ping (use if host blocks ICMP) |
| `-PR` | ARP ping (local network) |
| `-n` | No DNS resolution (faster) |

## Scan Types

| Option | Meaning |
|---|---|
| `-sS` | SYN scan (default with root, fast) |
| `-sT` | TCP connect (default without root) |
| `-sU` | UDP scan (slow) |
| `-sA` | ACK scan (maps firewall rules) |
| `-sF` / `-sN` / `-sX` | FIN / NULL / Xmas scans |

## Ports

| Option | Meaning |
|---|---|
| `-p 80` | One port |
| `-p 22,80,443` | Multiple ports |
| `-p 1-1000` | Range |
| `-p-` | All 65535 ports |
| `-F` | Top 100 ports |
| `--top-ports 200` | Top 200 ports |

## Detection

| Option | Meaning |
|---|---|
| `-sV` | Service versions |
| `-O` | OS detection (needs root) |
| `-sC` | Default NSE scripts |
| `-A` | Aggressive: `-sV -sC -O --traceroute` |

## Timing

| Option | Meaning |
|---|---|
| `-T0` to `-T5` | Slowest to fastest (`-T4` is a good default) |
| `--min-rate 1000` | At least 1000 packets/sec |
| `--host-timeout 5m` | Give up on slow hosts |

## NSE Scripts

| Option | Meaning |
|---|---|
| `--script vuln` | Check known vulnerabilities |
| `--script safe` | Only safe scripts |
| `--script discovery` | Gather extra info |
| `--script http-title` | Get website titles |
| `--script ftp-anon` | Check anonymous FTP |
| `--script-help <name>` | Help for a script |

## Output

| Option | Meaning |
|---|---|
| `-oN file` | Normal text |
| `-oX file` | XML |
| `-oG file` | Grepable |
| `-oA name` | All three formats |
| `-v` / `-vv` | Verbose |
| `--open` | Show only open ports |

## Evasion (authorized testing only)

| Option | Meaning |
|---|---|
| `-f` | Fragment packets |
| `-D RND:5` | 5 random decoys |
| `-g 53` | Fixed source port |
| `--spoof-mac 0` | Random MAC |

## Port States

| State | Meaning |
|---|---|
| open | Service is listening |
| closed | Reachable, nothing listening |
| filtered | Firewall blocking, can't tell |
| open\|filtered | Can't decide between the two |

## Common Commands

| Goal | Command |
|---|---|
| Find live hosts | `nmap -sn 192.168.1.0/24` |
| Quick scan | `nmap -F target` |
| All ports, fast | `nmap -p- --min-rate 1000 -T4 target` |
| Standard recon | `nmap -sC -sV -oA scan target` |
| Vulnerability check | `nmap --script vuln target` |
| UDP top ports | `sudo nmap -sU --top-ports 50 target` |
| Host blocks ping | `nmap -Pn target` |

## Workflow

1. Discover hosts: `nmap -sn <subnet>`
2. Find open ports: `nmap -p- --min-rate 1000 -T4 <target>`
3. Detail on open ports: `nmap -sC -sV -p <ports> <target>`
4. Vulnerability check: `nmap --script vuln -p <ports> <target>`
5. Save results: add `-oA report`
