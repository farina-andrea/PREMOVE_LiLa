# PREMOVE – Diachronic Dataset of Annotated Preverbed Motion Verbs in Ancient Greek and Latin

**Version:** 1.0  
**Authors/Contributors:** Andrea Farina, Marco Passarotti, Francesco Mambrini, Giovanni Moretti, Matteo Pellegrini  
**Date:** 2025  

---

## Overview

PREMOVE is a **diachronic, manually annotated dataset** of preverbed motion verbs in Ancient Greek and Latin. It focuses on the combination of **eight core motion verbs** with **sixteen preverbs per language**, capturing detailed **morphological, syntactic, semantic, geographical, and textual metadata** for each occurrence.  
The dataset facilitates research in **historical linguistics, corpus linguistics, computational lexicography, and digital humanities**, with links to external resources such as **Perseus, PHI, WHG**, and the **LiLa Knowledge Base**.

If you use PREMOVE in your research, please cite:

**Farina, Andrea**, 2025. PREMOVE – A diachronic dataset of Ancient Greek and Latin annotated PREverbed MOtion VErbs. Literary and Linguistic Data Service. http://hdl.handle.net/20.500.14106/2579

---

## Key Features

- **Lexical Coverage:** Eight motion verbs × sixteen preverbs in both Latin and Ancient Greek.  
- **Manual Annotation:** Semantic, morphological, and syntactic layers.  
- **Linked Data:** Tokens are linked to their **WordNet synsets**, corpus **passage URIs**, and other references.  
- **RDF/TTL Outputs:** Data exported in **Turtle format** using the **FRAC ontology** for linguistic attestations.  
- **Provenance:** Each attestation is linked to corpus passages and dataset metadata.  

---

## File Structure

| File | Description |
|------|-------------|
| `PREMOVE_WN_3.1.csv` | Original list of WordNet 3.1 token URIs. |
| `tokens_and_passages_URIs.csv` | Token–passage mappings retrieved from LiLa. |
| `tokens_and_passages_URIs_filtered.csv` | Filtered passages, excluding SentenceLayer passages. |
| `token_passage_synset_URIs.csv` | Merged CSV linking token URIs to synsets and passages. |
| `all_token_URIs.csv` | Complete CSV of all token annotations, including nouns. |
| `all_token_URIs.ttl` | RDF/Turtle file of token attestations, linking tokens to synsets and passages. |
| `PREMOVE_dataset_metadata.ttl` | Turtle file containing dataset metadata (creator, description, publisher, citation). |
| `prototype_circular_nodes_with_uris.png` | Example network visualization of a lexical concept and its attestations. |

---

## Data Generation Workflow

1. **Token Retrieval from WordNet**
    - Tokens in `PREMOVE_WN_3.1.csv` are queried against the **LiLa Knowledge Base** via **SPARQL** to retrieve corresponding passage URIs.

2. **Filtering and Merging**
    - Passages from the SentenceLayer are removed to focus on higher-level attestations.
    - Merged with original token–synset mappings to produce `token_passage_synset_URIs.csv`.

3. **RDF Graph Construction**
    - Lexical concepts, attestations, and references are modeled using the **FRAC ontology**.
    - Example visualizations can be generated using **NetworkX** and **Matplotlib**.

4. **Turtle (.ttl) Generation**
    - Tokens with valid synsets and passages are exported in Turtle format (`all_token_URIs.ttl`) for integration into **semantic web** and **linked data platforms**.
    - Dataset-level metadata is provided in `PREMOVE_dataset_metadata.ttl`.

---

## Ontologies and Standards Used

- **FRAC (Framework for Attested Content):** `http://www.w3.org/ns/lemon/frac#`  
- **OntoLex Lemon Model:** `http://www.w3.org/ns/lemon/ontolex#`  
- **RDF and Dublin Core Terms:** For provenance and bibliographic metadata.  
- **SPARQL:** Retrieval of tokens and passage URIs from LiLa Knowledge Base.  

---

## Usage Example

```python
import pandas as pd

# Load merged token–synset–passage CSV
df = pd.read_csv("token_passage_synset_URIs.csv")

# Inspect first few rows
print(df.head())

# Filter tokens linked to a specific Latin WordNet synset
latin_synset = "http://lila-erc.eu/data/lexicalResources/LatinWordNet/id/LexicalConcept/02013448-v"
subset = df[df["synset_URIs"] == latin_synset]
print(subset)
