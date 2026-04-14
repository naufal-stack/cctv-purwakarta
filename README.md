# 🚀 Mata Plat Engine: Multi-Gate AI ALPR
> **Advanced Smart Parking Solution** berbasis Deep Learning untuk deteksi kendaraan dan pengenalan plat nomor otomatis secara simultan pada banyak jalur kamera.

[![Python Version](https://img.shields.io/badge/python-3.9+-blue.svg?style=for-the-badge&logo=python&logoColor=white)](https://www.python.org/downloads/)
[![YOLOv8](https://img.shields.io/badge/Model-YOLOv8-success.svg?style=for-the-badge&logo=github)](https://ultralytics.com)
[![PaddleOCR](https://img.shields.io/badge/OCR-PaddleOCR-orange.svg?style=for-the-badge)](https://github.com/PaddlePaddle/PaddleOCR)
[![GPU Accelerated](https://img.shields.io/badge/Hardware-GPU--Enabled-red.svg?style=for-the-badge&logo=nvidia)](https://developer.nvidia.com/cuda-toolkit)

---

## 📌 Overview
**Mata Plat Engine** adalah inti pemrosesan (engine) dari ekosistem Smart Parking yang dikembangkan oleh **Pratama Solusi Teknologi**. Sistem ini menggunakan arsitektur *Multi-Threaded Shared Resource* yang memungkinkan pemrosesan banyak *stream* RTSP kamera gerbang secara bersamaan namun tetap hemat penggunaan VRAM.

### ✨ Fitur Unggulan
- 📹 **Multi-RTSP Stream**: Menangani banyak gerbang (entry/exit) dalam satu instance aplikasi.
- ⚙️ **Dynamic Configuration**: Mengambil daftar URL kamera secara otomatis melalui Dashboard API.
- 🧠 **Smart State Machine**: Mendeteksi apakah kendaraan sedang bergerak atau berhenti untuk efisiensi pemicuan OCR.
- 💎 **High Accuracy**: Kombinasi YOLOv8 untuk deteksi plat dan PaddleOCR untuk pembacaan teks yang presisi.
- 🔄 **Auto-Sync**: Sinkronisasi data kejadian (event) secara *real-time* ke MySQL dan Dashboard Management.

---

## 🛠️ Arsitektur Sistem
Sistem berjalan dengan membagi beban kerja ke dalam beberapa komponen utama:

| Komponen | Deskripsi |
| :--- | :--- |
| **Main Thread** | Mengelola siklus hidup aplikasi dan konfigurasi dinamis. |
| **Gate Engine Thread** | Unit pemrosesan independen untuk setiap jalur kamera (Multi-threading). |
| **Unified OCR Worker** | Worker tunggal berbasis *Queue* untuk memproses antrean gambar plat dari seluruh gerbang. |
| **Async Video Buffer** | Menangani *latency* RTSP agar frame tetap *up-to-date* tanpa membebani thread utama. |

---

## 📦 Persiapan & Instalasi

### 1. Prasyarat
- Python 3.9 ke atas.
- NVIDIA GPU (Sangat disarankan) dengan CUDA Toolkit terinstal.
- Driver MySQL.

### 2. Instalasi Dependensi
```bash
git clone [https://github.com/username/mata-plat-engine.git](https://github.com/username/mata-plat-engine.git)
cd mata-plat-engine
pip install -r requirements.txt
