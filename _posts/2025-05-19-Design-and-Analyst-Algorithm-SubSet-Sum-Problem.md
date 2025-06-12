# 🎯 Subset Sum Problem
## Desain dan Analisis Algoritma

---

## 🤔 Apa itu Subset Sum Problem?

**Subset Sum Problem** adalah salah satu masalah fundamental dalam ilmu komputer yang berkaitan dengan teori kompleksitas dan kriptografi.

### 📋 Definisi
Diberikan:
- 🔢 Himpunan bilangan bulat tidak kosong
- 🎯 Sebuah target angka **m**

**Tujuan:** Carilah subset (subhimpunan) yang jumlahnya sama dengan **m**.

### 🏷️ Klasifikasi Masalah
**Subset Sum Problem** termasuk dalam kategori **NP-Complete (Non-Deterministic Polynomial Complete)**:

- ❌ **Sulit dicari solusinya** - tidak ada algoritma efisien yang diketahui
- ✅ **Mudah diverifikasi** - jika sudah tahu jawabannya, bisa dicek dengan cepat
- 🔗 **Masalah lengkap** - semua masalah NP lainnya bisa diubah ke bentuk Subset Sum

> 💡 **Fun Fact:** Jika ada cara cepat untuk menyelesaikan Subset Sum, maka semua masalah NP bisa diselesaikan dengan cepat! Inilah inti dari masalah **P vs NP**.

---

## 💡 Contoh Subset Sum Problem

### ✅ Contoh 1: Solusi Ditemukan
```
Input:  arr[] = [3, 34, 4, 12, 5, 2], sum = 9
Output: BENAR ✓
Penjelasan: Ada subset {4, 5} dengan jumlah = 9
```

### ❌ Contoh 2: Solusi Tidak Ditemukan
```
Input:  arr[] = [3, 34, 4, 12, 5, 2], sum = 30
Output: SALAH ✗
Penjelasan: Tidak ada subset yang jumlahnya = 30
```

---

## 🛠️ Pendekatan Penyelesaian

### 1. 💪 Brute Force (Rekursif)

#### 🔄 Cara Kerja
Setiap elemen memiliki **2 pilihan**: diambil atau tidak diambil.

#### 📊 Kompleksitas Kombinasi
| Jumlah Elemen | Kombinasi | Nilai |
|---|---|---|
| 3 | 2³ | 8 |
| 10 | 2¹⁰ | 1,024 |
| 30 | 2³⁰ | 1,073,741,824 |

#### ⚡ Analisis Kompleksitas
- **Waktu:** O(2ⁿ)
- **Ruang:** O(n) - untuk stack rekursi

#### ✅ Kelebihan
- Sederhana dan mudah dipahami
- Pasti menemukan solusi jika ada

#### ❌ Kekurangan
- Tidak efisien untuk n yang besar
- Eksponensial time complexity

---

### 2. 🧠 Dynamic Programming

#### 🎯 Konsep
Menggunakan **tabel** untuk menyimpan hasil subproblem yang sudah dihitung, sehingga tidak perlu menghitung ulang.

#### 📊 Analisis Kompleksitas
- **Waktu:** O(n × T)
- **Ruang:** O(n × T) - bisa dioptimalkan menjadi O(T)

#### ✅ Kelebihan
- Efisien untuk target T yang tidak terlalu besar
- Menghindari perhitungan berulang

#### ❌ Kekurangan
- Memakan banyak memori untuk T yang besar
- Tidak cocok untuk target yang sangat besar

---

## 🔄 Variasi Masalah Subset Sum

### A. 🔻 Subset Sum dengan Elemen Negatif

**Masalah:** Elemen bisa berupa bilangan negatif.

**Contoh:**
```
S = {-7, -3, -2, 5, 8}, target = 0
Solusi: {-3, -2, 5} → (-3) + (-2) + 5 = 0 ✓
```

**Konsekuensi:**
- Dynamic Programming standar tidak cukup
- Indeks array tidak bisa negatif

---

### B. 🔢 Counting Subsets

**Tujuan:** Menghitung **berapa banyak** subset yang memenuhi syarat.

