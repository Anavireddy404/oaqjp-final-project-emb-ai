# Emotion Detector (Python & Flask)

### Project Overview

A lightweight web application that analyzes user-submitted text and detects the underlying emotion. Text is sent to IBM Watson NLP's Emotion Predict service, which returns scores for five emotions — anger, disgust, fear, joy, and sadness — along with the single dominant emotion. The app is served through a simple Flask backend and a Bootstrap front end.

### Features

- Text-based emotion analysis via IBM Watson NLP (`EmotionPredict` API)
- Returns per-emotion scores plus the dominant emotion
- Input validation — blank or invalid text returns a friendly error instead of crashing
- Unit tested (`test_emotion_detection.py`) against sample sentences for all five emotions
- Passes static code analysis with a perfect Pylint score (10.00/10)

### Tech Stack

- **Backend:** Python, Flask
- **NLP:** IBM Watson NLP (Emotion Predict API)
- **Frontend:** HTML, Bootstrap, vanilla JavaScript (AJAX)
- **Testing:** `unittest`
- **Linting:** Pylint

### Repository Structure

```
Emotion-Detector-Python-Flask-main/
├── EmotionDetection/
│   ├── __init__.py
│   └── emotion_detection.py       # Core emotion_detector() logic, calls Watson NLP API
├── templates/
│   └── index.html                 # Web UI
├── static/
│   └── mywebscript.js             # Front-end AJAX call to /emotionDetector
├── server.py                      # Flask app and routes
├── test_emotion_detection.py      # Unit tests for emotion_detector()
├── LICENSE
└── README.md
```

### How It Works

1. The user enters text in the web form and clicks **Run Sentiment Analysis**.
2. `mywebscript.js` sends an AJAX `GET` request to the Flask `/emotionDetector` route with the text as a query parameter.
3. `server.py` passes the text to `emotion_detector()` in `EmotionDetection/emotion_detection.py`.
4. `emotion_detector()` posts the text to IBM Watson NLP's `EmotionPredict` endpoint and parses the response into anger, disgust, fear, joy, and sadness scores, then computes the dominant emotion.
5. If the input is blank or the API returns no prediction, the app responds with `"Invalid text! Please try again!"` instead of the score breakdown.
6. The result is rendered back into the page without a full reload.

### Requirements

```
flask
requests
```

Install with:

```bash
pip install flask requests
```

### How to Run

1. Clone the repository:

   ```bash
   git clone https://github.com/<your-username>/Emotion-Detector-Python-Flask.git
   cd Emotion-Detector-Python-Flask
   ```

2. Install dependencies:

   ```bash
   pip install flask requests
   ```

3. Start the Flask server:

   ```bash
   python3 server.py
   ```

4. Open your browser to `http://localhost:5000` and enter text to analyze.

### Testing

Run the unit test suite with:

```bash
python3 -m unittest test_emotion_detection.py
```

Expected result:

```
Ran 1 test in 0.582s

OK
```

### Code Quality

Static analysis with Pylint rates `server.py` at **10.00/10**.

```bash
pylint server.py
```

### Results

Sample outputs captured from running `emotion_detector()` directly:

| Input Text | Anger | Disgust | Fear | Joy | Sadness | Dominant Emotion |
|---|---|---|---|---|---|---|
| "I love this new technology." | 0.0136 | 0.0017 | 0.0090 | 0.9719 | 0.0552 | joy |
| "I am so happy I am doing this." | 0.0043 | 0.0004 | 0.0035 | 0.9947 | 0.0127 | joy |
| "I hate working long hours." | 0.6500 | 0.0335 | 0.0557 | 0.0087 | 0.1968 | anger |

Unit tests confirm the dominant emotion is classified correctly across all five target emotions (joy, anger, disgust, sadness, fear) — see **Testing** above, which passed with `Ran 1 test in 0.582s / OK`.

Static analysis: `server.py` scores **10.00/10** on Pylint.


### License

Licensed under the Apache License 2.0 — see the [LICENSE](LICENSE) file for details.
