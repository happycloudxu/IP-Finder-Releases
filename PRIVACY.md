# Privacy Policy — IP-Finder

**Last updated: 9 November 2026**

IP-Finder is a Windows desktop application published by Dr. Xu's Studio ("we", "us"). This policy covers IP-Finder 2.00.10 and later, distributed through the Microsoft Store and as a direct download.

## Summary

IP-Finder does not collect, transmit, sell, or share personal information. There is no account, no sign-in, no analytics, no telemetry, no crash reporting, and no advertising.

## What the app shows you

To do its job, IP-Finder displays information that is already on your PC or that your network already reveals:

- **Your public (WAN) IP address**, retrieved from a public IP-echo service (see below).
- **Your local IPv4 addresses**, read from your network adapters.
- **Your computer name** and **your Windows user name**, read from Windows.
- **System details** — Windows edition and build, CPU name, physical and logical core counts, installed memory, and system uptime — shown in the main window's "This machine" panel and described in the About box.

None of this is sent anywhere by IP-Finder. It stays in the window, and in the clipboard only if you press a Copy button.

## Network requests

The only outbound connections IP-Finder makes are requests to public "what is my IP" services, so it can learn your public IP address. It tries these over HTTPS, in this order:

- api.ipify.org
- ifconfig.me
- checkip.amazonaws.com
- icanhazip.com

If none of those answers, it falls back to older, unencrypted plain-HTTP services:

- checkip.dyndns.org
- www.whatismyipaddress.com
- ipchicken.com

and finally to a WHOIS query on port 43 to whois.geektools.com.

These services necessarily see the IP address the request comes from, because that is the information being requested. We do not control them and they handle that data under their own privacy policies. The HTTPS requests also carry the standard User-Agent string `IP-Finder/<version>`, which identifies the application and its version — not you. The app sends nothing else: no account identifiers, no file contents, no usage data. Nothing about you is returned to or stored by the developer.

The application contains no author or project website links: nothing in the interface opens a browser.

## Local storage

The app stores one settings file, `%LOCALAPPDATA%\IP-Finder\IP-Finder.ini`, created on first use. It holds a single setting: whether the Autorun checkbox was left checked (a single `1` or `0` character). It contains no personal information. Deleting that file resets the checkbox to unchecked.

The app does not write to the Windows registry. It reads the CPU model name from `HKEY_LOCAL_MACHINE\HARDWARE\DESCRIPTION\System\CentralProcessor\0` to display it, and reads nothing else from the registry.

## Clipboard

When you press one of the Copy buttons, the displayed value (the machine report, the interface list, the computer name, the LAN address, or the WAN address) is placed on the Windows clipboard. This happens only on your explicit action, and nothing is read back from the clipboard.

## Children

IP-Finder is a network utility and is not directed at children. It collects no information from anyone, including children.

## Changes

If this policy changes, the revised version will be posted at this address with a new "last updated" date.

## Contact

Questions: use the support instructions on the download page.