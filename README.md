# IP-Finder — downloadable builds

**This repository hosts released builds only. It contains no source code.** The
IP-Finder source lives in a private repository and is not published here, and nothing in
this repository is imported, compiled or needed by the application.

One window, no installer: the WAN address your ISP sees, the LAN address of the link
you are actually using, and a short report on the machine — with the full detail one
click away behind **Details**.

IP-Finder is a native Win32 GUI written in C — a single statically linked executable
that calls Winsock, WinINet and the IP Helper API directly. There is no Python runtime
and nothing to install.

- **WAN IP** — asks several live HTTPS endpoints in turn and parses the answer.
- **ISP Provider** — names the network that owns the public address (for example
  `Example ISP (AS64500)`) by asking three provider services in turn, right after the WAN
  address appears, and shows `unknown` if none answers.
- **LAN IP** — ranks every unicast IPv4 address from `GetAdaptersAddresses` (up, has a
  default gateway, Ethernet/Wi-Fi, RFC 1918, not a virtual adapter such as Hyper-V,
  WSL, Docker or a VPN tunnel) and reports the best one, so a multi-homed machine
  shows its physical LAN link rather than whatever the resolver returns first.
- **All IPv4 addresses** — one line per adapter with its first address, prefix length
  and link state, live adapters first, disconnected (`169.254.x`) ones last, loopback
  labelled. **Details** opens the full per-adapter block: every address with prefix and
  dotted netmask, adapter description, MAC, gateway, DHCP server, DNS and WINS servers,
  link speed and MTU.
- **Machine report** — a five-line summary: machine and user, OS, CPU with cores and
  clock, memory total and available, primary GPU with VRAM. **Details** opens the full
  report: system manufacturer/model and BIOS, build and architecture, physical/logical
  cores, virtualization, memory and page file, every GPU with VRAM and driver version,
  every fixed disk with free space, display resolution and scaling, uptime.
- **Copy** button on every field, plus an **Autorun** checkbox whose state is kept in
  `%LOCALAPPDATA%\IP-Finder\IP-Finder.ini`, never in the registry.

## Which file do I download?

Get both from the [latest release](../../releases/latest).

| Asset | Size | What it is |
|---|---|---|
| **`IP-Finder.exe`** — start here | 278.5 KiB (285,184 bytes) | **The application.** Single 64-bit Windows executable, statically linked: no installer, no runtime DLLs, no configuration. Double-click and click **Refresh addresses** |
| `SHA256SUMS.txt` | 80 bytes | The checksum above in `sha256sum` format, for verifying the download |

Requires Windows. Nothing else — no Python, no `.NET`, no Visual C++ redistributable.

`IP-Finder.exe` is unsigned (there is no code-signing certificate), so SmartScreen may
show **"Windows protected your PC"** on first run: choose **More info → Run anyway**.
A matching SHA-256 proves the file left GitHub intact; it does not prove who built it
and does not suppress that prompt.

## Checksums

Every asset is byte-identical to the build that was verified before release. Confirm
after downloading:

```powershell
Get-FileHash .\IP-Finder.exe -Algorithm SHA256
```

```cmd
certutil -hashfile IP-Finder.exe SHA256
```

| Asset | Bytes | SHA-256 |
|---|---|---|
| `IP-Finder.exe` | 285,184 | `2be4fbd18ff9a16750ab4a3ab20036228f3f7913fee5ba40fb205b964de4d863` |
| `SHA256SUMS.txt` | 80 | `ae526ad6ad2ab93cea862e4eca7c579b4a19359db5e0ddb28cae303248be6229` |

## What's new

**2.00.15** — the three things reported against 2.00.14: headings that sat higher than
the buttons beside them, an interface list that stopped at `+N more`, and a details
report that ran one field into the next.

- The section headings are now 13 dialog units tall and share the exact y band of the
  **Details...** and **Copy** buttons next to them, with `SS_CENTERIMAGE` giving the same
  vertical centring those buttons apply to their own text. Button heights are unchanged.
- The cards were re-gridded rather than the font shrunk, so **ALL NETWORK INTERFACES**
  lists every adapter on an eight-adapter machine — eight rows in a 166 px box that needs
  160 px, last row fully visible, no scrollbar. The `+N more` line survives only as a
  guard for a machine with more adapters than the box can show.
- Every field in the details report now ends with a hard `\r\n` and a wrapped value
  continues indented under its value column, so an ISP name or an adapter description
  that runs to three lines no longer swallows the adapter after it. Each adapter block
  opens on a fresh line behind a blank separator.

**2.00.14** — the antivirus false positive is gone and nothing you see or click changed.
Defender was quarantining 2.00.13's exe as `Trojan:Win32/Bearfoos.A!ml`, an ML heuristic
rather than a malware signature; the build still carried GCC's symbol table, and
stripping it with `-s` took the file from 765,436 to 283,648 bytes and cleared the
verdict. Every feature, every endpoint and the autorun INI are unchanged. The verdict
stays model-dependent — a different engine, different definitions or a third-party
scanner could still decide differently — and the exe is unsigned, so SmartScreen may
still ask on first run.

**2.00.13** — the layout work the two builds above kept building on: section buttons
17 → 13 dialog units tall with the recovered height given to the interface box, summary
boxes sized from the text they actually hold so neither scrolls on launch, and an
**ISP Provider** row that reads `press Refresh` before the first lookup instead of
`unknown`, `looking up...` while a lookup runs, and `unknown` only when a completed
lookup genuinely failed.
## Privacy

IP-Finder collects nothing and has no telemetry. The full policy is in
[PRIVACY.md](PRIVACY.md).

## Issues and support

This repository has no issue tracker for the application source. Report problems through
whoever supplied your copy of the build.