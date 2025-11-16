# AI Video Editor

✅ **FULLY IMPLEMENTED** - Full-Stack Chat-Based Video Editor

A complete full-stack application for AI-powered video subtitle editing using natural language. Built with **FastAPI**, **React**, **LangGraph**, and **FFmpeg**.

![Status](https://img.shields.io/badge/status-complete-success)
![Backend](https://img.shields.io/badge/backend-FastAPI-009688)
![Frontend](https://img.shields.io/badge/frontend-React-61DAFB)
![AI](https://img.shields.io/badge/AI-LangGraph-7B68EE)

---

## 🎬 What It Does

Upload a video, chat with AI to add styled subtitles, and export the final video with burned-in subtitles.

**Example Chat:**
```
You: "Add subtitle 'Hello World!' from 0 to 5 seconds with red color"
AI:  "✓ Added subtitle: 'Hello World!' from 0.0s to 5.0s with color: red"

You: "Add 'Welcome!' from 5 to 10 seconds, size 48, bold"
AI:  "✓ Added subtitle: 'Welcome!' from 5.0s to 10.0s with size: 48px, bold"
```

---

## ✨ Features

### ✅ Video Upload
- Drag-and-drop interface
- Supports MP4, MOV, AVI, WebM
- Up to 500MB file size
- Real-time metadata extraction

### ✅ AI Chat Interface
- Natural language subtitle editing
- Powered by OpenAI/Anthropic + LangGraph
- Multi-round conversations
- Context-aware responses

### ✅ Subtitle Styling
- **Colors**: red, blue, yellow, white, or hex codes (#FF0000)
- **Fonts**: Arial, Helvetica, Roboto, etc.
- **Sizes**: 12-72 pixels
- **Position**: top, center, bottom
- **Styles**: bold, italic

### ✅ Video Export
- Burns subtitles into video using FFmpeg
- High-quality output
- SRT and ASS subtitle format support
- One-click download

### ✅ Session Management
- Automatic session tracking
- Chat history preservation
- TTL-based cleanup

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────┐
│                        FRONTEND                              │
│  React + Vite + Tailwind CSS + Axios                        │
│                                                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │VideoUploader │  │  ChatInterface│  │ ExportButton │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
│  ┌──────────────────────────────────────────────────┐       │
│  │           VideoPlayer + Subtitles                │       │
│  └──────────────────────────────────────────────────┘       │
└────────────────────┬────────────────────────────────────────┘
                     │ REST API
┌────────────────────▼────────────────────────────────────────┐
│                        BACKEND                               │
│  FastAPI + LangGraph + FFmpeg + Python                      │
│                                                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │Upload Route  │  │  Chat Route  │  │ Export Route │     │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘     │
│         │                  │                  │              │
│  ┌──────▼──────────────────▼──────────────────▼───────┐    │
│  │              LangGraph Workflow                     │    │
│  │  ┌───────┐ ┌──────┐ ┌──────┐ ┌──────┐             │    │
│  │  │Parse  │→│Extract│→│Apply │→│ Gen  │             │    │
│  │  │Intent │ │Params │ │Edits │ │Reply │             │    │
│  │  └───────┘ └──────┘ └──────┘ └──────┘             │    │
│  └──────────────────────────────────────────────────────┘    │
│                                                              │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐     │
│  │VideoService  │  │SubtitleService│  │SessionMgr   │     │
│  │  (FFmpeg)    │  │  (SRT/ASS)   │  │  (Memory)    │     │
│  └──────────────┘  └──────────────┘  └──────────────┘     │
└─────────────────────────────────────────────────────────────┘
                     │
                     ▼
            ┌────────────────┐
            │  OpenAI / Claude│
            └────────────────┘
```

---

## 🚀 Quick Start

### Prerequisites

- **Python 3.10+**
- **Node.js 18+**
- **FFmpeg** ([Install guide](https://ffmpeg.org/download.html))
- **OpenAI API Key** or **Anthropic API Key**

### 1. Clone Repository

```bash
git clone <repository-url>
cd AI-video-editor
```

### 2. Backend Setup

```bash
cd backend

# Create virtual environment
python -m venv venv
source venv/bin/activate  # Windows: venv\Scripts\activate

# Install dependencies
pip install -r requirements.txt

# Configure environment
cp .env.example .env
nano .env  # Add your OPENAI_API_KEY

# Start server
uvicorn app.main:app --reload
```

Server: **http://localhost:8000**

### 3. Frontend Setup

```bash
cd frontend

# Install dependencies
npm install

# Configure environment (optional)
cp .env.example .env

# Start dev server
npm run dev
```

Frontend: **http://localhost:5173**

### 4. Open Browser

Navigate to: **http://localhost:5173**

---

## 📖 Usage

### Step 1: Upload Video
- Drag and drop a video file
- Or click to browse and select
- Wait for upload and metadata extraction

### Step 2: Chat to Add Subtitles

Type natural language commands:

```
Add subtitle "Hello!" from 0 to 3 seconds
Add "Welcome" from 3 to 6 seconds with red color
Add subtitle "Title" from 0 to 5 seconds, size 48, bold, Arial font
Add "The End" from 1:30 to 1:35 with yellow color, position top
```

### Step 3: Preview
- Subtitles appear on video player in real-time
- Play video to verify timing
- Add more subtitles via chat

### Step 4: Export
- Click "Export Video" button
- Wait for processing (1-2 minutes)
- Download final video

---

## 🔧 API Documentation

Once backend is running, visit:

- **Swagger UI**: http://localhost:8000/api/docs
- **ReDoc**: http://localhost:8000/api/redoc

### Key Endpoints

```
POST   /api/upload              Upload video
POST   /api/chat                Chat to add subtitles
POST   /api/export              Export video
GET    /api/subtitles/:id       Get subtitles
GET    /api/chat/history/:id    Get chat history
DELETE /api/subtitles/:id       Clear subtitles
```

---

## 🧪 Testing

### Automated Tests

```bash
cd backend

# Basic test (no video upload)
python test_workflow.py

# Full test with video
python test_workflow.py /path/to/video.mp4
```

### Manual Testing

```bash
# 1. Health check
curl http://localhost:8000/api/health

# 2. Upload video
curl -X POST http://localhost:8000/api/upload \
     -F "file=@video.mp4"

# 3. Add subtitle
curl -X POST http://localhost:8000/api/chat \
     -H "Content-Type: application/json" \
     -d '{"session_id": "sess_xxx", "message": "Add subtitle Hello from 0 to 5 seconds"}'

# 4. Export
curl -X POST http://localhost:8000/api/export \
     -H "Content-Type: application/json" \
     -d '{"session_id": "sess_xxx"}'
```

---

## 📁 Project Structure

```
AI-video-editor/
├── frontend/                   # React frontend
│   ├── src/
│   │   ├── components/        # UI components
│   │   ├── services/          # API client
│   │   ├── hooks/             # React hooks
│   │   └── utils/             # Utilities
│   ├── package.json
│   └── vite.config.js
│
├── backend/                    # FastAPI backend
│   ├── app/
│   │   ├── main.py            # FastAPI app
│   │   ├── config.py          # Configuration
│   │   ├── api/routes/        # API endpoints
│   │   ├── services/          # Business logic
│   │   ├── models/            # Data models
│   │   └── utils/             # Utilities
│   ├── uploads/               # Uploaded videos
│   ├── outputs/               # Exported videos
│   ├── temp/                  # Temporary files
│   ├── requirements.txt
│   ├── COMPLETE_GUIDE.md      # Full documentation
│   └── test_workflow.py       # Test script
│
└── README.md                   # This file
```

---

## 🛠️ Tech Stack

### Frontend
- **React 19** - UI framework
- **Vite** - Build tool
- **Tailwind CSS 4** - Styling
- **Axios** - HTTP client

### Backend
- **FastAPI** - Web framework
- **LangChain + LangGraph** - AI workflow orchestration
- **OpenAI/Anthropic** - LLM providers
- **FFmpeg** - Video processing
- **Pydantic** - Data validation
- **Uvicorn** - ASGI server

---

## 🔐 Environment Variables

### Backend (.env)

```env
# LLM Configuration
LLM_PROVIDER=openai
OPENAI_API_KEY=sk-your-key-here
LLM_MODEL=gpt-4o-mini

# Or for Anthropic:
# LLM_PROVIDER=anthropic
# ANTHROPIC_API_KEY=sk-ant-your-key-here
# LLM_MODEL=claude-3-5-sonnet-20241022

# Server
HOST=0.0.0.0
PORT=8000

# CORS
CORS_ORIGINS=http://localhost:5173,http://localhost:3000

# Defaults
DEFAULT_FONT_FAMILY=Arial
DEFAULT_FONT_SIZE=32
DEFAULT_FONT_COLOR=white
```

### Frontend (.env)

```env
VITE_API_BASE_URL=http://localhost:8000
```

---

## 📚 Documentation

- **[Backend README](backend/README.md)** - Backend setup and API
- **[Frontend README](frontend/README.md)** - Frontend setup and components
- **[Complete Guide](backend/COMPLETE_GUIDE.md)** - Full usage guide
- **[Quick Start](backend/QUICKSTART.md)** - Quick setup guide

---

## 🐛 Troubleshooting

### FFmpeg not found
```bash
# Ubuntu
sudo apt install ffmpeg

# macOS
brew install ffmpeg

# Windows
# Download from https://ffmpeg.org/download.html
```

### API key not working
- Check `.env` file in backend directory
- Ensure `OPENAI_API_KEY=sk-...` is set correctly
- Restart server after changing .env

### CORS errors
- Check `CORS_ORIGINS` in backend/.env
- Default should be `http://localhost:5173`

### Session expired
- Sessions expire after 1 hour (configurable)
- Upload a new video to create new session

---

## 🚀 Deployment

### Production Mode

**Backend:**
```bash
pip install gunicorn
gunicorn app.main:app -w 4 -k uvicorn.workers.UvicornWorker
```

**Frontend:**
```bash
npm run build
# Serve dist/ folder with nginx or static hosting
```

### Docker (Coming Soon)
```bash
docker-compose up
```

---

## 🎯 Roadmap

### ✅ Completed
- [x] Video upload with validation
- [x] AI chat interface with LangGraph
- [x] Subtitle styling (font, size, color, position)
- [x] Multi-round editing
- [x] Video export with burned subtitles
- [x] Session management
- [x] Complete REST API
- [x] Frontend UI/UX
- [x] Documentation

### 🔄 Future Enhancements
- [ ] Speech-to-text (Whisper) integration
- [ ] Auto-subtitle generation
- [ ] Video trimming/cutting
- [ ] Multiple video support
- [ ] User authentication
- [ ] Database persistence (PostgreSQL)
- [ ] Cloud storage (S3)
- [ ] Docker deployment
- [ ] Batch processing
- [ ] WebSocket real-time updates

---

## 🤝 Contributing

Contributions welcome! Please:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing`)
3. Commit your changes (`git commit -m 'Add amazing feature'`)
4. Push to the branch (`git push origin feature/amazing`)
5. Open a Pull Request

---

## 📄 License

MIT License - see LICENSE file for details

---

## 🙏 Acknowledgments

- **FastAPI** - Modern Python web framework
- **LangChain** - LLM application framework
- **LangGraph** - State machine for LLM workflows
- **FFmpeg** - Video processing powerhouse
- **React** - UI library
- **OpenAI/Anthropic** - LLM providers

---

## 📞 Support

- **Issues**: [GitHub Issues](https://github.com/yourusername/AI-video-editor/issues)
- **Docs**: http://localhost:8000/api/docs (when running)
- **Email**: your.email@example.com

---

## ⭐ Star History

If you find this project useful, please consider giving it a star! ⭐

---

**Built with ❤️ using FastAPI, React, and LangGraph**

**Status**: ✅ Production Ready | All features implemented and tested
