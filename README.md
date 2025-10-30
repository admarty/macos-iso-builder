# macOS Installer ISO Builder with GitHub Actions

* Uses GitHub Actions to download official macOS installers directly from Apple servers and create true DVD-format macOS installer ISO files.
* The generated ISOs are compatible with **Proxmox VE**, **QEMU**, **VirtualBox**, and **VMware**.

## 📦 Usage

### Running the Workflow

1. **Fork** this repository.
2. Go to the **Actions** tab in your forked repository.
3. Select the **“Build macOS Installer ISO image”** workflow.
4. Click the **“Run workflow”** button.
5. Set the inputs:

   * **macOS version** – Choose a version (*Sequoia*, *Sonoma*, etc.).
   * **Specific version** *(optional)* – Enter a version like `15.7.1`, or leave blank to use the latest.
6. Click **“Run workflow”** again to start the build.

## 📥 Downloading the ISO

After the workflow finishes:

1. Open the completed workflow run.
2. Scroll to the **Artifacts** section at the bottom.
3. Download the ISO artifact (e.g. `macOS-Sequoia-15.7.1-ISO`).
4. Extract the ZIP file to get the `.iso`.

> [!Tip]
>
> * For best performance, use a macOS VM on **Proxmox VE** with iGPU or dGPU passthrough.
> * Installing macOS on Proxmox VE with [LongQT-sea/OpenCore-ISO](https://github.com/LongQT-sea/OpenCore-ISO) is recommended.
> * For Intel GVT-d iGPU passthrough, see [LongQT-sea/intel-igpu-passthru](https://github.com/LongQT-sea/intel-igpu-passthru).
