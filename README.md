# EM48 Fiji Workflow

A Fiji plugin for the original DAPI/NeuN/EM48 RGB-overlay workflow, using Cellpose-SAM and the original measurement and Excel-export behavior.

**[Download EM48 Workflow 0.1.3](https://github.com/jadenjinnn/em48-fiji-workflow/releases/download/v0.1.3/EM48_Workflow-0.1.3.jar)**

[Release page and checksums](https://github.com/jadenjinnn/em48-fiji-workflow/releases/tag/v0.1.3)

## Installation

1. Use Fiji with Java 21 or newer.
2. In Help > Update, enable the **Fiji-Cellpose** and **ResultsToExcel** update sites. Install **Auto Local Threshold** if it is missing. Apply updates and restart Fiji.
3. Download `EM48_Workflow-0.1.3.jar` and copy it into the `plugins` folder inside your Fiji installation. Remove any older EM48 Workflow JAR from that folder, then restart Fiji.
4. Confirm that **Cellpose-SAM...**, **Auto Local Threshold**, and **Read and Write Excel** are available.
5. Choose **Plugins > EM48 > EM48 Macro Compatibility Workflow**, select one 24-bit RGB overlay TIFF, and choose an output folder.

The Cellpose-SAM model is `cpsam_v2`. The first run may need to download the Python environment and model weights.

Save and close other images, and save/clear ROI Manager and Results before starting. Avoid editing or closing workflow images during processing. For another run in the same Fiji session, save/close the previous images and clear ROI Manager/Results first.

Leave the label-shuffling checkbox unchecked for the original behavior. The optional shuffle-disabled variant changes ROI order and can change order-dependent measurements.

The workflow is designed for the original DAPI/NeuN/EM48 RGB overlays and filename conventions. It preserves the original filename-based worksheet routing and sets scale to 0.16 micrometres per pixel; it is not a general-purpose arbitrary-image workflow.

## If the run is slow or fails

Keep the generated run folder, especially `diagnostics/diagnostics.json` and `diagnostics/diagnostics.log`, plus the Fiji error message. These report the last reached stage, software versions, memory observations and actual Cellpose device when observed.

The existing `torchversion=cpu` configuration uses a CPU-only PyTorch build on Windows/Linux, even though GPU use is requested. It can use Apple MPS on a supported Mac. This release preserves those settings. A minimum RAM requirement has not been established for this combined workflow; increasing Fiji's heap does not directly increase Python/GPU memory.

## Verified release

The scientific settings and formulas are unchanged. Testing covered three supplied images: 136 macro regression checks and 10 strict old/new comparisons passed. The complete workflow measured 203 to 165 seconds on the tested M1 Max / 32 GB Mac. This is a local measurement, not a speed guarantee for other computers.

Official dependency information:
- Fiji-Cellpose: https://imagej.net/plugins/fiji-cellpose
- ResultsToExcel: https://sites.imagej.net/ResultsToExcel/
- Auto Local Threshold: https://imagej.net/plugins/auto-local-threshold
