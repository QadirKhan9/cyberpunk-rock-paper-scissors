import streamlit as st
import random

st.set_page_config(page_title="CYBER R.P.S", page_icon="🪨", layout="centered")

# ==========================================
# 1. FUTURISTIC CSS STYLES (INJECTING HTML)
# ==========================================
st.markdown("""
    <style>
        /* Main Container and Background */
        .stApp {
            background: linear-gradient(135deg, #0f0c29, #302b63, #24243e);
            color: #ffffff;
        }

        /* Hide Standard Menu (for immersion) - Optional */
        #MainMenu {visibility: hidden;}
        footer {visibility: hidden;}

        /* Cyberpunk Title Style */
        .cyber-title {
            font-family: 'Courier New', Courier, monospace;
            text-align: center;
            font-size: 3rem;
            color: #00ffcc;
            text-shadow: 0 0 10px #00ffcc, 0 0 20px #00ffcc;
            border-bottom: 2px solid #ff00ff;
            padding-bottom: 10px;
            margin-bottom: 20px;
        }

        /* Subtitle Text */
        .cyber-text {
            font-family: 'Courier New', Courier, monospace;
            color: #ffffff;
            text-align: center;
            font-size: 1.2rem;
            letter-spacing: 2px;
        }

        /* Glowing Buttons - The "Feature" Look */
        div.stButton > button {
            background-color: transparent;
            color: #00ffcc;
            border: 2px solid #00ffcc;
            font-family: 'Courier New', Courier, monospace;
            font-size: 20px;
            font-weight: bold;
            padding: 15px;
            border-radius: 5px;
            box-shadow: 0 0 10px rgba(0, 255, 204, 0.5);
            transition: all 0.3s ease;
            width: 100%;
        }

        /* Button Hover Effect */
        div.stButton > button:hover {
            background-color: #00ffcc;
            color: #000;
            box-shadow: 0 0 20px #00ffcc, 0 0 40px #00ffcc;
            transform: scale(1.05);
            border-color: #ffffff;
        }

        /* Reset Button - distinct magenta styling */
        div[data-testid="column"]:has(button[kind="secondary"]) div.stButton > button {
            border-color: #ff00ff;
            color: #ff00ff;
            box-shadow: 0 0 10px rgba(255, 0, 255, 0.5);
        }
        div[data-testid="column"]:has(button[kind="secondary"]) div.stButton > button:hover {
            background-color: #ff00ff;
            color: #000;
            box-shadow: 0 0 20px #ff00ff, 0 0 40px #ff00ff;
        }

        /* Scoreboard Styling */
        .stMetric {
            background-color: rgba(0, 0, 0, 0.4);
            border: 1px solid #ff00ff;
            border-radius: 10px;
            padding: 10px;
            text-align: center;
            box-shadow: 0 0 10px rgba(255, 0, 255, 0.3);
        }
        [data-testid="stMetricValue"] {
            color: #ff00ff !important;
            font-family: 'Courier New', monospace !important;
            font-size: 2rem !important;
            text-shadow: 0 0 10px #ff00ff;
        }
        [data-testid="stMetricLabel"] {
            color: #ffffff !important;
            font-family: 'Courier New', monospace !important;
        }

        /* Result Animation Box */
        .result-box {
            background: rgba(0, 0, 0, 0.6);
            border: 2px solid #00ffcc;
            border-radius: 10px;
            padding: 20px;
            text-align: center;
            box-shadow: 0 0 15px #00ffcc;
            margin-top: 20px;
        }
        .result-text {
            font-size: 2rem;
            font-weight: bold;
            color: #fff;
            text-shadow: 0 0 10px #fff;
        }

        /* Streak badge */
        .streak-badge {
            text-align: center;
            font-family: 'Courier New', monospace;
            color: #ffcc00;
            text-shadow: 0 0 8px #ffcc00;
            font-size: 1rem;
            margin-top: 8px;
        }

        /* History log entries */
        .history-entry {
            font-family: 'Courier New', monospace;
            font-size: 0.95rem;
            color: #cfcfcf;
            padding: 4px 8px;
            border-left: 3px solid #00ffcc;
            margin-bottom: 4px;
            background: rgba(0, 255, 204, 0.05);
        }

        /* Hide default streamlit elements we don't want */
        .stProgress > div > div > div {
            background-color: #00ffcc;
        }
    </style>
""", unsafe_allow_html=True)

# ==========================================
# 2. GAME LOGIC & STATE
# ==========================================

if 'user_score' not in st.session_state:
    st.session_state.user_score = 0
if 'computer_score' not in st.session_state:
    st.session_state.computer_score = 0
if 'game_history' not in st.session_state:
    st.session_state.game_history = []
if 'current_streak' not in st.session_state:
    st.session_state.current_streak = 0  # positive = player win streak, negative = system streak
if 'best_streak' not in st.session_state:
    st.session_state.best_streak = 0

WINS = {"🪨": "✂️", "📄": "🪨", "✂️": "📄"}
NAMES = {"🪨": "ROCK", "📄": "PAPER", "✂️": "SCISSORS"}


