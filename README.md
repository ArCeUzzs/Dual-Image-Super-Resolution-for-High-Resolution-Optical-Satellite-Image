# Dual-Image-Super-Resolution-for-High-Resolution-Optical-Satellite-Image
This project implements a dual-input super-resolution network that enhances low-resolution (LR) satellite images into high-resolution (HR) outputs using concatenation-based feature fusion and an EDSR backbone.
The model is built and trained in PyTorch using the Proba-V dataset, which provides multi-temporal low-resolution satellite imagery with corresponding high-resolution references.

## Overview

This project targets the problem of enhancing the spatial resolution of satellite images captured at different times. Since high-res satellites are costly and limited, we leverage **multiple low-resolution inputs** captured over time to reconstruct the corresponding high-resolution image.

This approach is especially useful for missions like **Proba-V**, where the trade-off between spatial and temporal resolution limits imagery quality.

---

## Articles & Documentation

I’ve written a series of Medium blogs that explain this project step-by-step — from dataset preparation to building the model, training it, and visualizing results.

You can read the full journey here:

*  [Part 1: Dataset Creation & Preprocessing](https://medium.com/@Phineouse/dual-image-super-resolution-for-high-resolution-optical-satellite-imagery-data-preprocessing-605fe123152e)
  *Covers how the Proba-V satellite dataset was normalized, filtered, and restructured for dual-image SR training.*

*  [Part 2: Building the Model Architecture (EDSR + Fusion)](https://medium.com/@Phineouse/dual-image-super-resolution-for-high-resolution-optical-satellite-imagery-model-building-3aa1a58993d1)
  *Explains the PyTorch model architecture including the use of EDSR blocks, concatenation fusion, and PixelShuffle.*

*  [Part 3: Training, Evaluation (PSNR), and Inference](https://medium.com/@Phineouse/dual-image-super-resolution-for-high-resolution-optical-satellite-imagery-data-loader-class-and-f256e2679114)
  *Discusses training strategy, metrics, loss functions, and how to visualize and interpret the results.*
  
   All concepts are explained clearly with examples, visuals, and reasoning, so don’t worry if you’re new to this!

---

## Dataset
* [Main dataset PROBAV](https://drive.google.com/file/d/1BAGjd5ScCXNF2Y6ffBUopUnctqVhLq8J/view)
* [Preprocessed and final dualsr dataset ](https://kelvins.esa.int/proba-v-super-resolution/data/)

This project uses a preprocessed version of the **Proba-V Super-Resolution Dataset**. The structure is as follows:

```

dual\_sr\_dataset/
├── train/
│   ├── low\_res/
│   │   ├── imgsetXXXX\_LR0.png
│   │   ├── imgsetXXXX\_LR1.png
│   └── high\_res/
│       ├── imgsetXXXX\_HR.png
├── test/
│   ├── low\_res/
│   └── high\_res/

```

Each sample consists of:
- `LR0`: Low-res image at time t
- `LR1`: Low-res image at time t+1
- `HR`: Ground truth high-res image

---

## Model Architecture

The model combines dual inputs using **channel-wise concatenation** after feature extraction and processes the merged tensor through an **EDSR-style backbone** for refinement.
![Model](https://github.com/ArCeUzzs/Dual-Image-Super-Resolution-for-High-Resolution-Optical-Satellite-Image/blob/main/Architecture.png)


## Evaluation Metrics

The performance is evaluated using:

- **PSNR (Peak Signal-to-Noise Ratio)**

Higher values indicate better reconstruction.

---

## Results

Example: Dual inputs, model output, and ground truth comparison.
## 🔍 Sample Output

Here’s an example of how the model enhances resolution:

![Sample Output](https://github.com/ArCeUzzs/Dual-Image-Super-Resolution-for-High-Resolution-Optical-Satellite-Image/blob/main/outputSHOW.jpg)


> Sample outputs and intermediate visualizations are stored in the `sr_visualization/` directory.

---

## References

* [EDSR Paper (CVPR 2017)](https://arxiv.org/abs/1707.02921)
* [Proba-V Dataset](https://kelvins.esa.int/proba-v-super-resolution/)
* [PixelShuffle Docs](https://pytorch.org/docs/stable/generated/torch.nn.PixelShuffle.html)

---

