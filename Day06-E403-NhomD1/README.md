# 🚀 Thư Ký Kim — Máy Dịch Khái Niệm AI Sang Ngôn Ngữ Đời Thường

> **Hackathon Day 06 — Nhóm D1 | AI.20K Cohort 2**

## 📝 Mô Tả Sản Phẩm

**Thư ký Kim** giúp học viên hiểu các khái niệm AI/ML phức tạp bằng cách tạo **analogy cá nhân hoá** dựa trên sở thích của người dùng.

**Ví dụ:** Nhập khái niệm `RAG` + sở thích `bóng đá` → AI sinh ra câu chuyện giải thích RAG qua bóng đá kèm bảng mapping chi tiết từng thành phần kỹ thuật.

Sản phẩm gồm 3 tính năng chính:
- 🔍 **Analogy Engine** — Sinh analogy narrative + bảng mapping qua LangGraph Agent
- 💬 **Thư ký Kim Chat** — Chatbot hỏi đáp đa lượt, bám sát nội dung khóa học
- 📄 **PDF Viewer** — Xem slide bài giảng, bôi đen thuật ngữ để tra ngay

---

## 👥 Thành Viên Nhóm

| STT | Họ và Tên | MSSV | Vai trò |
|:---:|-----------|------|---------|
| 1 | Hoàng Đức Dũng | 2A202600814 | Repo owner, evidence, slide, API key admin |
| 2 | Vũ Quang Vinh | 2A202600935 | Code AI core |
| 3 | Nguyễn Trần Kiên | 2A202600739 | Viết system prompt |
| 4 | Đinh Văn Anh Khôi | 2A202600615 | Code Backend |
| 5 | Đoàn Công Phú | 2A202600929 | Code Frontend |

---

## 🚀 Hướng Dẫn Chạy Prototype

### Yêu cầu hệ thống

- **Python** ≥ 3.11
- **pip** hoặc **uv** (trình quản lý package)
- Một API key từ **OpenAI**, **Google Gemini**, hoặc **Ollama** đang chạy local

### Bước 1 — Clone repo

```bash
git clone <URL_REPO>
cd Day06-E403-NhomD1/codebase
```

### Bước 2 — Cài đặt dependencies

```bash
# Cách 1: dùng pip
pip install -r requirements.txt

# Cách 2: dùng uv (nhanh hơn)
uv pip install -r requirements.txt

# Cách 3: cài từ pyproject.toml
pip install -e .
```

### Bước 3 — Cấu hình biến môi trường

Tạo file `.env` trong thư mục `codebase/` (copy từ `.env.example`):

```bash
cp .env.example .env
```

Mở file `.env` và điền các giá trị:

```dotenv
# ── Bắt buộc: chọn MỘT trong ba provider bên dưới ──

# Provider 1: OpenAI
API_KEY=sk-xxxxxxxxxxxxxxxx        # API key OpenAI
LLM_ENDPOINT=https://api.openai.com/v1
MODEL=gpt-4o                       # Model sử dụng

# Provider 2: Google Gemini (qua OpenAI-compatible endpoint)
API_KEY=AIzaSy...                   # Google API key
LLM_ENDPOINT=https://generativelanguage.googleapis.com/v1beta/openai/
MODEL=gemini-2.5-flash

# Provider 3: Ollama (chạy local, không cần API key)
API_KEY=ollama                      # Giá trị bất kỳ
LLM_ENDPOINT=http://localhost:11434/v1
MODEL=qwen3.5:0.8b
```

> **Lưu ý:** Chỉ cần điền thông tin **một provider**. Server sử dụng `ChatOpenAI` (LangChain) với `base_url` tuỳ chỉnh nên tương thích với mọi provider có OpenAI-compatible API.

### Bước 4 — Khởi chạy server

```bash
uvicorn server:app --reload --port 8000
```

Mở trình duyệt tại: **http://localhost:8000**

### Bước 5 — (Tuỳ chọn) Chia sẻ URL public qua ngrok

```bash
ngrok http 8000
# → URL public dạng: https://xxxx.ngrok.io
```

### Chạy bằng CLI (không cần giao diện)

