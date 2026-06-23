# License Plate Detection Using OpenCV – Theory Explanation

This program performs **real-time license plate detection** using a webcam and OpenCV's **Haar Cascade Classifier**. It captures live video, detects license plates in each frame, draws rectangles around them, and displays the result on the screen.

---

# Aim

To detect vehicle license plates from a live webcam feed and highlight them using computer vision techniques.

---

# Software Requirements

* Python
* OpenCV (`cv2`)
* Webcam

Install OpenCV:

```bash
pip install opencv-python
```

---

# 1. Importing OpenCV

```python
import cv2
```

### Purpose

* Imports the OpenCV library.
* Provides functions for image processing, video capture, and object detection.

---

# 2. Loading the Haar Cascade Classifier

```python
plate_cascade = cv2.CascadeClassifier(
    cv2.data.haarcascades + "haarcascade_russian_plate_number.xml"
)
```

### What is a Haar Cascade?

A Haar Cascade is a pre-trained machine learning model used for object detection.

### Purpose

* Detects license plates in images.
* OpenCV provides the trained XML file.

### Output

The classifier is loaded into the variable:

```python
plate_cascade
```

---

# 3. Opening the Webcam

```python
cap = cv2.VideoCapture(0)
```

### Purpose

Starts video capture.

### Parameter

```python
0
```

means:

* Default webcam

Other examples:

```python
cv2.VideoCapture(1)
```

External camera

```python
cv2.VideoCapture("video.mp4")
```

Video file

---

# 4. Displaying Startup Message

```python
print("🚗 License Plate Detection Started... Press 'q' to quit.")
```

### Purpose

Informs the user that detection has started.

---

# 5. Infinite Loop

```python
while True:
```

### Purpose

Continuously:

1. Captures video frames
2. Detects plates
3. Displays output

until the user quits.

---

# 6. Capturing Frames

```python
ret, frame = cap.read()
```

### Returns

#### ret

```python
True
```

if frame is captured successfully.

#### frame

Contains the image from the webcam.

Example:

```python
frame = current_camera_image
```

---

# 7. Checking Camera Status

```python
if not ret:
    break
```

### Purpose

Stops the program if:

* Camera disconnects
* Frame capture fails

---

# 8. Converting Image to Grayscale

```python
gray = cv2.cvtColor(frame, cv2.COLOR_BGR2GRAY)
```

### Why Grayscale?

Object detection works faster on grayscale images because:

* Less memory
* Faster processing
* Color information isn't required

### Example

Original:

```text
Red Car
Blue Sky
Green Trees
```

Grayscale:

```text
Black, White, Gray Shades
```

---

# 9. Detecting License Plates

```python
plates = plate_cascade.detectMultiScale(
    gray,
    scaleFactor=1.1,
    minNeighbors=4,
    minSize=(30, 30)
)
```

### detectMultiScale()

Searches for license plates at different sizes.

---

## Parameters

### scaleFactor

```python
scaleFactor=1.1
```

Reduces image size by 10% at each scan.

Purpose:

* Detect large and small plates.

---

### minNeighbors

```python
minNeighbors=4
```

Controls detection accuracy.

Higher value:

* Fewer false detections

Lower value:

* More detections
* More mistakes

---

### minSize

```python
minSize=(30,30)
```

Ignores objects smaller than 30×30 pixels.

---

# 10. Loop Through Detected Plates

```python
for (x, y, w, h) in plates:
```

Each detected plate returns:

| Variable | Meaning       |
| -------- | ------------- |
| x        | Left position |
| y        | Top position  |
| w        | Width         |
| h        | Height        |

Example:

```python
(120, 180, 200, 60)
```

---

# 11. Drawing Rectangle Around Plate

```python
cv2.rectangle(
    frame,
    (x, y),
    (x + w, y + h),
    (0, 255, 0),
    2
)
```

### Purpose

Draws a green rectangle around the detected license plate.

### Parameters

* Starting point
* Ending point
* Green color `(0,255,0)`
* Thickness = 2 pixels

Example:

```text
+----------------+
| AP39AB1234     |
+----------------+
```

---

# 12. Adding Label

```python
cv2.putText(
    frame,
    "Plate",
    (x, y - 10),
    cv2.FONT_HERSHEY_SIMPLEX,
    0.8,
    (0, 255, 0),
    2
)
```

### Purpose

Displays the word:

```text
Plate
```

above the detected number plate.

---

# 13. Displaying Output Window

```python
cv2.imshow("License Plate Detection", frame)
```

### Purpose

Shows the processed video frame.

Example:

```text
--------------------------------
|                              |
|      Plate                   |
|   ┌───────────────┐          |
|   | AP39AB1234    |          |
|   └───────────────┘          |
|                              |
--------------------------------
```

---

# 14. Checking for Exit Key

```python
if cv2.waitKey(1) & 0xFF == ord('q'):
```

### Purpose

Waits for keyboard input.

If user presses:

```text
q
```

the program exits.

---

# 15. Releasing Resources

```python
cap.release()
```

### Purpose

Releases the webcam.

---

# 16. Closing Windows

```python
cv2.destroyAllWindows()
```

### Purpose

Closes all OpenCV display windows.

---

# Algorithm

1. Start program.
2. Load Haar Cascade classifier.
3. Open webcam.
4. Capture video frames continuously.
5. Convert frame to grayscale.
6. Detect license plates.
7. Draw rectangle and label around detected plates.
8. Display frame.
9. If user presses **q**, stop execution.
10. Release webcam and close windows.

---

# Applications

* Traffic Monitoring Systems
* Toll Plaza Automation
* Parking Management Systems
* Vehicle Tracking
* Security and Surveillance
* Automatic Number Plate Recognition (ANPR)

---

# Advantages

* Real-time detection
* Easy implementation
* Fast execution
* Works with webcam and video files

# Limitations

* Accuracy depends on lighting conditions.
* May fail with tilted or blurry plates.
* Detects the plate location only.
* Does not read the plate number.

To read the plate number, you can combine this project with OCR libraries such as **Tesseract OCR** (`pytesseract`) for a complete **Automatic Number Plate Recognition (ANPR)** system.
