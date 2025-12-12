# MAPS-Glioma: Modality-Specific Augmentation and Tissue-Adaptive Postprocessing for Robust Glioma Segmentation

**Team Tanzania**

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/)
[![PyTorch](https://img.shields.io/badge/PyTorch-1.12+-ee4c2c.svg)](https://pytorch.org/)

## Authors

- **Ayomide B. Oladele¹** [ORCID: 0009-0002-2883-5459]  
- Helena Machibya²³  
- Mariam Kaoneka⁴  
- Frederick Lyimo⁵  
- Debora Hoza²  
- Immaculata Kafumu²  
- Idris Olalekan⁶  
- Jeremiah Fadugba⁷  
- Dong Zhang⁸  
- Aondona Iorumbu⁹  
- Raymond Confidence¹⁰¹¹  
- Dr. Nicephorus Rutabasibwa¹²  
- Ugumba M. Kwikima²¹²  

### Affiliations

¹ Medical Artificial Intelligence Laboratory (MAI Lab), Lagos, Nigeria  
² Teneke Regional Referral Hospital, Tanzania  
³ Muhimbili University of Health and Allied Sciences (MUHAS), Tanzania  
⁴ Mwananyamala Regional Referral Hospital, Tanzania  
⁵ Muhimbili National Hospital, Tanzania  
⁶ PublicaAI, Nigeria  
⁷ University of Ibadan, Nigeria  
⁸ Muhimbili Orthopedic & Neurosurgery Institute, Tanzania  
⁹ Montreal Neurological Institute, McGill University, Canada  
¹⁰ Department of Biomedical Engineering, McGill University, Canada  
¹¹ Department of Electrical and Computer Engineering, University of British Columbia, Canada  
¹² Teneke Regional Referral Hospital, Tanzania  

---

## Abstract

Gliomas are the most frequent primary tumors affecting the central nervous system (CNS). In Sub-Saharan Africa (SSA), gliomas are associated with high mortality due to late-stage presentation and limited access to advanced imaging. Most existing brain tumor segmentation models fail to generalize to SSA populations because of lower-quality MRI scans and distinct tumor characteristics.  

**MAPS-Glioma** is a deep learning framework that integrates **modality-specific augmentation** and **tissue-adaptive postprocessing** on an optimized 3D U-Net architecture. Using the BraTS-Africa 2025 dataset, the model achieves robust segmentation of glioma subregions with Dice scores of **0.75 (ET)**, **0.73 (TC)**, and **0.87 (WT)**. This work aims to improve diagnostic accuracy and reduce health disparities in SSA.

---

## Keywords

`BraTS` · `3D U-Net` · `Convolutional Neural Network` · `Deep Learning` · `Glioma` · `MRI` · `Segmentation` · `Low-resource`

---

## Table of Contents

- [Repository Structure](#repository-structure)
- [Installation](#installation)
- [Usage](#usage)
- [Results](#results)
- [Citation](#citation)
- [License](#license)
- [Acknowledgments](#acknowledgments)

---

## Repository Structure

```
MAPS-Glioma-SSA/
│
├── README.md                # Project description and instructions
├── LICENSE                  # MIT License
├── .gitignore               # Ignore unnecessary files
├── requirements.txt         # Python dependencies
│
├── data/
│   ├── raw/                 # Raw MRI scans (not stored in repo)
│   ├── processed/           # Preprocessed MRI data (if shareable)
│   └── README.md            # Dataset instructions
│
├── notebooks/               # Exploratory analysis and visualizations
│
├── src/
│   ├── __init__.py
│   ├── data_processing.py   # Preprocessing and augmentation
│   ├── model.py             # 3D U-Net implementation
│   ├── train.py             # Training pipeline
│   ├── inference.py         # Inference and postprocessing
│   └── utils.py             # Helper functions
│
├── experiments/
│   └── config.yaml          # Hyperparameters and training settings
│
├── results/
│   ├── figures/             # Plots and segmentation examples
│   └── metrics.csv          # Dice and Hausdorff metrics
│
├── checkpoints/             # Trained model weights
│
└── docs/
    └── figures/             # Architecture diagrams and pipeline figures
```

> ⚠️ **Note:** Raw MRI data may contain patient-sensitive information. Store it externally and follow `data/README.md` instructions to download securely.

---

## Installation

### Prerequisites

- Python 3.8+
- CUDA-capable GPU (recommended)
- 16GB+ RAM

### Setup

```bash
# Clone repository
git clone https://github.com/Team-Tanzania/MAPS-Glioma-SSA.git
cd MAPS-Glioma-SSA

# Create virtual environment
python -m venv venv
source venv/bin/activate   # Linux/macOS
# venv\Scripts\activate    # Windows

# Install dependencies
pip install -r requirements.txt
```

---

## Usage

### 1. Prepare the Dataset

Follow instructions in `data/README.md` to organize MRI scans in the correct format.

### 2. Preprocessing and Augmentation

```bash
python src/data_processing.py --input data/raw --output data/processed
```

### 3. Train the Model

```bash
python src/train.py --config experiments/config.yaml
```

### 4. Run Inference and Postprocessing

```bash
python src/inference.py --model checkpoints/best_model.pth --input data/test
```

### 5. Evaluate Results

Metrics (Dice, Hausdorff95) are automatically saved in `results/metrics.csv`.

---

## Results

| Tumor Subregion      | Dice Score   | Hausdorff95 (mm) |
|----------------------|--------------|------------------|
| Enhancing Tumor (ET) | 0.75 ± 0.22  | 11.62 ± 13.68    |
| Tumor Core (TC)      | 0.73 ± 0.25  | 13.97 ± 13.12    |
| Whole Tumor (WT)     | 0.872 ± 0.17 | 8.86 ± 8.04      |

> **Key Findings:** MAPS-Glioma demonstrates robust segmentation of the whole tumor and significant improvement in challenging subregions (ET and TC) for SSA MRI data, addressing the unique characteristics of lower-resource imaging environments.

### Sample Segmentation Results

![Sample Segmentation](docs/figures/sample_segmentation.png)
*Example segmentation showing ET (red), TC (blue), and WT (green) overlaid on T1ce MRI.*

---

## Citation

If you use this repository, please cite:

```bibtex
@inproceedings{oladele2025maps,
  title={MAPS-Glioma: Modality-Specific Augmentation and Tissue-Adaptive Postprocessing for Robust Glioma Segmentation},
  author={Oladele, Ayomide B and Machibya, Helena and Kaoneka, Mariam and others},
  booktitle={BraTS-Africa Challenge},
  year={2025}
}
```

---

## License

This project is licensed under the MIT License. See [LICENSE](LICENSE) for details.

---

## Acknowledgments

We thank the **BraTS-Africa Challenge** organizers and collaborating hospitals in Tanzania for providing access to MRI datasets. This project is supported by the **Medical Artificial Intelligence Laboratory (MAI Lab)** and regional referral hospitals across Tanzania.

Special thanks to:
- Muhimbili University of Health and Allied Sciences (MUHAS)
- Teneke Regional Referral Hospital
- Mwananyamala Regional Referral Hospital
- Muhimbili National Hospital
- Montreal Neurological Institute, McGill University

---

## Contributing

We welcome contributions! Please feel free to submit a Pull Request. For major changes, please open an issue first to discuss what you would like to change.

---

## Contact

**Ayomide B. Oladele**  
Medical Artificial Intelligence Laboratory (MAI Lab)  
Email: [aoladele@smu.edu](mailto:aoladele@smu.edu)  
ORCID: [0009-0002-2883-5459](https://orcid.org/0009-0002-2883-5459)

---

## Disclosure of Interests

The authors have no competing interests to declare that are relevant to the content of this project.

---

**⭐ If you find this work useful, please consider starring the repository!**
