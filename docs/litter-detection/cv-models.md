---
sidebar_position: 1
---

# Computer Vision

We were given 3 pretrained Computer Vision, CV models of YOLOv8 and ResNet18 by Changi Airport Group for object detection and classification respectively.YOLOv8 can perform both object detection and classification, making it versatile for tasks that require identifying and classifying multiple objects in an imagesimultaneously. However, ResNet18 is primarily optimized for image classification, focusing on recognizing a single object or class per image, while YOLOv8 excels at detecting and localizing objects alongside classification, offering a broader range of use cases.


## Technical Specifications
**Trained dataset**
- TODO: add any info on the dataset CAG gave us


## Model Evaluation
### YOLOv8
Two YOLOv8 models were trained using the **Trash Annotations in Context (TACO) dataset** and an **in-house Changi Airport litterate dataset**. During preliminary testing with the Intel RealSense camera on both datasets, distinct performance differences were observed:

- The model trained on the **TACO dataset** showed poor object detection but performed relatively better in object classification tasks.
- The model trained on the **litterate dataset** exhibited fairly accurate object detection but lacked object classification capabilities.
Based on these findings, the litterate dataset model was selected for object detection in the final implementation. However, the TACO-based model remains under consideration for its ability to detect and classify litter at a minimum of **20 FPS**.

Additionally, confidence interval comparisons between the models revealed that the **TACO dataset model** provided an average confidence of **20% for detected objects**, while the **litterate dataset model** achieved an average confidence level of **70% for detected litter**.

### ResNet18
The **ResNet18** model was designed to be integrated with the **YOLOv8** model for litter classification. Upon detecting an object, the corresponding image would be cropped and transformed into a tensor input for classification by ResNet18.

During testing, we quickly observed that **ResNet18** performed poorly in terms of speed, achieving a maximum of **3 FPS** per classification, significantly slower than YOLOv8. Despite this, we chose to proceed with the ResNet18 model for classification purposes and optimized the implementation by running the model in parallel using threads, improving performance while maintaining classification accuracy of at least **50% on average**.

TODO: Add images on classification done in combined2

<div style={{ display:'flex', justifyContent:'center', alignItems:'center', marginBottom:'20px' }}>
    <img src="../IMG_5467.gif" height="319" style={{ marginRight: '30px' }}/>
    <img src="../video.gif" height="319"/>
</div>

### Model Retraining
TODO: Add on the fact that we need to upload the images detected to AWS for retraining of the resnet and yolov8 models.

## Summary

### Findings
1. YOLOv8 Litter Detection Model (trained on the litterate dataset) provided accurate object detection with an average confidence level of 70% and ran at 20 FPS.
2. TACO Dataset Model detected and classified objects at 20 FPS, but with lower object detection accuracy and an average confidence level of 20%.
3. ResNet18 Classification Model, when integrated with YOLOv8, performed at 3 FPS for classification but was successfully optimized by running in parallel using threads.
4. More testing is required to determine the validity of the other model combinations. For example, litter detection using the litterate dataset and litter classification done by the TACO dataset may be better than ResNet18 for classification.

### Limitations
1. TACO Dataset Model struggled with accurate object detection, limiting its overall performance despite better classification abilities.
2. ResNet18 suffered from slow classification speeds (3 FPS), reducing its real-time usability without optimization.
3. YOLOv8 (litterate dataset) did not perform object classification, only focusing on detection, necessitating integration with ResNet18 for classification tasks.