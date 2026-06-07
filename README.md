# Real-Time UAV Person Detection and Tracking using YOLO11s + ByteTrack


## Overview

This project implements a real-time UAV based person detection and multi-object tracking pipeline.

The system combines a fine-tuned YOLO11s detector with ByteTrack tracking for detecting small persons in drone videos.


## Pipeline


Drone Video Frames

↓

YOLO11s-1280 Detector

↓

ByteTrack Multi Object Tracking

↓

Person IDs + Trajectories



## Dataset

Dataset:

VisDrone2019-MOT


Used categories:

- pedestrian
- people


The dataset was converted into YOLO format for detector fine-tuning.



## Experiments


### Detector Benchmarking

Compared:

- YOLOv8
- YOLO11
- RT-DETR


Input resolutions:

- 640
- 960
- 1120
- 1280



## Fine Tuning

Selected model:

YOLO11s @ 1280 resolution


Training:

- Transfer learning from COCO weights
- AdamW optimizer
- Mixed precision training
- Early stopping



## Tracking

Compared:

- ByteTrack
- BoT-SORT
- BoT-SORT with camera motion compensation


ByteTrack provided the best speed-performance balance.



## Results


| Model | Tracker | FPS | MOTA | IDF1 | Precision | Recall |
|-|-|-|-|-|-|-|
|YOLO11s Base|ByteTrack|27.05|0.264|0.338|0.746|0.419|
|YOLO11s Fine Tuned|ByteTrack|26.48|0.293|0.395|0.667|0.618|


## Improvement

Fine tuning improved:

- Recall: 0.419 → 0.618
- IDF1: 0.338 → 0.395

while maintaining real-time speed.



## Deployment

The final model was exported to ONNX format.


ONNX Runtime + ByteTrack:

- Latency: 43.8 ms
- FPS: 22.83



## Demo

Base YOLO11s tracking:

demo/YOLO11s_Base_ByteTrack.mp4


Fine tuned YOLO11s tracking:

demo/YOLO11s_FT_ByteTrack.mp4



## Requirements


Install dependencies:


pip install -r requirements.txt

