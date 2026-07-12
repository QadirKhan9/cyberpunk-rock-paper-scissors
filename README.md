# 🪨📄✂️ Cyber R.P.S

A neon cyberpunk-themed Rock Paper Scissors game built with [Streamlit](https://streamlit.io/) — glowing buttons, a live scoreboard, win-streak tracking, and a match history log.

![Python](https://img.shields.io/badge/python-3.9%2B-blue)
![Streamlit](https://img.shields.io/badge/streamlit-app-ff4b4b)

## ✨ Features

- **Cyberpunk UI** — glowing neon buttons, animated hover effects, and a dark gradient background
- **Live scoreboard** — tracks player score, system score, and total rounds played
- **Streak tracker** — shows your current win/loss streak and best streak ever
- **Match log** — collapsible history of the last 10 rounds
- **Reset button** — wipe the scoreboard and start fresh anytime
- **Victory animation** — confetti balloons on every win 🎈

## 🚀 Getting Started

### Prerequisites

- Python 3.9+
- pip

### Installation

```bash
git clone https://github.com/<your-username>/cyber-rps.git
cd cyber-rps
pip install streamlit
```

### Run the app

```bash
streamlit run cyber_rps.py
```

The app will open automatically in your browser at `http://localhost:8501`.

## 🎮 How to Play

1. Click **ROCK 🪨**, **PAPER 📄**, or **SCISSORS ✂️**
2. The system randomly selects its move
3. Classic rules apply: Rock beats Scissors, Scissors beats Paper, Paper beats Rock
4. Track your progress on the scoreboard and streak badge
5. Hit **RESET SYSTEM** to start over

## 🛠️ Built With

- [Streamlit](https://streamlit.io/) — Python web app framework
- Custom CSS injected via `st.markdown` for the cyberpunk look

## 📄 License

This project is open source and available under the [MIT License](LICENSE).
