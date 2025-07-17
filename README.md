# Dental-OPG-Bone-Loss-Detection-using-YOLOv8-

## **Overview**

This project focuses on detecting dental conditions in Orthopantomogram (OPG) images using the YOLOv8 model from Ultralytics. The model identifies six classes of dental conditions: Healthy Teeth (HealthyT), Caries (C), Impacted Teeth (Imp), Broken Down Root (BDR), Infection (Inf), and Fractured Teeth (Ft). Implemented in a Google Colab with GPU acceleration, this codebase is designed to be reusable for users with their own OPG datasets.

## **Dataset**

- **Source**: Mendley Dataset
- **Classes**: 6 distinct dental conditions (**HealthyT**, **C**, **Imp**, **BDR**, **Inf**, **Ft**)
- **File Structure**:

```
dataset/
├── Original Dataset/
└── Augmented Dataset/
    ├── train/
    │   ├── images/      
    │   └── labels/    
    ├── valid/
    │   ├── images/       
    │   └── labels/
    └── test/
        ├── images/   
        └── labels/
```

Each image file in the images/ directories must have a corresponding label file in the labels/ directories with the same filename (e.g., image1.jpg corresponds to image1.txt). Label files contain annotations in YOLO format: `<class_id> <x_center> <y_center> <width> <height>`, with normalized coordinates. Users can adapt the code by updating the data.yaml file with their dataset paths.

## **Project Workflow**

**Data Preprocessing**

- The dataset is extracted from a zip file using the **zipfile** module and verified for correct directory structure.
- A **data.yaml** file is created to specify paths to training, validation, and test directories, along with class names.
- Images are loaded and processed for **YOLOv8** compatibility.

1. **Model Selection**

   - The **YOLOv8l** model from **Ultralytics** is used for object detection, leveraging its state-of-the-art performance for identifying dental conditions in OPG images.
   - The model is trained using **GPU** acceleration for efficient computation, with weights saved to /content/runs/train/exp/weights/best.pt.

2. **Model Evaluation**

   - The model is evaluated by comparing predicted bounding boxes and class labels against ground truth annotations.
   - Performance is assessed using **precision**, **recall**, and **mean Average Precision (mAP)**, as provided by YOLOv8’s default evaluation metrics.
   - Inference results are visualized with red bounding boxes, class labels, and confidence scores overlaid on images.

## **Installation & Usage**

### **Prerequisites**

Ensure **Python 3.8+** is installed along with the required packages:

```
pip install ultralytics torch torchvision matplotlib numpy pillow pyyaml
```

### **Running the Notebook**

1. Open the Notebook [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/14wyuCyCwAWvGYmDFW9ip0K6rlFZlTmnD)
2. Ensure your dataset is available in the working directory or update the zip_path in the notebook to point to your dataset zip file.
3. Run all cells to:
   - Install dependencies
   - Extract and verify the dataset
   - Create the data.yaml file
   - Train the **YOLOv8** model
   - Perform inference and visualize results
4. For inference, upload OPG images via **Google Colab**’s file upload widget to detect dental conditions with bounding boxes and confidence scores.

## **Notes**

- The notebook is optimized for **Google Colab** with **GPU** acceleration.
- Customize training by modifying the data.yaml file or **YOLOv8** parameters (e.g., epochs, batch size) in the notebook.
