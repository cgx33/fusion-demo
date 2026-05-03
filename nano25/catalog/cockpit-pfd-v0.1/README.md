# Cockpit PFD Demo (v0.1)

Avionics Primary Flight Display — attitude horizon, speed/altitude tapes,
heading indicator, flight director, V-speeds, FMA bar.

| Field | Value |
|---|---|
| Target | Nano25 |
| Fusion SDK | v4.0.3.22 |
| Binary size | 1.6 MB |
| Build mode | release / archive linkage (static) |
| Runtime deps | `libts`, `libm`, `glibc` (standard on Nano25) |

## Run on your Nano25

Assumes you have SSH access to your Nano25 (default IP `192.168.2.15`,
user `root`).

```bash
# 1. Download cockpit-pfd.elf from this catalog entry

# 2. Push to Nano25
scp cockpit-pfd.elf root@<nano25-ip>:/root/

# 3. Run
ssh root@<nano25-ip> "chmod +x /root/cockpit-pfd.elf && /root/cockpit-pfd.elf"
```

The UI appears on the display connected to your Nano25.

## Stop

`Ctrl+C` in the SSH session, or:

```bash
ssh root@<nano25-ip> "pkill cockpit-pfd"
```

## Want to build it yourself?

The Cockpit PFD source is part of the Fusion SDK Starter package
(workspace/sandbox/cockpit/ in the SDK). Download the SDK to compile
your own variants and start UI development — see the SDK download
section.
