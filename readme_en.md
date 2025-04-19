# YOLO11 Pose Drowsiness Detection

This project implements a drowsiness detection system using YOLO11 pose estimation. The system analyzes human pose from images and determines if a person is showing signs of drowsiness based on head position relative to shoulders.

## Features

- Detection of human poses using YOLO11 ONNX models
- Drowsiness detection based on head position (when head drops below shoulder level)
- Visual output with skeleton visualization and drowsiness alerts
- Support for custom models and confidence thresholds

## Requirements

- Python 3.6+
- OpenCV (`opencv-python`)
- NumPy
- ONNX Runtime (`onnxruntime`)

Install the required packages:

```bash
pip install opencv-python numpy onnxruntime
```

## Usage

The script can be run directly with default settings:

```bash
python drowsiness_yolo_pose.py
```

By default, it will:
- Use `yolo11n-pose.onnx` as the model
- Process `test.jpg` as the input image
- Save results to `drowsiness_output.jpg`

### Command-line Arguments

You can customize the execution with various command-line arguments:

```
--model        Path to the ONNX model (default: yolo11n-pose.onnx)
--image        Path to the input image (default: test.jpg)
--size         Input size for the model (default: 640)
--conf         Detection confidence threshold (default: 0.25)
--kpt-conf     Keypoint confidence threshold (default: 0.2)
--output       Path to save the output image (default: drowsiness_output.jpg)
--show         Display the result in a window
```

### Example

```bash
python drowsiness_yolo_pose.py --model yolo11n-pose.onnx --image person.jpg --show
```

## How It Works

1. **Pose Detection**: The system uses YOLO11 pose estimation to detect 17 key points on the human body (following COCO dataset keypoints definition).

2. **Drowsiness Detection Logic**: 
   - The system calculates the average Y-coordinate of head keypoints (nose, eyes, ears)
   - It also calculates the average Y-coordinate of shoulder keypoints
   - If the head position is lower than the shoulder position (i.e., head is drooping), drowsiness is detected

3. **Visual Output**:
   - Person bounding boxes are colored green (normal) or red (drowsiness detected)
   - Skeleton connections are drawn between keypoints
   - A warning message is displayed if drowsiness is detected

## Notes

- The detection accuracy depends on the quality of the input image and the performance of the YOLO11 pose model
- For optimal results, ensure the person's face and upper body are clearly visible
- The system is designed for single-image analysis; for real-time monitoring, additional code would be needed

## License

This project is available for open use. Please include appropriate attribution if you incorporate this code into your project.

## Acknowledgements

- This project utilizes YOLO11 pose estimation architecture
