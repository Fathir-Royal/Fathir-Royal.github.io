# 🔄 Kahn's Algorithm
## Algoritma Topological Sort untuk Graf Berarah Tanpa Siklus

---

## 📖 Definisi & Pengenalan

**Kahn's Algorithm** adalah algoritma fundamental yang digunakan untuk melakukan **topological sort** pada graf berarah tanpa siklus (DAG - Directed Acyclic Graph). Algoritma ini diperkenalkan oleh **Arthur B. Kahn pada tahun 1962** dan telah menjadi standar industri untuk menyelesaikan masalah dependency resolution.

### 🎯 **Tujuan Utama:**
Menyusun simpul-simpul dalam urutan sedemikian rupa sehingga **jika ada edge dari simpul U ke simpul V, maka U selalu muncul sebelum V** dalam urutan hasil.

### 🌟 **Keunggulan:**
- ✅ **Efisien**: Kompleksitas waktu O(V + E)
- ✅ **Sederhana**: Mudah dipahami dan diimplementasikan
- ✅ **Robust**: Dapat mendeteksi siklus dalam graf
- ✅ **Praktis**: Banyak aplikasi di dunia nyata

---

## 🏗️ Konsep Dasar & Terminologi

### 1. 🎯 **Graf Berarah (Directed Graph)**

Graf berarah adalah struktur data yang terdiri dari:
- **Vertices (V)**: Kumpulan simpul/node
- **Edges (E)**: Kumpulan sisi berarah yang menghubungkan simpul

```
Contoh Graf Berarah:
A → B → C
↓   ↓
D → E
```

### 2. 🚫 **DAG (Directed Acyclic Graph)**

**Directed Acyclic Graph** adalah graf berarah **tanpa siklus**:

| ✅ **Valid DAG** | ❌ **Invalid (Ada Siklus)** |
|------------------|----------------------------|
| A → B → C → D | A → B → C → A |
| Linear dependency | Circular dependency |

**Karakteristik DAG:**
- Tidak ada jalur yang kembali ke node asal
- Memungkinkan topological ordering
- Merepresentasikan dependency hierarchy
- Essential untuk scheduling problems

### 3. 📊 **In-degree**

**In-degree** adalah jumlah edge yang **masuk** ke suatu node:

```
Graf: A → B ← C
      ↓   ↑
      D → E

In-degree:
- A: 0 (tidak ada edge masuk)
- B: 2 (dari A dan E)
- C: 0 (tidak ada edge masuk)
- D: 1 (dari A)
- E: 1 (dari D)
```

**Fungsi In-degree dalam Kahn's:**
- 🔍 **Menentukan starting points** (in-degree = 0)
- 📈 **Mengukur dependency level**
- 🔄 **Memantau progress algorithm**
- 🚨 **Mendeteksi siklus**

### 4. 📏 **Topological Sort**

**Topological Sort** adalah pengurutan linear dari vertices dalam DAG yang memenuhi constraint dependency:

**Sifat-sifat:**
- 🎯 **Unique ordering tidak selalu ada** (bisa multiple valid solutions)
- 📋 **Semua dependency harus terpenuhi**
- 🔄 **Hasil dapat berbeda tergantung implementasi**
- ⚡ **Kompleksitas optimal O(V + E)**

---

## 🔧 Algoritma: Langkah Demi Langkah

### 📋 **Pseudocode:**

```
KAHN_ALGORITHM(Graph G):
1. Hitung in-degree untuk setiap node
2. Inisialisasi queue dengan nodes yang in-degree = 0
3. Inisialisasi result list kosong
4. WHILE queue tidak kosong:
   a. Dequeue node u
   b. Tambahkan u ke result
   c. Untuk setiap neighbor v dari u:
      - Kurangi in-degree[v]
      - Jika in-degree[v] = 0, enqueue v
5. Jika |result| = |V|: return result
   Else: "Graf memiliki siklus"
```

### 🎮 **Langkah Detail:**

