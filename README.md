# Dualtree

A high-performance C++ framework for **fully-dynamic k-nearest neighbor (kNN) joins** on high-dimensional data.  
It supports multiple index structures (HDR-Tree, Δ-Tree, Dualtree, etc.) and provides baseline methods for fair experimental comparison.

---

## 🚀 Features

- Dual-index architecture supporting both **query-set** and **reference-set** updates.
- Multiple modes for different algorithms and baselines:
  - `Scan` — brute-force linear scan baseline  
  - `HDRtree` — A single-side index structure built on the query set originally designed for reverse kNN search  
  - `Deltatree` — A single-side index structure built on the reference set originally designed for kNN search  
  - `Dualtree`, `Dualtreeopt`, `Dualtreefast` — dual-index and optimized variants equipped with theoretically guaranteed fine-grained pruning  
  - `idistance` — Another single-side index structure built on the reference set originally designed for kNN search  
  - `Spheretree` — Another single-side index structure built on the query set originally designed for reverse kNN search
- Compatible with a variety of real-world datasets.
- Optional GNU Scientific Library (GSL) linkage for numerical computation.

---

## 🏗️ Build Instructions

### Prerequisites
- **CMake ≥ 3.12**
- **C++14 or higher**
- **GCC / Clang / MSVC**
- **GSL (GNU Scientific Library)**  
  Default path (Windows): `D:/msys64/mingw64/`

### Build Steps
```bash
# Step 1: Create a build directory
mkdir build && cd build

# Step 2: Generate build files
cmake ..

# Step 3: Compile
make -j
```

> ✅ The compiled executable will be generated as:
> ```
> build/Dualtree.exe   (on Windows)
> build/Dualtree       (on Linux/macOS)
> ```

---

## 🧩 Run Instructions

### Syntax
```bash
./Dualtree <dataset_path> <method>
```

### Example
```bash
./Dualtree ./datasets/sun.txt Dualtreeopt
```

---

## 📦 Dataset Availability & Space Note

To keep the repository lightweight, the `datasets/` folder in this package **only includes** the following two datasets:
- `Normalized_WT.dat`
- `sun.txt`

All other datasets listed below are **publicly available** and can be freely downloaded from open sources on the web.  
Please place any additional datasets under `./datasets/` before running the program.

---

## 📚 Available Datasets
All datasets should be placed under the `./datasets/` folder.

| Dataset File | Description |
|---------------|-------------|
| `Normalized_WT.dat` | Weighted text / numeric dataset |
| `cifar.txt` | CIFAR image feature vectors |
| `audio.txt` | Audio embeddings |
| `enron.txt` | Textual (Enron emails) |
| `fashion-mnist-784-euclidean.txt` | MNIST-style image vectors |
| `millionSong.txt` | Million Song Dataset |
| `sun.txt` | SUN image features |
| `trevi.txt` | Trevi image patches |

---

## 🧪 Supported Methods
| Mode | Description |
|------|--------------|
| `Scan` | Linear scan baseline |
| `HDRtree` | Baseline: A single-side index structure built on the query set originally designed for reverse kNN search |
| `Deltatree` | Baseline: A single-side index structure built on the reference set originally designed for kNN search |
| `Dualtree` | Full dual-index |
| `Dualtreeopt` | Variant of Dualtree equipped with theoretically guaranteed fine-grained pruning obtained through rigorous deduction |
| `Dualtreefast` | Variant of Dualtree equipped with theoretically guaranteed fine-grained pruning obtained through simplified deduction |
| `idistance` | Another single-side index structure built on the reference set originally designed for kNN search |
| `Spheretree` | Another single-side index structure built on the query set originally designed for reverse kNN search |

---

## ⚙️ Configuration Notes

- The CMake script links against:
  ```
  D:/msys64/mingw64/lib/libgsl.a
  D:/msys64/mingw64/lib/libgslcblas.a
  ```
  Modify these paths in `CMakeLists.txt` if GSL is installed elsewhere.

- Optional build flags:
  | Option | Description |
  |---------|-------------|
  | `ENABLE_BIG_OBJECTS` | Enable large object flags (`/bigobj` or `-Wa,-mbig-obj`) |
  | `EIGEN_SAFE_MODE` | Disable Eigen static alignment for safer builds |

---

## 📂 Project Structure
```
Dualtree/
├── main.cpp                   # Entry point (command line interface)
├── CMakeLists.txt             # Build configuration
├── cpp and header files       # Core implementation files
├── datasets/                  # Place datasets here
└── README.md                  # Project documentation
```

---

## 🧪 Example Output
```
Dataset: Time in seconds for using linear scan on dataset sun.txt to maintain the join table against the mixed update = 5
```

---

## 💡 Tips

- Keep dataset paths **relative** (e.g., `./datasets/...`) to ensure portability.
- Use the Release build (`CMAKE_BUILD_TYPE=Release`) for benchmarking and performance evaluation.

---
