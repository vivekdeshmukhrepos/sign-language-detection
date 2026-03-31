# Sign Language Detection System

A real-time sign language detection system powered by **YOLOv5** and **Flask**. This application can detect sign language gestures from uploaded images or live camera feed, making it a valuable tool for bridging communication gaps.

![Sign Language Detection](https://img.shields.io/badge/Sign%20Language-Detection-blue)
![YOLOv5](https://img.shields.io/badge/Model-YOLOv5-green)
![Flask](https://img.shields.io/badge/Framework-Flask-lightgrey)
![Python](https://img.shields.io/badge/Python-3.8%2B-orange)

## 🌟 Features

- **Image-Based Detection**: Upload images to detect sign language gestures
- **Live Camera Detection**: Real-time detection using webcam feed
- **Modern UI**: Beautiful, responsive web interface with dark theme
- **Drag & Drop**: Easy image upload with drag and drop support
- **Base64 Encoding**: Efficient image transmission between client and server
- **High Accuracy**: Powered by state-of-the-art YOLOv5 object detection model

## 🏗️ Project Structure

```
sign-language-detection/
├── app.py                      # Main Flask application
├── requirements.txt            # Python dependencies
├── setup.py                    # Package setup file
├── Steps.txt                   # Setup instructions
├── README.md                   # This file
├── data/                       # Directory for input images
├── templates/
│   └── index.html              # Web UI template
├── SignLanguage/
│   ├── __init__.py
│   └── utils/
│       ├── __init__.py
│       └── main_utils.py       # Utility functions for image encoding/decoding
└── yolov5/                     # YOLOv5 detection model (submodule)
    ├── detect.py               # YOLOv5 detection script
    ├── weights/                # Model weights (best.pt should be placed here)
    └── runs/                   # Detection output directory
```

## 📋 Prerequisites

- Python 3.8 or higher
- pip (Python package manager)
- Git
- CUDA-compatible GPU (optional, for faster inference)

## 🚀 Installation

### 1. Clone the Repository

```bash
git clone https://github.com/vivekdeshmukhrepos/sign-language-detection.git
cd sign-language-detection
```

### 2. Install Dependencies

```bash
pip install -r requirements.txt
```

### 3. Set Up YOLOv5 Model

The YOLOv5 repository is already included as a submodule. You need to:

1. Place your trained model weights file (`best.pt`) in the `yolov5/` directory
2. Ensure the model is trained to recognize sign language gestures

### 4. Install the Package (Optional)

```bash
pip install -e .
```

## 🖥️ Usage

### Running the Application

Start the Flask server:

```bash
python app.py
```

The application will be available at: `http://localhost:8080`

### Using the Web Interface

1. **Upload an Image**:
   - Click on the upload area or drag and drop an image
   - Preview the uploaded image
   - Click "Detect Sign Language" to process

2. **Live Camera Detection**:
   - Click the "Live Camera" button in the header
   - The system will start detecting signs from your webcam feed

### API Endpoints

| Endpoint | Method | Description |
|----------|--------|-------------|
| `/` | GET | Serve the main web interface |
| `/predict` | POST | Process an image and return detection results |
| `/live` | GET | Start live camera detection |

#### `/predict` Request Format

```json
{
    "image": "<base64_encoded_image>"
}
```

#### `/predict` Response Format

```json
{
    "image": "<base64_encoded_result_image_with_detections>"
}
```

## 🛠️ Configuration

### Model Configuration

The detection parameters can be adjusted in `app.py`:

```python
os.system("cd yolov5/ && python detect.py --weights best.pt --img 416 --conf 0.5 --source ../data/inputImage.jpg")
```

- `--weights`: Path to your trained model weights
- `--img`: Input image size (default: 416)
- `--conf`: Confidence threshold for detections (default: 0.5)
- `--source`: Input source (image path, camera index, or video file)

## 📦 Dependencies

Key dependencies include:

- **Flask**: Web framework
- **Flask-CORS**: Cross-origin resource sharing
- **YOLOv5**: Object detection model
- **OpenCV**: Image processing
- **PyTorch**: Deep learning framework
- **NumPy**: Numerical computations
- **Pillow**: Image handling



### Training Your Own Model

To train a custom YOLOv5 model for sign language detection:

1. Collect and annotate your dataset with bounding boxes
2. Configure the YOLOv5 training parameters
3. Train the model using `yolov5/train.py`
4. Place the resulting `best.pt` in the `yolov5/` directory

### Troubleshooting

- **Port already in use**: Change the port in `app.py` (`app.run(host="0.0.0.0", port=8080)`)
- **Model not found**: Ensure `best.pt` is in the `yolov5/` directory
- **CUDA out of memory**: Reduce batch size or use CPU-only mode

---