#### **Step 1: Perhitungan In-degree** 🧮
```python
# Contoh graf: {A: [B, D], B: [C, E], C: [], D: [E], E: []}
in_degree = {A: 0, B: 1, C: 1, D: 1, E: 2}
```

#### **Step 2: Inisialisasi Queue** 📦
```python
queue = [A]  # Nodes dengan in-degree = 0
result = []
```

#### **Step 3: Processing Loop** 🔄
```
Iterasi 1: Process A
- result = [A]
- Update in-degree: B=0, D=0
- queue = [B, D]

Iterasi 2: Process B
- result = [A, B]  
- Update in-degree: C=0, E=1
- queue = [D, C]

Iterasi 3: Process D
- result = [A, B, D]
- Update in-degree: E=0
- queue = [C, E]

Iterasi 4: Process C
- result = [A, B, D, C]
- queue = [E]

Iterasi 5: Process E
- result = [A, B, D, C, E]
- queue = []
```

#### **Step 4: Validasi** ✅
```
|result| = 5 = |V| ✅
Topological Order: A → B → D → C → E
```

---

## 🎯 Contoh Lengkap dengan Analisis

### 📊 **Contoh 1: Graf Sederhana**

```
Graf Input:
1 → 2 → 3
1 → 4
2 → 4

Representasi:
{1: [2, 4], 2: [3, 4], 3: [], 4: []}
```

**Solusi Step-by-Step:**

| Step | Action | In-degree State | Queue | Result |
|------|--------|----------------|--------|---------|
| 0 | Initial | [1:0, 2:1, 3:1, 4:2] | [1] | [] |
| 1 | Process 1 | [2:0, 3:1, 4:1] | [2] | [1] |
| 2 | Process 2 | [3:0, 4:0] | [3, 4] | [1, 2] |
| 3 | Process 3 | [4:0] | [4] | [1, 2, 3] |
| 4 | Process 4 | [] | [] | [1, 2, 3, 4] |

**Hasil Akhir**: `[1, 2, 3, 4]` ✅

### 🧩 **Contoh 2: Graf Kompleks dengan Multiple Solutions**

```
Graf Input:
    A → C
    B → C → D
    B → D

Possible Orders:
- [A, B, C, D]
- [B, A, C, D]
```

**Analisis:**
- Nodes A dan B keduanya memiliki in-degree = 0
- Order processing A vs B pertama menghasilkan hasil berbeda
- Kedua hasil sama-sama valid! 🎉

---

## 💻 Implementasi Kode

### 🐍 **Python Implementation**

```python
from collections import deque, defaultdict

def kahns_algorithm(graph):
    """
    Implementasi Kahn's Algorithm untuk Topological Sort
    
    Args:
        graph: Dictionary {node: [list_of_neighbors]}
    
    Returns:
        List: Topological order atau None jika ada siklus
    """
    # Step 1: Hitung in-degree
    in_degree = defaultdict(int)
    
    # Inisialisasi semua nodes
    for node in graph:
        if node not in in_degree:
            in_degree[node] = 0
    
    # Hitung in-degree
    for node in graph:
        for neighbor in graph[node]:
            in_degree[neighbor] += 1
    
    # Step 2: Find nodes dengan in-degree = 0
    queue = deque()
    for node, degree in in_degree.items():
        if degree == 0:
            queue.append(node)
    
    # Step 3: Process queue
    result = []
    
    while queue:
        # Dequeue node
        current = queue.popleft()
        result.append(current)
        
        # Process neighbors
        for neighbor in graph.get(current, []):
            in_degree[neighbor] -= 1
            if in_degree[neighbor] == 0:
                queue.append(neighbor)
    
    # Step 4: Check for cycles
    if len(result) != len(in_degree):
        return None  # Cycle detected
    
    return result

# Contoh penggunaan
def demo_kahns():
    # Graf 1: Simple DAG
    graph1 = {
        1: [2, 4],
        2: [3, 4],
        3: [],
        4: []
    }
    
    # Graf 2: Complex DAG
    graph2 = {
        'A': ['C'],
        'B': ['C', 'D'],
        'C': ['D'],
        'D': []
    }
    
    # Graf 3: With Cycle (Invalid)
    graph3 = {
        'A': ['B'],
        'B': ['C'],
        'C': ['A']  # Creates cycle!
    }
    
    print("🎯 Contoh 1:", kahns_algorithm(graph1))
    print("🎯 Contoh 2:", kahns_algorithm(graph2))
    print("🚫 Contoh 3 (Cycle):", kahns_algorithm(graph3))

# Run demo
demo_kahns()
```

