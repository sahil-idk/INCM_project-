# DDM Experiment - Drift Diffusion Model Research Application

A complete web-based experiment application for testing adaptive decision boundary mechanisms under time pressure. Built for computational neuroscience research.

## 📋 Overview

This application implements a Random Dot Motion (RDM) task to investigate how people adjust their decision-making strategies under time pressure. The experiment collects behavioral data to test whether adaptive boundary models better explain human decision-making compared to classical fixed-boundary Drift Diffusion Models (DDM).

### Research Details

- **Researcher:** Sahil (Roll Number: 2023122006)
- **Duration:** 12-15 minutes per participant
- **Total Trials:** 120 trials (60 baseline + 60 time pressure)
- **Target:** 50 participants

## 🏗️ Project Structure

```
ddm-experiment/
├── frontend/                 # React frontend (Vite)
│   ├── src/
│   │   ├── components/      # UI components
│   │   │   ├── LandingPage.jsx
│   │   │   ├── ConsentForm.jsx
│   │   │   ├── Demographics.jsx
│   │   │   ├── Instructions.jsx
│   │   │   ├── RandomDotMotion.jsx
│   │   │   ├── ExperimentManager.jsx
│   │   │   ├── BreakScreen.jsx
│   │   │   ├── PostSurvey.jsx
│   │   │   └── CompletionScreen.jsx
│   │   ├── utils/           # Utility functions
│   │   │   ├── trialGenerator.js
│   │   │   ├── dataManager.js
│   │   │   └── api.js
│   │   ├── App.jsx
│   │   ├── main.jsx
│   │   └── index.css
│   ├── index.html
│   ├── package.json
│   └── vite.config.js
├── backend/                  # Node.js/Express backend
│   ├── src/
│   │   ├── models/          # MongoDB models
│   │   │   ├── Participant.js
│   │   │   └── Trial.js
│   │   ├── routes/          # API routes
│   │   │   ├── participants.js
│   │   │   ├── trials.js
│   │   │   └── data.js
│   │   ├── middleware/      # Validation & error handling
│   │   │   ├── validation.js
│   │   │   └── errorHandler.js
│   │   ├── config/
│   │   │   └── database.js
│   │   └── server.js
│   └── package.json
├── README.md
└── DEPLOYMENT.md
```

## 🚀 Quick Start

### Prerequisites

- **Node.js** v18 or higher
- **npm** or **yarn**
- **MongoDB** (local installation or MongoDB Atlas account)
- Desktop/laptop with keyboard (mobile not supported)

### Local Development Setup

#### 1. Clone the Repository

```bash
git clone <your-repo-url>
cd ddm-experiment
```

#### 2. Backend Setup

```bash
cd backend
npm install

# Create .env file
cp .env.example .env

# Edit .env and add your MongoDB connection string
# MONGODB_URI=mongodb://localhost:27017/ddm-experiment
# or use MongoDB Atlas connection string
```

#### 3. Frontend Setup

```bash
cd frontend
npm install

# Create .env file
cp .env.example .env

# Edit .env
# VITE_API_URL=http://localhost:5000
```

#### 4. Start Development Servers

Open two terminal windows:

**Terminal 1 - Backend:**
```bash
cd backend
npm run dev
```

**Terminal 2 - Frontend:**
```bash
cd frontend
npm run dev
```

The application will be available at:
- Frontend: `http://localhost:5173`
- Backend API: `http://localhost:5000`

## 🧪 Experiment Flow

1. **Landing Page** - Study overview
2. **Consent Form** - Informed consent
3. **Demographics** - Age, gender, handedness
4. **Instructions** - Task explanation
5. **Practice** - 10 trials with feedback
6. **Part A: Baseline** - 60 trials, no time limit
7. **Break Screen** - Brief pause
8. **Part B: Time Pressure** - 60 trials, 1-second deadline
9. **Post-Survey** - 3 questions
10. **Completion** - Debrief and participant ID

## 🎮 Task Specifications

### Random Dot Motion (RDM)

- **Canvas:** 600×600px, black background
- **Dots:** 200 white dots, 3px radius
- **Aperture:** Circular, 250px radius
- **Coherence levels:** 10%, 25%, 40%
- **Dot speed:** 2 pixels/frame
- **Target frame rate:** 60 FPS
- **Response keys:** F/← for LEFT, J/→ for RIGHT

### Conditions

**Baseline (60 trials):**
- No time limit
- 20 trials per coherence level
- Respond at your own pace

**Time Pressure (60 trials):**
- 1000ms response deadline
- Visual countdown timer
- 20 trials per coherence level
- "Too slow!" message for timeouts

## 📊 Data Collection

### Trial-Level Data

```javascript
{
  participantId: "P_1699824738_x7k9m2",
  trialNumber: 1,
  condition: "baseline" | "timePressure",
  coherence: 0.25,
  direction: "left" | "right",
  response: "left" | "right" | "timeout",
  rt: 847,  // milliseconds
  correct: true,
  timeout: false,
  timestamp: "2025-11-12T14:23:45.123Z"
}
```

### Participant-Level Data

- Demographics (age, gender, handedness)
- Post-survey responses (impulsivity, attention, task difficulty)
- Completion time and duration

## 🔌 API Endpoints

