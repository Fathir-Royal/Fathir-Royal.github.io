# 🌳 Huffman Coding 🌳

---

## 💡 Pengertian Huffman Coding 💡

[cite_start]Huffman Coding adalah algoritma kompresi data *lossless* (tanpa kehilangan data) yang berfungsi untuk mengurangi ukuran data. [cite: 3] [cite_start]Ini dilakukan dengan mengganti setiap karakter atau simbol dengan representasi biner yang didasarkan pada frekuensi kemunculannya. [cite: 3]

[cite_start]Algoritma ini pertama kali ditemukan oleh David A. Huffman pada tahun 1952. [cite: 4] Hingga saat ini, Huffman Coding banyak digunakan dalam berbagai sistem kompresi, termasuk:
* [cite_start]File ZIP [cite: 4]
* [cite_start]Format gambar [cite: 4]
* [cite_start]Protokol transmisi data [cite: 4]

---

## 🎯 Tujuan Huffman Coding 🎯

Tujuan utama dari Huffman Coding adalah:
* [cite_start]Mengompres data secara efisien tanpa kehilangan informasi (lossless). [cite: 5]
* [cite_start]Memberikan kode biner yang lebih pendek untuk simbol yang sering muncul. [cite: 6]
* [cite_start]Memberikan kode biner yang lebih panjang untuk simbol yang jarang muncul. [cite: 6]

---

## 🛠️ Bagaimana Huffman Coding Bekerja? 🛠️

[cite_start]Mari kita lihat contoh dengan string: `BCAADDDCCACACAC` [cite: 7]

**Informasi Awal:**
* [cite_start]Setiap karakter menempati 8 bit. [cite: 9]
* [cite_start]Ada total 15 karakter dalam string di atas. [cite: 9]
* [cite_start]Total bit yang diperlukan untuk mengirim string ini tanpa kompresi adalah $8 \times 15 = 120$ bit. [cite: 10]
* [cite_start]Dengan Huffman Coding, string dapat dimampatkan ke ukuran yang lebih kecil. [cite: 11]

[cite_start]Huffman Coding pertama-tama membuat pohon menggunakan frekuensi karakter, lalu menghasilkan kode untuk setiap karakter. [cite: 12]

Berikut adalah langkah-langkahnya:

1.  [cite_start]**Hitung frekuensi setiap karakter dalam string.** [cite: 9]
    * [cite_start]B: 1 [cite: 8]
    * [cite_start]C: 6 [cite: 8]
    * [cite_start]A: 5 [cite: 8]
    * [cite_start]D: 3 [cite: 8]

2.  [cite_start]**Urutkan karakter dalam urutan frekuensi yang meningkat.** [cite: 13]
    * [cite_start]B (1) [cite: 14]
    * [cite_start]D (3) [cite: 14]
    * [cite_start]A (5) [cite: 14]
    * [cite_start]C (6) [cite: 14]

3.  [cite_start]**Jadikan setiap karakter unik sebagai simpul daun.** [cite: 15]

4.  [cite_start]**Buat simpul kosong `z`.** [cite: 15]

5.  [cite_start]**Tetapkan frekuensi minimum ke anak kiri `z` dan frekuensi minimum kedua ke anak kanan `z`.** [cite: 16]
    [cite_start]**Tetapkan nilai `z` sebagai jumlah dari dua frekuensi minimum di atas.** [cite: 17]
    * Ambil dua frekuensi terkecil dari antrian prioritas Q (pada tahap sebelumnya itu 1 dan 3, yaitu milik B dan D). [cite_start]Jumlahkan kedua nilai tersebut, lalu tambahkan kembali angka 4 ini ke dalam Q sebagai *internal node* (`*`). [cite: 18]
    * Visualisasi:
        ```
           4
          / \
         1   3
        (B) (D)
        ```

6.  [cite_start]**Masukkan simpul `z` ke dalam pohon.** [cite: 19]

7.  [cite_start]**Ulangi langkah 3 sampai 5 untuk semua karakter.** [cite: 19]
    * Lanjutkan proses penggabungan:
        * Gabungkan `*` (frekuensi 4) dan `A` (frekuensi 5) menjadi simpul baru dengan frekuensi 9.
        * Visualisasi:
            ```
                9
               / \
              4   5
             / \  (A)
            1   3
           (B) (D)
            ```
        * Gabungkan `C` (frekuensi 6) dan `*` (frekuensi 9) menjadi simpul baru dengan frekuensi 15.
        * Visualisasi:
            ```
                  15
                 /  \
                6    9
               (C)  / \
                   4   5
                  / \  (A)
                 1   3
                (B) (D)
            ```

