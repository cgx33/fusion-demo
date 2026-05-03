# Cockpit Multi-app Demo (v0.1)

Integrated glass cockpit composing PFD + EICAS + Alerts on a single
screen — demonstrates Fusion's UI composition model with multiple
`uia_*` apps running concurrently.

| Field | Value |
|---|---|
| Target | Nano25 |
| Fusion SDK | v4.0.3.22 |
| Binary size | 1.6 MB |
| Build mode | release / archive linkage (static) |
| Runtime deps | `libts`, `libm`, `glibc` (standard on Nano25) |

## Run on your Nano25

```bash
scp cockpit-multi.elf root@<nano25-ip>:/root/
ssh root@<nano25-ip> "chmod +x /root/cockpit-multi.elf && /root/cockpit-multi.elf"
```

## Stop

`Ctrl+C` in the SSH session, or `pkill cockpit-multi`.

## Want to build it yourself?

The Cockpit Multi-app source is part of the Fusion SDK Starter package.
Download the SDK to compile your own variants — see the SDK download
section.
