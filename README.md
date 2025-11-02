# macOS Installer ISO Builder with GitHub Actions

Automatically download official macOS installers from Apple and create bootable `iso` or `dmg` images using GitHub Actions.

**Supported formats:**
* **ISO** – True DVD format compatible with **Proxmox VE**, **QEMU**, **VirtualBox**, and **VMware**
* **DMG** – For creating bootable macOS installer USB drive on Windows/Linux with `dd`, `BalenaEtcher`, `Rufus`

**Workflows available:**
* **macOS Recovery ISO (Recommended)** – Lightweight recovery image (build takes ~2-10 min) • Best for virtualization  
* **macOS Full Installer** – Complete offline installer (build takes ~20-60 min, 5-16GB) • Best for offline use

> [!NOTE]
> Due to GitHub Actions usage limits, use the **Build macOS Recovery ISO** workflow unless you specifically need an offline installer.
> 
> Already have a macOS **virtual machine?** Create full installer ISOs locally on your VM using [Create_macOS_ISO.command](https://github.com/LongQT-sea/OpenCore-ISO/blob/main/Create_macOS_ISO.command).

---

## Usage

1. **Fork** this repository.
2. Go to the **Actions** tab in your forked repository.
3. Click the green button **"I understand my workflows, go ahead and enable them"**.
4. Select the **"Build macOS Installer ISO/DMG image"** workflow.
5. Click the **"Run workflow"** button.
6. Configure the workflow inputs:

   * **macOS version** – Choose a version (*Sequoia*, *Sonoma*, etc.).
   * **Image format** – Choose `iso` for virtual machines or `dmg` for bootable USB drives.
   * **Specific version** *(optional)* – Enter a version like `15.6.1`, or leave blank for the latest.
7. Click the green button **"Run workflow"** to start the build.
8. Wait for the workflow to complete (this may take 15-60 minutes).
9. Open the completed workflow run and scroll to the **Artifacts** section.
10. Download the artifact (e.g., `macOS-Sequoia-15.6.1-ISO`).
   > [!Tip]
   > Enable [Cloudflare WARP](https://one.one.one.one/) for faster downloads.
11. Extract the ZIP file to get your `.iso` or `.dmg` file.

> [!NOTE]
> By default, artifacts are kept for 3 days. You can change this in the workflow YAML file.

> [!TIP]
> * For best performance, use a macOS VM on **Proxmox VE** with iGPU or dGPU passthrough.
> * Install macOS on Proxmox VE using [LongQT-sea/OpenCore-ISO](https://github.com/LongQT-sea/OpenCore-ISO).
> * For Intel GVT-d iGPU passthrough, see [LongQT-sea/intel-igpu-passthru](https://github.com/LongQT-sea/intel-igpu-passthru).

---

## Known Issues
You may occasionally encounter `hdiutil: couldn't eject "disk4" - Resource busy`. If this occurs, simply re-run the workflow.

## Legal Notice
This tool downloads macOS images directly from Apple's servers. Users are responsible for complying with Apple's Software License Agreement.
