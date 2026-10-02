# CIDR Subnet Calculator

Enter an IPv4 address with a CIDR prefix (for example `192.168.1.0/24`) and get the full breakdown: network address, broadcast address, netmask, wildcard mask, first and last usable host, total and usable host counts, and a binary view of the address with the network and host portions highlighted. Includes a helper to split a block into equal subnets. Single self-contained file, no external dependencies, works offline.

**Live demo:** https://0xelitesystem.github.io/cidr-subnet-calculator/

## Features

- Network and broadcast addresses
- Netmask and wildcard mask
- First and last usable host
- Total addresses and usable host count
- Binary view with the network bits and host bits color coded
- Private (RFC 1918), loopback, link-local, and multicast range labeling
- Subnet-splitting helper: split a block into N equal subnets and list each one with its range and usable host count
- Correct handling of the edge cases: `/31` point-to-point (RFC 3021) and `/32` single host
- Input validation with clear error messages
- Dark-mode toggle, keyboard usable

## How it works

All arithmetic runs in unsigned 32-bit integer space. IPv4 fits in 32 bits, so no big-integer library is needed. The mask is built by shifting `0xFFFFFFFF` left by `32 - prefix`, and every intermediate value is normalized with the unsigned right-shift operator (`>>> 0`) so the sign bit never turns a large address negative. The network address is `ip AND mask`, the broadcast is `network OR wildcard`, and the split helper walks the block in fixed-size steps. Host input such as `192.168.1.42/24` is normalized to its containing network before display.

## Use

1. Type an IPv4 address with a prefix, such as `192.168.1.0/24`, into "Address and prefix".
2. Click Calculate (or press Enter) and read the network, broadcast, masks, usable host range, host counts, and the binary view.
3. To split the block, enter the number of subnets and click Split.
4. Click Clear to start over.

## Why this exists

Subnet math is easy to fumble at the edges, especially `/31` and `/32`. This is one HTML file that does the 32-bit arithmetic in your browser, with no tracking and no network access, released under the MIT license.

## Privacy

Everything runs in your browser. The address you type is never sent anywhere. There are no external scripts, fonts, stylesheets, or analytics. Open the page source to confirm. It works fully offline.

The only thing the page stores is your light or dark theme choice, under the `theme` key in localStorage, after you click the theme button.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## Run locally

```
git clone https://github.com/0xelitesystem/cidr-subnet-calculator
cd cidr-subnet-calculator
```

Open `index.html` in a browser, or serve the folder with `python -m http.server 8000` and visit http://localhost:8000.

## Build

No build step. The whole tool is one `index.html` file with inline CSS and JavaScript.

## License

MIT. Copyright 0xelitesystem 2026.
