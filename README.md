# MockMate – AI-Powered Mock Interview Platform

> A full-stack platform for candidates to practice interviews with AI-generated questions, real-time speech recognition, and personalized performance feedback.

## 🌟 Features

- **AI-Generated Questions** – Dynamic interview questions using Google Gemini API  
- **Real-time Speech Recognition** – Live transcription with Web Speech API  
- **Instant Feedback** – AI-powered scoring and suggestions  
- **Multiple Job Roles & Levels** – Web, App, ML/AI, UX, Data roles; Fresher → Senior  
- **HR Dashboard** – Schedule, manage interviews, and track candidates  
- **Interview Rooms** – Unique links with timers  
- **Performance Analytics** – Track scores, strengths, and improvement areas  
- **Responsive Design** – Optimized for desktop & tablet  
- **Secure Authentication** – JWT-based login and permissions

---



## 📁 Project Structure

```
EchoPrep/
├── backend/                          # Node.js Express Server
│   ├── src/
│   │   ├── index.ts                 # Server entry point
│   │   ├── config/                  # Configuration
│   │   ├── models/                  # MongoDB schemas
│   │   ├── routes/                  # API endpoints
│   │   ├── middleware/              # Auth & validation
│   │   └── controllers/             # Business logic
│   ├── .env                         # Environment variables
│   ├── package.json
│   ├── tsconfig.json
│   └── README.md
│
├── frontend/                         # React + Vite
│   ├── src/
│   │   ├── pages/                   # Page components
│   │   ├── components/              # Reusable components
│   │   ├── contexts/                # State management
│   │   ├── hooks/                   # Custom hooks
│   │   ├── types/                   # TypeScript types
│   │   └── App.tsx
│   ├── .env
│   ├── vite.config.ts
│   ├── package.json
│   └── README.md
│
├── evaluator_service/               # AI Evaluation Service
│   ├── index.js                    # Express server
│   ├── .env
│   ├── package.json
│   └── README.md
│
├── .gitignore
├── README.md                        # This file
└── LICENSE
```

## 🛠️ Tech Stack

### Backend
| Technology | Purpose |
|-----------|---------|
| **Node.js** | Runtime environment |
| **Express.js** | Web framework |
| **TypeScript** | Type-safe JavaScript |
| **MongoDB** | NoSQL database |
| **JWT** | Authentication |
| **Socket.io** | Real-time communication (optional) |

### Frontend
| Technology | Purpose |
|-----------|---------|
| **React 18** | UI library |
| **TypeScript** | Type safety |
| **Vite** | Build tool & dev server |
| **Tailwind CSS** | Styling |
| **Context API** | State management |
| **Web Speech API** | Speech recognition |

### Evaluator Service
| Technology | Purpose |
|-----------|---------|
| **Node.js** | Runtime |
| **Express.js** | Web framework |
| **Google Gemini API** | AI for analysis |
| **JavaScript** | Language |

## 📋 Prerequisites

