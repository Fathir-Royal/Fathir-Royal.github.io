# 🎯 Activity Selection Problem (ASP)
## *Panduan Lengkap Algoritma Greedy untuk Pemilihan Aktivitas*

---

## 📚 **Daftar Isi**
1. [Pengertian ASP](#pengertian-asp)
2. [Pentingnya ASP](#pentingnya-asp)
3. [Batasan Masalah](#batasan-masalah)
4. [Greedy Algorithm](#greedy-algorithm)
5. [Strategi Penyelesaian](#strategi-penyelesaian)
6. [Contoh Kasus](#contoh-kasus)
7. [Implementasi C++](#implementasi-c)
8. [Kesimpulan](#kesimpulan)

---

## 🔍 **Pengertian ASP** {#pengertian-asp}

**Activity Selection Problem (ASP)** adalah masalah klasik dalam ilmu komputer yang bertujuan untuk memilih serangkaian aktivitas yang dapat dilakukan dalam satu periode waktu, dengan batasan bahwa aktivitas-aktivitas tersebut **tidak boleh tumpang tindih**.

### 🎯 **Tujuan Utama:**
- Memaksimalkan jumlah aktivitas yang dapat dipilih
- Memastikan tidak ada konflik waktu antar aktivitas
- Mengoptimalkan penggunaan sumber daya waktu

---

## 🌟 **Pentingnya ASP** {#pentingnya-asp}

ASP sangat penting karena banyak ditemukan dalam berbagai situasi di dunia nyata:

### 🏢 **Aplikasi Praktis:**
- 📅 **Jadwal Ruangan** - Mengatur penggunaan ruang meeting/kelas
- 💼 **Wawancara Kerja** - Menjadwalkan sesi wawancara tanpa konflik
- 🔧 **Pengelolaan Sumber Daya** - Optimasi alokasi mesin/peralatan
- 🎬 **Penjadwalan Produksi** - Mengatur timeline produksi film/acara
- 🏥 **Jadwal Dokter** - Mengoptimalkan jadwal konsultasi medis

---

## ⚠️ **Batasan Masalah (Constraints)** {#batasan-masalah}

### 🚫 **Tidak Boleh Ada Tumpang Tindih Aktivitas**
Aktivitas yang dipilih harus memiliki waktu mulai yang **lebih besar atau sama dengan** waktu selesai aktivitas yang sebelumnya dipilih.

**Rumus:** `start_time[i] ≥ finish_time[i-1]`

### ⏰ **Hanya Satu Aktivitas dalam Satu Waktu**
Kita tidak bisa melakukan lebih dari satu aktivitas yang berlangsung pada waktu yang sama. Hal ini mengharuskan kita untuk:
- 🎯 Memanfaatkan waktu yang ada dengan sebaik-baiknya
- 📊 Membuat keputusan optimal dalam pemilihan aktivitas
- ⚖️ Menyeimbangkan antara kuantitas dan efisiensi waktu

---

## 🧠 **Greedy Algorithm** {#greedy-algorithm}

### 📖 **Definisi**
**Greedy Algorithm** adalah pendekatan pemecahan masalah yang membuat keputusan terbaik atau optimal pada setiap langkah, dengan harapan bahwa keputusan-keputusan lokal yang optimal ini akan menghasilkan solusi yang **global optimal**.

### 🎯 **Prinsip Dasar Greedy:**
1. **Pilihan Serakah (Greedy Choice)** - Pilih yang terbaik saat ini
2. **Struktur Sub-masalah Optimal** - Masalah dapat dipecah menjadi sub-masalah
3. **Tidak Ada Backtracking** - Keputusan tidak dapat diubah

---

## 🤔 **Mengapa ASP Cocok dengan Greedy?** 

### ✅ **Alasan Kompatibilitas:**

#### 🏗️ **Memiliki Struktur Optimalitas Lokal**
- Memilih aktivitas yang selesai lebih cepat memberi ruang untuk aktivitas lain
- Keputusan lokal yang optimal mendukung solusi global

#### 🎪 **Solusi Optimal Terbentuk dari Keputusan Lokal**
- Setiap pilihan aktivitas berkontribusi pada solusi optimal keseluruhan
- Tidak memerlukan pertimbangan ulang terhadap keputusan sebelumnya

---

## 🛠️ **Strategi Penyelesaian dengan Algoritma Greedy** {#strategi-penyelesaian}

### 📝 **Langkah-langkah Penyelesaian ASP:**

#### **1️⃣ Urutkan Aktivitas**
```
🔄 Urutkan aktivitas berdasarkan waktu selesai (finish time)
   dari yang paling awal hingga paling akhir
```

#### **2️⃣ Pilih Aktivitas Pertama**
```
✅ Pilih aktivitas pertama dalam daftar terurut
   (aktivitas yang selesai paling cepat)
```

#### **3️⃣ Seleksi Aktivitas Berikutnya**
```
🔍 Pilih aktivitas berikutnya jika:
   waktu_mulai ≥ waktu_selesai_aktivitas_terakhir_yang_dipilih
```

#### **4️⃣ Iterasi**
```
🔁 Ulangi langkah ketiga sampai semua aktivitas diperiksa
```

---

## 📊 **Contoh Kasus** {#contoh-kasus}

### 🎮 **Contoh Soal 1**

Misalkan kita memiliki daftar aktivitas dengan waktu mulai dan waktu selesai sebagai berikut:

| Aktivitas | Waktu Mulai | Waktu Selesai |
|-----------|-------------|---------------|
| A | 1 | 4 |
| B | 2 | 3 |
| C | 4 | 6 |

**🎯 Tujuan:** Tentukan aktivitas maksimal yang dapat dipilih sehingga tidak ada aktivitas yang saling tumpang tindih!

### 🔄 **Proses Penyelesaian:**

#### **Langkah 1: Urutkan berdasarkan waktu selesai**
| Aktivitas | Waktu Mulai | Waktu Selesai |
|-----------|-------------|---------------|
| B | 2 | 3 |
| A | 1 | 4 |
| C | 4 | 6 |

#### **Langkah 2: Pilih Aktivitas Pertama**
✅ **Aktivitas B** dipilih (selesai paling cepat pada waktu 3)

#### **Langkah 3: Pilih Aktivitas yang Tidak Tumpang Tindih**
- 🔍 Periksa Aktivitas A: waktu mulai = 1, waktu selesai B = 3 → **1 < 3 (TIDAK DIPILIH)**
- 🔍 Periksa Aktivitas C: waktu mulai = 4, waktu selesai B = 3 → **4 ≥ 3 (DIPILIH)** ✅

### 🏆 **Solusi yang Ditemukan:**
- **Aktivitas terpilih:** B, C
- **Jumlah maksimal aktivitas:** 2

---

### 🎮 **Latihan Mandiri**

**Soal:** Misalkan kita memiliki daftar aktivitas berikut:

| Aktivitas | Waktu Mulai | Waktu Selesai |
|-----------|-------------|---------------|
| D | 3 | 5 |
| E | 1 | 2 |
| F | 6 | 8 |

**💡 Solusi:**
- **Aktivitas terpilih:** E, D, F  
- **Jumlah maksimal aktivitas:** 3

---

## 💻 **Implementasi C++** {#implementasi-c}

### 🏗️ **Struktur Program**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>
using namespace std;

// 📦 Struktur untuk merepresentasikan aktivitas
struct Activity {
    int start;   // ⏰ Waktu mulai
    int finish;  // 🏁 Waktu selesai
    char name;   // 🏷️ Nama aktivitas
};

// 🔄 Fungsi untuk mengurutkan berdasarkan waktu selesai
bool compare(Activity a, Activity b) {
    return a.finish < b.finish;
}

// 🎯 Fungsi utama untuk menyelesaikan ASP
void activitySelection(vector<Activity>& activities) {
    // 📊 Urutkan aktivitas berdasarkan waktu selesai
    sort(activities.begin(), activities.end(), compare);
    
    cout << "🏆 Aktivitas yang dipilih:\n";
    
    // ✅ Pilih aktivitas pertama
    int lastSelected = 0;
    cout << "📌 " << activities[0].name 
         << " (Waktu: " << activities[0].start 
         << " - " << activities[0].finish << ")\n";
    
    // 🔍 Pilih aktivitas berikutnya yang tidak tumpang tindih
    for (int i = 1; i < activities.size(); i++) {
        if (activities[i].start >= activities[lastSelected].finish) {
            cout << "📌 " << activities[i].name 
                 << " (Waktu: " << activities[i].start 
                 << " - " << activities[i].finish << ")\n";
            lastSelected = i;
        }
    }
}

// 🚀 Fungsi main
int main() {
    vector<Activity> activities = {
        {1, 4, 'A'},
        {3, 5, 'B'}, 
        {0, 6, 'C'},
        {5, 7, 'D'},
        {3, 9, 'E'},
        {5, 9, 'F'},
        {6, 10, 'G'},
        {8, 11, 'H'},
        {8, 12, 'I'},
        {2, 14, 'J'},
        {12, 16, 'K'}
    };
    
    activitySelection(activities);
    return 0;
}
```

### 🔍 **Penjelasan Implementasi:**

#### **📦 Struktur Activity**
Mendefinisikan tiga atribut:
- `start` - ⏰ Waktu mulai aktivitas
- `finish` - 🏁 Waktu selesai aktivitas  
- `name` - 🏷️ Identitas aktivitas

#### **🔄 Fungsi Compare**
Mengurutkan aktivitas berdasarkan waktu selesai menggunakan `sort()` dengan kriteria `finish time` ascending.

#### **🎯 Fungsi activitySelection**
- ✅ Pilih aktivitas pertama yang selesai lebih cepat
- 🔍 Gunakan loop untuk memilih aktivitas yang tidak tumpang tindih
- 📄 Cetak aktivitas yang dipilih beserta waktu mulai dan selesai

#### **🚀 Bagian Main**
- 📝 Mendefinisikan daftar aktivitas
- 🎯 Memanggil fungsi `activitySelection` untuk menyelesaikan ASP

### 📈 **Output Program:**
```
🏆 Aktivitas yang dipilih:
📌 A (Waktu: 1 - 4)
📌 C (Waktu: 4 - 6) 
📌 D (Waktu: 5 - 7)
```

**✨ Hasil:** Aktivitas yang dipilih adalah A, C, dan D. Program berhasil memilih aktivitas sebanyak mungkin yang tidak saling bertumpang tindih, sesuai dengan prinsip greedy.

---

## 📊 **Analisis Kompleksitas**

### ⏱️ **Time Complexity**
- **Sorting:** O(n log n)
- **Selection:** O(n)
- **Total:** **O(n log n)**

### 💾 **Space Complexity**
- **O(1)** - Hanya menggunakan variabel tambahan konstanta

---

## 🎯 **Kesimpulan** {#kesimpulan}

### 📋 **Ringkasan Pembelajaran:**

**Activity Selection Problem (ASP)** adalah masalah optimasi yang sangat umum dalam dunia nyata. Dengan pendekatan **greedy algorithm**, kita dapat menyelesaikannya secara efisien dan optimal.

### 🔑 **Poin Kunci:**
- 🎯 **Strategi:** Pilih aktivitas yang selesai paling awal
- ⚠️ **Constraint:** Pastikan tidak ada aktivitas yang bertabrakan  
- 🏢 **Aplikasi:** Cocok untuk penjadwalan (kelas, ruang, wawancara)
- ⚡ **Keunggulan:** Kesederhanaan logika dan efisiensi waktu komputasi

### 🌟 **Manfaat Praktis:**
1. **📈 Efisiensi Tinggi** - Kompleksitas waktu O(n log n)
2. **🎯 Solusi Optimal** - Menghasilkan jumlah aktivitas maksimal
3. **🔧 Mudah Implementasi** - Logika sederhana dan straightforward
4. **🌍 Aplikasi Luas** - Dapat diterapkan di berbagai domain

### 💡 **Rekomendasi Pengembangan:**
- Eksplorasi varian ASP dengan constraint tambahan
- Implementasi pada kasus real-world yang lebih kompleks
- Integrasi dengan sistem manajemen sumber daya

---