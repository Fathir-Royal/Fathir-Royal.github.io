# 👑 N-Queens Problem
## 🧠 Desain dan Analisis Algoritma

---

## ❓ Apa Itu N-Queens Problem?

N-Queens adalah sebuah masalah klasik dalam **algoritma** dan **teori komputasi**, yang bertujuan untuk menempatkan sejumlah ratu (queen) di papan catur berukuran **N × N**, dengan aturan:

> 🔸 **Tidak ada dua ratu** yang berada di baris, kolom, atau diagonal yang sama.

---

## 🎯 Tujuan N-Queens

1. 🛡️ **Penempatan Ratu yang Aman**  
   Setiap ratu harus ditempatkan tanpa mengancam ratu lain.

2. ⚠️ **Menghindari Konflik**  
   Algoritma harus mengecek konflik **horizontal**, **vertikal**, dan **diagonal**.

3. ✅ **Menemukan Semua Solusi**  
   Bisa mencari satu solusi valid atau semua solusi yang mungkin.

4. 🎓 **Melatih Pemahaman Algoritma**  
   - Memahami *backtracking*  
   - Belajar tentang *constraint satisfaction problems (CSP)*  
   - Meningkatkan logika & rekursi

---

## 📌 Batasan Masalah

1. ♟️ **Jumlah Ratu = Ukuran Papan (N)**  
   Harus ada tepat **N ratu** di papan **N × N**.

2. 📏 **Satu Ratu per Baris dan Kolom**  
   Tidak boleh lebih dari satu ratu di **baris atau kolom yang sama**.

3. ➗ **Tidak Ada Dua Ratu dalam Diagonal yang Sama**  
   Meliputi diagonal utama (↘) dan diagonal balik (↙).

4. ◻️ **Papan Harus Persegi (N × N)**

5. 👁️‍🗨️ **Posisi Aman Harus Dicek Sebelum Penempatan**  
   Jika tidak aman, harus dihindari (dengan *cut* dalam *backtracking*).

6. 🔢 **N ≥ 4 untuk Solusi Non-Trivial**  
   - ❌ Tidak ada solusi untuk N = 2 dan N = 3  
   - ✅ Solusi dimulai dari N = 4

7. 🚫 **Tidak Ada Rintangan di Papan**  
   Semua sel dianggap kosong dan dapat digunakan.

---

## 🧩 Dasar Teori: Backtracking

### 💡 Apa Itu Backtracking?

Backtracking adalah metode pencarian rekursif yang mencoba semua kemungkinan solusi dan **mundur (backtrack)** jika solusi tidak valid.

### 🔍 Kenapa Cocok untuk N-Queens?

- Masalah bersifat **rekursif** dan **bertahap**  
- Banyak solusi parsial bisa disaring sejak awal  
- Constraint jelas dan dapat divalidasi cepat  
- Lebih efisien dibanding brute force

---

## 🧭 Langkah-Langkah Penyelesaian

1. 🔢 **Mulai dari Baris Pertama**
2. 🧠 **Periksa Keamanan Posisi**
3. ✅ **Tempatkan Ratu Jika Aman**
4. 🔙 **Backtrack Jika Tidak Ada Posisi Aman**
5. 🧾 **Simpan Solusi Jika Semua Ratu Berhasil Ditempatkan**
6. 🔁 **(Opsional) Lanjutkan Cari Semua Solusi**

---

## 🧪 Latihan Soal

🧮 **Ukuran Papan:** 4 × 4  
🎯 **Target:** Tempatkan 4 ratu agar tidak saling menyerang

### 📍 Langkah-Langkah:

1. **Baris 0:** Kolom 0 ✅ → Tempatkan ratu di `(0,0)`
2. **Baris 1:** Kolom 2 ✅ → Tempatkan ratu di `(1,2)`
3. **Baris 2:** Kolom 3 ✅ → Tempatkan ratu di `(2,3)`
4. **Baris 3:** Kolom 1 ✅ → Tempatkan ratu di `(3,1)`

🎉 Semua ratu berhasil ditempatkan tanpa konflik!

---

## 💻 Implementasi dalam C++

```cpp
// Contoh kode (tidak disertakan dalam file PDF)
// Anda bisa menambahkan fungsi isSafe(), solveNQueens(), printBoard() sesuai struktur backtracking
````

🧾 **Penjelasan Output:**

* Posisi ratu (Q) dan sel kosong (.)
* Algoritma menelusuri posisi aman secara efisien

---

## 🧠 Kesimpulan

> N-Queens adalah masalah **penempatan** ratu di papan catur agar tidak saling menyerang.
> Algoritma **backtracking** sangat cocok karena dapat mengevaluasi posisi satu per satu dan mundur jika terjadi konflik.
> Solusi ditemukan secara **sistematis** dan **efisien**, meningkatkan pemahaman tentang **algoritma rekursif dan CSP**.

---