- **Node.js** v18 or higher
- **npm** v9 or higher (or **yarn**)
- **MongoDB Atlas** account (free tier: [mongodb.com/atlas](https://mongodb.com/atlas))
- **Google Gemini API** key (free tier: [ai.google.dev](https://ai.google.dev))
- **Git** for version control

## 🚀 Quick Start

### 1️⃣ Clone Repository

```bash
git clone https://github.com/vinod2400/Echo-Prep.git
cd Echo-Prep
```

### 2️⃣ Backend Setup

```bash
cd backend

# Install dependencies
npm install

# Create .env file with your credentials
cat > .env << 'EOF'
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/ai_interview?retryWrites=true&w=majority
JWT_SECRET=your_super_secret_jwt_key_here_min_32_chars
PORT=5000
FRONTEND_URL=http://localhost:5173
EVALUATOR_SERVICE_URL=http://localhost:8001
NODE_ENV=development
EOF

# Start development server
npm run dev
```

**Backend URL**: `http://localhost:5000`

### 3️⃣ Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Create .env file
cat > .env << 'EOF'
VITE_API_BASE_URL=http://localhost:5000/api
VITE_WS_URL=ws://localhost:5000
VITE_APP_TITLE=EchoPrep
VITE_ENABLE_ANALYTICS=false
EOF

# Start development server
npm run dev
```

**Frontend URL**: `http://localhost:5173`

### 4️⃣ Evaluator Service Setup

```bash
cd evaluator_service

# Install dependencies
npm install

# Create .env file
cat > .env << 'EOF'
GEMINI_API_KEY=your_gemini_api_key_here
PORT=8001
EOF

# Start service
npm start
```

**Service URL**: `http://localhost:8001`

---

## 🎯 How It Works

### Candidate Interview Flow

```
┌─────────────────────────────────────────────────────┐
│  1. Sign Up / Login as Candidate                    │
└─────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────┐
│  2. Setup Page                                      │
│  ├─ Select Job Role                                 │
│  ├─ Select Experience Level                         │
│  └─ Grant Camera & Microphone Permissions           │
└─────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────┐
│  3. Start Interview                                 │
│  ├─ Question reads aloud (Text-to-Speech)          │
│  ├─ User records answer (Speech-to-Text)           │
│  ├─ 3-minute timer per question                    │
│  └─ Submit or Skip                                  │
└─────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────┐
│  4. AI Analysis (Per Question)                      │
│  ├─ Gemini API evaluates answer                     │
│  ├─ Returns score (0-100)                           │
│  ├─ Provides feedback                               │
│  └─ Lists strengths & weaknesses                    │
└─────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────┐
│  5. Results Page                                    │
│  ├─ Average score across all answers                │
│  ├─ Overall feedback                                │
│  ├─ Compiled strengths & improvements               │
│  └─ Save to MongoDB                                 │
└─────────────────────────────────────────────────────┘
```

### HR Interview Flow

```
┌─────────────────────────────────────────────────────┐
│  1. HR Sign Up / Login                              │
└─────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────┐
│  2. HR Dashboard → Schedule Interview               │
│  ├─ Enter candidate email                           │
│  ├─ Select job role & experience level              │
│  ├─ Set duration (15-120 minutes)                   │
│  └─ Schedule date/time                              │
└─────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────┐
│  3. Generate Interview Room Link                    │
│  └─ Share with candidate                            │
└─────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────┐
│  4. Candidate Joins Room                            │
│  ├─ Verifies email matches                          │
│  ├─ Tests camera/microphone                         │
│  └─ Starts interview                                │
└─────────────────────────────────────────────────────┘
                        ↓
┌─────────────────────────────────────────────────────┐
│  5. Results Saved                                   │
│  └─ HR can view candidate results                   │
└─────────────────────────────────────────────────────┘
```

## 📡 API Endpoints

### Authentication
```
POST   /api/auth/signup              Register new user
POST   /api/auth/login               User login
GET    /api/auth/me                  Get current user profile
```

### Interviews (HR)
```
POST   /api/interviews               Create interview
GET    /api/interviews               Get user's interviews
GET    /api/interviews/room/:id      Get interview room details
PUT    /api/interviews/:id/cancel    Cancel interview
PUT    /api/interviews/room/:id/complete  Mark complete
```

### Results
```
POST   /api/interview-results        Save interview results
GET    /api/interview-results        Get user's results
GET    /api/interview-results/:id    Get specific result
```

### Evaluator Service
```
POST   /fetch-questions              Generate interview questions
POST   /evaluate-answer              Analyze answer & score
```

## 🔐 Environment Variables

### Backend (.env)
```env
# MongoDB Connection
MONGODB_URI=mongodb+srv://username:password@cluster.mongodb.net/database?retryWrites=true&w=majority

# JWT Secret (use strong, random string)
JWT_SECRET=your_very_secret_key_with_min_32_characters

# Server Configuration
PORT=5000
NODE_ENV=development

# CORS
FRONTEND_URL=http://localhost:5173

# Services
EVALUATOR_SERVICE_URL=http://localhost:8001
```

### Frontend (.env)
```env
VITE_API_BASE_URL=http://localhost:5000/api
VITE_WS_URL=ws://localhost:5000
VITE_APP_TITLE=EchoPrep
VITE_ENABLE_ANALYTICS=false
```

### Evaluator Service (.env)
```env
GEMINI_API_KEY=your_google_gemini_api_key
PORT=8001
```

## 🗄️ Database Schema

### Users Collection
```json
{
  "_id": ObjectId,
  "email": "user@example.com",
  "password": "hashed_bcrypt_password",
  "role": "candidate" | "hr",
  "firstName": "John",
  "lastName": "Doe",
  "company": "TechCorp",
  "position": "Senior Engineer",
  "createdAt": Date,
  "updatedAt": Date
}
```

### Interview Results Collection
```json
{
  "_id": ObjectId,
  "candidate": ObjectId,
  "interview": ObjectId,
  "jobRole": "web-developer",
  "experienceLevel": "mid-level",
  "totalScore": 82,
  "feedback": "Excellent performance!",
  "strengths": ["Communication", "Problem Solving"],
  "improvements": ["System Design"],
  "answers": [
    {
      "questionId": "q1",
      "questionText": "Tell me about yourself",
      "answerText": "I am...",
      "score": 85,
      "feedback": "Great answer!",
      "strengths": ["Clarity"],
      "weaknesses": []
    }
  ],
  "isHrScheduled": false,
  "cheatingDetected": false,
  "date": Date,
  "createdAt": Date
}
```

## 🚢 Deployment

### Frontend Deployment (Vercel)
```bash
cd frontend
npm run build
# Deploy dist/ folder to Vercel
```

### Backend Deployment (Railway/Render)
```bash
# Connect GitHub repo to Railway/Render
# Auto-deploys on push to main branch
```

### Set Production Environment Variables
- `MONGODB_URI` - Your production MongoDB URI
- `JWT_SECRET` - Strong random string
- `FRONTEND_URL` - Your deployed frontend URL
- `EVALUATOR_SERVICE_URL` - Your deployed service URL

## 📊 Performance Metrics

| Metric | Target |
|--------|--------|
| Backend Response Time | < 200ms |
| Frontend Load Time | < 2s |
| API Rate Limit | 100 req/min per user |
| Concurrent Users | Unlimited (MongoDB dependent) |

## 🔒 Security Features

- ✅ Password hashing with bcrypt
- ✅ JWT-based authentication
- ✅ CORS enabled with allowed origins
- ✅ Input validation & sanitization
- ✅ XSS prevention with DOMPurify
- ✅ Rate limiting
- ✅ Environment variables for secrets
- ✅ HTTPS in production

## 🧪 Testing

### Run Backend Tests
```bash
cd backend
npm run test
```

### Run Frontend Tests
```bash
cd frontend
npm run test
```

## 📚 Documentation

- [Backend README](./backend/README.md)
- [Frontend README](./frontend/README.md)
- [Evaluator Service README](./evaluator_service/README.md)

## 🤝 Contributing

1. Fork the repository
2. Create feature branch: `git checkout -b feature/AmazingFeature`
3. Commit changes: `git commit -m 'Add AmazingFeature'`
4. Push to branch: `git push origin feature/AmazingFeature`
5. Open Pull Request

### Commit Guidelines
```
feat: Add new feature
fix: Fix a bug
docs: Update documentation
style: Code style changes
refactor: Code refactoring
test: Add tests
chore: Update dependencies
```

## 📝 License

This project is licensed under the MIT License - see [LICENSE](LICENSE) file for details.

## 👨‍💻 Author

**Insha Khan**
- GitHub:https://github.com/InshaaKhan

## 🙏 Acknowledgments

- Google Gemini API for AI capabilities
- MongoDB for database solutions
- React and TypeScript communities
- All contributors

## 🎓 Learning Resources

- [React Documentation](https://react.dev)
- [Express.js Guide](https://expressjs.com)
- [MongoDB Manual](https://docs.mongodb.com)
- [Google Gemini API](https://ai.google.dev)
- [Vite Documentation](https://vitejs.dev)
- [TypeScript Handbook](https://www.typescriptlang.org/docs)

---

## 🚀 Roadmap

- [ ] Live video recording during interview
- [ ] Multiple language support
- [ ] Interview plagiarism detection
- [ ] Resume upload & analysis
- [ ] Mock salary negotiation module
- [ ] Interview analytics dashboard
- [ ] Social sharing of results
- [ ] Mobile app (React Native)
- [ ] Interview scheduling with calendar
- [ ] Email notifications

---

**Happy Interviewing! 🎉**

*Built with ❤️ to make interview preparation easier and more effective.*
# Echo-Prep-main
