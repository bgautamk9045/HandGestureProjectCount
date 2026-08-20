# 🖐️ Finger Counter

A real-time hand gesture counter built with **Python**, **OpenCV**, and **MediaPipe** — hold up your hand to the webcam and it detects how many fingers you're showing (0–5), displaying the count along with a matching image overlay.

## 📸 Demo

A working demo of this project is on my LinkedIn — [link in the post](#).

## 🚀 Features

- Real-time hand tracking via webcam
- Counts how many fingers are raised (0 to 5) using landmark position logic
- Displays a corresponding reference image overlay for the detected count
- Large on-screen digit showing the live finger count
- Live FPS counter for performance monitoring
- Built on a reusable `handDetector` class (`HandTrackingModule.py`)

## 🛠️ Tech Stack

- **Python 3**
- **[OpenCV](https://opencv.org/)** — video capture, image processing, drawing overlays
- **[MediaPipe](https://developers.google.com/mediapipe)** — hand landmark detection

## 📁 Project Structure

| File / Folder | Description |
|---|---|
| `HandTrackingModule.py` | Reusable hand-tracking class (`handDetector`) — detects hands and extracts landmark positions |
| `fingercounter.py` | Main script — reads landmark positions, determines which fingers are up, counts them, and overlays the matching image |
| `FingerImages/` | Reference images (one per count, 0–5) shown as an overlay in the top-left corner of the video feed |

## 📦 Installation

1. Clone the repository
   ```bash
   git clone https://github.com/porasnehra/finger_counter.git
   cd finger_counter
   ```

2. Install the dependencies
   ```bash
   pip install opencv-python mediapipe
   ```

## ▶️ Usage

Run the main script with your webcam connected:

```bash
python fingercounter.py
```

- Hold your hand up in front of the camera — the count of raised fingers (0–5) will be shown on screen, along with the matching image from `FingerImages/`.
- If your webcam isn't detected, change `cv2.VideoCapture(0)` to `cv2.VideoCapture(1)` (or vice versa) at the top of `fingercounter.py`.
- Press `q` (or close the window) to exit.

## ⚙️ How It Works

1. **Load Overlays** — On startup, all images inside the `FingerImages/` folder are read, resized to 200x200, and stored in a list.
2. **Track** — `HandTrackingModule.py`'s `handDetector` class uses MediaPipe to detect the hand and extract pixel coordinates for all 21 landmarks each frame.
3. **Count** — For each of the 5 fingertip landmarks (`[4, 8, 12, 16, 20]`):
   - The **thumb** is checked by comparing whether its tip is to the left/right of the joint below it (handles thumb orientation).
   - The other **4 fingers** are checked by comparing whether the tip is *above* the joint two positions below it (i.e., extended upward).
4. **Display** — The total count of raised fingers determines which image from `FingerImages/` is overlaid in the corner, and the same number is drawn in large text on screen.
5. **Measure Performance** — FPS is calculated each loop and displayed on screen.

## 🔮 Future Improvements

- Support both hands simultaneously with individual counts
- Add gesture-to-action mapping (e.g., 5 fingers = pause, 1 finger = next)
- Improve thumb detection to work reliably for both left and right hands
- Add a `requirements.txt` for easier setup

## 👤 Author

- GitHub: [@porasnehra](https://github.com/porasnehra)

## 📄 License

This project is open source and available for learning purposes.