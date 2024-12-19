---

# Vessel Detection and Distance Calculation in SAR Satellite Images

## Overview  
This project implements a deep learning-based solution to detect vessels in **Synthetic Aperture Radar (SAR)** satellite images and calculate their distances to nearby landmasses. By leveraging **YOLOv3, YOLOv4**, and **YOLOv4-tiny**, the system outputs annotated images with bounding boxes and distance labels for maritime applications such as surveillance, coastal monitoring, and search-and-rescue operations.

---

## Features  
- **Custom Dataset Creation**: Filtered and annotated a dataset of SAR satellite images.  
- **Model Training**: Trained YOLOv3, YOLOv4, and YOLOv4-tiny object detection models, achieving a **highest mAP of 82.96%**.  
- **Distance Calculation**: Implemented an algorithm to calculate **Euclidean distances** between detected ships and the nearest landmasses.  
- **Visualization**: Generated annotated outputs for interpretability and real-world usability.  

---

## Dataset  

### Source Dataset  
The original dataset was sourced from the **National Key Scientific Data Center for SAR**:  
[Original Dataset Link](https://radars.ac.cn/web/data/getData?newsColumnId=dd8bb26f-fb65-497b-8958-390951409d98&pageType=en)  

### Modified Dataset  
The dataset was manually filtered to remove noisy images and annotated to include two classes: **ship** and **land**.  
[Modified Dataset Link](https://drive.google.com/drive/folders/1G88HyBON0n9WBOzVxj0BNx2t3btvo56V?usp=sharing)  

**Final Dataset**:  
- **Size**: 2,500+ images  
- **Image Resolution**: 1200x800 pixels  
- **Annotations**: Bounding boxes in YOLO format  

---

## Results  
| Model       | Mean Average Precision (mAP) |
|-------------|-------------------------------|
| YOLOv3      | 74.82%                        |
| YOLOv4      | 82.96%                        |
| YOLOv4-tiny | 69.31%                        |

The **YOLOv4** model was chosen as the final implementation due to its accuracy.

---

## Project Structure  

```
yolov4/
│
├── backup/                       # Folder to store trained model weights
├── generate_test.py              # Script to generate test dataset
├── generate_train.py             # Script to generate train dataset
├── obj.data                      # Path configuration file for YOLOv4
├── obj.names                     # Class names for object detection
├── obj.zip                       # Zipped dataset with images and annotations
├── test.zip                      # Zipped test dataset

```

---

## Key Code Components  

The **`yolov4_distance_calculation.ipynb`** script performs the following steps:  

1. **Environment Setup**  
   - Clones and builds **Darknet** with GPU and OpenCV enabled.  
   - Downloads pretrained YOLOv4 weights.  

2. **Dataset Management**  
   - Uploads custom datasets (`obj.zip` and `test.zip`) and extracts them.  
   - Configures `obj.names`, `obj.data`, and `yolov4-obj.cfg`.  

3. **Model Training**  
   - Trains the YOLOv4 model using a custom dataset with pretrained weights (`yolov4.conv.137`).  
   - Generates **train.txt** and **test.txt** using helper scripts.

4. **Object Detection**  
   - Detects objects (ships and landmasses) using the trained YOLOv4 model.  
   - Bounding boxes are created, and centroids are calculated for ships and land areas.

5. **Distance Calculation**  
   - Implements the **Euclidean distance formula** to calculate the distance between each ship and the nearest landmass:
     ```python
     Distance = √((x_ship - x_land)² + (y_ship - y_land)²)
     ```
   - Accounts for image resolution and scaling to **real-world distances** (e.g., 5km x 5km coverage).  

6. **Visualization**  
   - Annotates detected ships and landmasses with bounding boxes and displays calculated distances on images.  
   - Outputs the results with varying color codes to indicate distance ranges.  

---

## Applications  
- **Maritime Surveillance**: Detect illegal fishing, smuggling, and unauthorized vessel activities.  
- **Environmental Monitoring**: Track vessel movements near ecologically sensitive zones.  
- **Search and Rescue**: Locate vessels in distress and provide timely intervention.

---

## Future Scope  
1. **Real-Time Monitoring**: Integrate live satellite feeds and alert systems.  
2. **Scalable Deployment**: Implement on cloud platforms for large-scale SAR data processing.  
3. **Dynamic Distance Calculation**: Adjust for real-time factors like tides and evolving coastlines.

---
