# EM48 Fiji Workflow

A Fiji plugin for the original DAPI/NeuN/EM48 RGB-overlay workflow, using Cellpose-SAM and the original measurement and Excel-export behavior.

**[Download EM48 Workflow 0.1.3](https://github.com/jadenjinnn/em48-fiji-workflow/releases/download/v0.1.3/EM48_Workflow-0.1.3.jar)**

[Release page, installation guide and checksums](https://github.com/jadenjinnn/em48-fiji-workflow/releases/tag/v0.1.3)

## 1. Download the plugin

Click **Download EM48 Workflow 0.1.3** above. No GitHub account is needed.

Alternatively, open this repository's **Releases**, select **v0.1.3**, expand **Assets**, and download **EM48_Workflow-0.1.3.jar**. Choose the JAR file, not the automatically generated source-code ZIP or TAR files. Keep the JAR intact; do not unzip or double-click it.

## 2. Prepare Fiji

1. Use [Fiji](https://imagej.net/software/fiji/) with **Java 21 or newer**. This is required for the complete Cellpose-SAM workflow.
2. In Fiji, open **Help > Update...**, then **Manage update sites**.
3. Enable **Fiji-Cellpose** and **ResultsToExcel**. Close the update-site manager, apply the changes in the updater, and restart Fiji.
4. Confirm that **Cellpose-SAM...**, **Auto Local Threshold**, and **Read and Write Excel** are available. If Auto Local Threshold is missing, follow its [installation instructions](https://imagej.net/plugins/auto-local-threshold).

The first Cellpose-SAM run may download its Python environment and model weights, so allow internet access and extra setup time. The model used by this workflow is `cpsam_v2`.

## 3. Install the downloaded JAR

1. Close Fiji.
2. Copy **EM48_Workflow-0.1.3.jar** into the **plugins** folder inside your Fiji installation.
3. Remove any older `EM48_Workflow-*.jar` from that folder so only one version is installed.
4. Start Fiji. The plugin should appear under **Plugins > EM48 > EM48 Macro Compatibility Workflow**.

To update later, replace the old EM48 Workflow JAR with the new release and restart Fiji.

## 4. Run the workflow

1. Save and close other images, and save/clear ROI Manager and Results before starting.
2. Choose **Plugins > EM48 > EM48 Macro Compatibility Workflow**.
3. Select one **24-bit RGB overlay TIFF, with a single image plane**, and choose an output folder.
4. Leave the label-shuffling checkbox **unchecked** to preserve the original workflow options and saved settings.
5. Let processing finish without editing or closing the workflow images.

The plugin creates a separate run folder containing Excel workbooks, table evidence, masks, ROI files and diagnostics. Input files are read without changing them. As in the original macro, an early exit when too few eligible puncta remain can produce evidence without Excel workbooks.

For another run in the same Fiji session, save/close the previous images and clear ROI Manager/Results first.

### Input and compatibility

The workflow is designed for the original **DAPI/NeuN/EM48 RGB overlays and filename conventions**. It preserves filename-based worksheet routing and sets the scale to **0.16 micrometres per pixel**. Use images prepared for that workflow; arbitrary images, stacks or different filename conventions may not produce meaningful results.

The optional shuffle-disabled variant changes ROI order and can change order-dependent measurements. Leave its checkbox unchecked for the original behavior.

## If the run is slow or fails

If the plugin menu is missing, check that the JAR is in the `plugins` folder of the Fiji installation you actually opened, then restart Fiji. If a dependency command is missing, repeat the update-site steps above.

If processing fails or runs slowly, keep the generated run folder, especially `diagnostics/diagnostics.json` and `diagnostics/diagnostics.log`, plus any Fiji error message. These report the last reached stage, software versions, memory observations and actual Cellpose device when observed. Record your operating system, RAM and graphics card when reporting the issue. Review logs for personal file paths before sharing them publicly.

The existing `torchversion=cpu` configuration uses a CPU-only PyTorch build on Windows/Linux, even though GPU use is requested. It can use Apple MPS on a supported Mac. This release preserves those settings. A minimum RAM requirement has not been established for this combined workflow; increasing Fiji's heap does not directly increase Python/GPU memory.

## Verified release

The scientific settings and formulas are unchanged. Testing covered three supplied images: 136 macro regression checks and 10 strict old/new comparisons passed. The complete workflow measured 203 to 165 seconds on the tested M1 Max / 32 GB Mac. This is a local measurement, not a speed guarantee for other computers.

Official dependency information:

- [Fiji-Cellpose](https://imagej.net/plugins/fiji-cellpose)
- [ResultsToExcel update site](https://sites.imagej.net/ResultsToExcel/)
- [Auto Local Threshold](https://imagej.net/plugins/auto-local-threshold)