**Output:**
```
🎯 Contoh 1: [1, 2, 3, 4]
🎯 Contoh 2: ['A', 'B', 'C', 'D']  # atau ['B', 'A', 'C', 'D']
🚫 Contoh 3 (Cycle): None
```

### ⚡ **C++ Implementation**

```cpp
#include <iostream>
#include <vector>
#include <queue>
#include <unordered_map>
using namespace std;

class KahnsAlgorithm {
private:
    unordered_map<int, vector<int>> graph;
    unordered_map<int, int> inDegree;
    
public:
    void addEdge(int u, int v) {
        graph[u].push_back(v);
        inDegree[v]++;
        if (inDegree.find(u) == inDegree.end()) {
            inDegree[u] = 0;
        }
    }
    
    vector<int> topologicalSort() {
        queue<int> q;
        vector<int> result;
        
        // Step 1: Find all nodes with in-degree 0
        for (auto& pair : inDegree) {
            if (pair.second == 0) {
                q.push(pair.first);
            }
        }
        
        // Step 2: Process queue
        while (!q.empty()) {
            int current = q.front();
            q.pop();
            result.push_back(current);
            
            // Reduce in-degree of neighbors
            for (int neighbor : graph[current]) {
                inDegree[neighbor]--;
                if (inDegree[neighbor] == 0) {
                    q.push(neighbor);
                }
            }
        }
        
        // Step 3: Check for cycles
        if (result.size() != inDegree.size()) {
            return {}; // Cycle detected
        }
        
        return result;
    }
    
    void printResult(const vector<int>& result) {
        if (result.empty()) {
            cout << "❌ Graf memiliki siklus!" << endl;
        } else {
            cout << "✅ Topological Order: ";
            for (int i = 0; i < result.size(); i++) {
                cout << result[i];
                if (i < result.size() - 1) cout << " → ";
            }
            cout << endl;
        }
    }
};

// Demo usage
int main() {
    KahnsAlgorithm kahn;
    
    // Build graph: 1→2→3, 1→4, 2→4
    kahn.addEdge(1, 2);
    kahn.addEdge(1, 4);
    kahn.addEdge(2, 3);
    kahn.addEdge(2, 4);
    
    vector<int> result = kahn.topologicalSort();
    kahn.printResult(result);
    
    return 0;
}
```

---

## 🌍 Aplikasi dalam Dunia Nyata

### 💼 **1. Software Development**

#### 📦 **Build Systems & Dependency Management**
```
Contoh: Package Dependencies
numpy → pandas → scikit-learn
      ↘ matplotlib → seaborn

Topological Order: numpy → pandas → matplotlib → scikit-learn → seaborn
```

**Use Cases:**
- **Maven/Gradle**: Java project dependencies
- **npm/yarn**: JavaScript package management  
- **pip**: Python package installation
- **Docker**: Multi-stage build dependencies

#### 🔨 **Compilation Pipeline**
```
Source Files Dependency:
main.cpp → utils.h → constants.h
        → math.h → constants.h

Compilation Order: constants.h → utils.h → math.h → main.cpp
```

### 🏭 **2. Project Management**

#### 📊 **Task Scheduling**
```
Project Tasks:
Design → Prototype → Testing
      → Development → Testing → Deployment

Valid Schedule: Design → Prototype → Development → Testing → Deployment
```