```bash
python main.py
# → Nhập khái niệm AI cần hiểu: RAG
# → Nhập sở thích cá nhân: bóng đá
# → Kết quả in ra terminal
```

---

## 🛠️ Công Nghệ, Công Cụ & API Đã Sử Dụng

### Model AI / LLM

| Model | Provider | Ghi chú |
|-------|----------|---------|
| **GPT-4o** | OpenAI | Model mặc định |
| **Gemini 2.5 Flash** | Google | Thay thế qua biến môi trường |
| **Qwen 3.5 (0.8B)** | Ollama (local) | Chạy offline, không tốn API |

Tất cả được gọi qua **`ChatOpenAI`** (LangChain) với `base_url` linh hoạt → dễ đổi provider.

### Framework & Thư viện Backend

| Công cụ | Phiên bản | Mục đích |
|---------|-----------|----------|
| **FastAPI** | ≥ 0.115 | Web framework REST API |
| **Uvicorn** | ≥ 0.34 | ASGI server chạy FastAPI |
| **LangGraph** | ≥ 0.6 | Orchestrate agent dạng state graph (check → evaluate → generate) |
| **LangChain** | ≥ 1.0 | Abstraction layer gọi LLM |
| **LangChain-OpenAI** | ≥ 1.2 | Connector OpenAI-compatible APIs |
| **LangChain-Google-GenAI** | ≥ 2.1 | Connector Google Gemini |
| **LangChain-Ollama** | ≥ 0.3 | Connector Ollama local |
| **Pydantic** | ≥ 2.8 | Validation request/response schemas |
| **python-dotenv** | ≥ 1.0 | Load biến môi trường từ `.env` |

### Công cụ dựng giao diện (Frontend)

| Công cụ | Mục đích |
|---------|----------|
| **HTML5 + CSS3 + Vanilla JS** | Giao diện single-page, không dùng framework JS |
| **PDF.js** (v3.11.174, CDN) | Render PDF trong trình duyệt + text layer cho bôi đen |
| **Tabler Icons** (CDN) | Bộ icon SVG cho UI |
| **localStorage** | Lưu lịch sử tra cứu (tối đa 50 mục) |

### Hạ tầng & DevOps

| Công cụ | Mục đích |
|---------|----------|
| **ngrok** | Tunnel localhost ra URL public để demo |
| **Git** | Quản lý mã nguồn |

---

## 📁 Cấu Trúc Thư Mục

```
Day06-E403-NhomD1/
├── README.md                   # ← Bạn đang đọc file này
├── spec/
│   └── spec.md                 # SPEC sản phẩm (AI Product Canvas)
└── codebase/
    ├── server.py               # FastAPI backend + LangGraph agent
    ├── main.py                 # Entry point CLI
    ├── pyproject.toml          # Cấu hình project & dependencies
    ├── requirements.txt        # Dependencies cho pip install
    ├── .env.example            # Mẫu biến môi trường
    ├── uv.lock                 # Lock file (uv)
    ├── static/
    │   ├── index.html          # Giao diện chính (PDF viewer + Analogy + Chat)
    │   └── index-old.html      # Phiên bản cũ (không sử dụng)
    └── logs/
        └── feedback.jsonl      # Log feedback từ người dùng
```

---

## 🔄 Kiến Trúc LangGraph Agent

```
check_input
  ├─ Sở thích mơ hồ → ask_clarify → END (hỏi lại user)
  └─ Sở thích rõ    → evaluate_confidence
                        ├─ confidence < 0.6 → fallback → END (gợi ý sửa)
                        └─ confidence ≥ 0.6 → generate_analogy → END ✅
```

---

## 🌐 API Endpoints

| Method | Endpoint | Mô tả |
|--------|----------|-------|
| `POST` | `/api/analogy` | Sinh analogy từ khái niệm + sở thích |
| `POST` | `/api/feedback` | Ghi feedback (accept / regenerate / fix / report) |
| `POST` | `/api/chat` | Chat đa lượt với Thư ký Kim |
| `GET` | `/health` | Health check |
| `GET` | `/` | Giao diện web (static HTML) |
| `GET` | `/public/*` | Serve PDF bài giảng |

---

<p align="center">
  <i>Hackathon - Day 06 | Nhóm D1 © 2026</i>
</p>