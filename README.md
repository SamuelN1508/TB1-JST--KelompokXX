# TB1-JST-Kelompok09: Analisis dan Implementasi Klasifikasi Data Menggunakan Perceptron dan ADALINE

Repository ini merupakan tugas resmi untuk **Tugas Besar 1 Mata Kuliah Jaringan Syaraf Tiruan (IT6053)** - Program Studi Informatika, Fakultas Teknologi Informasi, Universitas Kristen Duta Wacana (UKDW).

---

## 👥 Identitas Anggota Kelompok (Kelompok XX)
1. **Fransina Riyanty Batlayar** - NIM: `71231014`
2. **Amelia Agustin** - NIM: `71231038`
3. **Nengah Yesi Putri** - NIM: `71231047`
4. **Samuel Natanael** - NIM: `71231050`

---

## 📌 Deskripsi Kasus & Dataset
- **Judul Studi Kasus**: Pemetaan Topik dan Analisis Opini Publik terhadap Program Makan Bergizi Gratis (MBG).
- **Kesinambungan Tugas 1**: Melanjutkan analisis data crawling opini publik media sosial (YouTube) mengenai program nasional Makan Bergizi Gratis (MBG) yang diekstrak pada awal tahun 2026.
- **Ukuran Dataset**:
  - Total data mentah: 6.419 komentar.
  - Data tersaring & terlabel biner: **2.012 observasi**.
- **Label Kelas**:
  - `+1` (**Sentimen Positif**): Komentar apresiasi, dukungan, manfaat gizi anak, dan harapan program. (1.045 sampel)
  - `-1` (**Sentimen Negatif**): Komentar keluhan, kritik pengelolaan, kekhawatiran korupsi/kualitas makanan. (967 sampel)
- **Fitur Numerik ($X$)**:
  - `pos_score`: Frekuensi kata-kata bersentimen positif (*bagus, gizi, sehat, berkah, dukung, dll.*).
  - `neg_score`: Frekuensi kata-kata bersentimen negatif (*korupsi, maling, rusak, racun, kecewa, dll.*).
  - Fitur pendukung: `text_length` (panjang kata) dan `like_count`.

---

## 📂 Struktur Berkas Repositori
| Nama Berkas | Keterangan |
| :--- | :--- |
| `TB1_Kelompok09.ipynb` | Jupyter Notebook lengkap berisi kode implementasi Perceptron & ADALINE (NumPy mandiri), 8 eksperimen, grafik konvergensi, confusion matrix, dan decision boundary. |
| `TB1_KelompokXX.ipynb` | Salinan notebook dengan format penamaan umum sesuai template penugasan. |
| `dataset.csv` | Dataset hasil pra-pengolahan dan pelabelan biner yang digunakan langsung dalam eksperimen. |
| `README.md` | Dokumentasi lengkap proyek, identitas, instruksi eksekusi, ringkasan hasil, dan kontribusi anggota. |
| `requirements.txt` | Daftar dependensi pustaka Python yang diperlukan. |
| `TB1_Kelompok09.pdf` | Laporan formal studi kasus TB1 (5–8 halaman). |
| `Presentasi_TB1.pdf` | Slide presentasi ringkasan kasus, metode, eksperimen, dan hasil. |

---

## ⚙️ Petunjuk Instalasi dan Menjalankan Kode
1. **Clone repositori ini**:
   ```bash
   git clone https://github.com/SamuelNatanael/TB1-JST-KelompokXX.git
   cd TB1-JST-KelompokXX
   ```
2. **Siapkan lingkungan Python (Python 3.8+)**:
   ```bash
   python -m venv venv
   # Windows:
   venv\Scripts\activate
   # Linux/MacOS:
   source venv/bin/activate
   ```
3. **Instal seluruh dependensi**:
   ```bash
   pip install -r requirements.txt
   ```
4. **Jalankan Jupyter Notebook**:
   ```bash
   jupyter notebook TB1_KelompokXX.ipynb
   ```
   *Seluruh sel dapat dieksekusi secara berurutan dari atas ke bawah (Restart & Run All).*

