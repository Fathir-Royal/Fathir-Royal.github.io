# 🚀 Dijkstra's Algorithm
## *Algoritma Pencarian Jalur Terpendek*

---

## 📚 **Pengertian Dijkstra's Algorithm**

### 🧠 **Sejarah dan Penemu**
**Dijkstra's Algorithm** ditemukan oleh seorang ilmuwan komputer terkemuka, **Edsger Dijkstra**, dan pertama kali dipublikasikan pada tahun **1959**.

### 🎯 **Definisi**
Dijkstra's Algorithm merupakan sebuah algoritma untuk menyelesaikan masalah dengan tujuan **mencari lintasan terpendek** dalam sebuah graf berarah dengan bobot-bobot sisi yang bernilai **positif atau tak-negatif**. 

> 💡 **Catatan Penting**: Algoritma dijkstra merupakan jenis dari **"Greedy Algorithm"** atau algoritma rakus.

---

## 🎯 **Tujuan Dijkstra's Algorithm**

Dijkstra's algorithm digunakan untuk:
- ✅ Menentukan jalur terpendek dari satu titik (simpul) ke titik lainnya
- ✅ Bekerja dalam graf yang memiliki bobot positif
- ✅ Membantu menemukan rute tercepat atau termurah dari satu tempat ke tempat lain

---

## 🌍 **Kegunaan di Kehidupan Nyata**

### 1. 🗺️ **Pemetaan dan Navigasi Digital**
Algoritma ini digunakan oleh aplikasi navigasi seperti:
- **Google Maps** 🗺️
- **Waze** 🚗
- **GPS mobil** 📱

**Fungsi**: Menghitung rute tercepat atau terpendek dari satu lokasi ke lokasi lain dengan mempertimbangkan jarak dan waktu tempuh, bahkan dalam kondisi lalu lintas yang padat.

### 2. 🌐 **Jaringan Komputer dan Telekomunikasi**
Dalam sistem jaringan, algoritma Dijkstra membantu:
- ✅ Menentukan jalur pengiriman data yang paling optimal
- ✅ Memastikan data dikirim dengan kecepatan tinggi dan gangguan minimal
- ✅ Digunakan dalam routing protokol **OSPF (Open Shortest Path First)**

### 3. 🎮 **Pengembangan Game (Pathfinding)**
Dalam dunia game, terutama game strategi dan simulasi:
- ✅ Mengatur gerakan karakter atau objek secara otomatis
- ✅ Memastikan karakter memilih rute yang logis, cepat, dan aman
- ✅ Meningkatkan pengalaman bermain secara signifikan

### 4. 📦 **Perencanaan Logistik dan Transportasi**
Dalam industri logistik dan pengiriman:
- ✅ Merancang rute distribusi barang yang paling efisien
- ✅ Menghemat waktu, bahan bakar, dan biaya operasional
- ✅ Meningkatkan kecepatan layanan kepada pelanggan

### 5. 🤖 **Kecerdasan Buatan (Artificial Intelligence)**
Dalam bidang AI, algoritma Dijkstra menjadi dasar:
- ✅ Berbagai metode pencarian solusi
- ✅ Perencanaan rute dalam sistem cerdas
- ✅ Navigasi robot dalam lingkungan nyata
- ✅ Sistem rekomendasi untuk menemukan "jalur keputusan" terbaik

---

## ⚙️ **Cara Kerja Dijkstra's Algorithm**

Cara kerja Dijkstra's algorithm melibatkan beberapa langkah sederhana yang dijalankan secara berulang-ulang:

### 📝 **Langkah-Langkah Algoritma**

1. **🚀 Inisialisasi**
   - Tentukan simpul awal
   - Simpul ini diberi nilai jarak **0**
   - Semua simpul lainnya diberi nilai jarak **tak terhingga (∞)**

2. **🔍 Periksa Simpul Tetangga**
   - Dari simpul awal, periksa semua simpul tetangga
   - Hitung jarak total dari simpul awal ke simpul tersebut

3. **📊 Perbarui Jarak Minimum**
   - Jika jarak yang baru dihitung **lebih kecil** daripada jarak sebelumnya
   - Perbarui nilai jarak minimum simpul tersebut

