# Cockpit EICAS Demo (v0.1)

Engine Indication and Crew Alerting System — engine performance gauges,
caution/warning banner, system messages.

| Field | Value |
|---|---|
| Target | Nano25 |
| Fusion SDK | v4.0.3.22 |
| Binary size | 1.6 MB |
| Build mode | release / archive linkage (static) |
| Runtime deps | `libts`, `libm`, `glibc` (standard on Nano25) |

## Run on your Nano25

```bash
scp cockpit-eicas.elf root@<nano25-ip>:/root/
ssh root@<nano25-ip> "chmod +x /root/cockpit-eicas.elf && /root/cockpit-eicas.elf"
```

## Stop

`Ctrl+C` in the SSH session, or `pkill cockpit-eicas`.

## Want to build it yourself?

The Cockpit EICAS source is part of the Fusion SDK Starter package.
Download the SDK to compile your own variants — see the SDK download
section.
