This repository attempts to implement the CVPR 1999 paper (Statistical Color Models with Application to Skin Detection)



### 1. **Model Definition (`SkinColorModel` class)**

A 3D histogram (RGB) is used to estimate the probability of a pixel being skin or non-skin. The model consists of:

- `skin_hist`, `non_skin_hist`: Count histograms.
- `skin_prob`, `non_skin_prob`: Normalized histograms (probability estimates).
- Binning logic to reduce RGB from 256 levels to `bins` levels (e.g., 32).

**Functions:**

- `add_skin_sample(image)`: Adds skin pixel counts to histogram, ignoring white pixels.
- `add_non_skin_sample(image)`: Adds all pixels to non-skin histogram.
- `compute_probabilities()`: Normalizes histograms to convert to probability distributions.
- `classify_image(image, threshold)`: For each pixel, computes the ratio of skin/non-skin probability. If above `threshold`, pixel is classified as skin.

---

### 2. **Data Loading**

- `load_images_from_dir(directory)`: Loads all `.png`, `.jpg`, `.jpeg` files in a directory.

---

### 3. **Training Phase (`main()`)**

- Loads and processes images from `train_skin/`:
  - Extracts **skin pixels** (non-white).
  - Constructs a **non-skin version** by extracting white regions only and adds to non-skin model.
- Builds histograms for both classes.
- Converts count histograms to probabilities.

---

### 4. **Testing Phase**

- For each image in `test/`:
  - Classifies each pixel using histogram ratio.
  - Saves the segmented output (skin regions preserved, others white) to `results/`.

---

## 🧪 Example Use

1. Put your training images with skin-marked regions (rest white) in `train_skin/`.
2. Place test images in `test/`.
3. Run:

```
python main.py