**Applications:**
- **PERT Charts**: Critical path analysis
- **Gantt Charts**: Project timeline planning
- **CI/CD Pipelines**: Automated deployment stages
- **Manufacturing**: Assembly line optimization

### 🎓 **3. Academic & Learning**

#### 📚 **Course Prerequisites**
```
CS Curriculum:
Intro Programming → Data Structures → Algorithms
                 → Database Systems → Web Development
                 → Software Engineering

Learning Path: Intro → Data Structures → Database → Algorithms → Web Dev → SE
```

### 🧬 **4. Scientific Computing**

#### 🔬 **Computational Biology**
```
Gene Expression Networks:
Gene A activates → Gene B → Protein Production
        activates → Gene C → Metabolic Pathway

Processing Order: Gene A → Gene B → Gene C → Protein → Pathway
```

### 🎮 **5. Game Development**

#### 🎯 **Quest Systems**
```
RPG Quest Dependencies:
Tutorial → Collect Items → Fight Monster → Get Reward
        → Unlock Area → New Quests

Quest Completion Order ensures proper game progression
```

---

## 📊 Analisis Kompleksitas & Performa

### ⚡ **Time Complexity: O(V + E)**

**Breakdown:**
- **Calculating In-degree**: O(E) - iterate through all edges
- **Queue Operations**: O(V) - each vertex processed once
- **Edge Processing**: O(E) - each edge processed once
- **Total**: O(V + E) - linear time!

### 💾 **Space Complexity: O(V)**

**Breakdown:**
- **In-degree Array**: O(V)
- **Queue Storage**: O(V) worst case
- **Result Array**: O(V)
- **Graph Representation**: O(V + E) - not counted as algorithm overhead

### 📈 **Performance Comparison**

| Algorithm | Time | Space | Use Case | Pros | Cons |
|-----------|------|-------|----------|------|------|
| **Kahn's** | O(V+E) | O(V) | General topological sort | Simple, detects cycles | Requires extra space |
| **DFS-based** | O(V+E) | O(V) | Recursive approach | In-place possible | Stack overflow risk |
| **Lexicographic** | O(V²) | O(V) | Specific ordering needed | Deterministic output | Slower performance |

---

## 🔍 Advanced Topics & Variations

### 🎯 **1. Lexicographic Topological Sort**

Menghasilkan topological order yang **lexicographically smallest**:

```python
def lexicographic_topological_sort(graph):
    import heapq
    
    # Use min-heap instead of regular queue
    heap = []
    # ... (similar logic with heapq.heappush/heappop)
```

### 🔄 **2. All Possible Topological Orders**

Generate semua kemungkinan valid topological orders:

```python
def all_topological_sorts(graph):
    def backtrack(current_order, remaining_nodes):
        if not remaining_nodes:
            yield current_order[:]
            return
        
        for node in remaining_nodes:
            if can_be_next(node, current_order):
                # Try this node next
                # ... recursive exploration
```

### 🚨 **3. Cycle Detection & Reporting**

Enhanced version yang melaporkan siklus yang ditemukan:

```python
def kahns_with_cycle_detection(graph):
    result = kahns_algorithm(graph)
    
    if result is None:
        # Find and report the cycle
        cycle = find_cycle(graph)
        return None, cycle
    
    return result, None
```

### ⚡ **4. Parallel Kahn's Algorithm**

Implementasi paralel untuk graf besar:

```python
async def parallel_kahns(graph, num_workers=4):
    # Process multiple nodes with in-degree=0 simultaneously
    # Synchronization required for in-degree updates
    pass
```

---

## 🎯 Tips & Best Practices

### ✅ **Do's:**

1. **📊 Always validate input**: Pastikan graf adalah DAG
2. **🔍 Handle edge cases**: Empty graph, single node, disconnected components
3. **💾 Choose appropriate data structures**: 
   - Adjacency list untuk sparse graphs
   - Adjacency matrix untuk dense graphs
