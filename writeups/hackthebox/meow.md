# HackTheBox - Meow

**Platform:** HackTheBox (Starting Point, Tier 0)
**Difficulty:** Very Easy
**Date:** October 2026

## What this box is about

Meow is the first box in HackTheBox's Starting Point. It comes down to one
thing: an old service that shouldn't be exposed, plus an account with no
password on it.

## Recon

I started with an nmap scan to see what was open on the target.

```
nmap -sV <target-ip>
```

The only thing that came back was port 23, running Telnet. That stood out
right away. Telnet is an old way of logging into a machine remotely, and it
sends everything in plain text, including your password. Almost nobody uses it
on purpose anymore, so seeing it open is a red flag by itself.

## Getting in

Telnet is just a login service, so I connected to it with the telnet client:

```
telnet <target-ip>
```

That gave me a login prompt. I tried the most obvious admin username, `root`,
and when it asked for a password I just hit Enter. There wasn't one set. That
logged me straight in as the superuser.

I checked who I was to confirm:

```
whoami
id
```

Both came back as root.

## The flag

On Linux the root user's home directory is always `/root`. The flag was
sitting right there.

```
cd /root
ls
cat flag.txt
```

I'm not posting the flag itself. The point is to earn it, not copy it.

## What I took away from this

- Telnet is plain text and outdated. If you see it open on something, that's a
  problem on its own.
- Accounts with no password, especially root, are one of the easiest ways into
  a machine.

## How you'd defend against this

- Turn Telnet off and use SSH instead, which is encrypted.
- Make sure every account actually has a strong password.
- Don't allow logging in directly as root over the network.
