# ClearSight: Classical Image Dehazing and Visibility Enhancement

A Digital Image Processing (DIP) project that reduces haze in outdoor photographs using the **Dark Channel Prior (DCP)** method and classical image enhancement techniques. The project estimates atmospheric light and scene transmission to reconstruct images with improved visibility, contrast, and detail.

## Overview

Haze and fog reduce image visibility by scattering light through the atmosphere. This can lower contrast, obscure distant objects, and affect the appearance of colors.

**ClearSight** implements a classical image dehazing pipeline to estimate and reduce the effects of atmospheric haze. It also compares the dehazing results with traditional image enhancement methods.

The project uses five hazy photographs as input and generates dehazed images, intermediate processing results, comparison figures, and evaluation reports.

## Objectives

- Implement the Dark Channel Prior algorithm using classical image processing.
- Estimate atmospheric light from hazy input images.
- Calculate scene transmission maps.
- Reconstruct dehazed images using atmospheric scattering principles.
- Refine transmission maps to improve the reconstructed results.
- Compare DCP dehazing with contrast stretching and gamma correction.
- Evaluate image brightness, contrast, and processing time.
- Store results systematically for analysis and reproducibility.

## Methodology

The project follows this processing pipeline:

1. **Input images:** Load the five hazy photographs.
2. **Dark channel calculation:** Estimate the dark channel using local minimum intensity information.
3. **Atmospheric light estimation:** Estimate atmospheric light from pixels with high dark-channel values.
4. **Transmission estimation:** Estimate the amount of scene radiance reaching the camera.
5. **Transmission refinement:** Apply a local mean filtering operation to smooth the estimated transmission map.
6. **Image reconstruction:** Recover the scene radiance using the estimated atmospheric light and transmission.
7. **Baseline enhancement:** Apply contrast stretching and gamma correction for comparison.
8. **Evaluation:** Measure image brightness, contrast, and processing time.
9. **Visualization:** Compare the original, dehazed, refined, and baseline-enhanced images.

## Dark Channel Prior

The Dark Channel Prior is based on the observation that, in many haze-free outdoor image patches, at least one color channel of some pixels has a very low intensity.

For an RGB image \(I\), the dark channel is defined as:

\[
I^{dark}(x)=\min_{y\in\Omega(x)}
\left(\min_{c\in\{R,G,B\}} I^c(y)\right)
\]

where:

- \(I^c(y)\) is the intensity of color channel \(c\) at pixel \(y\).
- \(\Omega(x)\) is a local neighborhood around pixel \(x\).

The atmospheric scattering model is:

\[
I(x)=J(x)t(x)+A(1-t(x))
\]

where:

- \(I(x)\) is the observed hazy image.
- \(J(x)\) is the estimated haze-free scene radiance.
- \(t(x)\) is the scene transmission.
- \(A\) is the estimated atmospheric light.

The scene radiance is reconstructed as:

\[
J(x)=\frac{I(x)-A}{\max(t(x),t_0)}+A
\]

where \(t_0\) is a lower bound on transmission that helps prevent unstable division.

These equations form the foundation of the implemented dehazing pipeline.

## Image Enhancement Baselines

ClearSight includes two baseline enhancement techniques:

### Contrast Stretching

Contrast stretching expands the intensity range of an image to improve the distinction between darker and brighter regions.

### Gamma Correction

Gamma correction adjusts image brightness using a nonlinear intensity transformation. In this project, a gamma value of 0.8 is used as a comparison setting.

These methods provide reference points for evaluating the DCP-based dehazing results.

## Evaluation

The project records the following measurements:

| Metric | Purpose |
|---|---|
| Mean brightness | Measures average grayscale intensity |
| Contrast (standard deviation) | Measures the spread of grayscale intensity values |
| Processing time | Measures the execution time of the implemented methods |

Comparison figures are generated to visually inspect the input and enhanced images.

Because the current dataset does not contain corresponding haze-free reference images, reference-based metrics such as PSNR and MSE are not used to claim restoration accuracy. Improved brightness or contrast alone also does not guarantee better dehazing quality.

## Technologies Used

- **Programming language:** Python
- **Environment:** Google Colab
- **Image processing:** NumPy and Pillow
- **Visualization:** Matplotlib
- **Data analysis:** Pandas
- **Storage:** Google Drive
- **Version control:** GitHub

The dehazing logic is implemented using classical image-processing operations rather than trained AI, machine learning, or deep learning models.

## Project Structure

```text
ClearSight_Project/
├── data/
│   ├── hazy/
│   └── clear/
├── src/
├── notebooks/
├── results/
│   ├── original/
│   ├── dark_channel/
│   ├── atmospheric_light/
│   ├── transmission/
│   ├── refined_transmission/
│   ├── dehazed/
│   ├── contrast_stretching/
│   ├── gamma_correction/
│   ├── comparisons/
│   └── metrics/
│       ├── image_evaluation.csv
│       ├── processing_times.csv
│       ├── atmospheric_light_values.csv
│       └── transmission_summary.csv
└── README.md
```

*Note: The structure above describes the intended organization. Include only folders and files that actually exist in the GitHub repository. Some CSV files may be stored in their corresponding result subfolders.*

## How to Run

1. Open the project notebook (`ClearSight_Main.ipynb`) in Google Colab.
2. Connect Google Drive if the notebook uses Drive-based storage.
3. Place the hazy input photographs in `data/hazy/`.
4. Set the project directory in the notebook to match your environment.
5. Execute the notebook cells in order, beginning with image loading and continuing through dehazing, refinement, baseline enhancement, and evaluation.
6. Inspect the generated images in `results/dehazed/` and `results/refined_transmission/`.
7. Review the evaluation and processing-time CSV files in `results/metrics/` and other result folders.

The notebook requires the dependencies used by the implementation, including NumPy, Pillow, Matplotlib, and Pandas.

## Results

The project generates:

- Dark-channel visualizations.
- Atmospheric-light estimates.
- Transmission maps and refined transmission maps.
- Dehazed images using the DCP method.
- Refined dehazed images.
- Contrast-stretched and gamma-corrected images.
- Image comparison figures.
- CSV reports containing evaluation measurements and processing times.

The degree of improvement depends on the input image, haze density, scene content, and accuracy of the estimated atmospheric parameters.

## Future Improvements

- Implement an edge-preserving transmission refinement technique using classical image processing.
- Evaluate the method on a larger and more diverse collection of hazy images.
- Add side-by-side comparison galleries for every input image.
- Investigate additional classical enhancement methods.
- Evaluate the results against corresponding clear reference images when available.

## Project Type

Academic project in **Digital Image Processing (DIP)**.

## Acknowledgements

This project applies the Dark Channel Prior concept for single-image dehazing and uses classical image-processing operations for implementation and evaluation.

---

**ClearSight — Classical Image Dehazing and Visibility Enhancement**

*Reducing atmospheric haze through fundamental digital image processing techniques.*
