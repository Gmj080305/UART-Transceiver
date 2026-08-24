# UART (Universal Asynchronous Receiver Transmitter)

## Overview
UART is a serial communication protocol that doesn't use a shared clock signal — hence "asynchronous." "Universal" means it isn't tied to a specific transmitter/receiver pair; it's a general-purpose scheme for point-to-point serial data exchange.

## Physical Layer
Two devices connect with two crossed wires:
- Device A TX → Device B RX
- Device B TX → Device A RX

No clock line is needed. This keeps wiring simple compared to parallel buses, at the cost of lower throughput. Use UART for low-speed, low-complexity links; use parallel buses when speed matters more than pin count.

## Configuration
Before communicating, both devices must agree on:
- **Baud rate** — bits/sec, must match on both ends (commonly 9600)
- **Data length** — e.g. 8 bits, fixed and identical on both sides
- **Parity** (optional) — for basic error detection
- **Start/stop bits** — frame delimiters

## Frame Format
1. Idle line = logic high
2. **Start bit** = logic 0 → signals incoming data
3. **Data bits** (commonly 8), sent LSB first, NRZ encoding
4. **Parity bit** (optional) — set so the total count of 1s is even (even parity) or odd (odd parity); receiver recomputes and flags a mismatch as a transmission error
5. **Stop bit(s)** → line returns to idle high

## Pros
- Only 2 wires needed
- Simple, configurable frame (baud rate, data size)
- Full-duplex (independent TX/RX lines)
- Basic error detection via parity

## Cons
- Slower than parallel/synchronous links
- Start/stop/parity bits add overhead
- Both sides must be pre-configured with matching baud rate, since there's no shared clock to derive timing from

## Reference
[GeeksforGeeks – UART Protocol](https://www.geeksforgeeks.org/computer-networks/universal-asynchronous-receiver-transmitter-uart-protocol/)
