# Proyek Akhir Pembelajaran Mesin (INF62325)
## Analisis Klastering Tingkat Obesitas Berdasarkan Kebiasaan Makan dan Aktivitas Fisik Menggunakan K-Means

### Anggota Kelompok
- **Intan Fairuz Nur Asiyah** (2488010005)  
*(Varian Dasar)*
- **Tiara Salsabila** (2488010045)  
*(Varian Parameter/Perlakuan Data)*
- **Chantika Maharani** (2488010080)  
*(Varian Pemilihan Fitur)*


**Kelas:** Informatika 5C

---

### Informasi Proyek
- **Paket Dataset:** Estimation of Obesity Levels Based On Eating Habits and Physical Condition
- **Metode:** K-Means Clustering (Metode 3)
- **Repositori GitHub:** [Project-UAS-Dataset8-5C](https://github.com/chantika-maharani/Project-UAS-Dataset8)

---

### Deskripsi Dataset
Dataset yang digunakan berasal dari UCI Machine Learning Repository yaitu **Estimation of Obesity Levels Based On Eating Habits and Physical Condition**. Dataset ini mencakup data estimasi tingkat obesitas individu yang berasal dari negara Meksiko, Peru, dan Kolombia. Setiap baris data diberi label variabel target kelas `NObeyesdad` (tingkat obesitas) yang dikategorikan ke dalam tujuh tingkatan, mulai dari berat badan kurang hingga obesitas tipe III. Berdasarkan dokumentasi resminya, sekitar 77% data dibangkitkan secara sintetis menggunakan *tool* Weka dan filter SMOTE, sedangkan 23% sisanya dikumpulkan langsung dari responden melalui platform web.

Berdasarkan pemeriksaan mandiri melalui Google Colab:
- **Jumlah Baris (`df.shape`):** 2.111 baris (*records*)
- **Jumlah Kolom (`df.shape`):** 17 kolom (*attributes*)
- **Jumlah Nilai Kosong (`df.isnull().sum()`):** 0
- **Jumlah Baris Duplikat (`df.duplicated().sum()`):** 24 baris
- **Tautan Sumber Dataset:** [UCI Estimation of Obesity Levels Dataset](https://archive.ics.uci.edu/dataset/544/estimation+of+obesity+levels+based+on+eating+habits+and+physical+condition)
- **Fitur yang Digunakan:** `FAVC`, `FCVC`, `CAEC`, `FAF`, dan `TUE`.

---

Pada cabang klastering tidak ada pemisahan data latih dan data uji, karena tidak ada label yang diuji. Pembersihan dilakukan sekali atas seluruh data: buang duplikat (24 baris), pilih lima fitur sesuai proposal (FAVC, FCVC, CAEC, FAF, TUE) dan buang 12 kolom lainnya termasuk label NObeyesdad (dataset ini tidak punya kolom identitas), kodekan FAVC (no=0, yes=1) dan CAEC (no=0, Sometimes=1, Frequently=2, Always=3), imputasi median (tidak ada nilai hilang), lalu pembatasan pencilan dengan IQR 1,5 hanya pada FCVC, FAF, dan TUE. Hasilnya disimpan sebagai data_bersih.csv dan dipakai ketiga varian apa adanya. Penskalaan tidak dilakukan pada tahap pembersihan, melainkan di dalam tiap varian dan sekali lagi saat model final dilatih: StandardScaler di-fit satu kali pada data bersih, lalu disimpan sebagai scaler.pkl dan dipakai aplikasi web dengan transform, bukan fit_transform. Aplikasi web memakai fungsi kodekan yang sama dari alat.py agar masukan pengguna (ya/tidak dan kadang-kadang/sering/selalu) diubah ke angka dengan cara yang sama seperti di notebook. One-hot tidak dipakai; CAEC diperlakukan ordinal dengan asumsi jarak antartingkat sama, yang perlu disebut sebagai keterbatasan.

Mengapa berbeda dari cabang klasifikasi. Pada k-NN urutan wajibnya adalah bersihkan, pisahkan data, baru skalakan — penskalaan sebelum pemisahan membuat statistik data uji bocor ke pelatihan. Pada klastering tidak ada pemisahan, sehingga yang dijaga bukan kebocoran antar-himpunan, melainkan kesamaan skala dan pengodean antara notebook dan aplikasi web.

### Pertanyaan Analitik
> Ada berapa kelompok alami responden berdasarkan pola makan dan aktivitas, serta bagaimana masing-masing karakteristik kelompok yang terbentuk dengan menggunakan K-Means?

---

### Pembagian Varian Eksperimen
- **Intan Fairuz Nur Asiyah (Varian Dasar):** Membuat model klaster K-Means dasar menggunakan 5 fitur terpilih (`FAVC`, `FCVC`, `CAEC`, `FAF`, `TUE`) serta mengevaluasi sebaran klaster awalnya.
- **Tiara Salsabila (Varian Parameter / Perlakuan Data):** Melakukan uji coba penentuan jumlah klaster optimal ($k$) menggunakan Metode *Elbow* dan *Silhouette Score*, serta membandingkan hasil klaster sebelum dan sesudah penerapan *feature scaling*.
- **Chantika Maharani (Varian Pemilihan Fitur):** Membandingkan hasil pembentukan klaster K-Means dengan membedakan kombinasi subset fitur (misalnya membandingkan klaster yang dibentuk khusus dari fitur pola makan saja vs fitur aktivitas fisik), lalu menyusun profil serta penamaan tiap klaster.

---

### Cara Menjalankan Aplikasi & Notebook

#### 1. Prasyarat
Pastikan perangkat Anda sudah terinstal **Python 3.8+** dan **Git**.

#### 2. Clone Repositori
```bash
git clone [https://github.com/chantika-maharani/Project-UAS-Dataset8.git](https://github.com/chantika-maharani/Project-UAS-Dataset8.git)
cd Project-UAS-Dataset8