### Participants

- `POST /api/participants/create` - Create new participant
- `POST /api/participants/:id/demographics` - Submit demographics
- `POST /api/participants/:id/complete` - Mark as completed
- `GET /api/participants/:id` - Get participant details

### Trials

- `POST /api/trials/submit` - Submit trial data (batch)
- `GET /api/trials/:participantId` - Get all trials
- `GET /api/trials/:participantId/stats` - Get statistics

### Data Export

- `GET /api/data/export` - Download CSV of all data
- `GET /api/data/stats` - Get experiment statistics
- `GET /api/data/participants` - Get all participants

### Health

- `GET /api/health` - Server health check

## 📈 Accessing Your Data

### Option 1: CSV Export (Recommended)

Visit the API endpoint directly in your browser:
```
http://your-backend-url.com/api/data/export
```

This downloads a CSV file with all participant and trial data.

### Option 2: Statistics Dashboard

Get overall statistics:
```
http://your-backend-url.com/api/data/stats
```

### Option 3: MongoDB Direct Access

Connect to your MongoDB database using MongoDB Compass or the mongo shell:

```bash
mongo "your-connection-string"
use ddm-experiment
db.trials.find()
db.participants.find()
```

## 🛠️ Development

### Adding New Features

1. **Backend changes:** Modify routes in `backend/src/routes/`
2. **Frontend components:** Add to `frontend/src/components/`
3. **Trial logic:** Update `frontend/src/utils/trialGenerator.js`
4. **Data handling:** Modify `frontend/src/utils/dataManager.js`

### Testing Changes

1. Test on desktop browsers (Chrome, Firefox, Safari)
2. Verify data saves to MongoDB correctly
3. Check CSV export format
4. Test error handling (disconnect network, etc.)
5. Validate RT precision (use known delays)

## 🐛 Troubleshooting

### Backend won't start

```bash
# Check MongoDB connection
# Verify .env file exists and has correct MONGODB_URI
# Check if port 5000 is already in use
lsof -i :5000  # Mac/Linux
netstat -ano | findstr :5000  # Windows
```

### Frontend won't connect to backend

```bash
# Check frontend .env file
# Verify VITE_API_URL points to correct backend URL
# Check browser console for CORS errors
```

### Data not saving

1. Check browser console for errors
2. Verify MongoDB connection in backend logs
3. Check Network tab in browser DevTools
4. Data is auto-saved to localStorage as backup

### Poor performance / laggy animation

1. Close other browser tabs
2. Update graphics drivers
3. Reduce NUM_DOTS in RandomDotMotion.jsx
4. Check browser hardware acceleration

## 📱 Browser Compatibility

**Supported:**
- Chrome 90+
- Firefox 88+
- Safari 14+
- Edge 90+

**Not Supported:**
- Mobile browsers (by design - keyboard required)
- IE 11 or older

## 🔒 Data Privacy & Ethics

- All data is anonymous (no PII collected)
- Random participant IDs generated
- Informed consent required
- IRB approval recommended before deployment
- GDPR compliant (no personal data stored)

## 📚 Scientific Background

This experiment tests the **Adaptive Boundary Hypothesis** in decision-making:

- **Classical DDM:** Assumes fixed decision boundaries
- **Adaptive DDM:** Boundaries adjust based on time pressure
- **Hypothesis:** Time pressure lowers decision boundaries, leading to faster but potentially less accurate responses

### Key Metrics

1. **Response Time (RT):** Time from stimulus onset to response
2. **Accuracy:** Proportion of correct responses
3. **Speed-Accuracy Tradeoff:** Relationship between RT and accuracy
4. **Boundary Separation:** Inferred from RT distributions
5. **Drift Rate:** Evidence accumulation rate

## 📖 Citation

If you use this code for research, please cite:

```
Sahil (2023122006). DDM Experiment: Testing Adaptive Decision Boundaries
Under Time Pressure. [Software]. (2025).
```

## 📄 License

MIT License - see LICENSE file for details

## 🤝 Contributing

This is a research project. If you find bugs or have suggestions:

1. Open an issue on GitHub
2. Submit a pull request
3. Contact the researcher

## 📧 Contact

For questions about the experiment or data:
- **Researcher:** Sahil (Roll Number: 2023122006)
- Contact through your institution

## 🎯 Next Steps

1. Complete local testing with 2-3 test participants
2. Set up MongoDB Atlas (free tier)
3. Deploy to Vercel (frontend) and Render (backend)
4. Test deployed version thoroughly
5. Begin data collection
6. Monitor participant progress via API stats endpoint
7. Download data regularly using CSV export

See `DEPLOYMENT.md` for detailed deployment instructions.

## ✅ Pre-Deployment Checklist

- [ ] Test complete experiment flow locally
- [ ] Verify all 120 trials run correctly
- [ ] Test data saves to MongoDB
- [ ] Verify CSV export works
- [ ] Test on multiple browsers
- [ ] Check mobile warning displays
- [ ] Verify RT precision
- [ ] Test timeout functionality
- [ ] Check consent form displays properly
- [ ] Test error handling (network failures)

---

**Built with:** React, Vite, Node.js, Express, MongoDB, Canvas API

**Status:** ✅ Ready for deployment and data collection
