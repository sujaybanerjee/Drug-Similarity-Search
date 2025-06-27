## 🔍 Problem Statement

Given a database of molecular compounds, we want to retrieve the top-k most chemically similar drugs to a query compound. Traditional exact methods can be computationally expensive for large databases. Our solution applies **randomized algorithms** to trade off exactness for speed while maintaining high accuracy.

---

## 💡 Key Concepts

- **Molecular Fingerprints**: Binary vectors representing the presence/absence of molecular substructures.
- **Similarity Metric**: I used **Tanimoto similarity (Jaccard index)** to measure overlap between fingerprints.
- **Randomized Hashing**: Employed techniques inspired by **Locality-Sensitive Hashing (LSH)** and **minwise hashing** to reduce computation.
- **Random Projections**: Explored sparse random projections to compress fingerprint vectors while preserving neighborhood similarity.

---

## 🧠 Algorithm Summary

1. **Preprocessing**:
   - Parse SMILES strings or molecular graphs
   - Convert compounds to binary fingerprints using RDKit or an internal hashing scheme

2. **Randomized Similarity Search**:
   - Generate random hash functions (simulating permutations or projections)
   - Create compressed hash buckets for fingerprints
   - Use collision counts across hash buckets as proxy for similarity

3. **Querying**:
   - Given a new compound, compute its hashes
   - Retrieve candidate matches from similar buckets
   - Rank candidates using true Tanimoto similarity

---

## 🧪 Dataset

I used a curated subset of drug-like molecules from public databases such as:

- **ChEMBL**
- **DrugBank**
- Custom-formatted SMILES/CSV files provided during the course

Each molecule was represented as a binary vector (e.g., 1024 bits) indicating substructure presence.

---

## ⚙️ Implementation

- Language: Python
- Libraries: `RDKit`, `NumPy`, `scikit-learn` (for hashing), `matplotlib` (for visualization)
- Features:
  - Fingerprint generation from SMILES
  - Custom LSH-like scheme
  - Top-k result retrieval with timing benchmarks

---

## 📈 Results

- Achieved **>90% accuracy** in retrieving top-5 most similar drugs vs. brute-force Tanimoto comparisons
- **Speedup** of ~10x for databases with thousands of entries
- Demonstrated the **scalability** of randomized hashing for chemical search
