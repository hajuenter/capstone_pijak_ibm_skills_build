# SMARTSELLER AI

Project ini adalah aplikasi web full-stack cerdas yang mengintegrasikan dashboard interaktif di sisi frontend dengan modul Artificial Intelligence (AI) untuk peramalan penjualan (sales forecasting) serta analisis data analitik mendalam. Seluruh codebase dikelola dalam satu repositori tunggal (Monorepo).

---

## Deskripsi Proyek

**SMARTSELLER AI** dirancang untuk membantu pemilik bisnis mengoptimalkan strategi penjualan melalui pendekatan berbasis data. Fitur utama dari platform ini adalah **Prediksi Omset Penjualan** secara mingguan, yang memproyeksikan total pendapatan kotor (dalam USD) yang akan diterima toko per kategori produk spesifik, yaitu:

- **Clothing** (Pakaian)
- **Electronics** (Elektronik/Teknologi)
- **Beauty** (Kecantikan)

Prediksi ini didasarkan pada data historis penjualan yang telah dikumpulkan sebelumnya. Dengan memanfaatkan algoritma Machine Learning terkemuka (**Prophet** oleh Meta), website ini mampu menganalisis tren, pola musiman, dan data dari minggu-minggu sebelumnya untuk memberikan perkiraan omset penjualan di masa depan secara akurat.

Selain fitur prediksi, platform ini juga dilengkapi dengan metrik analitik dan fitur interaktif canggih lainnya:

- **Insight Demografi (Usia & Jenis Kelamin):** Analisis karakteristik pelanggan untuk memahami target pasar secara lebih spesifik.
- **Wawasan Gemini (Gemini Insights):** Integrasi AI generatif dari Google untuk memberikan interpretasi teks otomatis, rekomendasi strategi bisnis, dan narasi cerdas berdasarkan data penjualan Anda.
- **Aliran Pasar Langsung (Live Market Stream):** Pemantauan aktivitas pasar dan menyajikan berita-berita jenis produk yang viral atau trending secara real-time untuk pengambilan keputusan yang cepat.
- **Chat Konsultasi:** Fitur komunikasi interaktif untuk berkonsultasi mengenai hasil analitik bisnis maupun performa toko.

---

## Tech Stack

| Layer        | Teknologi                                             |
| ------------ | ----------------------------------------------------- |
| **Frontend** | React + TypeScript (Vite), Tailwind CSS, Lucide Icons |
| **Backend**  | Python, FastAPI                                       |
| **AI / ML**  | Prophet (Meta), Google Gemini API                     |
| **API Docs** | Swagger UI, Redoc                                     |

---

## Struktur Proyek (Project Structure)

```text
├── be/                         # Backend Directory (Python)
│   ├── ai/                     # Modul & Pipeline AI (Prophet Forecasting, dll.)
│   ├── server/                 # Server Backend (FastAPI) Gemini Integration
│   ├── .env.example            # Template Konfigurasi Environment Backend
│   ├── .python-version         # Spesifikasi Versi Python Proyek
│   └── requirements.txt        # Dependensi Library Python
│
└── fe/                         # Frontend Directory (React + TypeScript)
    └── client/                 # React Web Application (Vite, Tailwind CSS, dll.)
        └── .env.example        # Template Konfigurasi Environment Frontend
```

---

## Cara Menjalankan Proyek

### Clone Repositori

```bash
git clone https://github.com/hajuenter/capstone_pijak_ibm_skills_build.git
cd capstone_pijak_ibm_skills_build
```

### Prasyarat

Pastikan sudah terinstal di komputer Anda:

- Python `3.13.13`
- Node.js `18+` dan npm / yarn
- Git

---

### Backend (FastAPI + Prophet)

#### 1. Masuk ke direktori backend

```bash
cd be
```

#### 2. Membuat Virtual Environment (venv)

Virtual environment mengisolasi dependensi Python agar tidak tercampur dengan instalasi global.

```bash
# Buat venv bernama "venv"
python -m venv venv
```

#### 3. Mengaktifkan Virtual Environment

```bash
# Windows (Command Prompt / PowerShell)
venv\Scripts\activate

# macOS / Linux
source venv/bin/activate
```

> Tanda bahwa venv aktif: nama `(venv)` akan muncul di awal baris terminal Anda.

#### 4. Menginstal Dependensi

```bash
pip install -r requirements.txt
```

> Untuk menonaktifkan venv, cukup jalankan perintah `deactivate`.

#### 5. Menyiapkan File `.env`

Salin file template environment:

```bash
# Windows
copy .env.example .env

# macOS / Linux
cp .env.example .env
```

Kemudian buka file `.env` dan isi nilai untuk setiap variabel:

