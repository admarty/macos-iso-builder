## Build macOS Installer image via Github Action – No Mac Required

* Support **macOS 10.7 Lion** through **macOS 26 Tahoe** installers. 
* Download macOS installers exclusively from official Apple sources.
* Includes intelligent file size optimization to produce the smallest possible installer images.

**Supported formats:**
* **ISO** – True DVD/CD format compatible with **Proxmox VE**, **QEMU**, **VirtualBox**, and **VMware**
* **DMG** – For create bootable macOS installer USB drives on Windows with [Rufus](https://rufus.ie/en/#download) or on Linux with **`dd`**

**Available workflows:**
* **Recovery ISO (Recommended)** – Lightweight recovery image (build takes ~2-5 min) • Best for virtualization
* **Full Installer** – Complete offline installer (build takes ~10-60 min, 5-18GB) • Best for offline use

> [!IMPORTANT]
> * Use the **"Build macOS Recovery ISO image"** workflow unless you really need an offline installer.
> * GitHub-hosted runners are a free public resource — please use them responsibly.
> * If you already have macOS VM, you can build macOS ISO/DMG image using the following command (replace `tahoe` with your desired version):
```
curl -s https://raw.githubusercontent.com/LongQT-sea/macos-iso-builder/main/mkmaciso | bash -s tahoe
```

---

## Usage
> [!TIP]
> <details>
> <summary>Click here to watch a GIF showing how to complete steps 1–7</summary>
>
> ![How to fork and run workflow](https://raw.githubusercontent.com/LongQT-sea/macos-iso-builder/main/.github/how_to_fork_and_run_workflow.gif)
>
> </details>

1. **Fork** this repository (requires a GitHub account).
2. Navigate to the **Actions** tab in your forked repository.
3. Click the green **"I understand my workflows, go ahead and enable them"** button.
4. Select the **"Build macOS Installer ISO/DMG image"** or **"Build macOS Recovery ISO image"** workflow from the left sidebar.
5. Click the **"Run workflow"** button.
6. Configure the workflow inputs:

   * **macOS version** – Choose a version (*Sequoia*, *Sonoma*, etc.).
   * **Image format** – Choose `iso` for virtual machines or `dmg` for bootable USB drives.
7. Click the green **"Run workflow"** button to start the build.
8. Wait for the workflow to complete (this may take 10–60 minutes).
9. Open the completed workflow run and scroll down to the **Artifacts** section.
10. Download the artifact (e.g., `macOS_Sequoia_15.7.3.iso`).
11. Extract the ZIP file to get your `.iso` or `.dmg.img` file.

---

> [!TIP]
> After flashing the DMG image to the USB drive with [Rufus](https://rufus.ie/en/#download), there will be free/unallocated space remaining on the USB drive. Use Disk Management to create a new FAT32 partition and place your EFI folder there if needed.

> [!NOTE]
> By default, artifacts are kept for 7 days. You can change this in the workflow YAML file.

> [!TIP]
> * For best performance, use a macOS VM on **Proxmox VE** with iGPU or dGPU passthrough.
> * Install macOS on Proxmox VE using [LongQT-sea/OpenCore-ISO](https://github.com/LongQT-sea/OpenCore-ISO).
> * For Intel GVT-d iGPU passthrough, see [LongQT-sea/intel-igpu-passthru](https://github.com/LongQT-sea/intel-igpu-passthru).

---

## Legal Notice
This tool downloads macOS images directly from Apple's servers. Users are responsible for complying with Apple's Software License Agreement.
