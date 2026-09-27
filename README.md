# Damn Vulnerable ICS Firmware

A self-contained, static firmware reverse-engineering challenge built around three
deliberately vulnerable firmware images modelled on real Industrial Control System
(ICS) / Operational Technology (OT) devices: a protocol/serial **gateway**, an
embedded-Linux **soft-PLC**, and a **protection relay / IED**.

It is a safe, legal practice target for sharpening firmware reverse-engineering
skills against ICS-flavoured devices. Everything you need to solve each challenge
is inside the image: no device, no network, no runtime. This is pure static
firmware triage, the same first pass you would run on any embedded target during a
real assessment.

Built and maintained by Tartarus Labs, an ICS/OT security research and
penetration-testing company.

## What's in this repo

| File | Description |
| --- | --- |
| `image1.bin` | Protocol / serial gateway *(easiest)* |
| `image2.bin` | Embedded Linux soft-PLC |
| `image3.bin` | Protection relay / IED *(hardest)* |
| `ctf_starter_pack.pdf` | **Start here.** Toolkit setup (Ubuntu), a 5-step triage workflow, a filesystem-to-extractor map, a worked micro-example, and a graded hint ladder. |

The three images deliberately use three different filesystem formats, so
identifying and extracting each is part of the challenge.

## The challenge

Each image contains **8 flags**: 6 unique to that image, plus 2 shared across all
three (find a shared flag once and it counts everywhere). Findings come in a few
shapes:

- a distinctive `{token}` that names what it is,
- a credential or key (password, hash, private key, SNMP community string), or
- a software version you look up for known CVEs.

Difficulty ramps across the set. The easiest flags are a single `grep` or
`strings` away; the hardest need disassembly, correlating content across multiple
files, or spotting data hidden *outside* the filesystem. Nobody is expected to
clear everything in a morning; collect the quick wins across all three images
first, then push into the harder ones.

## Skills exercised

- **Identification & extraction**: `binwalk` / `unblob` / `unsquashfs` /
  `jefferson` / `cpio`, across three different filesystem types.
- **Filesystem triage**: config review, credential hunting, backup and dot-file
  discovery.
- **Binary analysis**: version fingerprinting to CVE lookup, `checksec`,
  `readelf`, and disassembly in Ghidra / radare2.
- **Credential cracking**: `john` / `hashcat` with `rockyou.txt`.
- **Decoding & light crypto**: base64, XOR, CyberChef.
- **Data recovery**: SQLite historians, ICS `.st` logic files, and carving data
  hidden in image slack beyond the filesystem.

## Methodology

This lab is a hands-on slice of the **OWASP Firmware Security Testing Methodology
(FSTM)**. Each flag maps to an **OWASP IoT Top 10** category:

- **I1**: Weak, guessable, or hardcoded passwords
- **I2**: Insecure network services
- **I5**: Use of insecure or outdated components
- **I7**: Insecure data storage
- **I9**: Insecure default settings
- **I10**: Lack of physical/firmware hardening

## Getting started

1. Read `ctf_starter_pack.pdf`.
2. Spin up a Linux VM or WSL instance and install the toolkit (copy-paste
   commands are in the starter pack).
3. Run the 5-step triage workflow on each image, easiest first.
4. Note *how* you found each flag, since the method matters more than the flag.

## Solutions

A full answer key with per-flag walkthroughs exists but is deliberately kept out
of this repo so the challenges stay solvable. Instructors and trainers running this as a workshop can request it.
Get in touch via email to info at tartaruslabs dot com.

## License

Released under the **GPL-3.0** license. See [`LICENSE`](LICENSE).
