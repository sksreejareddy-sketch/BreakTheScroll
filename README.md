📵 Doom Scroll Detector
Your webcam watches while you study. The moment you pick up your phone, it plays a loud siren and calls you out.
![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)
<!-- Add a screenshot or GIF here, e.g. ![demo](demo.gif) -->
How it works
The browser captures your webcam feed (Colab itself has no camera or speakers).
Each frame is sent to Python, where YOLO (Ultralytics) and OpenCV look for a `cell phone` (COCO class 67).
Python returns the detection boxes to the browser.
If a phone is seen for a few frames in a row, the browser draws a red box, plays a loud siren, shows a warning banner and speaks a random callout.
The page tracks your study time and the number of phone pickups.
> **Note on PyGame:** PyGame needs real audio hardware, which Colab doesn't have, so sound is played through the browser instead. PyGame is still part of the stack for a planned local version.
Tech stack
Python
OpenCV
YOLO (Ultralytics, `yolo11n`)
PyGame
Google Colab
Quick start
Click the Open in Colab badge above.
Go to Runtime → Change runtime type and choose a T4 GPU (CPU also works, just slower).
Run every cell from top to bottom (Runtime → Run all).
In the last cell, click Start studying and allow camera access.
Pick up your phone and get called out. 😈
> ⚠️ The siren is **loud**. Lower your volume before running the preview cell.
Privacy
Everything runs in your own Colab session. Your webcam frames go from your browser to your own Colab runtime for detection, and nothing is stored or sent to the author of this project.
Tuning
Setting	Where	Effect
`CONF`	Model cell	Lower = catches more phones, more false alarms. Higher = fewer false alarms.
`CONFIRM_FRAMES`	Last cell	Consecutive frames with a phone before the alarm fires.
`COOLDOWN_MS`	Last cell	Minimum time between alarms while you keep holding the phone.
Model	Model cell	Use `yolo11s.pt` for better accuracy, `yolo11n.pt` for speed.
Troubleshooting
Camera won't start: allow camera access in your browser (camera icon in the address bar). Use Chrome and keep the Colab tab open and in focus.
No sound: browsers only allow audio after a click, so always use the Start studying button. Check the tab isn't muted.
Phone not detected: hold it so the body or screen is clearly visible, or lower `CONF` to `0.25`.
Too many false alarms: raise `CONF` to `0.5` or `CONFIRM_FRAMES` to `3`.
Slow or low fps: use a GPU runtime, or lower `imgsz` in `process_frame` to `320`.
Disconnected: Colab stops idle sessions. Re-run the last cell.
Ideas for the future
Warn when you leave your seat (detect `person`)
Log phone pickups to a CSV and chart focus time per session
Fine-tune YOLO on photos of a person holding a phone for better accuracy
Local PyGame + OpenCV version for real-time use outside Colab
Hosted web app (Gradio on Hugging Face Spaces)
License
MIT. Feel free to use, modify and share.
