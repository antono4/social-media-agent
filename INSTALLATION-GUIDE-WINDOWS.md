# 🪟 Panduan Instalasi OpenHands di Windows 11

> ⚠️ **PERHATIAN PENTING**: OpenHands membutuhkan **Docker Desktop** atau **WSL2** untuk berjalan di Windows karena memiliki dependency Unix-specific (`fcntl` module).

## Pilihan Setup

| Metode | Tingkat Kesulitan | Rekomendasi |
|--------|------------------|-------------|
| 🐳 **Docker Desktop** | ⭐ Mudah | ✅ **Disarankan** |
| 🐧 **WSL2** | ⭐⭐ Medium | Alternatif baik |

---

## ✅ Opsi A: Docker Desktop (⭐ Disarankan)

### Step 1: Install Docker Desktop

1. Download dari https://www.docker.com/products/docker-desktop/
2. Run installer
3. Restart komputer
4. Buka **Docker Desktop** (pastikan icon hijau muncul di system tray)

### Step 2: Clone Repository

```powershell
git clone https://github.com/antono4/social-media-agent.git
cd social-media-agent
```

### Step 3: Setup Agent Folder

```powershell
# Buat folder agents
New-Item -ItemType Directory -Path "$env:USERPROFILE\.openhands\agents" -Force

# Copy agent file
Copy-Item "agents\social-media-content-creator.md" "$env:USERPROFILE\.openhands\agents\"
```

### Step 4: Setup API Key

1. Buka https://app.all-hands.dev/settings/api-keys
2. Buat API key baru
3. Set environment variable:

```powershell
$env:OPENHANDS_API_KEY = "your-api-key-here"
```

### Step 5: Jalankan dengan Docker

```powershell
docker run -it `
  -v "$env:USERPROFILE\.openhands:/root/.openhands" `
  -e OPENHANDS_API_KEY="your-api-key-here" `
  allhandshub/openhands:latest
```

---

## ✅ Opsi B: WSL2 (Windows Subsystem for Linux)

### Step 1: Enable WSL2

Buka **PowerShell as Administrator**, jalankan:

```powershell
wsl --install
```

Restart komputer.

### Step 2: Setup di WSL

Buka **Ubuntu** (dari Start Menu), jalankan:

```bash
# Update sistem
sudo apt update && sudo apt upgrade -y

# Install Python
sudo apt install python3 python3-pip python3-venv git -y

# Clone repository
git clone https://github.com/antono4/social-media-agent.git
cd social-media-agent

# Setup virtual environment
python3 -m venv venv
source venv/bin/activate

# Install OpenHands
pip install openhands

# Setup API Key
export OPENHANDS_API_KEY="your-api-key-here"

# Setup agent folder
mkdir -p ~/.openhands/agents
cp agents/social-media-content-creator.md ~/.openhands/agents/
```

### Step 3: Jalankan OpenHands

```bash
# Aktifkan environment (jika belum)
source venv/bin/activate

# Jalankan
openhands
```

---

## 📋 Checklist Setup

- [ ] Docker Desktop terinstall & running **ATAU** WSL2 terinstall
- [ ] Repository sudah di-clone
- [ ] API Key sudah diset
- [ ] Agent file sudah di-copy ke `~/.openhands/agents/`
- [ ] OpenHands berhasil dijalankan

---

## 🔧 Troubleshooting

### Docker Error: "docker daemon is not running"

1. Buka **Docker Desktop**
2. Tunggu sampai icon hijau muncul
3. Atau restart Docker service: `Restart-Service com.docker.Service`

### WSL Error: "WSL is not installed"

```powershell
# Buka PowerShell as Admin
wsl --install -d Ubuntu
```

### Error: "ModuleNotFoundError: No module named 'fcntl'"

✅ **Normal untuk Python direct install** - Gunakan Docker atau WSL2 sebagai gantinya.

---

## 🚀 Quick Start (Setelah Setup)

1. Buka Docker Desktop **ATAU** Ubuntu (WSL)
2. Jalankan OpenHands
3. Ketik request Anda:

```
Load the social-media-content-creator agent
```

---

## 📚 Struktur Folder

```
%USERPROFILE%\.openhands\  (Windows)
~/.openhands/               (WSL/Linux)
└── agents\
    └── social-media-content-creator.md
```

---

## Butuh Bantuan?

- 📖 Dokumentasi Resmi: https://docs.openhands.dev/
- 🐳 Docker Docs: https://docs.docker.com/
- 🐧 WSL Docs: https://docs.microsoft.com/en-us/windows/wsl/

---

*Updated: Python direct install TIDAK didukung karena OpenHands membutuhkan modul Unix. Gunakan Docker atau WSL2.*