def get_outcome(user, computer):
    if user == computer:
        return "DRAW", "#ffff00"
    if WINS[user] == computer:
        return "VICTORY", "#00ffcc"
    return "DEFEAT", "#ff00ff"


def reset_game():
    st.session_state.user_score = 0
    st.session_state.computer_score = 0
    st.session_state.game_history = []
    st.session_state.current_streak = 0
    st.session_state.best_streak = 0


# ==========================================
# 3. UI LAYOUT
# ==========================================

st.markdown('<h1 class="cyber-title">CYBER R.P.S</h1>', unsafe_allow_html=True)
st.markdown('<p class="cyber-text">INITIATE PROTOCOL // SELECT WEAPON</p>', unsafe_allow_html=True)

st.markdown("<br>", unsafe_allow_html=True)

# Scoreboard
col1, col2, col3 = st.columns([1, 1, 1])
with col1:
    st.metric("PLAYER", st.session_state.user_score)
with col2:
    st.metric("SYSTEM", st.session_state.computer_score)
with col3:
    st.metric("ROUNDS", len(st.session_state.game_history))

# Streak display
if st.session_state.current_streak > 0:
    st.markdown(
        f'<p class="streak-badge">🔥 PLAYER STREAK: {st.session_state.current_streak}'
        f' &nbsp;|&nbsp; BEST: {st.session_state.best_streak}</p>',
        unsafe_allow_html=True,
    )
elif st.session_state.current_streak < 0:
    st.markdown(
        f'<p class="streak-badge">⚠️ SYSTEM STREAK: {abs(st.session_state.current_streak)}'
        f' &nbsp;|&nbsp; BEST: {st.session_state.best_streak}</p>',
        unsafe_allow_html=True,
    )
else:
    st.markdown(
        f'<p class="streak-badge">BEST STREAK: {st.session_state.best_streak}</p>',
        unsafe_allow_html=True,
    )

st.markdown("<br>", unsafe_allow_html=True)

# Weapon selection buttons
c1, c2, c3 = st.columns([1, 1, 1])
rock_btn = c1.button("🪨 ROCK", key="rock")
paper_btn = c2.button("📄 PAPER", key="paper")
scissors_btn = c3.button("✂️ SCISSORS", key="scissors")

# Fixed selection logic: only one button can be True per rerun,
# so a simple if/elif chain is safer than dict-keying on booleans.
user_choice = None
if rock_btn:
    user_choice = "🪨"
elif paper_btn:
    user_choice = "📄"
elif scissors_btn:
    user_choice = "✂️"

if user_choice:
    options = ["🪨", "📄", "✂️"]
    comp_choice = random.choice(options)

    result, color_code = get_outcome(user_choice, comp_choice)

    if result == "VICTORY":
        st.session_state.user_score += 1
        st.session_state.current_streak = max(1, st.session_state.current_streak + 1)
        st.session_state.best_streak = max(st.session_state.best_streak, st.session_state.current_streak)
        st.balloons()
    elif result == "DEFEAT":
        st.session_state.computer_score += 1
        st.session_state.current_streak = min(-1, st.session_state.current_streak - 1)
        st.session_state.best_streak = max(st.session_state.best_streak, abs(st.session_state.current_streak))
    else:
        st.session_state.current_streak = 0

    st.session_state.game_history.append(
        {"user": user_choice, "comp": comp_choice, "result": result}
    )

    result_html = f"""
    <div style="text-align: center;">
        <div class="result-box">
            <h2 style="color:{color_code}; text-shadow: 0 0 10px {color_code}; margin:0;">
                {result}
            </h2>
            <p style="font-size: 1.5rem; color: white;">
                PLAYER: {user_choice} ({NAMES[user_choice]}) <br>
                SYSTEM: {comp_choice} ({NAMES[comp_choice]})
            </p>
        </div>
    </div>
    """
    st.markdown(result_html, unsafe_allow_html=True)

else:
    st.markdown("""
    <div style="text-align: center; margin-top: 30px; color: #555;">
        <h2>WAITING FOR INPUT...</h2>
        <p>SYSTEM READY.</p>
    </div>
    """, unsafe_allow_html=True)

# ==========================================
# 4. MATCH HISTORY + RESET
# ==========================================

st.markdown("<br>", unsafe_allow_html=True)

if st.session_state.game_history:
    with st.expander(f"📜 MATCH LOG ({len(st.session_state.game_history)} rounds)", expanded=False):
        for i, round_data in enumerate(reversed(st.session_state.game_history[-10:]), 1):
            st.markdown(
                f'<div class="history-entry">'
                f'ROUND {len(st.session_state.game_history) - i + 1}: '
                f'{round_data["user"]} vs {round_data["comp"]} → {round_data["result"]}'
                f'</div>',
                unsafe_allow_html=True,
            )
        if len(st.session_state.game_history) > 10:
            st.caption("Showing last 10 rounds only.")

st.markdown("<br>", unsafe_allow_html=True)
reset_col1, reset_col2, reset_col3 = st.columns([1, 1, 1])
with reset_col2:
    if st.button("🔄 RESET SYSTEM", key="reset", type="secondary"):
        reset_game()
        st.rerun()
