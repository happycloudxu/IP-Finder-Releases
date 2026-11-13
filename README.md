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
| **`IP-Finder.exe`** — start here | 747.5 KiB (765,436 bytes) | **The application.** Single 64-bit Windows executable, statically linked: no installer, no runtime DLLs, no configuration. Double-click and click **Refresh addresses** |
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
| `IP-Finder.exe` | 765,436 | `c8a09f66c853c011fc9b7a2216bc762f9d372bd2238bbc71ebc26d349b16a612` |
| `SHA256SUMS.txt` | 80 | `fe7ea9ad689482c52a9ac015f8f949e19c8c9913ce4b04462b5883ce957039a3` |

## What's new

**2.00.12** — the window keeps its size and shape; a fourth row appears in
**IP ADDRESSES**, and both report boxes wrap instead of hiding text behind a horizontal
scrollbar.

- **ISP Provider** sits under Computer / Local / Public and names the network that owns
  the public address, as `Provider Name (AS####)`. It is looked up only after the WAN
  address is known and is skipped entirely when that lookup fails, tries three services
  in turn so one blocked endpoint cannot empty the row, and shows `unknown` when none
  answers. **Copy** puts the full name — for example
  `Example ISP, Inc. (AS64500)` — on the clipboard while the row
  shows the short form that fits its column.
- **THIS MACHINE** and **ALL NETWORK INTERFACES** wrap long entries onto continuation
  lines aligned under the value column, and neither box carries a horizontal scrollbar at
  any display scaling. A vertical scrollbar remains only as a fallback for a machine with
  more adapters than the box can hold.
- **Details** windows now open at the size of their content instead of a fixed, mostly
  empty frame, are centred on the monitor that owns the main window, stay resizeable, and
  scroll vertically only when a report is genuinely long.
- Everything else is unchanged: the full report is still one **Copy** away, report rows
  still use a fixed-pitch font so the space-padded columns line up, and every field is
  best effort — anything Windows or a driver does not publish is omitted rather than
  shown as zero.

See the [releases page](../../releases) for the notes for each version.

## Privacy

IP-Finder collects nothing and has no telemetry. The full policy is in
[PRIVACY.md](PRIVACY.md).

## Issues and support

This repository has no issue tracker for the application source. Report problems through
whoever supplied your copy of the build.
