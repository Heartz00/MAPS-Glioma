# Dataset Instructions

## BraTS-Africa 2025 Dataset

This directory contains instructions for organizing the BraTS-Africa 2025 MRI dataset for training the MAPS-Glioma model.

## Directory Structure

```
data/
├── raw/
│   ├── BraTS-AFR-00001/
│   │   ├── BraTS-AFR-00001_t1.nii.gz
│   │   ├── BraTS-AFR-00001_t1ce.nii.gz
│   │   ├── BraTS-AFR-00001_t2.nii.gz
│   │   ├── BraTS-AFR-00001_flair.nii.gz
│   │   └── BraTS-AFR-00001_seg.nii.gz
│   ├── BraTS-AFR-00002/
│   │   └── ...
│   └── ...
│
└── processed/
    ├── train/
    ├── val/
    └── test/
```

## Dataset Acquisition

### Official BraTS-Africa Challenge

1. Register for the BraTS-Africa 2025 Challenge at: [https://www.synapse.org/brats2025](https://www.synapse.org/)
2. Accept the data use agreement
3. Download the training and validation datasets
4. Extract the files to `data/raw/`

### File Naming Convention

Each patient case should have the following files:
- `{CASE_ID}_t1.nii.gz` - T1-weighted MRI
- `{CASE_ID}_t1ce.nii.gz` - T1-weighted contrast-enhanced MRI
- `{CASE_ID}_t2.nii.gz` - T2-weighted MRI
- `{CASE_ID}_flair.nii.gz` - FLAIR MRI
- `{CASE_ID}_seg.nii.gz` - Ground truth segmentation (training only)

## Preprocessing

After downloading the data, run the preprocessing script:

```bash
python src/data_processing.py --input data/raw --output data/processed
```

This script will:
1. Verify data integrity
2. Perform skull stripping (optional)
3. Normalize intensities per modality
4. Crop to foreground
5. Split into train/val/test sets
6. Generate data statistics

## Data Statistics

After preprocessing, the following statistics will be saved in `data/processed/stats.json`:

- Total number of cases
- Train/val/test split sizes
- Intensity statistics per modality (mean, std, percentiles)
- Tumor region statistics (volume, location)

## Label Definitions

The segmentation masks use the following label convention:

- **Label 0**: Background
- **Label 1**: Necrotic and non-enhancing tumor core (NCR)
- **Label 2**: Peritumoral edematous/invaded tissue (ED)
- **Label 4**: GD-enhancing tumor (ET)

### Tumor Regions

These labels are combined to define three nested regions:

- **Enhancing Tumor (ET)**: Label 4
- **Tumor Core (TC)**: Labels 1 + 4
- **Whole Tumor (WT)**: Labels 1 + 2 + 4

## Data Quality Checks

Run the quality check script to identify potential issues:

```bash
python src/utils.py --check-data data/raw
```

This will flag:
- Missing modalities
- Corrupted files
- Misaligned scans
- Unusual intensity ranges
- Empty segmentation masks

## Privacy and Ethics

⚠️ **Important**: This dataset contains sensitive medical information.

- **Do not** share raw data publicly
- **Do not** commit data files to Git repositories
- Follow HIPAA and local data protection regulations
- Use anonymized case IDs only
- Obtain necessary IRB approvals before publication

## Troubleshooting

### Issue: Missing files

**Solution**: Verify all required modalities are present for each case. Remove cases with missing data or use imputation techniques.

### Issue: Memory errors during preprocessing

**Solution**: Reduce batch size in `src/data_processing.py` or process cases sequentially.

### Issue: Inconsistent image dimensions

**Solution**: The preprocessing script handles resampling. Check `config.yaml` for `resample_resolution` settings.

## Citation

If you use the BraTS-Africa dataset, please cite:

```bibtex
@article{brats-africa2025,
  title={The Brain Tumor Segmentation (BraTS) Challenge 2025: Glioma Segmentation in Sub-Saharan Africa},
  author={BraTS Challenge Organizers},
  journal={arXiv preprint},
  year={2025}
}
```

## Contact

For dataset-specific questions, contact the BraTS-Africa challenge organizers:  
[brats-challenge@example.org](mailto:brats-challenge@example.org)

For repository-specific questions, open an issue on GitHub.
