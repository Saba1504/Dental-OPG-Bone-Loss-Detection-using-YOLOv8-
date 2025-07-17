# Dental-OPG-Bone-Loss-Detection-using-YOLOv8-

This project uses YOLOv8 to detect **bone loss in dental X-ray images (OPG images)**. The dataset was sourced from Roboflow and includes annotations for various dental conditions, but the model is trained specifically to detect **bone loss**.

---

## 📁 Dataset

- **Source:** [Roboflow: dadad-rvg](https://universe.roboflow.com/arshs-workspace414141/dadad-rvg/dataset/5)
- **Classes Focused On:** `bone loss` (Other classes in dataset were ignored for this project)
- **Structure:**
dadad_dataset/
├── train/
├── valid/
├── test/
└── data.yaml


---

## 🤖 Model Selection & Rationale

We chose **YOLOv8n (nano)** as our object detection model for the following reasons:

- **Lightweight and fast**: Ideal for quick experimentation and inference.
- **Pretrained weights**: Accelerates training time and boosts performance on small datasets.
- **Accurate and efficient** for real-time object detection tasks.
- **Scalable**: Easy to switch to larger models (YOLOv8s, m, l, x) if needed.

---

## 🏗️ Training Configuration

| Parameter        | Value        |
|------------------|--------------|
| Model            | YOLOv8n      |
| Epochs           | 50           |
| Image Size       | 640x640      |
| Batch Size       | 16           |
| Optimizer        | SGD          |
| Learning Rate    | 0.01         |
| Validation Split | 20%          |

---

## 📊 Evaluation Metrics

After training, the model was evaluated using standard object detection metrics:

| Metric       | Score |
|--------------|-------|
| **mAP@0.5**   | 0.74  |
| **Precision** | 0.70  |
| **Recall**    | 0.65  |
| **F1 Score**  | 0.67  |

---

## ❌ Why Some Metrics Are Below Expectation

### 🔻 Issue: Low Recall
- The model missed several cases of bone loss, likely due to:
- Small training set size
- Complex image patterns
- Class imbalance

### 🔻 Issue: Moderate Precision
- Some false positives are detected, possibly due to:
- Similar-looking features (e.g., shadows, fillings)
- Imperfect annotations in the dataset

---

## ✅ Suggestions to Improve Results

- **Data Augmentation**: Flip, rotate, and contrast adjustments to increase data diversity.
- **More Epochs**: Train for 100–200 epochs to improve learning.
- **Use a Bigger Model**: Try `yolov8m` or `yolov8l` for better accuracy.
- **Clean Annotations**: Ensure labels are precise and consistent.
- **Transfer Learning**: Start with pretrained weights on medical datasets.

---

## 🧪 Inference Example

You can test an X-ray image using:

```bash
!yolo task=detect mode=predict model=runs/detect/train/weights/best.pt source=/path/to/image.png conf=0.5
