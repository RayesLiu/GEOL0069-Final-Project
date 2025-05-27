# 🌍 Surface Water Detection in the Po River Delta Using Sentinel-2 and Spectral Indices
![image](https://github.com/user-attachments/assets/3d837b11-552f-4442-b4e8-8fd030c7e12d)

This notebook demonstrates how open-access satellite data and basic machine learning techniques can be used to map water bodies in complex environments. The study focuses on the Po River Delta in Northern Italy using Sentinel-2 imagery and simple but effective classification methods.

---

## 🧠 What This Project Does

The goal of this project is to classify surface water using three well-known spectral indices and compare two classification approaches:

- **Indices used**: NDWI, SWI, and MNDWI
- **Methods used**: Simple thresholding vs. K-means clustering (k=2)
- **Target output**: A clean, binary water mask for each method + index combo

This project answers:  
**Which spectral index performs best at detecting water, and is unsupervised clustering better than simple thresholding?**

---

## 🛰 Data Source & Study Area

- **Satellite**: Sentinel-2 L2A
- **Bands used**: B03 (Green), B05 (Red Edge), B08 (NIR), B11 (SWIR1)
- **Spatial resolution**: 10–20 meters
- **Source**: [Copernicus Data Space Browser](https://dataspace.copernicus.eu/)
- **Region**: Po River Delta, Northern Italy  
  Chosen for its dense river network, dynamic land-water boundaries, and good data availability
![image](https://github.com/user-attachments/assets/7c8d8ac0-ecea-4d8e-9d55-64012f6b4ad5)
---

## 📌 Key Steps

### 1. Data Preparation
- Downloaded Sentinel-2 imagery
- Selected cloud-free scenes over the Po River Delta
- Uploaded relevant bands to Google Drive and accessed them via Colab

### 2. Preprocessing
- Read `.jp2` band files using `rasterio`
- Normalized each band (0–1 scale)
- Applied downsampling for performance
- Generated a basic cloud mask to filter noisy areas

### 3. Spectral Index Calculation
- **NDWI** = (Green - NIR) / (Green + NIR)  
- **SWI** = (Red Edge - SWIR1) / (Red Edge + SWIR1)  
- **MNDWI** = (Green - SWIR1) / (Green + SWIR1)

These indices are widely used for identifying water, each with its strengths depending on surface cover and background noise.

### 4. Classification
- **Thresholding**: Pixels > 0 are labeled as water  
- **K-means Clustering**: Uses value similarity to group into water/non-water automatically

### 5. Visualization & Evaluation
- Compared outputs visually for each method
- Plotted histograms to validate index distributions
- Evaluated clustering with:
  - Silhouette Score
  - Davies-Bouldin Index
  - Calinski-Harabasz Score
![image](https://github.com/user-attachments/assets/896632dd-798f-4627-8674-794cd8d28ceb)

### 6. Emissions Monitoring
- Tracked energy usage and CO₂ footprint using `codecarbon`

---

## 📊 Key Results

| Index  | Best Method | Notes |
|--------|-------------|-------|
| NDWI   | K-means     | Good overall, but struggles with vegetation shadows  
| SWI    | Threshold   | Noisy, prone to confusion in built-up areas  
| MNDWI  | K-means     | Best performer—precise edges, stable in mixed land use  

K-means generally outperformed thresholding due to its adaptability. Among indices, **MNDWI** consistently produced the cleanest, most accurate results.

---
## ♻️ Environmental Cost of This Project

Alongside the scientific goals of this project, sustainability and low computational impact were also considered. The entire process—from data preprocessing to classification—was performed on **Google Colab** using CPU resources only. No heavy model training or GPU computation was involved.
### 🧮 Carbon Footprint Measurement

To track the emissions generated during the workflow, we used the [`codecarbon`](https://mlco2.github.io/codecarbon/) Python package. This tool estimates the CO₂ emissions of code execution based on hardware, runtime, and data center location.

**📊 Actual Emissions Generated:**    
**Total: 0.000490 kg CO₂**

This is roughly equivalent to:
- Boiling a kettle once 🔌  
- Watching 3 minutes of HD video streaming 📺  
- Producing ~1 sheet of recycled A4 paper 📄

> By comparison, a 1-hour Zoom call emits ~0.15–1 kg CO₂ depending on setup (IEA, 2022).

## ✅ Sustainability Measures Taken

- Open-access data (Sentinel-2) — no fieldwork or travel required  
- Efficient preprocessing (downsampling, cropping)  
- No model training — only unsupervised clustering (K-means)  
- Execution via shared cloud infrastructure (Google Colab)  
- Carbon tracking embedded in the pipeline

This reinforces the idea that even when working on modest AI projects, we should strive to minimize our environmental footprint.

> 🌿 *Low emissions, high awareness: responsible AI research starts with small, intentional choices.*

---

## 💻 How to Use

### ✅ Requirements
- Google Colab
- Libraries: `rasterio`, `numpy`, `matplotlib`, `scikit-learn`, `codecarbon`

### 🚀 Instructions
1. Download Sentinel-2 data from the Copernicus Hub  
2. Upload selected bands to Google Drive  
3. Open the notebook in Colab and run cells step by step  
4. Adjust clustering settings or thresholds if desired  
5. Review visual and quantitative outputs to compare results

---

## 🧾 Files Included

- `Water_Body_Classification_in_the_Po_River_Delta_Using_Sentinel_2_and_NDWI.ipynb`: Full notebook
- Processed results and plots: NDWI, SWI, and MNDWI masks
- Histograms and cloud masks
- README for setup and context
---

## 👤 Author

**Rayes Liu**  
UCL Earth Sciences Third-Year Student | GEOL0069: AI for Earth Observation  

---

## 📚 References

- Center for Climate Change. 2023. How Salty Is the Po Delta? Machine and Deep Learning May Help Find the Answer. CMCC Foundation. https://www.cmcc.it/article/how-salty-is-the-po-delta-machine-and-deep-learning-may-help-find-the-answer.

---

> 🌐 Built with free satellite data, open tools, and a curiosity for Earth from above.
