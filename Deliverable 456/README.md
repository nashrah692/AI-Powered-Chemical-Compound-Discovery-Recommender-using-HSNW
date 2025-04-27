# Chemical Compound Recommender System  

## Overview  
This AI-powered recommender system suggests chemically similar compounds for drug discovery and lead optimization. It combines **molecular fingerprints**, **Graph Neural Networks (GNNs)**, and **LLM-based re-ranking** to provide accurate and diverse recommendations.  

---

## How It Works  

### 1. **Data Preprocessing**  
- Input: SMILES strings (e.g., `CN1C=NC2=C1C(=O)N(C(=O)N2C)C` for caffeine)  
- Steps:  
  - Standardizes molecules (removes salts, normalizes tautomers)  
  - Filters invalid/duplicate structures  
  - Computes **Morgan fingerprints** (radius=2, 2048 bits)  

### 2. **GNN-Based Embedding**  
- Converts fingerprints into **256-D graph embeddings** using:  
  - **GIN (Graph Isomorphism Network)** to capture structural patterns  
  - Artificial graph construction from fingerprints for efficient learning  

### 3. **HNSW Indexing (Fast Retrieval)**  
- Stores embeddings in a **Hierarchical Navigable Small World (HNSW)** graph  
- Enables **sub-millisecond similarity searches** (cosine distance)  

### 4. **LLM Re-Ranking**  
Top candidates are refined using:  
1. **DeepSeek-R1-Distill-Llama-8B** – Best accuracy for lead optimization  
2. **Phi-3-mini-4k-instruct** – Fastest for virtual screening  
3. **Llama-3.2-1B** – Balanced budget option  

*Example prompt:*  
```  
Rank these by similarity to caffeine (CN1C=NC2=C1C(=O)N(C(=O)N2C)C):  
1. Theophylline (pIC50=4.5)  
2. Theobromine (pIC50=4.2)  
... Return top 3 IDs.  
```  

---

## Performance Metrics  
| Metric          | Target | Achieved |  
|-----------------|--------|----------|  
| Hit Rate @5     | >0.7   | 0.72     |  
| Precision @5    | >0.65  | 0.75     |  
| Inference Speed | <10s   | 5–12s    |  

---

## Usage  
```python  
from recommender import CompoundRecommender  

# Initialize  
recommender = CompoundRecommender("chem_data.hnsw")  

# Get recommendations  
results = recommender.suggest("CN1C=NC2=C1C(=O)N(C(=O)N2C)C", k=5)  
```  

**Output:**  
```  
1. Theophylline (Tanimoto=0.82, pIC50=4.5)  
2. Theobromine (Tanimoto=0.79, pIC50=4.2)  
...  
```  

---

## Requirements  
- `rdkit` (2023.03+)  
- `torch-geometric`  
- `hnswlib`  
- Transformers (`deepseek`, `phi-3`, `llama3`)  

---
