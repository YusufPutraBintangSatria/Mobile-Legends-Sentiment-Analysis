# ⚔️ Mobile Legends Sentiment Analysis: "Dark System" or Skill Issue?

![Python](https://img.shields.io/badge/Python-3.10%2B-blue?style=for-the-badge&logo=python&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/scikit--learn-%23F7931E.svg?style=for-the-badge&logo=scikit-learn&logoColor=white)
![Pandas](https://img.shields.io/badge/pandas-%23150458.svg?style=for-the-badge&logo=pandas&logoColor=white)
![Google Play Scraper](https://img.shields.io/badge/Google_Play_Scraper-FF0000?style=for-the-badge&logo=google-play&logoColor=white)

> **Analisis Sentimen Ulasan Pengguna Aplikasi Mobile Legends: Bang Bang di Google Play Store Menggunakan Algoritma Naive Bayes dan Decision Tree.**

## 📋 Daftar Isi
- [Latar Belakang](#-latar-belakang)
- [Alur Kerja Proyek](#-alur-kerja-proyek)
- [Tech Stack](#-tech-stack)
- [Instalasi & Penggunaan](#-instalasi--penggunaan)
- [Tahapan Analisis](#-tahapan-analisis)
  - [1. Data Scraping](#1-data-scraping)
  - [2. Preprocessing](#2-preprocessing)
  - [3. Labeling (Lexicon Based)](#3-labeling-lexicon-based)
  - [4. Modeling & Evaluasi](#4-modeling--evaluasi)
- [📊 Hasil & Temuan Utama](#-hasil--temuan-utama)
- [Rencana Pengembangan (Gen AI Integration)](#-rencana-pengembangan-gen-ai-integration)
- [Kontak](#-kontak)

---

## 📖 Latar Belakang
Mobile Legends: Bang Bang adalah salah satu game MOBA mobile terpopuler di Indonesia. Namun, kepuasan pemain sering kali fluktuatif akibat isu teknis, *matchmaking* (sering disebut "Dark System"), dan perilaku pemain lain (*toxic*).

Proyek ini bertujuan untuk:
1.  Menganalisis opini publik secara otomatis dari ribuan ulasan nyata.
2.  Membandingkan performa algoritma **Naive Bayes** dan **Decision Tree** dalam mengklasifikasikan sentimen (Positif/Negatif).
3.  Mengidentifikasi kata kunci utama yang menjadi keluhan atau pujian pengguna.

---

## 🔄 Alur Kerja Proyek
![Workflow Diagram](https://img.shields.io/badge/Diagram-Coming_Soon-lightgrey)
*(Disarankan: Buat diagram blok sederhana: Scraping -> Cleaning -> Labeling -> TF-IDF -> Modeling -> Viz)*

1.  **Data Gathering**: Scraping data ulasan langsung dari Google Play Store.
2.  **Preprocessing**: Membersihkan data teks kotor menjadi format yang siap diolah mesin.
3.  **Labeling**: Menggunakan pendekatan Lexicon-based (InSet) untuk menentukan *ground truth* sentimen.
4.  **Feature Extraction**: Mengubah teks menjadi vektor angka menggunakan **TF-IDF**.
5.  **Modeling**: Melatih model Naive Bayes dan Decision Tree dengan berbagai rasio data (80:20, 70:30, dll).
6.  **Evaluation**: Mengukur performa menggunakan Accuracy, Precision, Recall, F1-Score, dan 10-Fold Cross Validation.

---

## 🛠 Tech Stack
* **Language:** Python
* **Data Processing:** Pandas, NumPy
* **Scraping:** `google-play-scraper`
* **NLP & Preprocessing:** `NLTK`, `Sastrawi` (Stemming Bahasa Indonesia), RegEx
* **Machine Learning:** Scikit-Learn (MultinomialNB, DecisionTreeClassifier, TfidfVectorizer)
* **Visualization:** Matplotlib, Seaborn, WordCloud

---

## 💻 Instalasi & Penggunaan

1.  **Clone repositori ini:**
    ```bash
    git clone [https://github.com/username-kamu/Mobile-Legends-Sentiment-Analysis.git](https://github.com/username-kamu/Mobile-Legends-Sentiment-Analysis.git)
    cd Mobile-Legends-Sentiment-Analysis
    ```

2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Jalankan Notebook:**
    Buka file `.ipynb` di folder `notebooks/` menggunakan Jupyter Notebook atau Google Colab.

---

## 🔍 Tahapan Analisis

### 1. Data Scraping
Mengambil **5,375 ulasan** terbaru dari aplikasi Mobile Legends di Google Play Store region Indonesia (`id`).
* *Library:* `google-play-scraper`
* *Output:* Data mentah berisi username, rating, tanggal, dan teks ulasan.

### 2. Preprocessing
Tahap krusial untuk membersihkan *noise* pada data teks:
* **Cleaning:** Menghapus URL, HTML tags, emoji, angka, dan tanda baca.
* **Case Folding:** Mengubah huruf menjadi kecil (lowercase).
* **Normalisasi:** Mengubah kata gaul/singkatan (e.g., "gk" -> "tidak", "bgs" -> "bagus") menggunakan kamus kustom.
* **Stopword Removal:** Menghapus kata umum yang tidak bermakna (e.g., "yang", "dan").
* **Stemming:** Mengubah kata berimbuhan menjadi kata dasar menggunakan **Sastrawi** (e.g., "bermain" -> "main").

### 3. Labeling (Lexicon Based)
Karena data hasil scraping tidak memiliki label sentimen (positif/negatif) secara eksplisit pada teksnya (selain bintang), dilakukan pelabelan otomatis menggunakan kamus kata sentimen (Lexicon InSet).
* Skor Positif > Skor Negatif = **Positif**
* Skor Negatif > Skor Positif = **Negatif**

### 4. Modeling & Evaluasi
Dua algoritma diuji dengan pembagian data latih:uji yang berbeda (80:20, 75:25, 70:30, 60:40).

**Validasi:** Dilakukan **10-Fold Cross Validation** untuk memastikan model tidak *overfitting* dan performanya konsisten.

---

## 📊 Hasil & Temuan Utama

### Performa Model (Akurasi Rata-rata 10-Fold CV)
| Model | Akurasi Terbaik | Rasio Split Terbaik |
| :--- | :---: | :---: |
| **Naive Bayes** | **87.17%** | 80:20 |
| Decision Tree | 84.92% | 80:20 |

> **Kesimpulan Teknis:** Algoritma **Naive Bayes** terbukti lebih unggul dan stabil dibandingkan Decision Tree untuk kasus klasifikasi teks ulasan ini, dengan akurasi tertinggi mencapai ~87%.

### Insight dari WordCloud
* **Positif:** Kata-kata seperti *"bagus"*, *"seru"*, *"mabar"*, dan *"event"* mendominasi, menunjukkan apresiasi terhadap gameplay dan event in-game.
* **Negatif:** Kata-kata seperti *"lag"*, *"sinyal"*, *"dark system"*, *"jaringan"*, dan *"tolol"* (merujuk pada rekan tim) sering muncul. Ini mengindikasikan masalah utama ada pada stabilitas koneksi dan sistem matchmaking.

---

## 🚀 Rencana Pengembangan (Gen AI Integration)
Sebagai langkah menuju **Gen AI Engineer**, proyek ini memiliki potensi pengembangan lebih lanjut:

1.  **LLM-based Labeling:** Mengganti metode Lexicon-based dengan **Large Language Models (GPT-3.5/4 atau Gemini)** untuk pelabelan data yang lebih akurat, terutama dalam mendeteksi sarkasme.
2.  **Summarization:** Menggunakan LLM untuk membuat ringkasan otomatis dari keluhan pengguna per minggu.
3.  **Chatbot Keluhan:** Membangun RAG (Retrieval-Augmented Generation) sederhana di mana user bisa bertanya "Apa keluhan utama minggu ini?" dan bot menjawab berdasarkan database ulasan.

---

## ✨ Gen AI Experiment: Handling Sarcasm with Gemini 2.0 Flash

Selain menggunakan metode Lexicon-based (InSet), saya melakukan eksperimen lanjutan menggunakan **Large Language Model (Google Gemini 2.0 Flash)** untuk menangani kelemahan metode tradisional, khususnya dalam mendeteksi **Sarkasme**.

### Masalah pada Metode Lama (Lexicon)
Metode Lexicon bekerja dengan mencocokkan kata. Kalimat yang mengandung kata positif ("Hebat", "Mantap") akan otomatis dianggap Positif, meskipun konteksnya menyindir.

### Solusi dengan LLM
LLM mampu memahami konteks kalimat secara utuh. Berikut adalah hasil komparasi pada sampel data:

| Ulasan User | Label Lexicon (Metode Lama) | Label Gemini LLM (Metode Baru) | Analisis |
| :--- | :---: | :---: | :--- |
| *"Game seru banget, grafiknya hd!"* | ✅ Positif | ✅ Positif | Kedua metode setuju. |
| *"Dasar moonton dark system..."* | ❌ Negatif | ✅ Negatif | Kedua metode setuju. |
| **"Hebat banget sinyalnya, ping 200ms terus, mantap!"** | ⚠️ **Positif** (Salah Deteksi) | ✅ **Negatif** (Akurat) | **LLM berhasil mendeteksi sarkasme**, sedangkan Lexicon gagal karena ada kata "Hebat" & "Mantap". |

**Bukti Eksekusi Code:**
![Hasil LLM](images/llm_sarcasm_detection.png)

> *Code eksperimen ini dapat dilihat pada file [`experiment_llm_labeling.py`](experiment_llm_labeling.py).*

--- 

## 👤 Kontak
**Bintang**
* [LinkedIn](https://www.linkedin.com/in/yusuf-putra-bintang-satria-274a87388)
* [GitHub](https://github.com/YusufPutraBintangSatria)
* Email: bintang.satria1322@gmail.com

---
*Feel free to ⭐ this repository if you find it useful!*
