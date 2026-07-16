# 🪟 Panduan Instalasi OpenHands di Windows 11 (Python Direct)

Panduan ini akan membantu Anda setup OpenHands di Windows 11 tanpa Docker.

## Prasyarat

- Windows 11 (64-bit)
- Minimum 8GB RAM (disarankan 16GB)
- Minimal 10GB free disk space

---

## Step 1: Install Python

### Cara 1: Microsoft Store (⭐ Disarankan untuk Pemula)

1. Buka **Microsoft Store**
2. Cari **"Python 3.11"** atau **"Python 3.12"**
3. Klik **Install**
4. Pastikan centang **"Add Python to PATH"**

### Cara 2: Download Manual

1. Kunjungi https://www.python.org/downloads/windows/
2. Download installer **Python 3.11** atau **3.12**
3. Run installer
4. **PENTING**: Centang **"Add Python to PATH"** di bawah
5. Klik **"Install Now"**

### Verifikasi Python

Buka **Command Prompt** atau **PowerShell**, ketik:

```bash
python --version
```

Seharusnya muncul: `Python 3.11.x` atau `Python 3.12.x`

---

## Step 2: Install Git

Git diperlukan untuk clone repository dan management.

1. Download dari https://git-scm.com/download/win
2. Run installer dengan setting default
3. Verifikasi dengan command:

```bash
git --version
```

---

## Step 3: Clone OpenHands Repository

Buka **PowerShell** atau **Command Prompt**, jalankan:

```bash
# Clone repository
git clone https://github.com/All-Hands-AI/OpenHands.git

# Masuk ke folder
cd OpenHands
```

---

## Step 4: Setup Virtual Environment (Disarankan)

```bash
# Buat virtual environment
python -m venv venv

# Aktifkan virtual environment
.\venv\Scripts\activate

# Upgrade pip
pip install --upgrade pip
```

---

## Step 5: Install Dependencies

```bash
# Install OpenHands dengan semua dependencies
pip install openhands

# Atau jika ingin install dari source
pip install -e .
```

---

## Step 6: Setup API Key

OpenHands membutuhkan LLM API key. Pilihan:

### Opsi A: OpenHands Cloud (⭐ Termudah)
1. Buka https://app.all-hands.dev/settings/api-keys
2. Buat API key baru
3. Set environment variable:

```bash
setx OPENHANDS_API_KEY "your-api-key-here"
```

### Opsi B: Provider Lain (OpenAI, Anthropic, dll)

```bash
# OpenAI
setx OPENAI_API_KEY "sk-your-key-here"

# Anthropic
setx ANTHROPIC_API_KEY "sk-ant-your-key-here"
```

**Catatan**: `setx` akan persisten. Tutup dan buka terminal baru setelahnya.

---

## Step 7: Buat Folder Agent

Copy file agent ke folder user-level:

```bash
# Buat folder agents (jika belum ada)
mkdir %USERPROFILE%\.openhands\agents

# Copy agent file
copy agents\social-media-content-creator.md %USERPROFILE%\.openhands\agents\
```

---

## Step 8: Jalankan OpenHands

### Mode Interaktif (CLI)

```bash
openhands
```

### Mode Headless (untuk automasi)

```bash
openhands --headless
```

### Dengan model spesifik

```bash
setx LLM_MODEL "anthropic/claude-sonnet-4-5-20250929"
openhands
```

---

## Step 9: Verifikasi Agent Terdaftar

Setelah OpenHands berjalan, ketik:

```
Load the social-media-content-creator agent
```

Agent akan aktif dan siap digunakan!

---

## Troubleshooting

### Error: "Python is not recognized"

1. Buka **System Properties** → **Environment Variables**
2. Edit **PATH**, tambahkan:
   - `C:\Users\YourUsername\AppData\Local\Programs\Python\Python311\`
   - `C:\Users\YourUsername\AppData\Local\Programs\Python\Python311\Scripts\`

### Error: "Permission denied" saat install

Jalankan PowerShell sebagai Administrator.

### Error: SSL/TLS certificates

```bash
pip install --upgrade certifi
```

### Virtual environment tidak activate

```bash
# Pastikan Execution Policy允许
Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser

# Aktifkan ulang
.\venv\Scripts\activate
```

---

## Quick Command Reference

```bash
# Clone & Setup
git clone https://github.com/All-Hands-AI/OpenHands.git
cd OpenHands

# Setup environment
python -m venv venv
.\venv\Scripts\activate
pip install openhands

# Set API Key (ganti dengan key Anda)
setx OPENHANDS_API_KEY "your-api-key-here"

# Copy agent
mkdir %USERPROFILE%\.openhands\agents
copy agents\social-media-content-creator.md %USERPROFILE%\.openhands\agents\

# Jalankan
openhands
```

---

## Struktur Folder Akhir

```
%USERPROFILE%\.openhands\
└── agents\
    └── social-media-content-creator.md  ← Agent Anda
```

---

## Tips & Best Practices

1. **Selalu gunakan virtual environment** - Menghindari conflict antar project
2. **Restart terminal** setelah set environment variables
3. **Update regularly** - Jalankan `pip install --upgrade openhands` secara berkala
4. **Backup API keys** - Simpan di tempat aman

---

## Butuh Bantuan?

- 📖 Dokumentasi: https://docs.openhands.dev/
- 💬 GitHub Issues: https://github.com/All-Hands-AI/OpenHands/issues
- 📝 Dokumentasi Agent: https://docs.openhands.dev/sdk/guides/agent-file-based

---

*Panduan ini dibuat untuk Windows 11 dengan Python direct install. Untuk setup dengan Docker atau WSL2, lihat dokumentasi resmi OpenHands.*
