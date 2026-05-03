# Fusion Demos

Pre-built Fusion graphics demos for evaluation on Coregraphix
hardware. Customer-facing distribution: download bitstream + SD image
to provision a Fusion-capable board, then iterate via single-ELF
demos.

## Repository layout

```
fusion-demo/
├── README.md                   ← this file
├── catalog.json                ← master index (consumed by the website)
└── <target>/                   ← per-target content (currently: nano25/)
    ├── README.md               ← target-specific landing
    ├── vendor/                 ← vendor hardware documentation
    ├── setup/                  ← Tier 1: one-time provisioning
    │   ├── README.md           ← 2-step procedure (HW + SW)
    │   ├── firmware/           ← Step 1: FPGA bitstream + Quartus scripts
    │   └── sdcard/             ← Step 2: Linux + Fusion image
    └── catalog/                ← Tier 2: additional demos (single ELF each)
        ├── README.md
        └── <demo>-v<x.y>/
            ├── README.md
            └── manifest.json
```

Heavy binaries (`.jic`, `.img.gz`, `.elf`) are not committed to git;
they are distributed as **GitHub Release assets** attached to a tag
matching the asset's version. See each per-asset README for the
download location.

## Customer journey

| Tier | What | Time |
|---|---|---|
| 0 | Watch a video on the Coregraphix website | 30 sec |
| 1 | Provision your Nano25 (FPGA bitstream + Linux SD image) | ~20 min |
| 2 | Drop additional ELF demos on the provisioned Nano25 | 5 min/demo |
| 3 | Download the SDK Starter and develop your own UI | 1 h |

This repository hosts Tier 1 (`<target>/setup/`) and Tier 2
(`<target>/catalog/`).
Tier 0 (videos) lives on the Coregraphix website.
Tier 3 (SDK) lives in the
[`fusion-release`](https://github.com/cgx33/fusion-release) repository.

## How to use this repository

- **As a customer**: Browse [`nano25/setup/`](nano25/setup/) to provision
  your board, then browse [`nano25/catalog/`](nano25/catalog/) for
  additional demos. Each entry's README has step-by-step instructions
  and a link to the corresponding GitHub Release for the binary.
- **As the website**: Fetch
  [`catalog.json`](catalog.json) at runtime and render cards from it.
- **Adding a demo**: Create `<target>/catalog/<demo>-v<x.y>/` with a
  README + manifest.json, add an entry to `catalog.json`, then tag
  and create a GitHub Release with the ELF as an asset.

## Asset distribution model

| File type | Location | Reason |
|---|---|---|
| Source files (READMEs, JSON, scripts) | Tracked in git | Small, version-controlled, browsable |
| `golden_top_hps.jic` (~16 MB) | GitHub Release asset | Versioning per setup release |
| `nano25-fusion.img.gz` (~1.4 GB) | GitHub Release asset | Exceeds git size limits |
| Demo `.elf` (~1.6 MB each) | GitHub Release asset | Versioning per demo release |
