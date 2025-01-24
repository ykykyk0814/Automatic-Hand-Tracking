# Automatic-Hand-Tracking with SAM 2
This project combines Mediapipe Hand Tracking and the Segment Anything Model (SAM 2) to track hands in a video and generate segmentation masks for each frame. The processed video is then saved with the generated masks applied.

## Features
- **Hand Detection**: Utilizes Mediapipe to detect hand landmarks in video frames.
- **Hand Segmentation**: Uses SAM 2 to generate masks for hands based on detected landmarks.
- **Video Processing**: Outputs a new video with masks applied to highlight hands in each frame.

---

## Installation

### Prerequisites
Ensure you have Python 3.9+ installed. Install the necessary dependencies as follows:

```bash
pip install mediapipe opencv-python torch torchvision torchaudio
pip install git+https://github.com/facebookresearch/segment-anything.git
```

### Model Checkpoints
Download the SAM 2 ViT-B checkpoint file:

```bash
wget https://dl.fbaipublicfiles.com/segment_anything/sam_vit_b_01ec64.pth -O sam_vit_b_01ec64.pth
```

Upload the downloaded file to the project directory.

---

## Usage

### Input Requirements
- A video file (e.g., `test.mp4`).
- The SAM 2 model checkpoint file (`sam_vit_b_01ec64.pth`).

### Running the Project

1. Clone the repository or copy the code into your environment.
2. Run the following script, replacing the input and output paths:

```python
from track_hands_with_sam2 import track_hands_with_masks

input_video = "path/to/your/video.mp4"
output_video = "path/to/output/video.mp4"
sam_checkpoint = "path/to/sam_vit_b_01ec64.pth"

track_hands_with_masks(input_video, output_video, sam_checkpoint)
```

3. The processed video with segmentation masks will be saved to `output_video`.

---

## Function Documentation

### `track_hands_with_masks`
Processes a video to detect hands and apply segmentation masks.

#### Parameters
- `input_video_path` (str): Path to the input video file.
- `output_video_path` (str): Path to save the processed video.
- `sam_checkpoint_path` (str): Path to the SAM 2 model checkpoint.
- `sam_model_type` (str, optional): Type of SAM model to use (default: `vit_b`).

---

## Example Output
The output is a video where detected hands are highlighted with segmentation masks in green. The masks are generated for every frame of the input video.

---

## Notes
- The SAM model's `weights_only=True` option is recommended to prevent unsafe deserialization of models.
- Ensure your input video and SAM checkpoint file paths are correct.
- Test the project with different SAM model types (`vit_l`, `vit_h`) for improved accuracy, depending on your application.

---

## Troubleshooting

### Common Issues
1. **`PytorchStreamReader failed reading zip archive`**:
   - Ensure the checkpoint file is downloaded correctly and matches the expected size (~357 MB).

2. **Dimension mismatch errors**:
   - Ensure the mask is expanded to match the frame dimensions using `np.repeat`.

3. **`torch.load` warnings**:
   - Use `weights_only=True` when loading SAM checkpoints to avoid unsafe deserialization.

---

## License
This project is licensed under the MIT License. Refer to the `LICENSE` file for more information.

---

## Acknowledgments
- [Mediapipe](https://google.github.io/mediapipe/) for hand detection.
- [Segment Anything](https://github.com/facebookresearch/segment-anything) by Meta AI for segmentation.

For additional support, please contact the maintainer or open an issue in the project repository.

