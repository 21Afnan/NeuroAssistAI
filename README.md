<div align="center">

<img src="https://capsule-render.vercel.app/api?type=waving&color=0:1A0B2E,50:4A1D7A,100:B388FF&height=210&section=header&text=NeuroAssistAI&fontSize=54&fontColor=FFFFFF&fontAlignY=36&desc=Reproducing%20deep-learning%20research%20for%20brain%20tumour%20diagnosis&descSize=16&descAlignY=58" width="100%" alt="NeuroAssistAI"/>

<p>
  <img src="https://img.shields.io/badge/PyTorch-EE4C2C?style=for-the-badge&logo=pytorch&logoColor=white" alt="PyTorch"/>
  <img src="https://img.shields.io/badge/FastAPI-009688?style=for-the-badge&logo=fastapi&logoColor=white" alt="FastAPI"/>
  <img src="https://img.shields.io/badge/OpenCV-5C3EE8?style=for-the-badge&logo=opencv&logoColor=white" alt="OpenCV"/>
  <img src="https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white" alt="Vercel"/>
  <img src="https://img.shields.io/badge/License-MIT-B388FF?style=for-the-badge" alt="MIT License"/>
</p>

**[Live demo](https://neuroassistai.vercel.app/)** · [Source paper](https://onlinelibrary.wiley.com/doi/full/10.1155/2022/1830010) · [Dataset](https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset)

</div>

---

## What this project is

A [2022 study on brain tumour classification and glioma stage prediction](https://onlinelibrary.wiley.com/doi/full/10.1155/2022/1830010) described its method but published no code. **NeuroAssistAI** is our rebuild of that work from the paper alone, done as course research for Artificial Neural Networks and Computer Vision at NUML, and then turned into a working web application that a non-specialist can use.

It follows the paper's two-step idea:

1. **Is there a tumour, and what kind?** A CNN reads an MRI scan and sorts it into glioma, meningioma, pituitary or no tumour.
2. **If it is a glioma, how advanced is it?** A separate neural network predicts the glioma stage from the patient's gene-mutation results.

> Built to support a clinician's reading of a scan, never to replace it.

## Results

| Part | Result |
|---|---|
| Glioma stage prediction (ANN on gene-mutation data) | 83% accuracy |
| Multi-class tumour ROI detection (YOLOv9, reproducing an [IEEE 2024 method](https://ieeexplore.ieee.org/document/10721653)) | 97% accuracy |
| Lightweight transfer-learning extension | CNN from scratch 92% to 94%, fine-tuned ResNet-18 96% to 97% (see [TumorSense-AI](https://github.com/21Afnan/TumorSense-AI)) |

## How it works

```
MRI image ──> grayscale, 224 x 224, normalise ──> CNN (3 conv blocks) ──> glioma | meningioma | pituitary | no tumour
                                                                  │
                                                     glioma? ─────┘
                                                        │
             gender, age + 7 gene mutations ──> ANN (3 hidden layers) ──> glioma stage
```

**Tumour classifier** (`models/TumorModel.py`): three convolution and max-pool blocks (32, 64, 128 filters) followed by two fully connected layers (512, 256) and a four-class output.

**Glioma stage model:** a feed-forward network with ReLU layers (100, 50, 30 units). Its nine inputs are gender, age at diagnosis and seven mutation flags: IDH1, TP53, ATRX, PTEN, EGFR, CIC and PIK3CA.

**Guidance for other results:** for meningioma, pituitary and no-tumour predictions the API returns a short precaution note.

## API

`API.py` serves both models with FastAPI.

| Method | Endpoint | Input | Returns |
|---|---|---|---|
| `POST` | `/predict-image` | MRI image file | `tumor_type`, plus a precaution note or a request for mutation data if it is a glioma |
| `POST` | `/predict-glioma-stage` | JSON: `gender`, `age`, `idh1`, `tp53`, `atrx`, `pten`, `egfr`, `cic`, `pik3ca` | `glioma_stage` |
| `GET` | `/` | | health check |

## Run it locally

```bash
pip install torch torchvision fastapi uvicorn pillow python-multipart
uvicorn API:app --reload
```

The glioma stage weights (`models/glioma_stages.pth`) are in the repo. The CNN weights (`models/BTD_model.pth`) are too large for GitHub; place the file in `models/` before starting the API. `main.py` runs the same pipeline from the command line on an image in `images/`.

## Project structure

```
NeuroAssistAI/
├── API.py               # FastAPI service for both models
├── main.py              # command-line pipeline
├── utils.py             # mutation input and precaution helpers
├── models/
│   ├── TumorModel.py    # CNN and ANN definitions
│   └── glioma_stages.pth
└── images/              # sample MRI scans for each class
```

## Tech stack

| Layer | Technology |
|---|---|
| Models | PyTorch (CNN, ANN), YOLOv9, ResNet-18 |
| Data | Kaggle Brain Tumor MRI dataset, gene-mutation records |
| Backend | FastAPI, Uvicorn |
| Frontend and hosting | Web app on Vercel, Ngrok for the model API |
| Tools | OpenCV, NumPy, Matplotlib |

## Disclaimer

This is a research and learning project. It is not a medical device and must not be used to make clinical decisions.

---

<div align="center">

Team course project by **Afnan Shoukat** and classmates, BS Artificial Intelligence, NUML Islamabad

<a href="mailto:afnanshoukat35@gmail.com"><img src="https://img.shields.io/badge/Email-afnanshoukat35%40gmail.com-B388FF?style=for-the-badge&logo=gmail&logoColor=white&labelColor=1A0B2E" alt="Email"/></a>
<a href="https://www.linkedin.com/in/afnanshoukat"><img src="https://img.shields.io/badge/LinkedIn-Afnan%20Shoukat-B388FF?style=for-the-badge&logo=linkedin&logoColor=white&labelColor=1A0B2E" alt="LinkedIn"/></a>
<a href="https://github.com/21Afnan"><img src="https://img.shields.io/badge/GitHub-21Afnan-B388FF?style=for-the-badge&logo=github&logoColor=white&labelColor=1A0B2E" alt="GitHub"/></a>

Released under the [MIT License](LICENSE).

</div>
