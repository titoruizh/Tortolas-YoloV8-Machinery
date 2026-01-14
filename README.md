# 🚜 Mining Asset Detection: YOLOv8 on Drone Orthomosaics
### Automated Monitoring at Las Tórtolas Tailings Facility

![Python](https://img.shields.io/badge/Python-3.9+-blue?logo=python)
![YOLOv8](https://img.shields.io/badge/Model-YOLOv8-green)
![GeoAI](https://img.shields.io/badge/Focus-GeoAI-orange)
![Status](https://img.shields.io/badge/Status-Completed-success)

## 📋 Project Overview

This project implements a **Computer Vision pipeline** to automate the detection and segmentation of mining assets (Heavy Machinery, Light Vehicles, and Piping) within the **Las Tórtolas Tailings Dam (Anglo American)**.

Using high-resolution drone orthomosaics, the system moves beyond simple detection, converting pixel-based inference into **geospatial vectors** ready for GIS analysis (ArcGIS/QGIS/Civil3D).

---

## 📸 Model Performance

<p align="center">
  <img src="https://github.com/user-attachments/assets/4a0b0dea-186f-4cb5-9269-ac2af27f00d3" alt="Heavy Machinery Detection" width="45%">
  &nbsp; &nbsp;
  <img src="https://github.com/user-attachments/assets/9f5d177a-06ba-452d-acc3-c92e17018b5f" alt="Light Vehicle Detection" width="45%">
</p>
<p align="center">
  <em>Figure 1: Validation Batch Results. Left: Heavy Machinery. Right: Light Vehicles (Camionetas).</em>
</p>

---

## 🛠️ The Workflow (GeoAI Pipeline)

The challenge with mining imagery is the scale. Standard YOLO cannot process a 5GB TIFF file. I developed a workflow to handle geospatial data:

1.  **Data Ingestion:** High-resolution Drone Orthomosaics (GeoTIFF/ECW).
2.  **Tiling Strategy:** Automated script to slice massive rasters into $640 \times 640$ chips ensuring geospatial reference is preserved.
3.  **Labeling:** Custom dataset annotation using **Roboflow** (Classes: *Trucks, Excavators, Piping*).
4.  **Training:** Fine-tuning **YOLOv8** (Ultralytics) on GPU for instance segmentation/detection.
5.  **Geo-Inference:**
    * Inference on new orthomosaics.
    * **Pixel-to-Coordinate Transformation:** Mapping bounding boxes/masks back to UTM coordinates (WGS84 / Local Grid).
    * **Vector Export:** Output as `.shp` or `.geojson` for Mining Operations.

## 🚀 Key Features

* **Multi-Class Detection:** Specialized in distinguishing between mining service trucks ("Camionetas") and heavy operation machinery.
* **Infrastructure Monitoring:** Capable of detecting piping lines ("Tuberías") for maintenance inspection.
* **GIS Integration:** The final output is not just an image, but a spatial layer compatible with **Global Mapper** and **Civil3D**.

## 💻 Tech Stack

* **Core:** Python, PyTorch
* **Vision:** YOLOv8 (Ultralytics), OpenCV
* **Geospatial:** GDAL, Rasterio, Shapely, Geopandas
* **Data Ops:** Roboflow

---

## 📊 Results & Impact

* Automated inventory of assets in vast areas (Tailings Dam).
* Reduced time for operational heatmap generation.
* Improved safety monitoring by detecting vehicle presence in restricted zones.
