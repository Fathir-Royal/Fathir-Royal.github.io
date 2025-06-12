# 🎒 Fractional Knapsack Problem
## *Panduan Lengkap Algoritma Greedy untuk Optimasi Kapasitas*

---

## 📚 **Daftar Isi**
1. [Definisi Fractional Knapsack](#definisi)
2. [Permasalahan Utama](#permasalahan)
3. [Jenis Knapsack Problem](#jenis-knapsack)
4. [Konsep Fractional Knapsack](#konsep)
5. [Algoritma Greedy](#algoritma-greedy)
6. [Contoh Kasus & Penyelesaian](#contoh-kasus)
7. [Implementasi Program](#implementasi)
8. [Analisis Kompleksitas](#analisis-kompleksitas)
9. [Kesimpulan](#kesimpulan)

---

## 🔍 **Definisi Fractional Knapsack** {#definisi}

### 📖 **Pengertian**
**Fractional Knapsack** adalah varian dari masalah knapsack (ransel) dalam algoritma, di mana kita **boleh mengambil sebagian dari suatu item** (misalnya setengah, seperempat, dsb.) untuk memaksimalkan nilai total barang dalam kapasitas ransel tertentu.

### 🔤 **Etimologi**
- **Fractional** 📐 = Berasal dari kata "fraction" yang berarti pecahan atau bagian
  - Dalam konteks ini, kamu boleh mengambil sebagian dari suatu item (tidak harus utuh)
- **Knapsack** 🎒 = Berasal dari kata "knap" (menggigit) + "sack" (karung)
  - Ini adalah metafora untuk kapasitas penyimpanan terbatas
  - Representasi tas atau ransel dengan kapasitas maksimum tertentu

---

## ⚡ **Permasalahan Utama** {#permasalahan}

### 🎯 **Inti Masalah**
Pada dasarnya, **Knapsack Problem** adalah sebuah masalah yang muncul ketika kita memiliki:

#### 📦 **Komponen Utama:**
- 🎒 **Sebuah tas** yang memiliki **kapasitas terbatas**
- 📊 **Barang-barang** dengan **berat** dan **nilai** tertentu
- 🎯 **Tujuan:** Memilih barang yang dapat dimasukkan ke dalam tas untuk **memaksimalkan nilai total**

### 🤔 **Tantangan:**
- ⚖️ Bagaimana memilih kombinasi barang yang optimal?
- 📏 Bagaimana mengelola keterbatasan kapasitas?
- 💰 Bagaimana memaksimalkan return on investment (ROI)?

---

## 🏷️ **Jenis Knapsack Problem** {#jenis-knapsack}

### 📋 **Perbandingan Jenis Knapsack**

| Aspek | 0/1 Knapsack | Fractional Knapsack |
|-------|--------------|---------------------|
| 🔢 **Pengambilan Item** | Utuh saja (0 atau 1) | Boleh sebagian (0 ≤ x ≤ 1) |
| 🧮 **Algoritma Optimal** | Dynamic Programming | Greedy Algorithm |
| ⏱️ **Kompleksitas Waktu** | O(nW) | O(n log n) |
| 💾 **Kompleksitas Ruang** | O(nW) | O(1) |
| 🎯 **Solusi** | Integer Solution | Real Number Solution |

### **1️⃣ 0/1 Knapsack Problem:**
```
🚫 Constraint: Kita hanya bisa memilih barang utuh
❌ Tidak bisa mengambil sebagian (fractional)
🎯 Solusi: 0 (tidak diambil) atau 1 (diambil semua)
```

### **2️⃣ Fractional Knapsack Problem:**
```
✅ Flexibility: Kita bisa mengambil sebagian dari barang
📐 Fractional: Tidak hanya barang utuh (0.5, 0.75, dll.)
🎯 Solusi: Nilai real antara 0 dan 1
```

---

## 🧠 **Konsep Fractional Knapsack** {#konsep}

### 🎒 **Analogi Sederhana**
Bayangkan kamu memiliki sebuah tas dengan kapasitas terbatas, dan ada beberapa barang yang memiliki berat dan nilai tertentu.

#### 🎯 **Tujuan Utama:**
- Memaksimalkan nilai barang yang kita bawa
- Tidak melebihi kapasitas tas yang tersedia
- Isi tas dengan barang yang memberi **nilai tertinggi per unit berat**

#### ⚔️ **Keunggulan Fractional:**
Karena ini **fractional**, kamu boleh **"memotong" barang**! 

**Contoh:** 
- 🥇 Kamu cuma bisa bawa 3 kg dari emas seberat 5 kg
- ✅ Gak apa-apa, yang penting nilainya tetap ikut proporsional
- 💰 Nilai yang didapat = (3/5) × nilai_total_emas

---

## 🔧 **Algoritma Greedy untuk Fractional Knapsack** {#algoritma-greedy}

### 📝 **Langkah-langkah Algoritma:**

#### **1️⃣ Hitung Rasio Nilai-Berat**
```
📊 Untuk setiap barang i:
   ratio[i] = value[i] / weight[i]
```

#### **2️⃣ Urutkan Berdasarkan Rasio**
```
🔄 Sort semua barang berdasarkan ratio secara descending
   (dari rasio tertinggi ke terendah)
```

#### **3️⃣ Greedy Selection**
```
🎯 Untuk setiap barang (mulai dari rasio tertinggi):
   - Jika berat_barang ≤ sisa_kapasitas:
     ✅ Ambil seluruh barang
   - Jika berat_barang > sisa_kapasitas:
     📐 Ambil sebagian: (sisa_kapasitas / berat_barang)
```

#### **4️⃣ Update dan Repeat**
```
🔄 Update sisa kapasitas dan total nilai
   Lanjutkan hingga kapasitas habis atau tidak ada barang lagi
```

---

## 📊 **Contoh Kasus & Penyelesaian** {#contoh-kasus}

### 🎮 **Soal Latihan**

Sebuah tas memiliki kapasitas maksimum **50 kg**. Tersedia 3 barang berikut:

| Barang | Berat (kg) | Nilai (Rp) | Rasio (Nilai/Berat) |
|--------|------------|------------|---------------------|
| A | 10 | 60 | ? |
| B | 20 | 100 | ? |
| C | 30 | 120 | ? |

**🎯 Pertanyaan:** Anda boleh mengambil barang sebagian atau seluruhnya. Tentukan nilai maksimum yang dapat dibawa oleh tas dengan strategi Fractional Knapsack!

---

### 🔍 **Penyelesaian Step-by-Step**

#### **Langkah 1: 📊 Hitung Nilai per Berat**
Hitung rasio (value/weight) untuk masing-masing barang:

| Barang | Perhitungan | Rasio |
|--------|-------------|-------|
| A | 60 ÷ 10 | **6.0** |
| B | 100 ÷ 20 | **5.0** |
| C | 120 ÷ 30 | **4.0** |

#### **Langkah 2: 🔄 Urutkan Berdasarkan Rasio Tertinggi**
Urutkan barang dari rasio tertinggi ke terendah:

| Ranking | Barang | Rasio | Berat (kg) | Nilai (Rp) |
|---------|--------|-------|------------|------------|
| 1️⃣ | A | 6.0 | 10 | 60 |
| 2️⃣ | B | 5.0 | 20 | 100 |
| 3️⃣ | C | 4.0 | 30 | 120 |

#### **Langkah 3: 🎯 Proses Greedy Selection**

##### **📦 Inisialisasi:**
- Kapasitas awal tas = **50 kg**
- Total nilai = **0**

##### **🥇 Ambil Barang A (Rasio tertinggi: 6.0)**
```
📊 Barang A: 10 kg, nilai 60
✅ Masih muat → ambil seluruhnya
📏 Sisa kapasitas = 50 - 10 = 40 kg
💰 Total nilai = 0 + 60 = 60
```

##### **🥈 Ambil Barang B (Rasio kedua: 5.0)**  
```
📊 Barang B: 20 kg, nilai 100
✅ Masih muat → ambil seluruhnya  
📏 Sisa kapasitas = 40 - 20 = 20 kg
💰 Total nilai = 60 + 100 = 160
```

##### **🥉 Ambil Barang C (Rasio ketiga: 4.0)**
```
📊 Barang C: 30 kg, nilai 120
❌ Tidak muat seluruhnya → ambil sebagian
📐 Hanya bisa ambil: 20 kg dari 30 kg
📊 Proporsi = 20/30 = 2/3 = 0.667
💰 Nilai yang diambil = (2/3) × 120 = 80
📏 Sisa kapasitas = 20 - 20 = 0 kg
💰 Total nilai = 160 + 80 = 240
```

### 🏆 **Hasil Akhir:**
- **Barang yang diambil:**
  - ✅ Barang A: 10 kg (100%)
  - ✅ Barang B: 20 kg (100%)  
  - 📐 Barang C: 20 kg (66.7%)
- **Total berat:** 50 kg (kapasitas penuh)
- **Nilai maksimum:** **240 Rp**

---

## 💻 **Implementasi Program** {#implementasi}

### 🐍 **Implementasi Python**

```python
class Item:
    def __init__(self, value, weight, name):
        self.value = value
        self.weight = weight  
        self.name = name
        self.ratio = value / weight
    
    def __repr__(self):
        return f"{self.name}(v:{self.value}, w:{self.weight}, r:{self.ratio:.2f})"

def fractional_knapsack(capacity, items):
    """
    🎯 Menyelesaikan Fractional Knapsack Problem
    
    Args:
        capacity: Kapasitas maksimum tas
        items: List of Item objects
    
    Returns:
        tuple: (max_value, selected_items_detail)
    """
    # 📊 Urutkan berdasarkan rasio nilai/berat (descending)
    items.sort(key=lambda x: x.ratio, reverse=True)
    
    max_value = 0
    selected_items = []
    remaining_capacity = capacity
    
    print("🔄 Urutan barang berdasarkan rasio:")
    for i, item in enumerate(items, 1):
        print(f"{i}. {item}")
    print()
    
    # 🎯 Greedy selection
    for item in items:
        if remaining_capacity <= 0:
            break
            
        if item.weight <= remaining_capacity:
            # ✅ Ambil seluruh barang
            fraction = 1.0
            taken_weight = item.weight
            taken_value = item.value
            remaining_capacity -= item.weight
            
            print(f"✅ Ambil {item.name} seluruhnya:")
            print(f"   📦 Berat: {taken_weight} kg")
            print(f"   💰 Nilai: {taken_value}")
            print(f"   📏 Sisa kapasitas: {remaining_capacity} kg")
        else:
            # 📐 Ambil sebagian barang
            fraction = remaining_capacity / item.weight
            taken_weight = remaining_capacity
            taken_value = item.value * fraction
            remaining_capacity = 0
            
            print(f"📐 Ambil {item.name} sebagian:")
            print(f"   📊 Proporsi: {fraction:.3f} ({fraction*100:.1f}%)")
            print(f"   📦 Berat: {taken_weight} kg dari {item.weight} kg")
            print(f"   💰 Nilai: {taken_value:.2f} dari {item.value}")
            print(f"   📏 Sisa kapasitas: {remaining_capacity} kg")
        
        max_value += taken_value
        selected_items.append({
            'name': item.name,
            'fraction': fraction,
            'weight_taken': taken_weight,
            'value_taken': taken_value
        })
        
        print(f"   🏆 Total nilai sementara: {max_value:.2f}")
        print()
    
    return max_value, selected_items

# 🎮 Contoh penggunaan
if __name__ == "__main__":
    # 📊 Data barang
    items = [
        Item(60, 10, 'A'),   # ratio = 6.0
        Item(100, 20, 'B'),  # ratio = 5.0  
        Item(120, 30, 'C')   # ratio = 4.0
    ]
    
    capacity = 50
    
    print("🎒 FRACTIONAL KNAPSACK PROBLEM")
    print("=" * 40)
    print(f"📏 Kapasitas tas: {capacity} kg")
    print(f"📦 Jumlah barang: {len(items)}")
    print()
    
    max_value, selected = fractional_knapsack(capacity, items)
    
    print("🏆 HASIL AKHIR:")
    print("=" * 40)
    print(f"💰 Nilai maksimum: {max_value:.2f}")
    print("📋 Detail barang yang dipilih:")
    
    total_weight = 0
    for item in selected:
        total_weight += item['weight_taken']
        percentage = item['fraction'] * 100
        print(f"   • {item['name']}: {item['weight_taken']} kg "
              f"({percentage:.1f}%) - Nilai: {item['value_taken']:.2f}")
    
    print(f"📦 Total berat: {total_weight} kg")
    print(f"📊 Efisiensi kapasitas: {(total_weight/capacity)*100:.1f}%")
```

### 🚀 **Output Program:**
```
🎒 FRACTIONAL KNAPSACK PROBLEM
========================================
📏 Kapasitas tas: 50 kg
📦 Jumlah barang: 3

🔄 Urutan barang berdasarkan rasio:
1. A(v:60, w:10, r:6.00)
2. B(v:100, w:20, r:5.00)
3. C(v:120, w:30, r:4.00)

✅ Ambil A seluruhnya:
   📦 Berat: 10 kg
   💰 Nilai: 60
   📏 Sisa kapasitas: 40 kg
   🏆 Total nilai sementara: 60.00

✅ Ambil B seluruhnya:
   📦 Berat: 20 kg
   💰 Nilai: 100
   📏 Sisa kapasitas: 20 kg
   🏆 Total nilai sementara: 160.00

📐 Ambil C sebagian:
   📊 Proporsi: 0.667 (66.7%)
   📦 Berat: 20 kg dari 30 kg
   💰 Nilai: 80.00 dari 120
   📏 Sisa kapasitas: 0 kg
   🏆 Total nilai sementara: 240.00

🏆 HASIL AKHIR:
========================================
💰 Nilai maksimum: 240.00
📋 Detail barang yang dipilih:
   • A: 10 kg (100.0%) - Nilai: 60.00
   • B: 20 kg (100.0%) - Nilai: 100.00
   • C: 20 kg (66.7%) - Nilai: 80.00
📦 Total berat: 50 kg
📊 Efisiensi kapasitas: 100.0%
```

---

## 📈 **Analisis Kompleksitas** {#analisis-kompleksitas}

### ⏱️ **Time Complexity**

| Operasi | Kompleksitas | Penjelasan |
|---------|--------------|------------|
| 📊 Menghitung Rasio | O(n) | Untuk setiap barang |
| 🔄 Sorting | **O(n log n)** | Mengurutkan berdasarkan rasio |
| 🎯 Greedy Selection | O(n) | Iterasi sekali untuk setiap barang |
| **Total** | **O(n log n)** | Didominasi oleh operasi sorting |

### 💾 **Space Complexity**
- **O(1)** atau **O(n)** tergantung implementasi
- O(1) jika hanya menyimpan hasil
- O(n) jika menyimpan detail semua barang yang dipilih

### 🔍 **Perbandingan dengan Metode Lain**

| Metode | Time Complexity | Space Complexity | Optimal? |
|--------|----------------|------------------|----------|
| **Fractional Knapsack (Greedy)** | O(n log n) | O(1) | ✅ Ya |
| 0/1 Knapsack (DP) | O(nW) | O(nW) | ✅ Ya |
| Brute Force | O(2^n) | O(n) | ✅ Ya |

---

## 🎯 **Kelebihan dan Kekurangan** 

### ✅ **Kelebihan Fractional Knapsack**
1. **🚀 Efisiensi Tinggi** - Kompleksitas O(n log n)
2. **🎯 Solusi Optimal** - Greedy menghasilkan solusi optimal
3. **🧠 Mudah Dipahami** - Logika sederhana dan intuitif
4. **💾 Hemat Memori** - Space complexity O(1)
5. **🔧 Implementasi Mudah** - Tidak memerlukan struktur data kompleks

### ⚠️ **Kekurangan dan Keterbatasan**
1. **📐 Tidak Realistis** - Dalam dunia nyata, tidak semua barang bisa dipotong
2. **🔢 Terbatas pada Fractional** - Tidak cocok untuk 0/1 knapsack
3. **📊 Solusi Real Number** - Hasil bisa berupa pecahan/desimal
4. **⚖️ Asumsi Proporsionalitas** - Nilai harus proporsional dengan berat

---

## 🌟 **Aplikasi Praktis**

### 🏭 **Industri dan Bisnis**
- **🏭 Industri Kimia** - Mixing berbagai bahan kimia
- **⛽ Industri Minyak** - Blending berbagai jenis minyak
- **🥤 Industri Makanan** - Mixing ingredien dalam resep
- **💊 Farmasi** - Komposisi obat dengan bahan aktif

### 📊 **Keuangan dan Investasi**
- **💰 Portfolio Optimization** - Alokasi dana investasi
- **📈 Resource Allocation** - Distribusi budget perusahaan
- **🏦 Asset Management** - Manajemen aset liquid

### 🔬 **Riset dan Pengembangan**
- **🧪 Penelitian Kimia** - Optimasi komposisi eksperimen
- **📊 Data Science** - Feature selection dengan continuous weights
- **🤖 Machine Learning** - Ensemble methods dengan weighted models

---

## 🏆 **Kesimpulan** {#kesimpulan}

### 📋 **Ringkasan Key Points:**

1. **🎯 Fleksibilitas Fractional**
   - Dalam Fractional Knapsack, kita dapat memilih sebagian barang
   - Memberikan solusi yang lebih optimal dibandingkan 0/1 knapsack dalam konteks fractional

2. **🧠 Algoritma Greedy yang Efektif**
   - Solusinya menggunakan algoritma greedy dengan memilih barang berdasarkan rasio nilai terhadap berat tertinggi
   - Greedy choice property memastikan solusi optimal

3. **📝 Metodologi Terstruktur**
   - **Langkah-langkah:** Hitung rasio → Urutkan barang → Masukkan barang ke tas
   - Prosedur yang sistematis dan mudah diimplementasikan

4. **⚡ Efisiensi Computational**
   - Solusi ini memiliki kompleksitas waktu **O(n log n)**
   - Sangat efisien untuk dataset besar

### 🌟 **Nilai Tambah:**
- **🔧 Practical Application** - Banyak aplikasi di dunia nyata
- **📚 Educational Value** - Contoh excellent untuk belajar greedy algorithm
- **🎯 Optimal Solution** - Menghasilkan solusi yang mathematically optimal
- **💡 Intuitive Logic** - Mudah dipahami dan dijelaskan

### 🚀 **Rekomendasi Pengembangan:**
- Eksplorasi varian knapsack problem lainnya
- Implementasi untuk kasus multi-dimensional knapsack
- Integrasi dengan sistem optimasi enterprise
- Penelitian aplikasi pada bidang AI dan machine learning

---

### 💡 **Topik Diskusi Menarik:**
- Bagaimana jika ada constraint tambahan?
- Aplikasi fractional knapsack di bidang lain?
- Perbandingan dengan algoritma optimasi lainnya?
- Implementasi untuk real-world scenarios?

---