---

## 📊 Ringkasan Hasil Eksperimen (8 Konfigurasi)
Semua pengujian dijalankan selama **50 Epoch** dengan pembagian data **80% Train : 20% Test** (`stratified`, `random_state = 42`):

| No | Model | Learning Rate ($\alpha$) | Epoch | Standardisasi | Akurasi Latih (%) | Akurasi Uji (%) | Status Konvergensi |
| :-: | :--- | :-: | :-: | :-: | :-: | :-: | :--- |
| 1 | Perceptron | 0.001 | 50 | Ya | 98.76% | 98.51% | Konvergen stabil |
| 2 | Perceptron | 0.010 | 50 | Ya | 98.76% | 98.51% | Konvergen stabil |
| 3 | Perceptron | 0.100 | 50 | Ya | 98.76% | 98.51% | Konvergen stabil |
| 4 | Perceptron | 0.010 | 50 | **Tidak** | 98.76% | 98.51% | Konvergen stabil |
| 5 | ADALINE | 0.001 | 50 | Ya | 98.76% | 98.51% | MSE turun bertahap |
| 6 | ADALINE | 0.010 | 50 | Ya | 98.76% | 98.51% | MSE konvergen cepat |
| 7 | ADALINE | 0.100 | 50 | Ya | 98.76% | 98.51% | MSE konvergen optimum |
| 8 | ADALINE | 0.010 | 50 | **Tidak** | 98.76% | 98.51% | Konvergen stabil |

### Temuan Utama:
1. **Separabilitas Data**: Data memiliki pemisahan polaritas yang sangat tegas pada fitur leksikon (`pos_score` vs `neg_score`), menghasilkan akurasi uji > 98%.
2. **Perbedaan Pembelajaran**:
   - **Perceptron** memperbarui bobot hanya saat terjadi salah klasifikasi secara diskrit ($e \in \{-2, 0, 2\}$). Perubahan nilai $\alpha$ pada Perceptron dengan inisialisasi bobot nol hanya menskalakan magnitudo vektor bobot tanpa mengubah orientasi garis pemisah.
   - **ADALINE** memperbarui bobot secara kontinu berdasarkan deviasi keluaran linear $z$ terhadap target $y$ menggunakan *Batch Gradient Descent* untuk meminimalkan fungsi kuadratik MSE.
3. **Pentingnya Standardisasi**: Standardisasi membuat kontur fungsi loss berbentuk lingkaran simetris sehingga ADALINE mencapai konvergensi gradien lebih cepat dan terhindar dari osilasi.

---

## 🤝 Pembagian Kontribusi Anggota
- **Fransina Riyanty Batlayar (71231014)**: Penelusuran artikel ilmiah pendukung, perumusan latar belakang masalah, dan penyusunan dokumen laporan.
- **Amelia Agustin (71231038)**: Pra-pengolahan dataset sentimen MBG, pembersihan teks, dan penyusunan materi slide presentasi.
- **Nengah Yesi Putri (71231047)**: Perhitungan manual 2 langkah Perceptron & ADALINE, analisis kurva pembelajaran, dan evaluasi confusion matrix.
- **Samuel Natanael (71231050)**: Implementasi mandiri algoritma Perceptron & ADALINE dengan NumPy, perancangan 8 konfigurasi eksperimen, otomasi visualisasi *decision boundary*, dan integrasi repositori GitHub.

---

## 📚 Referensi Ilmiah
1. **Rosenblatt, F. (1958)**. *The perceptron: A probabilistic model for information storage and organization in the brain*. Psychological Review, 65(6), 386–408. https://doi.org/10.1037/h0042519
2. **Widrow, B., & Hoff, M. E. (1960)**. *Adaptive switching circuits*. IRE WESCON Convention Record, Part 4, 96–104.
3. **Raschka, S. (2015)**. *Python Machine Learning: Unlock deeper insights into Machine Learning with this vital guide to cutting-edge predictive analytics*. Packt Publishing.
