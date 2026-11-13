# Hybrid CNN-RNN Fusion for Enhanced Breast Cancer Detection in Early Stage

Code for the paper published in the **ARPN Journal of Engineering and Applied Sciences**, Vol. 19, No. 14 (2024), pp. 947–951.

**Paper:** [arpnjournals.com/jeas/jeas_0724_9484.htm](https://arpnjournals.com/jeas/jeas_0724_9484.htm) · **DOI:** [10.59018/072425](https://doi.org/10.59018/072425)

**Authors:** V. Krishna Sree, A. Pavan Dheeraj, S. Shyamala
Department of Electronics and Communication Engineering, VNR Vignana Jyothi Institute of Engineering and Technology, Hyderabad, India

---

## Overview

Breast cancer is one of the most common cancers in women, and early detection is key to lowering its death rate. This project classifies **breast ultrasound images** into three classes: **normal**, **benign** and **malignant**.

Most CNN-RNN approaches run the two networks in series: a CNN extracts image features and an RNN processes them afterwards. Our model instead extracts features with a **combined CNN + LSTM structure**, with an extra **ReLU + softmax** layer. The softmax layer turns each prediction into class probabilities and picks the most likely class.

The project includes:
- **A training notebook** (`BreastCancer.ipynb`) covering preprocessing, model building, training and evaluation
- **A Django web app** (`Cancer/`, `CancerApp/`) that lets you upload an ultrasound image and see the predicted class
- **The trained model** (`model/`) and **sample test images** (`testImages/`)

## Results

The hybrid model reached **99.35% accuracy** on the test set.

| Model | Accuracy |
|---|---|
| Recurrent neural network (RNN) | 63.15% |
| CNN + gated recurrent units (GRU) | 86.21% |
| 5-layer convolutional neural network (CNN) | 87.00% |
| **Proposed model (CNN + LSTM + ReLU/softmax)** | **99.35%** |

Validation accuracy levels off after about 11 epochs. The best accuracy came from a network of about 14 layers, a depth chosen by experiment.

## Dataset

This project uses the **Breast Ultrasound Images Dataset (BUSI)**: 780 ultrasound images, each with a segmentation mask, in three classes. Together that's 1,560 files, which the study split 80/20 into training and test sets:

| Label | Class | Total | Train | Test |
|---|---|---|---|---|
| 0 | Benign | 874 | 699 | 175 |
| 1 | Malignant | 420 | 336 | 84 |
| 2 | Normal | 266 | 212 | 54 |
| | **Total** | **1,560** | **1,247** | **313** |

Preprocessing steps: normalization, shuffling, and the train/test split.

> The dataset (~200 MB) is not included in this repo. Download it from [Kaggle](https://www.kaggle.com/datasets/aryashah2k/breast-ultrasound-images-dataset) and unzip it into a `Dataset/` folder containing `benign/`, `malignant/` and `normal/`.
>
> Source: Al-Dhabyani W., Gomaa M., Khaled H., Fahmy A. *Dataset of breast ultrasound images.* Data in Brief, 28, 104863 (2020). [doi:10.1016/j.dib.2019.104863](https://doi.org/10.1016/j.dib.2019.104863)

## Repository structure

```
├── BreastCancer.ipynb    # Model training and evaluation notebook
├── BreastCancer.html     # Notebook exported with all outputs and plots
├── model/                # Trained model files
├── Cancer/               # Django project settings
├── CancerApp/            # Django app (upload page + prediction)
├── testImages/           # Sample ultrasound images to try
├── manage.py             # Django entry point
├── requirements.txt      # Python dependencies
├── run.bat               # Windows helper script
└── runServer.bat         # Starts the web app on Windows
```

## How to run

**1. Install dependencies**
```bash
pip install -r requirements.txt
```

**2. Start the web app**
```bash
python manage.py runserver
```
On Windows you can double-click `runServer.bat` instead.

**3. Open** `http://127.0.0.1:8000` in your browser, upload an image from `testImages/`, and see the prediction.

**To retrain the model**, download the dataset, update the dataset path in `BreastCancer.ipynb`, and run all cells.

## Citation

If you use this work, please cite:

```bibtex
@article{sree2024hybrid,
  title   = {Hybrid CNN-RNN Fusion for Enhanced Breast Cancer Detection in Early Stage},
  author  = {Sree, V. Krishna and Dheeraj, A. Pavan and Shyamala, S.},
  journal = {ARPN Journal of Engineering and Applied Sciences},
  volume  = {19},
  number  = {14},
  pages   = {947--951},
  year    = {2024},
  doi     = {10.59018/072425}
}
```

## Disclaimer

This is a research project, not a medical device. It must not be used for real diagnosis.
