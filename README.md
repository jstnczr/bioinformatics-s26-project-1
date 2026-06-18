# Comparative Sequence Analysis of Plastic-Degrading Enzymes

**Author:** Justin Temporada  
**Institution:** University of Waterloo, Honours Biology (Bioinformatics Option)  
**Summer 2026**

---

## Background

Plastic pollution remains one of the most pressing environmental challenges of our 
time. Recent research has identified microorganisms capable of enzymatically 
degrading petrochemical plastics — offering a biological route to plastic waste 
management. This project was inspired by Dadzie (2022), an MSc thesis proposal 
from the University of Waterloo that explored engineering *Pseudomonas putida* 
KT2440 to use PET and polyethylene waste as feedstock for producing PHA, a 
biodegradable bioplastic. Before engineering better enzymes, it helps to understand 
how they are evolutionarily related and which regions of their sequences are 
functionally conserved. This project takes a computational approach to those 
same enzymes.

---

## Enzymes

| Enzyme | Organism | Target | NCBI Accession |
|--------|----------|--------|----------------|
| PETase | *Ideonella sakaiensis* | PET | GAP38373.1 |
| MHETase | *Ideonella sakaiensis* | PET intermediate | GAP38911.1 |
| Cut1 (Cutinase) | *Thermobifida fusca* | PET | ADV92528.1 |
| Tcur1278 (Lipase) | *Thermonospora curvata* | PET | CDN67545.1 |
| alkB | *Pseudomonas oleovorans* | Polyethylene | CAB51047.1 |

---

## Pipeline

| Step | Script | Description |
|------|--------|-------------|
| 1 | `fetch_sequences.py` | Download sequences from NCBI |
| 2 | `align_sequences.py` | Align with MUSCLE v5.3 |
| 3 | `distance_matrix.py` | Pairwise % identity between all enzymes |
| 4 | `phylo_tree.R` | Neighbor-Joining phylogenetic tree |
| 5 | `conserved_regions.R` | Identify conserved positions across PET hydrolases |
| 6 | `pymol_visualization.pml` | Visualize conserved residues on PETase structure *(in progress)* |

---

## Findings

The distance matrix revealed that PETase shares ~45.6% sequence identity with both 
Cut1 and Tcur1278, while Cut1 and Tcur1278 share 53.9% with each other — placing 
all three firmly within the same serine hydrolase family. MHETase, despite coming 
from the same organism as PETase, shares only 9-10% identity with the PET 
hydrolases, indicating it is structurally unrelated. alkB sits even further apart 
at 4-11% identity, consistent with its role as an alkane hydroxylase rather than 
an ester hydrolase.

The phylogenetic tree confirms these