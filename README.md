# Subnet Calculator

A single-file IPv4 and IPv6 subnet calculator that shows the bit-level math behind every result. No build step and no dependencies: open `index.html` in a browser.

## Features

- **IPv4**: accepts `192.168.10.77/26`, `172.20.33.200 255.255.240.0`, or a bare address. Shows network, broadcast, usable host range and count, subnet and wildcard masks, historic class, and scope (RFC 1918 private, CGNAT, loopback, documentation and so on). Handles /31 point-to-point links (RFC 3021) and /32 host routes.
- **IPv6**: accepts full, `::`-compressed, and embedded-IPv4 forms (`::ffff:192.0.2.1`). Shows network, last address, address count, how many /64 LANs fit, the expanded and compressed (RFC 5952) forms, prefix mask, host part, and address type (global unicast, ULA, link-local, multicast and so on).
- **Bit by bit**: the address, mask, network, and broadcast/last address as colored bits (IPv4) or hex digits plus a binary zoom on the boundary hextet (IPv6). Click the mask row to move the prefix.
- **Splitter**: divides the network into smaller subnets and highlights the one that contains your address.

## How it works

1. An IPv4 address is a 32-bit number and an IPv6 address is a 128-bit number.
2. The prefix length `/p` means the first `p` bits identify the network and the rest identify a host. The mask is `p` ones followed by zeros.
3. **Network address = address AND mask.** This clears every host bit.
4. **Broadcast / last address = network OR (NOT mask).** This sets every host bit.
5. **Host count**: with `h` host bits a block has 2^h addresses. IPv4 subtracts 2 (network and broadcast), except /31 and /32. IPv6 has no broadcast, so every address counts.
6. **Splitting**: borrowing `n` host bits for the network gives 2^n smaller subnets.

IPv4 math uses JavaScript Numbers with `>>> 0` to keep results unsigned. IPv6 math uses `BigInt`, because JavaScript's bitwise operators on Numbers only work on 32 bits.
