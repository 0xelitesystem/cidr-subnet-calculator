# CIDR Subnet Calculator

Enter an IPv4 address with a CIDR prefix (for example `192.168.1.0/24`) and get the full breakdown: network address, broadcast address, netmask, wildcard mask, first and last usable host, total and usable host counts, and a binary view of the address with the network and host portions highlighted. Includes a helper to split a block into equal subnets. Single self-contained file, no external dependencies, works offline.

## Live demo

https://0xelitesystem.github.io/cidr-subnet-calculator/

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

## Privacy

Everything runs in your browser. The address you type is never sent anywhere. There are no external scripts, fonts, stylesheets, or analytics. Open the page source to confirm. It works fully offline.

## More

Part of a catalog of single-file browser tools and plain-language references, all MIT licensed and dependency-free: [0xelitesystem.github.io](https://0xelitesystem.github.io/). Built by [elitesystem.ai](https://elitesystem.ai).

## License

MIT. Copyright 0xelitesystem 2026.
