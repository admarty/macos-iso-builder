## Overview

A comprehensive toolkit for creating bootable macOS installer images, consisting of two main components:

1. **mkmaciso** – An automation script that uses only macOS built-in tools and commands to download and install the full macOS installer from Apple's servers into /Applications, then generate the smallest possible installer image for macOS installation.
2. **GitHub workflows** – Action workflows that run `mkmaciso` on Azure datacenter-hosted Mac minis, for users who don't have a working macOS.

## Quick Start

> [!Note]
> **New users:** Before building, open [Release page](https://github.com/LongQT-sea/mkmaciso/releases/tag/forks-list) to see if someone already built what you need!

See [Usage Guide](#usage-guide) for detailed instructions.

## Table of Contents

- [Image Format Details](#image-format-details)
- [Supported macOS Versions](#supported-macos-versions)
- [Usage Guide](#usage-guide)
- [Usage Tips](#usage-tips)
- [Requirements for mkmaciso](#requirements-for-mkmaciso)
- [Acknowledgments](#acknowledgments)
- [Legal Notice](#legal-notice)
- [License](#license)

---

## Image Format Details

The `mkmaciso` script can generate macOS installer images in two different formats, each optimized for specific use cases:

### ISO Format (Hybrid UDF/HFS)
- **Best for:** Virtual machine installations
- **Compatible with:** Proxmox VE, QEMU, VirtualBox, VMware
- **How to use:** Attach the ISO as a virtual DVD/CD drive to your VM
- **Format details:** True DVD/CD format image that can be mounted in Windows and used across all major virtualization platforms

### DMG Format (Raw Disk Image with GUID Partition Table)
- **Best for:** Creating bootable USB installation media
- **Compatible with:** Physical Mac hardware installations
- **How to use:** Flash to USB drive using [Rufus](https://rufus.ie/en/#download) (Windows) or `dd` (Linux) or `asr` (macOS)
- **Format details:** Raw disk image with GUID Partition Table, can also be converted to other virtual disk formats (VHD, VMDK) for use with virtual machines

---

## Supported macOS Versions

| Version | Codename | Year | | Version | Codename | Year |
|---------|----------|------|-|---------|----------|------|
| 10.7    | Lion     | 2011 | | 10.15   | Catalina   | 2019 |
| 10.8 | Mountain Lion | 2012 | | 11 | Big Sur | 2020 |
| 10.9 | Mavericks | 2013 | | 12 | Monterey | 2021 |
| 10.10 | Yosemite | 2014 | | 13 | Ventura | 2022 |
| 10.11 | El Capitan | 2015 | | 14 | Sonoma | 2023 |
| 10.12 | Sierra | 2016 | | 15 | Sequoia | 2024 |
| 10.13 | High Sierra | 2017 | | 26 | Tahoe | 2025 |
| 10.14 | Mojave | 2018 |

---

## Usage Guide
Two methods are available:
- [Method 1](#method-1): Run `mkmaciso` in the cloud using GitHub Action, for users who don't have a working macOS
- [Method 2](#method-2): Run `mkmaciso` locally, for users who already have macOS

### Method 1
**Available workflows:**
* **Recovery ISO (Recommended)** – Lightweight recovery image (build takes ~2-5 min) • Best for virtualization
* **Full Installer** – Complete offline installer (build takes ~10-60 min, 5-18GB) • Best for offline use

> [!TIP]
> <details>
> <summary>Click here to watch a visual guide (GIF) showing steps 1-7</summary>
>
> ![How to fork and run workflow](https://raw.githubusercontent.com/LongQT-sea/mkmaciso/main/.github/how_to_fork_and_run_workflow.gif)
>
> </details>

1. **Fork** this repository (requires a GitHub account).
2. Navigate to the **Actions** tab in your forked repository.
3. Click the green **"I understand my workflows, go ahead and enable them"** button.
4. Select the **"Build Full Installer ISO/DMG image"** or **"Build Recovery ISO image"** workflow from the left sidebar.
5. Click the **"Run workflow"** button.
6. Configure the workflow inputs:

   * **macOS version** – Choose a version (*Sequoia*, *Sonoma*, etc.).
   * **Image format** – Choose `iso` for virtual machines or `dmg` for bootable USB drives.
7. Click the green **"Run workflow"** button to start the build.
8. Wait for the workflow to complete (this may take 10–60 minutes).
9. Open the completed workflow run and scroll down to the **Artifacts** section.
10. Download the artifact (e.g., `macOS_Sequoia_15.7.3.iso`).
11. Extract the ZIP file to get your `.iso` or `.dmg.img` file. The file is now ready to use!
> [!NOTE]
> By default, artifacts are kept for 7 days. You can change this in the workflow YAML file.

---

### Method 2

If you already have access to a working macOS system or macOS virtual machine, you can run the script directly using Terminal.app:

**Quick run** (replace 'tahoe' with your desired version):
```bash
curl -s https://raw.githubusercontent.com/LongQT-sea/mkmaciso/main/mkmaciso | bash -s tahoe
```

**Download the script first, then run with parameters:**
```bash
curl -O https://raw.githubusercontent.com/LongQT-sea/mkmaciso/main/mkmaciso
chmod +x mkmaciso

./mkmaciso --help
```

**Interactive mode:**
```bash
./mkmaciso
```

---

## Usage Tips

### For Virtual Machines (ISO Format)
> [!NOTE]
> Attach the ISO image as a virtual CD/DVD drive to your VM.

> [!TIP]
> **Proxmox VE Users:**
>
> For the best macOS VM performance on Proxmox VE:
> - Enable iGPU or dGPU passthrough for near-native graphics performance
> - Consider using [LongQT-sea/OpenCore-ISO](https://github.com/LongQT-sea/OpenCore-ISO) for streamlined macOS installation
> - For Intel integrated graphics passthrough, see [LongQT-sea/intel-igpu-passthru](https://github.com/LongQT-sea/intel-igpu-passthru)

### For USB Drives (DMG Format)
> [!TIP]
> After flashing, there will be free/unallocated space remaining on the USB drive. Use Disk Management to create a new FAT32 partition and place your EFI folder there if needed.

> [!CAUTION]
> When flashing under Linux with `dd`, double-check the target device! `dd` will overwrite without confirmation.

---

## Requirements for mkmaciso

| Requirement | Details |
|-------------|---------|
| **OS** | Minimum macOS 10.9 (macOS 11+ recommended) |
| **Architecture** | Intel (x86_64) recommended; Apple Silicon supported with limitations |
| **Disk Space** | 20-40 GB temporary; final image varies |
| **Internet** | Required for downloading from Apple servers |
| **Privileges** | Administrator (sudo) access required |

---

## Acknowledgments

- **Apple** — For macOS and the software update infrastructure
- **[Mavericks Forever](https://mavericksforever.com/)** — For documenting the macOS 10.9 recovery server protocol
- **[InsanelyMac community](https://www.insanelymac.com/forum/topic/338810-create-legit-copy-of-macos-from-apple-catalog/)** — For research on direct Apple CDN downloads

---

## Legal Notice

This tool downloads macOS images directly from Apple's official servers. Users are responsible for complying with [Apple's Software License Agreement](https://www.apple.com/legal/sla/). macOS is a trademark of Apple Inc.

---

## License

This project is licensed under the GPLv3 License. See [LICENSE](LICENSE) for details.
