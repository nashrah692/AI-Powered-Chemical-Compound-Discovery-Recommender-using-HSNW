# AI-Powered-Chemical-Compound-Discovery-Recommender-using-HSNW

Dataset for project was downloaded from "KAGGLE"

Dataset Name: "SMILES_Big_Data_Set.csv"

Main Goal of the Project: "A system that suggests novel chemical compounds for drug development, material science, or industrial applications based on existing molecular structures."

Basic Roadmap:
1. Data Collection – Gather molecular data from PubChem, ChEMBL, or DrugBank and extract structures in SMILES format.
2. Preprocessing – Standardize compounds, remove duplicates, and generate molecular fingerprints using RDKit.
3. Vectorization & Indexing – Convert fingerprints into embeddings with GNNs and store in HNSW/Faiss for fast similarity search.
4. Recommendation Module – Retrieve similar compounds based on structure, properties, and synthesis feasibility.
5. Evaluation & Optimization – Validate using Tanimoto similarity, recall@k, and precision, refining with experimental data.

This project is divided into three Deliverables (overview):
- Deliverable 01: Data Preprocessing, Embeddings, HNSW, etc.
- Deliverable 02: Tuning of LLMs based on dataset and with HNSW.
- Deliverable 03: Tuning of LLMs with RAG based technique.
