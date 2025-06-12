# 🌳 Depth-First Search (DFS)
## Algoritma Penelusuran Graf yang Mendalam

---

## 📝 Definisi

**Depth-First Search (DFS)** adalah salah satu metode penelusuran fundamental dalam struktur data seperti graf atau pohon. Algoritma ini bekerja dengan prinsip "**mendalam terlebih dahulu**" - mirip seperti menjelajahi labirin dengan cara mengikuti satu jalur hingga mentok, baru kemudian kembali dan mencoba jalur lainnya.

### 🎯 Cara Kerja DFS:
1. **Mulai** dari simpul awal
2. **Kunjungi** simpul sedalam mungkin pada satu cabang
3. **Backtrack** (mundur) ketika tidak ada jalur lain
4. **Ulangi** proses untuk cabang yang belum dikunjungi

DFS dapat diimplementasikan menggunakan:
- 🔄 **Rekursi** (pendekatan natural)
- 📚 **Stack** (pendekatan iteratif)

---

## 🔧 Jenis-Jenis DFS

### 1. 🔄 **DFS Rekursif**
- Menggunakan call stack sistem
- Implementasi paling sederhana dan intuitif
- Cocok untuk graf kecil hingga menengah

### 2. 📚 **DFS Iteratif (Stack-based)**
- Menggunakan struktur data stack eksplisit
- Lebih terkontrol penggunaan memorinya
- Menghindari stack overflow pada graf besar

### 3. 🔍 **DFS untuk Deteksi Siklus**
- Mendeteksi apakah graf memiliki cycle
- Menggunakan status: WHITE, GRAY, BLACK
- Penting untuk validasi graf

### 4. 📊 **DFS untuk Topological Sort**
- Mengurutkan simpul berdasarkan dependensi
- Berguna untuk scheduling dan prerequisite

### 5. 🧩 **DFS untuk Komponen Terhubung**
- Menemukan Strongly Connected Components (SCC)
- Algoritma Kosaraju dan Tarjan
- Analisis struktur graf kompleks

### 6. ⏱️ **DFS Terbatas Kedalaman (IDDFS)**
- Iterative Deepening Depth-First Search
- Kombinasi DFS dan BFS
- Memory-efficient untuk ruang pencarian besar

---

## ⚠️ Tantangan & Keterbatasan

### 🚧 **Tantangan Utama:**

#### 1. 🔄 **Deteksi Siklus**
- **Masalah**: DFS dapat terjebak dalam infinite loop
- **Solusi**: Menggunakan array `visited[]` untuk menandai simpul yang sudah dikunjungi
- **Implementasi**: Status tracking (WHITE-GRAY-BLACK)

#### 2. 💾 **Penggunaan Memori Tinggi**
- **Masalah**: Rekursi mendalam dapat menyebabkan stack overflow
- **Solusi**: Implementasi iteratif dengan stack eksplisit
- **Batasan**: O(V) space complexity untuk worst case

#### 3. 🎯 **Tidak Menjamin Jalur Terpendek**
- **Masalah**: DFS menemukan jalur pertama, bukan yang optimal
- **Alternatif**: Gunakan BFS atau algoritma Dijkstra untuk jalur terpendek
- **Use Case**: DFS cocok untuk "menemukan jalur", bukan "jalur terbaik"

### 🚫 **Batasan Algoritma:**

| Aspek | Keterbatasan | Dampak |
|-------|--------------|--------|
| **Efisiensi** | Tidak efisien untuk graf besar dan kompleks | Time complexity O(V+E) |
| **Scope** | Hanya menjelajah satu komponen terhubung | Perlu loop untuk semua komponen |
| **Optimality** | Tidak cocok untuk mencari jalur terpendek | Gunakan BFS/Dijkstra |
| **Memory** | Risiko stack overflow pada graf dalam | Implementasi iteratif |
| **Cycles** | Tidak otomatis menangani siklus | Perlu visited tracking |

---

## 🌍 Penerapan dalam Dunia Nyata

### 💻 **Sistem Komputer:**
- **File Explorer**: Menjelajah folder dan subfolder
- **Compiler**: Dependency resolution
- **Operating System**: Process scheduling

### 🎮 **Game Development:**
- **Pathfinding**: Eksplorasi jalur di maze atau dungeon
- **AI Decision**: Game tree traversal
- **Level Generation**: Procedural maze creation

### 🧠 **Artificial Intelligence:**
- **Puzzle Solving**: Sudoku, N-Queens, Crossword
- **Decision Trees**: Machine learning algorithms
- **Search Problems**: State space exploration

