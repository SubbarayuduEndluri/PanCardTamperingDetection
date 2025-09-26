# PAN Card Tampering Detection

**Author:** Subbarayudu Endluri
**Registration No:** 229X1A3234
**College:** G. Pulla Reddy Engineering College, Kurnool
**Email:** [subbarayuduendluri1230@gmail.com](mailto:subbarayuduendluri1230@gmail.com)

---

## Project Overview

This project detects possible tampering in PAN card images by comparing an *original* and a *suspected/tampered* image using Structural Similarity Index (SSIM) and image-difference-based contour detection. The pipeline highlights regions of change and outputs a similarity score to help conclude whether a PAN card is likely tampered.

## Key Features

* Compare two images (original vs tampered) using SSIM.
* Visualize grayscale images, difference map and highlight suspected tampered regions using bounding boxes.
* Streamlit demo app for easy upload and visualization of results.
* Resizing and pre-processing to handle different image dimensions.

## Technologies & Libraries

* Python 3.8+
* OpenCV (`opencv-python`)
* Pillow (`Pillow`)
* scikit-image (`scikit-image` for SSIM)
* Matplotlib (`matplotlib`) — for plotting in notebooks
* Streamlit (`streamlit`) — for building the web UI
* pyngrok / localtunnel (optional) — for exposing the Streamlit app while testing

## Files in the Repository

* `Pan_Card_Tampering_Detection.ipynb` — Colab notebook with code, visualizations and instructions.
* `app.py` — Streamlit application to upload images and view results (included in the notebook as commented code).
* `README.md` — (this file) project description and usage.
* `requirements.txt` — list of Python dependencies (optional: generate from environment).

## Installation

### 1. Local / virtual environment (recommended)

```bash
# create and activate a virtual environment (Linux / macOS)
python3 -m venv venv
source venv/bin/activate

# (Windows)
# python -m venv venv
# venv\Scripts\activate

# install packages
pip install opencv-python Pillow streamlit scikit-image matplotlib
```

Optional (for remote sharing while testing):

```bash
pip install pyngrok localtunnel
```

### 2. Google Colab

Open `Pan_Card_Tampering_Detection.ipynb` in Colab and run the cells. Colab already allows `files.upload()` for interactive testing.

## Usage

### Notebook (Colab)

1. Upload both the **original** and **suspected/tampered** PAN card images when prompted.
2. The notebook will convert the images to grayscale, resize if needed, compute SSIM, and display the original, tampered and difference images.
3. The notebook also shows bounding boxes around regions that differ between the two images (using thresholding + contour detection).

### Streamlit App (app.py)

1. Save the `app.py` file (there is a full example in the notebook).
2. Run locally:

```bash
streamlit run app.py
```

3. The app UI lets you upload both images and will display:

   * Original image
   * Tampered image
   * Difference image (SSIM map)
   * Both images with bounding boxes marking detected changed regions
   * SSIM similarity score and a short conclusion message

Optional: to expose the app publicly while testing you can use `localtunnel` or `pyngrok`:

```bash
# example with localtunnel (installed via npm):
# npx localtunnel --port 8501

# or with pyngrok (Python):
from pyngrok import ngrok
ngrok.connect(8501)
```

## How it Works (Short)

1. Convert both images to grayscale.
2. Resize the tampered image to the original's size if dimensions differ.
3. Compute SSIM (Structural Similarity Index) between the two grayscale images. SSIM returns a score in [-1, 1] (normally between 0 and 1 for images) and a difference map.
4. Convert the SSIM difference map to an 8-bit image and apply thresholding (Otsu or adaptive) to get a binary mask of changed regions.
5. Find contours on the binary mask, then draw bounding rectangles on both original and tampered images to highlight suspicious regions.

## Interpreting Results

* **SSIM ≈ 1.0** — Images are nearly identical (likely untampered).
* **SSIM > 0.9** — Highly similar; minor differences may be due to scanning, compression, or lighting.
* **0.7 < SSIM ≤ 0.9** — Noticeable differences; investigate manually (possible minor tampering or large format/scan differences).
* **SSIM ≤ 0.7** — Significant differences; likely tampering or entirely different documents.

> These thresholds are empirical — fine-tune for your dataset and expected imaging conditions.

## Tips to Improve Robustness

* Pre-align images using feature matching (ORB / SIFT) if rotation/translation exists.
* Use illumination normalization or histogram matching to reduce false positives caused by lighting differences.
* Use OCR (Tesseract) to extract text fields and compare textual similarity in addition to pixel-based detection.
* Use deep-learning based forgery detection models for more challenging tampering (splicing, copy-move, GAN edits).

## Example Commands (from the notebook)

* Install packages (Colab cell):

```python
!pip install opencv-python pillow streamlit scikit-image
```

* Run Streamlit app locally:

```bash
streamlit run app.py
```

## Contributing

Contributions are welcome. If you want to add features (better pre-processing, OCR comparison, or a model-based tampering detector), please open an issue or submit a pull request.

## Acknowledgements & References

* `scikit-image` — Structural Similarity Index (SSIM) implementation
* OpenCV documentation — image processing utilities
* Streamlit — for the web UI

---

## Contact

If you have questions or want to collaborate, contact: **[subbarayuduendluri1230@gmail.com](mailto:subbarayuduendluri1230@gmail.com)**

*README generated for upload to GitHub. If you want a shorter/longer version, or a README with badges (e.g., build / license / python versions), tell me and I will update it.*
