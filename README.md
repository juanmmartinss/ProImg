# Satellite Image Processing for Water Body Monitoring

## Project Overview

This project focuses on the study, analysis, and application of Image Processing (IP) techniques to perform the segmentation and monitoring of water bodies using multispectral satellite imagery.

The main objective is to develop a methodology in Python that effectively differentiates water areas from other land cover classes using spectral indices and thresholding. The final segmentation result will be rigorously validated using the **Dice Metric**.

## Repository Structure

The repository is organized into distinct folders, reflecting the project's data collection and processing phases:

| Folder/File | Content | Purpose |
| :--- | :--- | :--- |
| `guides/linked/ee-api-colab-setup.ipynb` | Google Earth Engine (GEE) Script. | This notebook contains the code used to **filter, select 20 scenes, and export** the Sentinel-2 images to Google Drive. This is the **Data Acquisition** step. |
| `02_Processing_e_Analise/` | Main Python script and Output Images. | Contains the core Python script for pre-processing, NDWI calculation, segmentation, and the **Dice Metric calculation** for validation. |
| `Raw_TIFF_Images/` | *Not included in GitHub, but the data source.* | 20 Sentinel-2 satellite images (Bands B3 and B8) exported from GEE. |
| `Final_Report.pdf` | (To be added later) | The complete report adhering to all course requirements. |

## Methodology and Technologies

### 1. Data Acquisition (GEE)

* **Script Location:** `guides/linked/ee-api-colab-setup.ipynb`
* **Source:** Sentinel-2 satellite images (COPERNICUS/S2\_SR Collection).
* **Filters:** Images filtered by Area of Interest (AOI), Date (`[Your Study Period]`), and low Cloud Cover (less than **2%**).
* **Bands Used:** **Band 3 (Green)** and **Band 8 (Near-Infrared - NIR)**, which are essential for the NDWI index.

### 2. Processing and Analysis (Python)

The processing workflow follows the mandatory project steps: **Pre-processing** and **Processing**.

| Step | Technique Applied | Brief Description |
| :--- | :--- | :--- |
| **Pre-processing** | TIFF Reading (Rasterio), Data Cleaning (Numpy). | Prepares the B3 and B8 bands for index calculation. |
| **Processing** | **NDWI Calculation** (Normalized Difference Water Index). | Application of the formula: $(Green - NIR) / (Green + NIR)$. |
| **Segmentation** | **Thresholding** (e.g., Otsu's Method). | Converts the NDWI into a binary image (0 = No Water, 1 = Water), resulting in the **Obtained Segmentation**. |
| **Validation** | **Dice Metric** (Dice Similarity Coefficient). | Compares the **Obtained Segmentation** with the **Ground Truth** (water mask from MapBiomas) to measure accuracy. A Dice value closer to 1 (100%) indicates a better result. |

## Requirements and Execution

To run the project locally (after exporting the images from GEE), the following Python libraries are required:

* `ee` (Google Earth Engine)
* `geemap`
* `numpy`
* `rasterio`
* `scikit-image` (or OpenCV)
* `scipy`

**Installation:**
```bash
pip install geemap numpy rasterio scikit-image scipy
