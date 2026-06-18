# Comparative Sequence Analysis of Plastic-Degrading Enzymes

**Author:** Justin Temporada  
**Institution:** University of Waterloo, Honours Biology (Bioinformatics Option)  
**Summer 2026**

---

## Background

Plastic waste is a major environmental problem, and one of the more interesting 
biological solutions involves bacteria that have evolved enzymes capable of 
breaking down plastics like PET. This project was directly inspired by Dadzie (2022), 
an MSc thesis proposal from the University of Waterloo on engineering *Pseudomonas 
putida* KT2440 to convert plastic waste into PHA, a biodegradable bioplastic. The 
thesis worked with four plastic-degrading genes and I wanted to understand those 
same enzymes computationally: how related are they, and what do they share at 
the sequence level?

---

## Enzymes

| Enzyme | Organism | Target | NCBI Accession |
|--------|----------|--------|----------------|
| PETase | *Ideonella sakaiensis* | PET | GAP38373.1 |
| MHETase | *Ideonella sakaiensis* | PET intermediate (MHET) | GAP38911.1 |
| Cut1 (Cutinase) | *Thermobifida fusca* | PET | AAZ54921.1 |
| Tcur1278 (Lipase) | *Thermonospora curvata* | PET | CDN67545.1 |
| alkB | *Pseudomonas oleovorans* | Polyethylene | CAB51047.1 |

---

## Pipeline

| Step | Script | Description |
|------|--------|-------------|
| 1 | `fetch_sequences.py` | Download protein sequences from NCBI |
| 2 | `align_sequences.py` | Multiple sequence alignment with MUSCLE v5.3 |
| 3 | `distance_matrix.py` | Pairwise % identity between all enzymes |
| 4 | `phylo_tree.R` | Neighbor-Joining phylogenetic tree |
| 5 | `conserved_regions.R` | Identify conserved positions across PET hydrolases |
| 6 | `pymol_visualization.pml` | Visualize catalytic triad (Ser160, Asp206, His237) on PETase crystal structure (PDB: 6EQE) |

---

## Findings

PETase shares ~47.4% sequence identity with Cut1 and ~45.3% with Tcur1278, while 
Cut1 and Tcur1278 share 53.7% with each other. This places all three firmly within 
the same serine hydrolase family. MHETase, despite coming from the same organism 
as PETase, shares less than 10% identity with the PET hydrolases and sits on its 
own branch entirely. It is a structurally different enzyme that works alongside 
PETase in *I. sakaiensis* to complete PET degradation. alkB is the most distant 
of all at 4-12% identity, consistent with it being a completely different class 
of enzyme targeting polyethylene through oxidation rather than ester hydrolysis.

The phylogenetic tree confirms these relationships. PETase, Cut1, and Tcur1278 
cluster together on the same branch with strong bootstrap support, suggesting 
PETase shares evolutionary ancestry with cutinase and lipase-type serine hydrolases. 
This is interesting because Cut1 and Tcur1278 naturally break down cutin and 
plant polyesters respectively, not PET, yet they are PETase's closest relatives. 
This supports the idea that PETase evolved from a pre-existing serine hydrolase 
that gradually adapted to degrade PET. alkB and MHETase both sit on long isolated 
branches, consistent with their distinct biochemical mechanisms.

Conservation analysis identified 113 fully conserved positions out of 775 total 
alignment positions (14.6%) across PETase, Cut1, and Tcur1278. Among these are 
the catalytic triad residues Ser160, Asp206, and His237 (PETase PDB numbering), 
confirmed conserved across all three PET hydrolases and responsible for ester bond 
hydrolysis. Structural visualization in PyMOL confirmed all three residues cluster 
together in the active site of the PETase crystal structure (PDB: 6EQE).

---

## Results

| Figure | Description |
|--------|-------------|
| `results/phylogenetic_tree.png` | Rooted NJ tree with bootstrap support |
| `results/conservation_profile.png` | Conservation profile across alignment |
| `results/petase_structure.png` | PETase crystal structure with catalytic triad highlighted |

---

## How to Reproduce

```bash
pip install biopython
```

Download the appropriate MUSCLE executable for your OS from 
https://github.com/rcedgar/muscle/releases and place it in 
the project root. This repo includes the Windows 64-bit version.

```bash
python scripts/fetch_sequences.py
python scripts/align_sequences.py
python scripts/distance_matrix.py
```

In RStudio (set working directory to project root first):
```r
source("scripts/phylo_tree.R")
source("scripts/conserved_regions.R")
```

In PyMOL (open the application and run in the command line): 
@scripts/pymol_visualization.pml

---

## Tools
Python 3.13, Biopython, MUSCLE v5.3, R 4.3, ape, ggplot2, PyMOL

---

## Reference
Dadzie, E. (2022). *Biocatalytic Production of PHA Using Petrochemical Plastics 
as Feedstock*. MSc Thesis Proposal, University of Waterloo. Supervisor: Dr. Trevor Charles.