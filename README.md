🇬🇧 English | [🇭🇷 Hrvatski](README.hr.md)

# Hand Gesture Calculator

Course project: Robot Vision, FERIT Osijek

A real-time calculator controlled by hand gestures, built with Python, OpenCV
and MediaPipe. It uses a webcam to read hand gestures for numbers and
mathematical operations, so no keyboard is needed.

## Game Modes

**Easy: Free input**
- No timer or target number
- Build expressions freely with gestures
- Good for learning the controls

**Medium: 2 numbers, 1 operation, 25 seconds**
- A target number is shown on screen
- Input: `Number → Operation → Number`
- A correct answer scores a point and starts a new round
- A wrong answer or timeout ends the game

**Hard: 3 numbers, 2 operations, 20 seconds**
- Harder target numbers, less time
- Input: `Number → Operation → Number → Operation → Number`
- Expressions are evaluated left to right

## Gestures and Controls

| Gesture | Input |
|---|---|
| ✊ Closed fist | `+` (addition) |
| ✌️ V-sign (index + middle finger) | `-` (subtraction) |
| 👍 Thumb up | `*` (multiplication) |
| 🤙 Thumb + pinky | `/` (division) |
| ☝️ 0–5 fingers extended | Number (0–5) |

Each gesture must be held steady for **1.5 seconds** to be confirmed. A
progress bar at the bottom of the screen shows the remaining time.

## Getting Started

### Prerequisites
- Python 3.10+
- Webcam

### Option 1: Run locally
```bash
git clone https://github.com/sucicnina/Hand-gesture-Calculator.git
cd Hand-gesture-Calculator/project
pip install -r requirements.txt
python main.py
```

### Option 2: Docker (Linux with X11)
```bash
xhost +local:docker
docker compose up --build
```

The Docker setup uses X11 forwarding for the GUI and mounts `/dev/video0`.
If your webcam is on a different device, adjust `docker-compose.yml`.

## Project Structure

```
main.py            # Entry point: package check, launches the GUI
gui.py             # Tkinter interface: difficulty selection and game view
calculator.py      # Game logic, state machine, scoring, expression building
hand_detector.py   # Hand detection, finger counting, gesture recognition
overlay.py         # OpenCV drawing helpers (panel, timer, game over)
challenge.py       # Target number generation for Medium and Hard
requirements.txt   # Python dependencies
Dockerfile
docker-compose.yml
```

## Tech Stack
- **OpenCV**: webcam capture and frame rendering
- **MediaPipe**: detection of 21 hand landmarks
- **Tkinter**: desktop GUI and difficulty selection
- **Pillow**: rendering emojis on frames
- **NumPy**: frame manipulation

## How It Works
1. The app opens a Tkinter window where you choose the difficulty.
2. The webcam feed is shown in real time with hand landmarks overlaid.
3. MediaPipe detects how many fingers are extended (numbers 0–5) and
   recognizes hand shapes for mathematical operations.
4. Each input must be held for 1.5 seconds, which prevents accidental inputs.
5. Once the full expression is entered, it is evaluated and compared with the
   target. A correct answer scores a point; a wrong one ends the game.

## Known Limitations
- Numbers are limited to **0–5** (one hand, finger count)
- Division only works when the result is a whole number
- Good lighting is needed for reliable hand detection
- Webcam passthrough in Docker is supported on Linux only

## My Contribution (Nina Sučić)
I worked on **hand landmark detection**: locating the 21 key points of the
hand in each webcam frame using MediaPipe (`hand_detector.py`). These
landmarks are the basis for counting extended fingers and recognizing the
gestures for numbers and operations.

## Authors
Luka Idžanović, Dino Veršić, Nina Sučić, Lovro Žižanović

Mentor: doc. dr. sc. Petra Pejić
Faculty: FERIT Osijek, 1st year of graduate studies, Artificial Intelligence and Robotics
