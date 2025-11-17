## macOS Installer Image Builder – No Mac Required

* Generate bootable macOS installer images directly from Apple's servers via GitHub Actions.
* Includes intelligent file size optimization to produce the smallest possible installer images.

**Supported formats:**
* **ISO** – True DVD format compatible with **Proxmox VE**, **QEMU**, **VirtualBox**, and **VMware**
* **DMG** – Create bootable macOS installer USB drives on Windows with [Rufus](https://rufus.ie/en/#download) or on Linux with **`dd`**

**Available workflows:**
* **macOS Recovery ISO (Recommended)** – Lightweight recovery image (build takes ~2-5 min) • Best for virtualization
* **macOS Full Installer** – Complete offline installer (build takes ~20-60 min, 5-18GB) • Best for offline use

> [!IMPORTANT]
> * Use the **"Build macOS Recovery ISO image"** workflow unless you really need an offline installer.
> * GitHub-hosted runners are a free public resource — please use them responsibly.
> * Already have a macOS VM? Build macOS Installer ISO inside your VM with [Create_macOS_ISO.command](https://github.com/LongQT-sea/OpenCore-ISO/blob/main/Create_macOS_ISO.command)

---

## Usage

1. **Fork** this repository.
2. Go to the **Actions** tab in your forked repository.
3. Click the green **"I understand my workflows, go ahead and enable them"** button.
4. Select the **"Build macOS Installer ISO/DMG image"** or **"Build macOS Recovery ISO image"** workflow.
5. Click the **"Run workflow"** button.
6. Configure the workflow inputs:

   * **macOS version** – Choose a version (*Sequoia*, *Sonoma*, etc.).
   * **Image format** – Choose `iso` for virtual machines or `dmg` for bootable USB drives.
7. Click the green **"Run workflow"** button to start the build.
8. Wait for the workflow to complete (this may take 20-60 minutes).
9. Open the completed workflow run and scroll to the **Artifacts** section.
10. Download the artifact (e.g., `macOS-Sequoia-15.7.2-ISO`).
> [!TIP]
> Enable [Cloudflare WARP](https://one.one.one.one/) for faster downloads.
11. Extract the ZIP file to get your `.iso` or `.dmg` file.

---

> [!TIP]
> To create a bootable macOS installer USB drive on Windows:
> 1. Open [Rufus](https://rufus.ie/en/#download)
> 2. Click **SELECT**, change the filter to **"All files"**, then select your `.dmg`
> 3. Click **START**
> 4. Optional: After flashing the `dmg` image to the USB drive with Rufus, there will be free/unallocated space remaining on the USB drive. Use Disk Management to create a new FAT32 partition and place your EFI there if needed.

> [!NOTE]
> By default, artifacts are kept for 5 days. You can change this in the workflow YAML file.

> [!TIP]
> * For best performance, use a macOS VM on **Proxmox VE** with iGPU or dGPU passthrough.
> * Install macOS on Proxmox VE using [LongQT-sea/OpenCore-ISO](https://github.com/LongQT-sea/OpenCore-ISO).
> * For Intel GVT-d iGPU passthrough, see [LongQT-sea/intel-igpu-passthru](https://github.com/LongQT-sea/intel-igpu-passthru).

---

## Legal Notice
This tool downloads macOS images directly from Apple's servers. Users are responsible for complying with Apple's Software License Agreement.