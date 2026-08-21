# 🖐️ Finger Counter & Hand Tracking

A real-time Finger Counting and Hand Tracking project built using Python, OpenCV, and MediaPipe. The application detects a hand through the webcam, tracks its landmarks, identifies raised fingers, and displays the total finger count.

## 🚀 Features

- Real-time hand tracking using MediaPipe
- Detects 21 hand landmarks
- Counts raised fingers from 0–5
- Displays finger count on the webcam feed
- Shows corresponding finger images
- Displays real-time FPS
- Reusable HandTrackingModule

## 🛠️ Tech Stack

- **Python**
- **OpenCV** – webcam and image processing
- **MediaPipe** – hand landmark detection

## 📁 Project Structure

- HandGestureProjectCount/ 
   - GestureImages/
       - 1.png 
       - 2.png 
       - 3.png 
       - 4.png 
       - 5.png 
       - 6.png
  - fingurecounter.py 
  - HandTrackingModule.py
  - requirements.txt
  - README.md

## 🧠 How It Works

Webcam ->
   
OpenCV captures frame ->
   
MediaPipe detects hand ->
   
21 landmarks are extracted ->
   
Finger positions are analyzed ->
   
Number of raised fingers is calculated ->
   
Result is displayed on screen

For the four fingers, the program compares the Y-coordinate of the fingertip with its lower joint. For the thumb, it compares the X-coordinate to determine whether it is extended.

Example:

tipIds = [4, 8, 12, 16, 20]

These represent the fingertips of the thumb, index, middle, ring, and pinky fingers.

## 📦 Installation

1. Clone the repository
   ```bash
   git clone https://github.com/bgautamk9045/HandGestureProjectCount
   cd HandGestureProjectCount
   ```

2. Install the dependencies
   ```bash
   pip install opencv-python mediapipe
   ```

## How to Run

py fingurecounter.py

- Hold your hand up in front of the camera — the count of raised fingers (0–5) will be shown on screen, along with the matching image from `GestureImages/`.

If the webcam doesn't open, try changing:

cv2.VideoCapture(0)
to:
cv2.VideoCapture(1)

## ⚙️ How It Works

1. **Load Overlays** — On startup, all images inside the `GestureImages/` folder are read, resized to 200x200, and stored in a list.
2. **Track** — `HandTrackingModule.py`'s `handDetector` class uses MediaPipe to detect the hand and extract pixel coordinates for all 21 landmarks each frame.
3. **Count** — For each of the 5 fingertip landmarks (`[4, 8, 12, 16, 20]`):
   - The **thumb** is checked by comparing whether its tip is to the left/right of the joint below it (handles thumb orientation).
   - The other **4 fingers** are checked by comparing whether the tip is *above* the joint two positions below it (i.e., extended upward).
4. **Display** — The total count of raised fingers determines which image from `GestureImages/` is overlaid in the corner, and the same number is drawn in large text on screen.
5. **Measure Performance** — FPS is calculated each loop and displayed on screen.

## 🔮 Future Improvements

- Support both hands simultaneously with individual counts
- Add gesture-to-action mapping (e.g., 5 fingers = pause, 1 finger = next)
- Improve thumb detection to work reliably for both left and right hands
- Add a `requirements.txt` for easier setup

## 👤 Author

- GitHub: [@bgautamk9045](https://github.com/bgautamk9045)

## 📄 License

This project is open source and available for learning purposes.