```dotenv
GEMINI_API_KEY_A=isi_api_key_anda_di_sini
GEMINI_API_KEY_B=isi_api_key_anda_di_sini
GEMINI_API_KEY_C=isi_api_key_anda_di_sini
GEMINI_API_KEY_D=isi_api_key_anda_di_sini
```

> Dapatkan Gemini API Key di [https://aistudio.google.com/app/api-keys](https://aistudio.google.com/app/api-keys)

#### 6. Menjalankan Server FastAPI

Pastikan posisi terminal Anda berada di dalam direktori be, dan jalankan perintah ini di terminal anda

```bash
uvicorn server.main:app --reload --host 0.0.0.0 --port 8000
```

Server berjalan di `http://0.0.0.0:8000` atau `http://localhost:8000`

> Catatan: Seluruh akses API wajib menggunakan prefix /api/time-series pada base URL.

---

## API Documentation

Setelah backend berjalan, dokumentasi API dapat diakses melalui tautan berikut:

| Antarmuka      | URL Lokal                                                  | Deskripsi                                                                          |
| :------------- | :--------------------------------------------------------- | :--------------------------------------------------------------------------------- |
| **Swagger UI** | [http://localhost:8000/docs](http://localhost:8000/docs)   | Dokumentasi interaktif untuk menguji endpoint secara langsung.                     |
| **Redoc**      | [http://localhost:8000/redoc](http://localhost:8000/redoc) | Dokumentasi alternatif dengan tata letak yang bersih dan berfokus pada skema data. |

> **Tips:** Jika Anda mengakses server dari perangkat lain (seperti HP) yang berada dalam satu jaringan Wi-Fi, ganti `localhost` dengan IP lokal komputer Anda (contoh: `http://192.168.1.XX:8000/docs`).

---

## Model AI

Model forecasting yang digunakan adalah **Prophet (Meta)**, dilatih secara otomatis dari data historis penjualan. Model yang sudah dilatih disimpan di dalam repositori dan dapat diakses langsung tanpa perlu mengunduh dari sumber eksternal.

**Lokasi Penyimpanan Model:** [Unduh via Google Drive](https://drive.google.com/drive/folders/1rHVglp-hbOY_SXv7-P7iF09QTjkJ7Qim)

Untuk mengakses prediksi model, gunakan endpoint API berikut:
| Antarmuka | URL |
| ------------ | ------------------------------------------------ |
| **Forecast** | `http://localhost:8000/api/time-series/forecast` |

> **Catatan:** Untuk melihat dan menguji daftar endpoint lainnya, silakan kunjungi dokumentasi API interaktif melalui **Swagger UI** atau **Redoc** yang tersedia pada server.

---

### Frontend (React + TypeScript)

#### 1. Masuk ke direktori frontend

```bash
cd fe/client
```

#### 2. Menginstal Dependensi Node

```bash
npm install
```

#### 3. Menyiapkan File `.env`

Salin file template environment:

```bash
# Windows
copy .env.example .env

# macOS / Linux
cp .env.example .env
```

Kemudian buka file `.env` dan isi URL server backend yang sedang berjalan:

```dotenv
VITE_API_URL=http://localhost:8000
```

> **Catatan:** Jika backend di-deploy ke server, ganti `http://localhost:8000` dengan URL publik server Anda.

#### 4. Menjalankan Development Server

```bash
npm run dev
```

Aplikasi frontend berjalan di `http://localhost:5173`

---

## Live Demo

Aplikasi sudah di-deploy dan dapat diakses langsung tanpa perlu instalasi lokal:

| Layanan                  | URL                                                                                                        |
| :----------------------- | :--------------------------------------------------------------------------------------------------------- |
| **Frontend**             | [https://capstone-pijak-ibm-skills-build.vercel.app](https://capstone-pijak-ibm-skills-build.vercel.app)   |
| **Backend Base API URL** | [https://backuppijak-production.up.railway.app](https://backuppijak-production.up.railway.app)             |
| **Swagger UI**           | [https://backuppijak-production.up.railway.app/docs](https://backuppijak-production.up.railway.app/docs)   |
| **Redoc**                | [https://backuppijak-production.up.railway.app/redoc](https://backuppijak-production.up.railway.app/redoc) |

> **Catatan:** Backend di-deploy menggunakan Railway **free tier**. Jika server tidak merespons atau loading lambat, kemungkinan instance sedang dalam kondisi _sleep_ (tidak aktif). Tunggu beberapa detik lalu coba muat ulang halaman. Jika masih tidak bisa diakses, silakan jalankan proyek secara lokal mengikuti panduan di atas.

---

## Lisensi

Proyek ini dibuat sebagai bagian dari program **Pijak in collaboration with IBM SkillsBuild**.

<p align="center"><small>© 2026 hajuenter. All rights reserved.</small></p>
