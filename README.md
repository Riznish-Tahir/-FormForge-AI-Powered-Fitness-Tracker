# 🏋️ FormForge — AI-Powered Fitness Tracker

<div align="center">

![FormForge Banner](https://img.shields.io/badge/FormForge-AI%20Fitness%20Tracker-00ff88?style=for-the-badge&logo=data:image/svg+xml;base64,PHN2ZyB4bWxucz0iaHR0cDovL3d3dy53My5vcmcvMjAwMC9zdmciIHZpZXdCb3g9IjAgMCAyNCAyNCI+PHBhdGggZmlsbD0id2hpdGUiIGQ9Ik0xMiAyQzYuNDggMiAyIDYuNDggMiAxMnM0LjQ4IDEwIDEwIDEwIDEwLTQuNDggMTAtMTBTMTcuNTIgMiAxMiAyem0tMiAxNGwtNC00IDEuNDEtMS40MUwxMCAxMy4xN2w2LjU5LTYuNTlMMTggOGwtOCA4eiIvPjwvc3ZnPg==)

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![MediaPipe](https://img.shields.io/badge/MediaPipe-Pose-blue?logo=google)](https://mediapipe.dev)
[![Claude AI](https://img.shields.io/badge/Powered%20by-Claude%20AI-orange)](https://anthropic.com)
[![No Install](https://img.shields.io/badge/Install-None%20Required-00ff88)](.)
[![Single File](https://img.shields.io/badge/Size-1%20HTML%20File-purple)](.)

**Real-time pose estimation + AI gym coaching. One file. No install. Open in Chrome and train.**

[🚀 Live Demo](#quick-start) · [📹 Watch Video](#demo) · [🐛 Report Bug](issues) · [💡 Request Feature](issues)

</div>

---

## 📸 Preview

```
┌─────────────────────────────────────────────────────┐
│  📷 Camera Feed              │  🤖 AI Coach          │
│  ┌──────────────────┐        │  "Drive through your  │
│  │  [skeleton       │        │   heels — chest up!"  │
│  │   overlay on     │        │                       │
│  │   live video]    │        │  📐 Joint Angles      │
│  │                  │        │  Left Knee:  87°  ████│
│  │  REPS  SETS TIME │        │  Right Knee: 91°  ████│
│  │   8     2  2:14  │        │  Left Hip:  142°  ███ │
│  │                  │        │                       │
│  │  Form Score: 92% │        │  Avg Form: 88%        │
│  └──────────────────┘        │  Best Rep: 96%        │
└─────────────────────────────────────────────────────┘
```

---

## ✨ Features

### 🦾 Real-Time Pose Tracking
- **MediaPipe Pose** — 33-point body landmark detection at ~30fps
- Skeleton overlay rendered live on canvas
- Joint angle computation using vector mathematics
- Smoothed landmarks for stable tracking

### 🏋️ Exercise Library

| Exercise | Joints Tracked | Form Checks |
|----------|---------------|-------------|
| 🦵 Squat | Knees + Hips | Depth, knee cave, back angle |
| 💪 Push-Up | Elbows + Hips | Depth, body alignment, elbow flare |
| 🏃 Lunge | Knees + Hips | Knee tracking, depth, balance |
| 🏋 Shoulder Press | Elbows + Shoulders | Lockout, back arch, control |

### 🤖 AI Gym Coach (Claude API)
- Generates **personalized feedback** every 5 reps
- Triggers automatically when form score drops below 60%
- Contextual advice based on exercise, rep count, and current form
- Adapts language to your session history

### 📊 Analytics
- **Form Score 0–100** — per-rep biomechanical evaluation
- Live joint angle bars for 6 joints
- Rep history log with timestamps
- Session stats: average form, best rep, total reps, sets

### 📱 Android Support
- Front and rear camera switching with one tap
- Optimized for `facingMode: environment` (rear camera = better angle)
- Responsive layout for mobile screens

---

## 🚀 Quick Start

### Option 1 — Direct Download
```bash
# Download the file
curl -O https://raw.githubusercontent.com/yourusername/formforge/main/fitness_tracker.html

# Open in Chrome
open fitness_tracker.html   # macOS
start fitness_tracker.html  # Windows
xdg-open fitness_tracker.html  # Linux
```

### Option 2 — Clone & Run
```bash
git clone https://github.com/Riznish-Tahir/-FormForge-AI-Powered-Fitness-Tracker
cd formforge
# Open fitness_tracker.html in Chrome
```

### Option 3 — GitHub Pages
Visit: `https://yourusername.github.io/formforge`

> ⚠️ **Chrome recommended.** Safari may have getUserMedia limitations on some devices.

---

## 🔑 AI Coach Setup (Optional)

The app works without an API key — pose tracking and rep counting are always active. The AI coach requires an Anthropic API key.

1. Get a free API key at [console.anthropic.com](https://console.anthropic.com)
2. Open `fitness_tracker.html` in a text editor
3. The app calls the Anthropic API directly from the browser

> ⚠️ For production use, proxy the API call through a backend to protect your key.

---

## 🧠 How It Works

### Pose Estimation Pipeline

```
Camera Frame
     ↓
MediaPipe Pose
     ↓
33 Body Landmarks (x, y, z, visibility)
     ↓
┌────────────────────────────────┐
│  Joint Angle Computation       │
│  angle(A, B, C) = arccos(      │
│    dot(BA, BC) / |BA||BC|      │
│  )                             │
└────────────────────────────────┘
     ↓
Exercise Evaluator (per exercise)
     ↓
┌──────────────┬──────────────┐
│ Form Score   │ Phase State  │
│ 0-100        │ UP / DOWN    │
└──────────────┴──────────────┘
     ↓
Rep Counter (phase transition detection)
     ↓
AI Coach (Claude API — every 5 reps or form < 60)
```

### Rep Counting Logic

```javascript
// Phase detection — squat example
if (phase === 'up' && kneeAngle < downThreshold + 15) {
  phase = 'down';          // entered descent
} else if (phase === 'down' && kneeAngle > upThreshold - 15) {
  phase = 'up';            // completed rep
  countRep();
}
```

### Form Scoring

Each exercise has a scoring function that evaluates:
- **Range of motion** — did you hit the required depth?
- **Body alignment** — are key joints in correct relative position?
- **Symmetry** — are bilateral joints balanced?

Score starts at 100 and deducts points for each detected issue.

---

## 📁 File Structure

```
formforge/
├── fitness_tracker.html    ← Entire application (single file)
├── README.md
└── LICENSE
```

### Dependencies (CDN — no install needed)

| Library | Version | Purpose |
|---------|---------|---------|
| MediaPipe Pose | latest | Body landmark detection |
| MediaPipe Camera Utils | latest | Camera stream management |
| MediaPipe Drawing Utils | latest | Skeleton visualization |
| Anthropic API | v1 | AI coaching feedback |

---

## 🎯 Exercises — Form Criteria

### Squat
| Metric | Good | Warning | Bad |
|--------|------|---------|-----|
| Knee angle (bottom) | < 95° | 95–110° | > 110° |
| Hip lean | Upright | Slight forward | Excessive |
| Knee tracking | Over toes | Neutral | Caving in |

### Push-Up
| Metric | Good | Warning | Bad |
|--------|------|---------|-----|
| Elbow angle (bottom) | < 95° | 95–110° | > 110° |
| Body line | Straight | Slight sag | Hip sag/pike |

### Lunge
| Metric | Good | Warning | Bad |
|--------|------|---------|-----|
| Front knee angle | ~90° | 90–110° | > 110° |
| Knee tracking | Over ankle | Neutral | Past toes |

### Shoulder Press
| Metric | Good | Warning | Bad |
|--------|------|---------|-----|
| Elbow at top | > 150° | 140–150° | < 140° |
| Back arch | Neutral | Slight | Excessive |

---

## 🔧 Configuration

Edit these constants in the JS to tune for your body type:

```javascript
const EXERCISES = {
  squat: {
    downAngle: 90,    // knee angle at bottom of movement
    upAngle: 160,     // knee angle at top of movement
    // ↑ Increase downAngle if reps aren't counting (shallower depth)
    // ↓ Decrease upAngle if false reps on lockout
  }
}
```

---

## 📱 Android Usage

**Recommended setup for best tracking:**
1. Open Chrome on Android
2. Load the HTML file (or GitHub Pages link)
3. Allow camera permission
4. Tap **🔄** button to switch to rear camera
5. Place phone 6–8 feet away, angled at your full body
6. Select exercise → Press **START**

**Best camera angles:**
- Squats/Lunges: Side profile (90° to direction of movement)
- Push-ups: Side profile or slight overhead
- Shoulder Press: Front-facing works well

---

## 🛠 Development

### Extending with New Exercises

```javascript
// 1. Add to EXERCISES config
const EXERCISES = {
  deadlift: {
    name: 'Deadlift',
    downAngle: 60,
    upAngle: 170,
    trackJoints: ['lhip', 'rhip', 'lknee', 'rknee'],
    tips: {
      back: 'Keep your back flat — don\'t round!',
      hinge: 'Push hips back, not knees forward.',
      good: 'Perfect hip hinge!'
    }
  }
};

// 2. Add evaluator function
function evalDeadlift(lm, angles) {
  let score = 100;
  // ... your form checks
  return { formScore: score, feedback: 'your tip' };
}

// 3. Add case to processExercise()
case 'deadlift':
  primaryAngle = (angles.lhip + angles.rhip) / 2;
  ({ formScore, feedback } = evalDeadlift(lm, angles));
  break;

// 4. Add button to HTML exercise selector
```

### Running Locally with HTTPS (required for camera on some browsers)

```bash
# Using Python
python -m http.server 8080

# Using Node
npx serve .

# Using Caddy (auto HTTPS)
caddy file-server --listen :443
```

---

## 🔒 Privacy

- **No data leaves your device** (except AI coach calls to Anthropic API)
- No video is recorded or stored
- No analytics or tracking
- Camera permission is only used for real-time processing
- All pose computation runs locally in the browser

---

## 🗺 Roadmap

- [ ] **Plank hold timer** with alignment scoring
- [ ] **Pull-up counter** (overhead detection)
- [ ] **Workout programs** (sets × reps × rest timer)
- [ ] **Rep tempo tracking** (time under tension)
- [ ] **Export session data** (CSV / JSON)
- [ ] **Voice coaching** (text-to-speech for AI tips)
- [ ] **Multi-person tracking**
- [ ] **PWA support** (install as app)
- [ ] **Offline mode** (local LLM for coaching)

---

## 🤝 Contributing

Contributions welcome! Please:

1. Fork the repo
2. Create a feature branch: `git checkout -b feature/deadlift-tracking`
3. Commit changes: `git commit -m 'Add deadlift form analysis'`
4. Push: `git push origin feature/deadlift-tracking`
5. Open a Pull Request

**Good first issues:**
- Add a new exercise evaluator
- Improve form scoring thresholds
- Add rep tempo detection
- Improve mobile layout

---

## 📄 License

MIT License — see [LICENSE](LICENSE) for details.

Free to use, modify, and distribute. Commercial use permitted.

---

## 🙏 Acknowledgements

- [Google MediaPipe](https://mediapipe.dev) — pose estimation backbone
- [Anthropic Claude](https://anthropic.com) — AI coaching intelligence
- [MediaPipe Pose Docs](https://developers.google.com/mediapipe/solutions/vision/pose_landmarker) — landmark reference

---

<div align="center">

**Built with 💪 by developers who skip leg day responsibly**

⭐ Star this repo if FormForge helped your workout!

[Report Bug](issues) · [Request Feature](issues) · [Discussions](discussions)

</div>
