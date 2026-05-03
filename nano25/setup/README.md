# Nano25 Fusion Setup (Tier 1)

Provision your DE25-Nano board to run Fusion. This is a **one-time
two-step setup** that turns a factory Nano25 into a Fusion-capable
device.

After completing both steps, your Nano25 boots directly into the
default Fusion demo. From that point you can also drop additional
ELF demos via SCP without re-flashing — see [`../catalog/`](../catalog/).

## Why two steps?

The Nano25 (Altera Agilex 5 SoC) has two distinct compute domains:

| Domain | What lives there | Provisioning |
|---|---|---|
| **FPGA fabric** | Fusion GPU (custom RTL/IP) | Bitstream programmed into on-board QSPI flash |
| **HPS (ARM)** | Linux + Fusion userspace + apps | OS image flashed onto MicroSD card |

Both must carry our content for Fusion to run. Step 1 provisions the
FPGA, step 2 provisions the HPS.

## Prerequisites

- DE25-Nano board
- 5V DC power supply (board comes with one)
- USB Type-C cable (board to your PC)
- MicroSD card, ≥ 8 GB
- MicroSD card reader/writer
- **Quartus Prime Pro v25.1.1+** (free for Agilex 5)
  with the USB Blaster III driver installed.
  See [`../vendor/DE25_Nano_Getting_Started_Guide.pdf`](../vendor/DE25_Nano_Getting_Started_Guide.pdf) §2 for installation.
- A SD-card flashing tool (Win32 Disk Imager, Rufus, or `dd` on Linux/macOS)

The Quartus Programmer requirement is intentional: Fusion targets
embedded engineers already developing on Altera FPGAs, so this tool
is part of your existing toolchain.

## Step 1 — Program the FPGA bitstream

Burns the Fusion FPGA bitstream into the Nano25's QSPI flash so it
loads automatically on every power-up.

→ See [`firmware/README.md`](firmware/README.md)

Time: ~5 minutes. One-time per board (persistent in QSPI).

## Step 2 — Flash the SD card

Writes the Linux + Fusion userspace image onto a MicroSD card.

→ See [`sdcard/README.md`](sdcard/README.md)

Time: ~15 minutes (mostly write time). One-time per card.

## After both steps

1. Insert the MicroSD into the Nano25
2. Connect the display (HDMI)
3. Power on (5V DC)
4. The default Fusion demo runs

You now have a Fusion-capable Nano25. Move on to
[`../catalog/`](../catalog/) to try additional Fusion demos without
re-flashing the SD card.

## Troubleshooting

If the Fusion demo does not appear on the display after boot:

- Check that the user LED7 is flashing (HPS booted)
- Verify the MSEL switches are set to AS mode (`001`) per the
  Terasic guide — see
  [`../vendor/DE25_Nano_Getting_Started_Guide.pdf`](../vendor/DE25_Nano_Getting_Started_Guide.pdf) §3.2
- Try the UART terminal (Putty, COM port @ 115200) to see HPS boot
  logs — see Terasic guide §5.6

If the QSPI programming (step 1) fails:

- Verify USB Blaster III appears in Windows Device Manager (JTAG
  cables → USB Blaster III)
- Re-source `program_qspi_flash/` from Quartus shell (so
  `QUARTUS_ROOTDIR` is set)