4. **🔒 Tandai Simpul sebagai 'Terkunci'**
   - Setelah semua tetangga simpul diperiksa
   - Simpul ini ditandai sebagai **"terkunci"** (sudah diperiksa)
   - Algoritma akan beralih ke simpul berikutnya dengan jarak terpendek yang belum diperiksa

5. **🔄 Ulangi Langkah 2-4**
   - Langkah ini diulang hingga semua simpul telah diperiksa
   - Atau jarak terpendek ke simpul tujuan telah ditemukan

> 🎯 **Hasil**: Dengan pendekatan ini, algoritma memastikan jalur terpendek dari simpul awal ke simpul tujuan.

---

## 📊 **Langkah-Langkah Menggunakan Metode Tabel**

### **Tahap 1**: 📋 Buat Tabel
- Buat tabel dengan kolom untuk tempat
- Jarak dari simpul dan baris untuk posisi simpul

### **Tahap 2**: 🎯 Pilih Simpul
- Pilih simpul awal dan simpul tujuan
- **Syarat**: Simpul tersebut harus terhubung secara langsung

### **Tahap 3**: 📏 Hitung Jarak
- Hitung jarak beberapa simpul tujuan yang telah dipilih

### **Tahap 4**: ⭐ Pilih Jarak Terpendek
- Setelah semua simpul diuji
- Pilih jarak yang terpendek

### **Tahap 5**: 🔄 Iterasi
- Simpul yang dipilih akan menjadi acuan untuk tahap selanjutnya
- Ulangi seperti sebelumnya sampai semua simpul telah diuji
- Setiap simpul telah mendapat jarak terpendeknya

---

## 📝 **Contoh Permasalahan**

### 🎯 **Studi Kasus**: Mencari Rute Terpendek dari M ke W

**Pertanyaan**: Bagaimana cara mencari rute terpendek dari M ke W dan bobotnya?

**Jawaban**: 
- **Rute terpendek**: M → O → Q → W
- **Bobot jarak akhir**: **11**

---

## 💻 **Implementasi dalam C++**

### 🔧 **Kode Program**
```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <climits>

using namespace std;

// Struktur untuk menyimpan edge
struct Edge {
    int to, weight;
};

// Fungsi Dijkstra
vector<int> dijkstra(int start, int n, vector<vector<Edge>>& graph) {
    vector<int> dist(n, INT_MAX);
    priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> pq;
    
    dist[start] = 0;
    pq.push({0, start});
    
    while (!pq.empty()) {
        int u = pq.top().second;
        pq.pop();
        
        for (Edge& e : graph[u]) {
            int v = e.to;
            int weight = e.weight;
            
            if (dist[u] + weight < dist[v]) {
                dist[v] = dist[u] + weight;
                pq.push({dist[v], v});
            }
        }
    }
    
    return dist;
}

int main() {
    // Implementasi graf dan penggunaan algoritma
    // ...
    return 0;
}
```

### 📤 **Output Contoh**
```
Jarak terpendek dari simpul 0:
Simpul 0: 0
Simpul 1: 4
Simpul 2: 12
Simpul 3: 19
Simpul 4: 21
```

---

## 📚 **Latihan Soal**

### 🎯 **Soal Latihan**
**Cari nilai dan lintasan terpendek dari simpul S ke simpul E!**

### ✅ **Jawaban**
- **Lintasan Terpendek**: S → A → D → E atau S → A → C → E
- **Nilai**: **4**

---

## 🎯 **Kesimpulan**

Dijkstra's algorithm adalah salah satu algoritma pencarian jalur terpendek yang **sangat penting** dalam dunia komputasi dan teknologi. 

### 🔑 **Poin Utama**:
- ✅ Bekerja dengan prinsip **Greedy** untuk menemukan rute terpendek
- ✅ Efektif untuk graf berbobot positif
- ✅ Langkah-langkah sistematis yang menjamin hasil optimal
- ✅ Berbagai penerapan nyata yang luas

### 🌟 **Penerapan Utama**:
- 🗺️ Sistem navigasi (Google Maps)
- 🌐 Jaringan komputer
- 🎮 Pengembangan game
- 📦 Logistik
- 🤖 Kecerdasan buatan

### 💡 **Keunggulan**:
Melalui implementasi yang baik, seperti dalam bahasa pemrograman C++, kita dapat mengaplikasikan Dijkstra untuk memecahkan permasalahan kompleks secara **efisien dan tepat**.

---