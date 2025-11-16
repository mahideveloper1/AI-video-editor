# AI Video Editor

✅ **FULLY IMPLEMENTED** - Full-Stack AI-Powered Chat-Based Video Subtitle Editor

A complete full-stack application for intelligent video subtitle editing using natural language. Built with **FastAPI**, **React 19**, **LangGraph**, **Google Gemini AI**, and **FFmpeg**.

![Status](https://img.shields.io/badge/status-complete-success)
![Backend](https://img.shields.io/badge/backend-FastAPI-009688)
![Frontend](https://img.shields.io/badge/frontend-React_19-61DAFB)
![AI](https://img.shields.io/badge/AI-Gemini_+_LangGraph-7B68EE)

---

## 🎥 About

AI Video Editor revolutionizes subtitle editing by allowing you to use natural language instead of manual timing and styling. Simply chat with the AI - "add 'Hello World' at 5 seconds in red color" - and watch as it handles all the technical details.

The application features real-time preview, multi-round editing, and exports professional videos with permanently burned-in subtitles.

---

## ✨ Key Features

### 🤖 Intelligent Chat-Based Editing
- **Natural Language Commands**: "Add 'Hello' at 5 seconds with red color, size 48"
- **Context-Aware**: "Make the previous subtitle blue"
- **Smart Modification**: Edit existing subtitles by referencing them
- **Flexible Time Parsing**: Supports "5 seconds", "1:30", "2 minutes", etc.

### 🎨 Advanced Subtitle Styling
- **Colors**: Named colors (red, blue, yellow) or hex codes (#FF0000)
- **Fonts**: Arial, Helvetica, Roboto, Times New Roman, and more
- **Sizes**: 12-72 pixels
- **Position**: Top, center, or bottom
- **Styles**: Bold, italic, or combinations

### 👁️ Real-Time Preview & Export
- **Live Preview**: See subtitles overlaid on video instantly
- **Separate Preview Button**: Generate and review video before downloading
- **Smart Export**: Download only when satisfied with results
- **Multi-Round Editing**: Continue editing and re-exporting the same video

### 🔄 Intelligent Subtitle Modification
- **Reference Previous Subtitles**: "Make the last subtitle red"
- **Index-Based Editing**: "Change subtitle 1 to size 48"
- **Contextual Understanding**: AI knows which subtitle you're referring to
- **Partial Updates**: Only changes what you specify, keeps the rest

### 🎯 User-Friendly Interface
- **Drag & Drop Upload**: Simple video upload interface
- **Clean Chat UI**: Spacious text input with visual feedback
- **Responsive Video Player**: Adapts to screen size with visible controls
- **Side-by-Side Actions**: Preview and Download buttons for clear workflow

---

## 🚀 Quick Start

### Prerequisites

Before you begin, ensure you have the following installed:

- **Python 3.9+** - [Download Python](https://www.python.org/downloads/)
- **Node.js 18+** - [Download Node.js](https://nodejs.org/)
- **FFmpeg** - Video processing library
  - **Windows**: Download from [ffmpeg.org](https://ffmpeg.org/download.html) and add to PATH
  - **macOS**: `brew install ffmpeg`
  - **Linux**: `sudo apt install ffmpeg`
- **Google Gemini API Key** - [Get API Key](https://makersuite.google.com/app/apikey) (Free tier available)

### 1. Clone Repository

```bash
git clone https://github.com/mahideveloper1/AI-video-editor.git
cd AI-video-editor
```

### 2. Backend Setup

#### Install Dependencies

```bash
cd backend
pip install -r requirements.txt
```

#### Configure Environment

Create a `.env` file in the `backend` directory:

```env
# backend/.env

# LLM Configuration
LLM_PROVIDER=google
LLM_MODEL=gemini-1.5-flash
LLM_TEMPERATURE=0.7

# Google Gemini API Key (Get from https://makersuite.google.com/app/apikey)
GOOGLE_API_KEY=your_gemini_api_key_here

# Optional: Other LLM Providers
# OPENAI_API_KEY=your_openai_key_here
# ANTHROPIC_API_KEY=your_anthropic_key_here

# Server Configuration
HOST=0.0.0.0
PORT=8000

# CORS Origins (comma-separated)
CORS_ORIGINS=http://localhost:5173,http://localhost:3000

# File Storage Directories
UPLOAD_DIR=uploads
OUTPUT_DIR=outputs
TEMP_DIR=temp

# Video Processing Settings
MAX_FILE_SIZE=524288000
ALLOWED_EXTENSIONS=mp4,avi,mov,mkv,webm
VIDEO_QUALITY=medium
FFMPEG_THREADS=4

# Subtitle Defaults
DEFAULT_FONT_FAMILY=Arial
DEFAULT_FONT_SIZE=24
DEFAULT_FONT_COLOR=white
DEFAULT_SUBTITLE_POSITION=bottom

# Session Management
SESSION_TIMEOUT=3600
```

#### Start Backend Server

```bash
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

Backend will be available at: **http://localhost:8000**

API Documentation: **http://localhost:8000/docs**

### 3. Frontend Setup

#### Install Dependencies

```bash
cd ../frontend
npm install
```

#### Configure Environment (Optional)

Create `.env` file in the `frontend` directory if you need custom API URL:

```env
# frontend/.env
VITE_API_BASE_URL=http://localhost:8000
```

#### Start Development Server

```bash
npm run dev
```

Frontend will be available at: **http://localhost:5173**

### 4. Verify Installation

1. **Check FFmpeg**: Run `ffmpeg -version` in terminal
2. **Test Backend**: Visit http://localhost:8000/docs
3. **Test Frontend**: Visit http://localhost:5173
4. **Upload a video** and try adding a subtitle!

---

## 📖 Usage Guide

### Basic Workflow

#### 1. Upload Video
```
- Click upload area or drag & drop a video file
- Supported formats: MP4, AVI, MOV, MKV, WEBM
- Max file size: 500MB
- Video metadata extracted automatically
```

#### 2. Add Subtitles via Chat

**Simple Examples:**
```
"Add subtitle 'Hello World' from 0 to 5 seconds"
"Add 'Welcome!' at 10 seconds with red color"
"Add 'Chapter 1' from 1:30 to 1:35, size 48, bold"
```

**Advanced Examples:**
```
"Add 'The End' from 2 minutes to 2:10 with yellow color, Arial font, position top"
"Add subtitle 'Important!' at 30 seconds, size 36, red, bold, italic"
```

#### 3. Modify Existing Subtitles

**Reference by Position:**
```
"Make the previous subtitle red"
"Change the last subtitle to blue"
"Make the last one bigger"
```

**Reference by Index:**
```
"Make subtitle 1 bigger"
"Change subtitle 2 to size 48"
"Change the first subtitle to yellow"
```

#### 4. Preview Video
```
- Click "Preview Video" button
- Video generates with burned-in subtitles
- Review in video player
- Make more edits if needed
```

#### 5. Download Video
```
- Click "Download Video" button
- Video downloads with all subtitles permanently burned in
- Continue editing or start a new session
```

### Advanced Features

#### Time Format Options
```
Seconds:           "5 seconds", "10s", "15"
Minutes:Seconds:   "1:30", "2:45", "0:30"
Full Format:       "2 minutes 30 seconds"
Hours:Min:Sec:     "1:30:45"
```

#### Color Options
```
Named Colors:  red, blue, green, yellow, white, black, orange, purple, pink
Hex Codes:     #FF0000, #00FF00, #0000FF, #FFFF00
RGB:           rgb(255, 0, 0)
```

#### Font Options
```
Common Fonts:  Arial, Helvetica, Roboto, Times New Roman
System Fonts:  Georgia, Verdana, Courier New, Comic Sans MS
Custom:        Any font name installed on the system
```

#### Styling Options
```
Size:      12-72 pixels (e.g., "size 48")
Position:  top, center, bottom
Bold:      "bold" or "make it bold"
Italic:    "italic" or "make it italic"
```

---

## 🏗️ Architecture

```
┌─────────────────────────────────────────────────────────────────┐
│                         FRONTEND (React 19)                      │
│                                                                  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐          │
│  │VideoUploader │  │VideoPlayer   │  │ChatInterface │          │
│  └──────────────┘  └──────────────┘  └──────────────┘          │
│  ┌──────────────┐  ┌──────────────┐                            │
│  │PreviewButton │  │ExportButton  │                            │
│  └──────────────┘  └──────────────┘                            │
└────────────────────────┬───────────────────────────────────────┘
                         │ REST API (Axios)
┌────────────────────────▼───────────────────────────────────────┐
│                   BACKEND (FastAPI + Python)                    │
│                                                                  │
│  ┌──────────────┐  ┌──────────────┐  ┌──────────────┐         │
│  │Upload Route  │  │Chat Route    │  │Export Route  │         │
│  └──────┬───────┘  └──────┬───────┘  └──────┬───────┘         │
│         │                  │                  │                  │
│         │       ┌──────────▼──────────┐      │                  │
│         │       │  LangGraph Workflow  │      │                  │
│         │       │  ┌────────────────┐ │      │                  │
│         │       │  │ Parse Intent   │ │      │                  │
│         │       │  └────────┬───────┘ │      │                  │
│         │       │  ┌────────▼───────┐ │      │                  │
│         │       │  │Extract Params  │ │      │                  │
│         │       │  └────────┬───────┘ │      │                  │
│         │       │  ┌────────▼───────┐ │      │                  │
│         │       │  │ Apply Edits    │ │      │                  │
│         │       │  └────────┬───────┘ │      │                  │
│         │       │  ┌────────▼───────┐ │      │                  │
│         │       │  │Generate Reply  │ │      │                  │
│         │       │  └────────────────┘ │      │                  │
│         │       └─────────────────────┘      │                  │
│         │                  │                  │                  │
│  ┌──────▼──────────────────▼──────────────────▼───────┐         │
│  │              Services Layer                        │         │
│  │  ┌──────────┐ ┌──────────┐ ┌──────────┐          │         │
│  │  │  Video   │ │ Subtitle │ │ Session  │          │         │
│  │  │ Service  │ │ Service  │ │ Manager  │          │         │
│  │  │(FFmpeg)  │ │(SRT/ASS) │ │(Memory)  │          │         │
│  │  └──────────┘ └──────────┘ └──────────┘          │         │
│  └───────────────────────────────────────────────────┘         │
└────────────────────────┬───────────────────────────────────────┘
                         │
                         ▼
              ┌──────────────────────┐
              │  Google Gemini API    │
              │  (gemini-1.5-flash)   │
              └──────────────────────┘
```

---

## 🛠️ Tech Stack

### Frontend
- **React 19** - Latest UI framework with improved features
- **Vite** - Lightning-fast build tool and dev server
- **Tailwind CSS 4** - Utility-first CSS framework
- **Axios** - Promise-based HTTP client

### Backend
- **FastAPI** - Modern, high-performance Python web framework
- **LangGraph** - State machine for LLM workflow orchestration
- **LangChain** - Framework for developing LLM applications
- **Google Gemini 1.5 Flash** - Fast, efficient AI language model
- **FFmpeg** - Complete video processing solution
- **Pydantic** - Data validation using Python type annotations
- **Uvicorn** - Lightning-fast ASGI server

### Infrastructure
- **FFmpeg** - Video encoding, subtitle burning
- **Python 3.9+** - Backend runtime
- **Node.js 18+** - Frontend runtime

---

## 📁 Project Structure

```
AI-video-editor/
├── backend/                       # FastAPI Backend
│   ├── app/
│   │   ├── main.py               # Application entry point
│   │   ├── config.py             # Configuration management
│   │   ├── api/
│   │   │   └── routes/
│   │   │       ├── upload.py     # Video upload endpoint
│   │   │       ├── chat.py       # Chat processing endpoint
│   │   │       └── export.py     # Video export endpoint
│   │   ├── models/
│   │   │   ├── schemas.py        # Pydantic models
│   │   │   └── state.py          # LangGraph state definitions
│   │   ├── services/
│   │   │   ├── llm_service.py    # LangGraph workflow
│   │   │   ├── video_service.py  # FFmpeg integration
│   │   │   └── subtitle_service.py # SRT/ASS generation
│   │   └── utils/
│   │       ├── session.py        # Session management
│   │       └── helpers.py        # Utility functions
│   ├── uploads/                  # Uploaded videos
│   ├── outputs/                  # Exported videos
│   ├── temp/                     # Temporary subtitle files
│   ├── requirements.txt          # Python dependencies
│   └── .env                      # Environment variables
│
├── frontend/                      # React Frontend
│   ├── src/
│   │   ├── components/
│   │   │   ├── VideoUploader.jsx
│   │   │   ├── VideoPlayer.jsx
│   │   │   ├── ChatInterface.jsx
│   │   │   ├── ChatMessage.jsx
│   │   │   ├── PreviewButton.jsx
│   │   │   └── ExportButton.jsx
│   │   ├── hooks/
│   │   │   └── useVideoSession.js
│   │   ├── services/
│   │   │   └── api.js            # API client
│   │   ├── utils/
│   │   │   ├── constants.js
│   │   │   └── helpers.js
│   │   ├── App.jsx               # Main application
│   │   └── main.jsx              # Entry point
│   ├── package.json              # Node dependencies
│   └── vite.config.js            # Vite configuration
│
└── README.md                      # This file
```

---

## 🔧 Configuration

### LLM Provider Options

The application supports multiple LLM providers. Configure in `backend/.env`:

**Google Gemini (Recommended - Free Tier)**
```env
LLM_PROVIDER=google
LLM_MODEL=gemini-1.5-flash
GOOGLE_API_KEY=your_key_here
```

**OpenAI**
```env
LLM_PROVIDER=openai
LLM_MODEL=gpt-4o-mini
OPENAI_API_KEY=your_key_here
```

**Anthropic Claude**
```env
LLM_PROVIDER=anthropic
LLM_MODEL=claude-3-haiku-20240307
ANTHROPIC_API_KEY=your_key_here
```

### Video Quality Settings

Configure in `backend/.env`:
- `VIDEO_QUALITY=high` - Best quality (CRF 18, slower, larger files)
- `VIDEO_QUALITY=medium` - Balanced (CRF 23, recommended)
- `VIDEO_QUALITY=low` - Fast processing (CRF 28, smaller files)

---

## 🐛 Troubleshooting

### Common Issues

**Issue: FFmpeg not found**
```
Error: FFmpeg is not installed or not accessible
```
**Solution:**
- Windows: Download from [ffmpeg.org](https://ffmpeg.org/download.html), extract, and add to PATH
- macOS: `brew install ffmpeg`
- Linux: `sudo apt install ffmpeg`
- Verify: `ffmpeg -version`

**Issue: Invalid API key**
```
Error: 401 Invalid authentication credentials
```
**Solution:**
- Check `.env` file has correct `GOOGLE_API_KEY`
- Get free key from https://makersuite.google.com/app/apikey
- Restart backend server after updating `.env`

**Issue: Video upload fails**
```
Error: File too large or unsupported format
```
**Solution:**
- Check file size is under 500MB (configurable in `.env`)
- Use supported formats: MP4, AVI, MOV, MKV, WEBM
- Ensure video is not corrupted

**Issue: Subtitle export fails on Windows**
```
Error: Unable to parse subtitle path
```
**Solution:**
- Ensure no special characters in file paths
- Avoid spaces in directory names if possible
- Restart backend server
- Check FFmpeg is properly installed

**Issue: Port already in use**
```
Error: Address already in use
```
**Solution:**
- Change port in `backend/.env`: `PORT=8001`
- Or kill process using port 8000: `lsof -ti:8000 | xargs kill` (Mac/Linux)
- Windows: `netstat -ano | findstr :8000` then `taskkill /PID <PID> /F`

**Issue: CORS errors in browser**
```
Error: Access blocked by CORS policy
```
**Solution:**
- Check `CORS_ORIGINS` in `backend/.env` includes frontend URL
- Default should be `http://localhost:5173`
- Restart backend after changing `.env`

**Issue: Duplicate subtitles in preview**
```
Subtitles appear twice during preview
```
**Solution:** This has been fixed in the latest version. Update your code or reload the page.

---

## 📚 API Documentation

Once the backend is running, visit:

- **Swagger UI**: http://localhost:8000/docs
- **ReDoc**: http://localhost:8000/redoc

### Key Endpoints

```
POST   /api/upload              Upload video file
POST   /api/chat                Process chat message and add/modify subtitles
POST   /api/export              Export video with burned subtitles
GET    /api/download/{filename} Download exported video
GET    /uploads/{filename}      Access uploaded video
GET    /outputs/{filename}      Access exported video
```

---

## 🎯 Feature Highlights

### ✅ Implemented Features

- [x] **Video Upload** - Drag & drop, file validation, metadata extraction
- [x] **AI Chat Interface** - Natural language subtitle editing
- [x] **LangGraph Workflow** - 4-node intelligent processing pipeline
- [x] **Subtitle Modification** - Edit existing subtitles by reference
- [x] **Smart Styling** - Font, size, color, position, bold, italic
- [x] **Time Parsing** - Multiple time format support
- [x] **Real-Time Preview** - Live subtitle overlay
- [x] **Separate Preview** - Generate and review before download
- [x] **Video Export** - FFmpeg subtitle burning
- [x] **Session Management** - Persistent editing sessions
- [x] **Multi-Round Editing** - Continue editing same video
- [x] **Responsive UI** - Clean, modern interface
- [x] **Error Handling** - Comprehensive error messages
- [x] **API Documentation** - Auto-generated Swagger docs

### 🔄 Future Enhancements

- [ ] **Auto-Subtitle Generation** - Whisper AI integration for automatic transcription
- [ ] **Multi-Language Support** - Support for multiple subtitle tracks
- [ ] **Video Trimming** - Cut and trim videos
- [ ] **Batch Processing** - Process multiple videos at once
- [ ] **User Authentication** - User accounts and saved projects
- [ ] **Database Persistence** - PostgreSQL for permanent storage
- [ ] **Cloud Storage** - S3/Google Cloud for video files
- [ ] **Docker Deployment** - Containerized deployment
- [ ] **WebSocket Updates** - Real-time processing updates
- [ ] **Advanced Animations** - Subtitle transitions and effects

---

## 🤝 Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

---

## 🙏 Acknowledgments

- **FastAPI** - Modern Python web framework
- **LangChain & LangGraph** - LLM application framework and workflow orchestration
- **Google Gemini** - Powerful AI language model with free tier
- **FFmpeg** - Complete video processing solution
- **React Team** - For the amazing React 19
- **Vite Team** - Lightning-fast build tool
- **Tailwind CSS** - Excellent utility-first CSS framework

---

## 📞 Support & Contact

- **GitHub Issues**: [Report Issues](https://github.com/mahideveloper1/AI-video-editor/issues)
- **Documentation**: http://localhost:8000/docs (when running)
- **Developer**: Mahi Developer

---

## ⭐ Star This Repository

If you find this project useful, please consider giving it a star! ⭐

Your support helps make this project better.

---

**Built with ❤️ using FastAPI, React 19, Google Gemini, and LangGraph**

**Status**: ✅ Production Ready | All core features implemented and tested