**Contoh:**
```
S = {2, 3, 5, 6, 8, 10}, sum = 10
```

**Solusi DP:**
- Tabel: `dp[i][j]` = banyak subset dari elemen 0..i-1 yang totalnya j
- **Rumus:** `dp[i][j] = dp[i-1][j] + dp[i-1][j - arr[i-1]]`

---

### C. 🎯 Closest Subset Sum

**Tujuan:** Jika tidak ada subset dengan jumlah tepat, cari yang **paling dekat**.

**Contoh:**
```
S = {1, 3, 4, 8}, target = 10
Kemungkinan: {1,3,4}=8, {3,8}=11, {1,8}=9
Terdekat: 9 dan 11
```

---

### D. 🎒 Hubungan dengan 0/1 Knapsack Problem

#### 🤝 Persamaan
- Sama-sama memilih subset dengan batasan tertentu
- Sama-sama bisa diselesaikan dengan Dynamic Programming

#### 🔄 Perbedaan
| Aspect | Subset Sum | 0/1 Knapsack |
|---|---|---|
| **Tujuan** | Total sum = target | Maksimalkan nilai |
| **Constraint** | Nilai = berat | Berat ≠ nilai |
| **Output** | Boolean (ada/tidak) | Nilai maksimum |

---

## ⚠️ Kompleksitas & Keterbatasan

### 🔴 NP-Complete
- ❌ Tidak ada algoritma efisien (polinomial) untuk semua kasus
- ✅ Solusi bisa diverifikasi dengan cepat
- 🔗 Masalah fundamental dalam teori kompleksitas

### 📊 Keterbatasan Praktis
| Metode | Kompleksitas Waktu | Kompleksitas Ruang | Keterbatasan |
|---|---|---|---|
| **Brute Force** | O(2ⁿ) | O(n) | Tidak efisien untuk n besar |
| **Dynamic Programming** | O(n × sum) | O(n × sum) | Tidak efisien untuk sum besar |

---

### 📝 Studi Kasus
```
Diberikan: S = {2, 4, 5, 9}, Target T = 18
Pertanyaan: Apakah ada subset yang jumlahnya = 18?
```

### 1. 🔄 Implementasi Brute Force (Rekursif)

#### 🎯 Cara Kerja
1. **Fungsi rekursif** mencoba setiap elemen dengan 2 pilihan
2. **Base case:** jika sum = target, simpan subset
3. **Vektor result** menyimpan semua subset yang valid

#### ⚡ Karakteristik
- Kompleksitas: O(2ⁿ)
- Menjelajahi semua kemungkinan kombinasi
- Cocok untuk dataset kecil

---

### 2. 🧠 Implementasi Dynamic Programming

#### 📊 Struktur Data
- **Tabel DP:** berukuran (n + 1) × (T + 1)
- **dp[i][j]:** true jika ada subset dari {S[0]...S[i-1]} yang jumlahnya j

#### 🔍 Algoritma Rekonstruksi
- **Fungsi findSubset:** menelusuri tabel dp
- **Backtracking:** mencari elemen yang menyebabkan dp[i][j] = true

#### ⚡ Karakteristik
- **Kompleksitas Waktu:** O(n × T)
- **Kompleksitas Ruang:** O(n × T)
- Efisien untuk target yang moderat

---

### 📋 Ringkasan
**Subset Sum Problem** adalah masalah fundamental dalam computer science yang mencari subset dari kumpulan angka dengan jumlah sama dengan target tertentu.

### 🏷️ Karakteristik Utama
- 🔴 **Kategori:** NP-Complete
- ⚡ **Kompleksitas:** Tidak ada solusi efisien universal
- 🔍 **Verifikasi:** Mudah memverifikasi solusi
- 🌟 **Aplikasi:** Kriptografi, optimisasi, teori kompleksitas

### 💡 Pembelajaran Penting
1. **Brute Force:** Sederhana tapi tidak efisien
2. **Dynamic Programming:** Lebih efisien untuk kasus tertentu
3. **Variasi:** Banyak varian dengan karakteristik berbeda
4. **Keterbatasan:** Masalah inherent dalam kompleksitas komputasi

---