### 📱 **Social Networks:**
- **Friend Recommendations**: Analisis hubungan sosial
- **Community Detection**: Menemukan kelompok terhubung
- **Influence Propagation**: Viral content analysis

### 🔬 **Scientific Applications:**
- **Bioinformatics**: Protein structure analysis
- **Chemistry**: Molecular graph traversal
- **Physics**: Network analysis

---

## 📊 Contoh Implementasi

### 🎯 **Contoh 1: Traversal Lengkap**

```
Graf:
    A
   / \
  B   C
 /     \
D       E
|
F

Urutan DFS dari A: A → B → D → F → C → E
```

**Langkah-langkah:**
1. Mulai dari **A** ✅
2. Pilih **B** (child pertama) ✅
3. Dari B, pilih **D** ✅
4. Dari D, pilih **F** ✅
5. F tidak punya child, backtrack ke D, lalu B, lalu A
6. Dari A, pilih **C** ✅
7. Dari C, pilih **E** ✅

### 🔍 **Contoh 2: Pencarian Target**

```
Graf yang sama, mencari F:
Urutan: A → B → D → F ✅ (FOUND!)
```

### 🏆 **Latihan: Graf Kompleks**

```
Graf 12 simpul:
A terhubung ke B, C
B terhubung ke A, E
E terhubung ke B, H
H terhubung ke E, I
I terhubung ke H, L
L terhubung ke I, J
... (dan seterusnya)

Mencari jalur A → J:
Hasil: A → B → E → H → I → L → J
```

---

## 💻 Implementasi Kode

### 🐍 **Python Implementation**

```python
def dfs_recursive(graph, start, visited=None, path=None):
    """
    DFS Rekursif dengan tracking path
    """
    if visited is None:
        visited = set()
    if path is None:
        path = []
    
    visited.add(start)
    path.append(start)
    print(f"Mengunjungi: {start}")
    
    for neighbor in graph[start]:
        if neighbor not in visited:
            dfs_recursive(graph, neighbor, visited, path)
    
    return path

def dfs_iterative(graph, start):
    """
    DFS Iteratif menggunakan Stack
    """
    visited = set()
    stack = [start]
    path = []
    
    while stack:
        vertex = stack.pop()
        if vertex not in visited:
            visited.add(vertex)
            path.append(vertex)
            print(f"Mengunjungi: {vertex}")
            
            # Tambahkan neighbors ke stack (reverse order)
            for neighbor in reversed(graph[vertex]):
                if neighbor not in visited:
                    stack.append(neighbor)
    
    return path

# Contoh Graf
graph = {
    'A': ['B', 'C'],
    'B': ['A', 'D'],
    'C': ['A', 'E'],
    'D': ['B', 'F'],
    'E': ['C'],
    'F': ['D']
}

# Eksekusi
print("🔄 DFS Rekursif:")
path1 = dfs_recursive(graph, 'A')

print("\n📚 DFS Iteratif:")
path2 = dfs_iterative(graph, 'A')
```

### ⚡ **Kompleksitas:**
- **Time Complexity**: O(V + E)
  - V = jumlah vertex (simpul)
  - E = jumlah edge (sisi)
- **Space Complexity**: O(V)
  - Untuk visited set dan call stack/explicit stack

---

## 📈 Analisis Performa

| Aspek | DFS | BFS | Dijkstra |
|-------|-----|-----|----------|
| **Time** | O(V+E) | O(V+E) | O(V²) atau O(E log V) |
| **Space** | O(V) | O(V) | O(V) |
| **Jalur Terpendek** | ❌ | ✅ (unweighted) | ✅ (weighted) |
| **Memory Usage** | Rendah | Tinggi | Sedang |
| **Use Case** | Exploration | Shortest Path | Optimal Path |

---

## 🎯 Kesimpulan

### ✅ **Kelebihan DFS:**
- **Sederhana** dan mudah diimplementasikan
- **Memory efficient** untuk pencarian mendalam
- **Fleksibel** untuk berbagai aplikasi
- **Natural** untuk problem solving rekursif

### ⚠️ **Kekurangan DFS:**
- **Tidak optimal** untuk jalur terpendek
- **Risiko stack overflow** pada graf dalam
- **Dapat terjebak** dalam infinite loop tanpa visited tracking
- **Hanya satu komponen** per eksekusi

### 🚀 **Rekomendasi Penggunaan:**
- ✅ **Gunakan DFS untuk**: Deteksi siklus, topological sort, maze solving, puzzle games
- ❌ **Hindari DFS untuk**: Shortest path problems, level-order traversal, optimal solution finding

---