8.  [cite_start]**Untuk setiap simpul non-daun, tetapkan 0 ke tepi kiri dan 1 ke tepi kanan.** [cite: 20]
    * Visualisasi Pohon Huffman Akhir:
        ```
                  15
                 /  \
                0    1
               /      \
              6        9
             (C)      / \
                     0   1
                    /     \
                   4       5
                  / \     (A)
                 0   1
                /     \
               1       3
              (B)     (D)
        ```

9.  [cite_start]**Buat tabel yang menyatakan jumlah kode dari diagram pohon tadi.** [cite: 21]

| Character | Code | Frequency | Size (bits) |
| :-------- | :--- | :-------- | :---------- |
| A         | 11   | 5         | [cite_start]$5 \times 2 = 10$ [cite: 22] |
| B         | 100  | 1         | [cite_start]$1 \times 3 = 3$ [cite: 22] |
| C         | 0    | 6         | [cite_start]$6 \times 1 = 6$ [cite: 22] |
| D         | 101  | 3         | [cite_start]$3 \times 3 = 9$ [cite: 22] |

* [cite_start]**Total ukuran string ini tanpa encoding adalah 120 bit.** [cite: 23]
* [cite_start]**Setelah di-encoding, total ukuran kode adalah 28 bit.** [cite: 23]
* [cite_start]**Ukuran total keseluruhan (karakter + frekuensi + encoded) adalah $32 \text{ (karakter)} + 15 \text{ (frekuensi)} + 28 \text{ (encoded)} = 75$ bit.** [cite: 23]

---

## 📝 Latihan Huffman Coding 📝

[cite_start]Mari kita coba dengan kata "sisfo". [cite: 24]

Berikut adalah diagram *Huffman Tree* untuk "sisfo":

```
         5
        / \
       0   1
      /     \
     2       3
    (S)     / \
           0   1
          /     \
         1       2
        (O)     / \
               0   1
              /     \
             1       1
            (I)     (F)
```
*Note: The tree diagram in the original source has inconsistencies in character placement relative to their frequencies, but the overall structure and derived codes are based on the correct frequencies.*

[cite_start]Berikut adalah tabel frekuensi dan kode hasil encoding: [cite: 25]

| Character | Frequency | Code | Size (bits) |
| :-------- | :-------- | :--- | :---------- |
| S         | 2         | 0    | [cite_start]$2 \times 1 = 2$ [cite: 26] |
| i         | 1         | 110  | [cite_start]$1 \times 3 = 3$ [cite: 26] |
| f         | 1         | 111  | [cite_start]$1 \times 3 = 3$ [cite: 26] |
| o         | 1         | 10   | [cite_start]$1 \times 2 = 2$ [cite: 26] |

* [cite_start]**Total string setelah encoding adalah 10 bit.** [cite: 27]
* [cite_start]**Total keseluruhan tabel adalah $32 \text{ (bit)} + 5 \text{ (frekuensi)} + 10 \text{ (encoding)} = 47$ bit.** [cite: 28]

---

## 💻 Hasil Implementasi (Contoh) 💻

[cite_start]Contoh output dari program implementasi Huffman Coding: [cite: 29]

```
Masukkan teks yang akan di-encode: sisfo

Kode Huffman:
i:10
s: 11
f:01
o:00

Teks ter-encode (bit stream): 1110110100
Teks setelah decode: sisfo
Ukuran asli: 40 bit
Ukuran setelah kompresi: 10 bit
Ruang yang tersimpan: 75.0000%
```
*Note: Ada sedikit perbedaan kode Huffman pada hasil inputan dibandingkan dengan tabel manual. Hal ini bisa terjadi tergantung pada implementasi pohon Huffman (misalnya, penugasan 0/1 untuk anak kiri/kanan pada frekuensi yang sama).*

---

## ➕ Implementasi C++ ➕

(Bagian ini merujuk pada kode sumber C++ yang disediakan dalam dokumen)

Implementasi C++ menunjukkan struktur kode untuk:
* Mendefinisikan node pohon Huffman.
* Membuat fungsi untuk menghitung frekuensi karakter.
* Membangun pohon Huffman.
* Menghasilkan kode Huffman untuk setiap karakter.
* Meng-encode dan men-decode teks.

---