4. **🚀 Consider performance**: Use heap untuk lexicographic order
5. **🧪 Test thoroughly**: Multiple valid orderings possible

### ❌ **Don'ts:**

1. **🚫 Don't assume unique solution**: Multiple valid orders possible
2. **⚠️ Don't ignore cycle detection**: Always check result length
3. **💥 Don't use on cyclic graphs**: Algorithm will fail
4. **🐌 Don't use inefficient data structures**: Avoid nested loops
5. **🔒 Don't modify graph during processing**: Maintain immutability

### 🛠️ **Common Pitfalls:**

```python
# ❌ Wrong: Modifying original graph
def bad_kahns(graph):
    while graph:  # Modifying during iteration!
        # ... process nodes
        del graph[node]  # DON'T DO THIS

# ✅ Correct: Working with copies
def good_kahns(graph):
    in_degree = calculate_in_degree(graph.copy())
    # ... process without modifying original
```

---

## 🧪 Testing & Validation

### 🔬 **Test Cases Template**

```python
def test_kahns_algorithm():
    test_cases = [
        # Test 1: Simple linear chain
        {
            'graph': {'A': ['B'], 'B': ['C'], 'C': []},
            'expected': ['A', 'B', 'C'],
            'description': 'Linear dependency chain'
        },
        
        # Test 2: Multiple starting points
        {
            'graph': {'A': ['C'], 'B': ['C'], 'C': []},
            'expected_options': [['A', 'B', 'C'], ['B', 'A', 'C']],
            'description': 'Multiple valid orderings'
        },
        
        # Test 3: Cycle detection
        {
            'graph': {'A': ['B'], 'B': ['C'], 'C': ['A']},
            'expected': None,
            'description': 'Cycle should be detected'
        },
        
        # Test 4: Empty graph
        {
            'graph': {},
            'expected': [],
            'description': 'Empty graph handling'
        }
    ]
    
    for i, test in enumerate(test_cases):
        result = kahns_algorithm(test['graph'])
        print(f"Test {i+1}: {test['description']} - {'✅' if validate_result(result, test) else '❌'}")

def validate_result(result, test_case):
    if 'expected' in test_case:
        return result == test_case['expected']
    elif 'expected_options' in test_case:
        return result in test_case['expected_options']
    return False
```

---

## 📚 Kesimpulan & Takeaways

### 🎯 **Key Points:**

1. **🔄 Kahn's Algorithm** adalah metode standar untuk topological sorting
2. **📊 Kompleksitas optimal** O(V + E) membuatnya sangat efisien
3. **🚨 Built-in cycle detection** memberikan robustness
4. **🌍 Aplikasi luas** dari software engineering hingga project management
5. **💡 Implementasi sederhana** namun powerful untuk dependency resolution

### ✅ **Kapan Menggunakan Kahn's:**
- ✅ Dependency resolution dalam build systems
- ✅ Task scheduling dengan prerequisites  
- ✅ Course planning dengan prerequisites
- ✅ Pipeline processing dengan stages
- ✅ Data flow analysis

### ❌ **Kapan Tidak Menggunakan:**
- ❌ Graf dengan siklus (gunakan cycle detection first)
- ❌ Shortest path problems (gunakan Dijkstra/BFS)
- ❌ Undirected graphs (tidak applicable)
- ❌ Real-time systems dengan hard constraints

### 🚀 **Next Steps untuk Pembelajaran:**

1. **📖 Study Related Algorithms:**
   - DFS-based Topological Sort
   - Strongly Connected Components (SCC)
   - Longest Path in DAG

2. **💻 Practice Implementation:**
   - Solve LeetCode topological sort problems
   - Build a simple task scheduler
   - Implement dependency resolver

3. **🔬 Explore Advanced Topics:**
   - Parallel topological sorting
   - Dynamic topological sorting
   - Topological sort with priorities

---