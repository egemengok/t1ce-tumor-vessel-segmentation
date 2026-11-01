# t1ce-tumor-vessel-segmentation
Training code for the tumor (Attention U-Net) and vascular (Swin UNETR) segmentation models on contrast-enhanced T1-weighted MRI.

# Tumor and Vascular Segmentation from Contrast-Enhanced T1-Weighted MRI

This repository contains the model training code used in the following article. If you use this code, please cite:

> Cekic, E., Gok, E., Yildirim, Y., Gurbuzer, M., Hamzaoglu, C., Yilmaz, C., Olgun, O., Coban, G., Tunc, O., Katirci, I., Tatar, I., Grimm, F., Isikay, A. I., Turkoglu, M. E., Berker, M., Baskaya, M. K., Tatagiba, M. & Hanalioglu, S. Deep Learning-Based Automatic Segmentation and 3D Reconstruction of Whole-Brain Anatomy from Contrast-Enhanced T1-weighted MRI in Patients with Brain Tumors. Manuscript under review (2026).

| Notebook | Model | Task |
| --- | --- | --- |
| `vascular_segmentation_swin_unetr.ipynb` | Swin UNETR | Artery and vein segmentation |
| `tumor_segmentation_attention_unet.ipynb` | Attention U-Net | Tumor segmentation |

## Requirements

Requires a CUDA-capable GPU and PyTorch. The models were trained on an NVIDIA A100 (80 GB). The first cell of each notebook installs MONAI 1.5.2 and the remaining dependencies.

## Data

Inputs are preprocessed contrast-enhanced T1-weighted MRI volumes in NIfTI format (RAS orientation, 0.6-mm isotropic voxels, skull-stripped, N4 bias field corrected, min-max scaled to 0-255).

```
data/
  splits.json
  vascular/<subject_id>/<subject_id>_image.nii.gz
  vascular/<subject_id>/<subject_id>_label.nii.gz
  tumor/<subject_id>/<subject_id>_image.nii.gz
  tumor/<subject_id>/<subject_id>_tumor_label.nii.gz
```

`splits.json` contains three lists of subject identifiers: `train`, `validation`, and `test`. Vascular labels: 0 background, 1 artery, 2 vein. Tumor labels: 0 background, 1 tumor.

## Usage

Run the cells in order. Hyperparameters are defined in the configuration cell. Training logs, checkpoints, and test-set predictions are saved to `outputs/`.

## Author

Code written by Egemen Gok (egemengok@hacettepe.edu.tr).
