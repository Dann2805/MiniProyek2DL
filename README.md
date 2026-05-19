# MiniProyek2DL
📄 README.md

Mini Proyek 2: Automated Essay Scoring (AES) 2.0 Berbasis LLM
Repositori/Arsip ini berisi implementasi proyek Automated Essay Scoring (AES) 2.0, sebuah sistem penilaian esai siswa secara otomatis menggunakan Large Language Model (LLM). Proyek ini difokuskan pada penggunaan infrastruktur komputasi ringan (CPU-only) sehingga memanfaatkan Small Language Model (SLM) Qwen 0.5B melalui framework lokal Ollama.

📌 Deskripsi Proyek
Sistem ini dirancang untuk membaca data esai siswa dan memprediksi nilai (score) dalam skala 1 hingga 6. Sistem membandingkan dua metode pendekatan prompting:

Zero-Shot Learning: LLM menilai esai secara langsung berdasarkan instruksi dasar tanpa contoh acuan.

Few-Shot Learning: LLM menilai esai dengan panduan 2 contoh esai ekstrem (skor rendah dan skor tinggi) dari data latih sebagai jangkar referensi (anchor).

Sistem ini juga dilengkapi dengan arsitektur eksekusi Offline (Two-Stage Execution) untuk mengakali batasan kompetisi Kaggle yang mewajibkan fitur internet dimatikan saat melakukan submisi (offline submission).

📂 Struktur Arsip (DL_MP2.rar)
Setelah diekstrak, folder DL_MP2 memiliki struktur sebagai berikut:

Plaintext
DL_MP2/
│
├── .venv/                   # Python Virtual Environment (Dependencies siap pakai)
├── train.csv                # (Dataset) Data latih berisi sampel esai dan skor asli
├── test.csv                 # (Dataset) Data uji yang esainya akan diprediksi
├── submission.csv           # (Output) Hasil prediksi skor untuk disubmit ke Kaggle
└── notebook_utama.ipynb     # (Script) Source code utama implementasi Pipeline AES
(Catatan: Direktori .venv/ memuat library bawaan seperti pandas, requests, dan transformers yang di-isolasi khusus untuk proyek ini).

⚙️ Persyaratan Sistem (Requirements)
Sistem Operasi: Linux/Ubuntu (Disarankan) atau environment Kaggle Notebook.

Python 3.8+

RAM: Minimal 8 GB (Untuk menjalankan LLM di atas memori CPU).

Aplikasi Ollama terinstal di dalam sistem.

🚀 Cara Menjalankan Proyek Secara Lokal
1. Ekstrak Arsip dan Masuk ke Direktori
Ekstrak file DL_MP2.rar lalu buka terminal/CMD dan arahkan ke dalam folder proyek:

Bash
cd DL_MP2
2. Aktifkan Virtual Environment
Gunakan environment yang sudah disediakan di dalam paket RAR ini:

Windows: .\.venv\Scripts\activate

Linux/Mac: source .venv/bin/activate

3. Jalankan Server Ollama
Pastikan Ollama berjalan di latar belakang (background) untuk menerima request API lokal:

Bash
ollama serve
4. Unduh Model Bahasa (Jika belum ada)
Pastikan model Qwen berukuran 0.5B sudah ditarik ke dalam sistem Ollama Anda:

Bash
ollama pull qwen:0.5b
5. Eksekusi Script Penilaian
Jalankan file notebook/script Python (notebook_utama.ipynb). Skrip tersebut akan:

Memuat dataset uji (test.csv).

Memformat teks dengan instruksi Few-Shot.

Mengirimkan prompt ke API lokal http://localhost:11434/api/generate.

Melakukan penyaringan regex re.search(r'[1-6]') pada jawaban LLM.

Menyimpan hasil akhir ke dalam file submission.csv.

📊 Hasil Evaluasi
Zero-Shot: Eksekusi token lebih cepat, namun model rentan mengalami halusinasi teks dan kurang mematuhi format wajib (angka tunggal).

Few-Shot: Eksekusi sedikit lebih lambat karena context window lebih besar, namun menghasilkan sebaran nilai yang jauh lebih akurat dan patuh pada format penilaian (1-6). Oleh karena itu, Few-Shot menjadi strategi final yang digunakan dalam submisi proyek ini.
