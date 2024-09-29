---
sidebar_position: 1
---

# OAK-1 W 

The **[OAK-1 W](https://shop.luxonis.com/products/oak-1-w?variant=44051403571423)** is an 12MP AI camera that features on-device Neural Network inferencing and Computer Vision capabilities.


## Technical Specifications
**Camera Specifications:**
12MP rolling shutter camera with DFOV of 120°

- Dimensions: 36x54.5x27.8 mm
- Weight: 53.1g


``` text title="Sensor Specifications"
DFOV/HFOV/VFOV:         120°/95°/70°
Resolution:             12MP (4056x3040)
Focus:                  FF: 60cm - ∞
Max Framerate:          60 FPS
Spectral range:         Visible only
Shutter Type:           Rolling
Sensor size:            1/2.3"
F-number:               2.8 ± 5%
Effective Focal Length:	2.75mm
Pixel size:          	1.12µm
```

## Testing
During the testing phase of our project, we encountered challenges when attempting to assess the performance of the YOLOv8 computer vision (CV) model for litter detection using the OAK-1W camera. The OAK-1W requires its own interface to access the video feed, and we discovered that it comes with its own built-in AI model, which posed difficulties when trying to integrate our existing YOLOv8 model.

After conducting some research, we utilized the [Luxonis blob convertor](https://tools.luxonis.com/) to compile a blob and JSON file which was necessary for DepthAI to decode the output from the YOLOv8 model on the OAK-1W. Unfortunately, no output was observed from the model during these attempts.

In order to verify that the model was functioning correctly, we decided to test it using the built-in webcam of a Lenovo ThinkPad. This test resulted in some detections, although they were not highly accurate. Upon further investigation, we hypothesized that the OAK-1W’s wide-angle lens might be distorting the input image, making it difficult for the model to recognize objects effectively.

<div style={{ display:'flex', justifyContent:'center', alignItems:'center', marginBottom:'20px' }}>
    <img src="../lenovo_cam_1.jpg" style={{ marginRight: '30px' }}/>
    <img src="../lenovo_cam.gif" height="319"/>
</div>

To address this, we experimented with undistorting the wide-angle image by adjusting the resolution, aiming to simulate a non-wide-angle camera. As a result, we achieved detection outcomes similar to those obtained with the Lenovo webcam, although the detections remained inaccurate.

Due to the need for image processing on the OAK-1W during the undistortion phase, we observed a significant impact on the smoothness of the video feed, which affected the frame rate. To maintain a functional level of performance, it is essential to optimize the frames per second (FPS) as much as possible while still performing undistortion and detection tasks efficiently.

Additionally, we observed that decreasing the resolution led to an increase in detections. Hence, if possible, we could reduce the resolution to force more false positive detections and increase mesh size for undistortion. 

## Summary

### Findings
1. Avoid wide angle camera since the model was not trained using it
2. If impossible, increase mesh size for undistortion
3. We can decrease resolution (isp scale) to force more false positive detections
4. CV model was not up to expectations in terms of confidence and reliability


### Limitations
1. OAK-1W's wide angle view interferes with the image recognition due to image distortion
2. The OAK-1W requires specific interfaces and configurations to use external AI models, making it harder to integrate custom models like YOLOv8.