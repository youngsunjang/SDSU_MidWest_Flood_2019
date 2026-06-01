# SDSU Midwest Flood Dataset 2019

This repository provides the **SDSU Midwest Flood Dataset 2019**, a benchmark dataset composed of true-color satellite imagery from the 2019 Midwest USA flooding event. Each image is paired with a binary mask indicating flooded areas.

The dataset is intended for flood detection and semantic segmentation research using satellite imagery.

---

## Important Update

The Hugging Face version of this dataset has been revised to provide **segmentation-ready image-mask pairs**.

Each sample now contains:

- `image`: RGB satellite image
- `mask`: binary flood mask image
- `file_name`: original image filename
- `mask_file_name`: corresponding mask filename

The corrected Hugging Face version contains **500 image-mask pairs**. The previous Hugging Face viewer displayed 1,000 rows because the original `Image/` and `Mask/` folders were interpreted as separate image-folder classes.

For most users, we recommend loading the dataset directly from Hugging Face using the `datasets` library.

---

## Load the Dataset from Hugging Face

```python
from datasets import load_dataset
import numpy as np

dataset = load_dataset("youngsun05/SDSU_MidWest_Flood_2019")

sample = dataset["train"][0]

image = sample["image"]   # PIL RGB image
mask = sample["mask"]     # PIL binary mask image

print(image.mode, image.size)
print(mask.mode, mask.size)

mask_array = np.array(mask.convert("L"))
mask_array = (mask_array > 0).astype("uint8")

print(mask_array.shape)
print(np.unique(mask_array))
```

Expected output:

```text
RGB (700, 700)
L (700, 700)
[0 1]
```

The original mask image uses pixel values `0` for non-flooded areas and `255` for flooded areas. The example above converts the mask into a binary array with values `0` and `1`.

Hugging Face Dataset Page:  
https://huggingface.co/datasets/youngsun05/SDSU_MidWest_Flood_2019

---

## Example Notebook

A starter notebook is available for loading and visualizing the dataset:

- [`load_and_visualize.ipynb`](./notebooks/load_and_visualize.ipynb): Load the dataset from Hugging Face, inspect image-mask pairs, visualize masks, and create simple overlays.

---

## Dataset Contents

- Images: true-color satellite imagery
- Masks: binary masks for flooded areas
- Number of image-mask pairs: 500
- Image size: 700 × 700 pixels
- Mask values: 0 for non-flooded areas and 255 for flooded areas
- States covered: Iowa, Kansas, Montana, Nebraska, and South Dakota
- Images per location: 10

The original dataset archive contains two folders:

```text
Dataset.zip
├── Image/
│   ├── anomaly-1-IA_1.png
│   ├── anomaly-1-IA_2.png
│   └── ...
└── Mask/
    ├── label_anomaly-1-IA_1.png
    ├── label_anomaly-1-IA_2.png
    └── ...
```

For example:

```text
Image/anomaly-1-IA_1.png
Mask/label_anomaly-1-IA_1.png
```

---

## Download the Original Dataset Archive

The original zip file is also available through Google Drive:

[Download Dataset via Google Drive](https://drive.google.com/file/d/1igApdCt7QOYH7L76iMnBZkz_rvt9Pyaz/view?usp=sharing)

For semantic segmentation experiments, we recommend using the Hugging Face version because it provides explicit `image` and `mask` columns.

---

## Paper

If you use this dataset in your research or project, please cite the following paper:

> **A Novel Dataset for Flood Detection Robust to Seasonal Changes in Satellite Imagery**  
> *Youngsun Jang, Dongyoun Kim, Chulwoo Pack, and Kwanghee Won*  
> Presented at the **ACM RACS 2024** conference, Pompei, Italy, November 5–8, 2024.

[Download PDF of the paper](./Paper.pdf)  
[arXiv link](https://arxiv.org/abs/2507.23193)

> **Note**: Although this paper was presented at ACM RACS 2024, the session was not published in the official proceedings. Therefore, this GitHub repository, the Hugging Face dataset page, and the arXiv version serve as the official references.

---

## How to Cite

Please use the following BibTeX entry if you use this dataset or paper in your work:

```bibtex
@misc{jang2024midwestflood,
  title={A Novel Dataset for Flood Detection Robust to Seasonal Changes in Satellite Imagery},
  author={Youngsun Jang and Dongyoun Kim and Chulwoo Pack and Kwanghee Won},
  year={2024},
  note={Presented at ACM RACS 2024. Available at \url{https://github.com/youngsunjang/SDSU_MidWest_Flood_2019}, \url{https://huggingface.co/datasets/youngsun05/SDSU_MidWest_Flood_2019}, and \url{https://arxiv.org/abs/2507.23193}},
}
```

---

## License

This dataset is distributed under the **CC-BY-4.0 License**, allowing sharing and adaptation with appropriate credit.
