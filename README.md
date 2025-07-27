# NeuroAssistAI

# 🧬 NeuroAssistAI — Diagnosing Minds with Machines

> _“Where Machine Learning Meets Medicine”_  
> Powered by Deep Learning, Built for Neurologists, and Inspired by Real-World Clinical Needs.

🎯 Live Demo: [Visit App →](https://neuroassistai.vercel.app/)  
📂 Dataset: [Kaggle – Brain MRI](https://www.kaggle.com/datasets/masoudnickparvar/brain-tumor-mri-dataset)  
📑 Paper: [Source Research](https://onlinelibrary.wiley.com/doi/full/10.1155/2022/1830010)

---

## 🧠 Why NeuroAssistAI?

Medical professionals spend hours analyzing brain scans.  
**NeuroAssistAI** aims to reduce the diagnostic load by performing:

🔍 **Stage 1:** Detect if a brain tumor exists and classify it  
🧪 **Stage 2:** If Glioma → Predict its medical stage (I–IV) using gene mutation data

> A smart, responsive AI pipeline — built to assist, not replace.

---

## 🔧 System in Action

### 👁️‍🗨️ Tumor Classification

- 🎯 Input: Grayscale MRI image
- 🧠 Model: Custom CNN in PyTorch
- 🎯 Output: One of `No Tumor`, `Pituitary`, `Meningioma`, `Glioma`

### 🧬 Glioma Stage Prediction

- 📄 Input: Gene mutation test results (numerical)
- 🔗 Model: ANN with ReLU layers
- 📈 Output: Stage I, II, III, or IV

---

## 🧪 Want to Try It?

🚀 Try the real thing → [**Live Web App**](https://neuroassistai.vercel.app/)  
🧠 Upload your image, input gene data, get results in seconds!

---

## 🧰 Tools & Technologies

| Layer       | Stack                          |
|-------------|-------------------------------|
| Language    | Python 3.10                    |
| Backend     | FastAPI                        |
| AI Models   | PyTorch (CNN & ANN)            |
| Frontend    | React + Vercel Deployment      |
| Utils       | OpenCV, Matplotlib, NumPy      |
| Dataset     | Brain MRI Scans (Kaggle)       |

---

## 📂 What's Inside?

```bash
NeuroAssistAI/
├── main.py              # App entry
├── API.py               # FastAPI backend
├── utils.py             # Preprocessing tools
├── models/
│   ├── BTD_model.pth          # CNN (external download)
│   └── glioma_stages.pth      # ANN (included)
├── images/              # Demo/test images
├── requirements.txt     # Required libraries
└── README.md            # You're here!

---
## 👩‍💻 Project Developed By

**Afnan Shoukat**  
🎓 Bachelors in Artificial Intelligence 
📍 Islamabad, Pakistan  
📧 [afnanshoukat011@gmail.com](mailto:afnanshoukat35@gmail.com)  
🔗 [LinkedIn](https://www.linkedin.com/in/afnan-shoukat-030306267)

> Passionate about AI for healthcare, building tools that assist doctors and make a real difference.


