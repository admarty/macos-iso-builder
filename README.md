# macOS Installer ISO Builder with GitHub Actions

Automatically download official macOS installers from Apple and create bootable `iso` or `dmg` images using GitHub Actions.

**Supported formats:**
* **ISO** – true DVD-format compatible with **Proxmox VE**, **QEMU**, **VirtualBox**, and **VMware**
* **DMG** – For creating bootable USB drives

## Workflows Available

### 1. Recovery ISO (Recommended)
Creates a lightweight recovery ISO that downloads macOS during installation.
* **Faster** – Completes in ~2-10 minutes
* **Best for** – Most virtualization use cases

### 2. Full Installer image
Creates a complete offline installer image (~5-16GB).
* **Slower** – Takes 20-60 minutes to build
* **Best for** – Offline installations or when you need the complete installer

> [!Note]
> Due to GitHub Actions usage limits, please use the **Recovery ISO** workflow unless you specifically need an offline installer. 
> 
> **Already have a macOS VM?** You can create full installer ISOs locally using [Create_macOS_ISO.command](https://github.com/LongQT-sea/OpenCore-ISO/blob/main/Create_macOS_ISO.command).

---

## Usage

1. **Fork** this repository.
2. Go to the **Actions** tab in your forked repository.
3. Click the green button **"I understand my workflows, go ahead and enable them"**.
4. Select the **"Build macOS Installer ISO image"** workflow.
5. Click the **"Run workflow"** button.
6. Configure the workflow inputs:

   * **macOS version** – Choose a version (*Sequoia*, *Sonoma*, etc.).
   * **Image format** – Choose `iso` for Virtual Machines or `dmg` for bootable USB drives.
   * **Specific version** *(optional)* – Enter a version like `15.6.1`, or leave blank for the latest.
7. Click the green **"Run workflow"** button to start the build.
8. Wait for the workflow to complete (this may take 15-60 minutes).
9. Open the completed workflow run and scroll to the **Artifacts** section.
10. Download the artifact (e.g., `macOS-Sequoia-15.6.1-ISO`).
   > [!Tip]
   > Enable [Cloudflare WARP](https://one.one.one.one/) for faster downloads.
11. Extract the ZIP file to get your `.iso` or `.dmg` file.

---

> [!Note]
> By default, the artifact is kept for 3 days. You can change this in the workflow YAML file.

> [!Tip]
> * For best performance, use a macOS VM on **Proxmox VE** with iGPU or dGPU passthrough.
> * Installing macOS on Proxmox VE with [LongQT-sea/OpenCore-ISO](https://github.com/LongQT-sea/OpenCore-ISO) is recommended.
> * For Intel GVT-d iGPU passthrough, see [LongQT-sea/intel-igpu-passthru](https://github.com/LongQT-sea/intel-igpu-passthru).

## Legal Notice
This tool downloads macOS images directly from Apple's servers.
Users are responsible for complying with Apple's Software License Agreement.