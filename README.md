# mCherry-Nanobody-Fusion 

## Problem  
Breast cancers that overexpress the **human epidermal growth factor receptor 2 (HER2)** represent a particularly aggressive subtype and are associated with poor clinical outcomes. Detecting HER2 status is essential for diagnosis and treatment planning, since HER2-targeted therapies improve survival.  

Current clinical assays (immunohistochemistry and FISH) are effective but limited:  
- Require fixed samples  
- Are time-consuming  
- Rely on specialized reagents  
- Cannot be applied to live-cell monitoring  

What is needed is a **rapid, reliable, and live-cell compatible probe** that can identify HER2+ cells with high specificity and provide a bright fluorescent readout for both diagnostics and research.  

---

## Method  

We designed a panel of **mCherry–nanobody fusion proteins** that combine:  
- **mCherry**: a bright, photostable red fluorescent protein  
- **Anti-HER2 nanobody**: a small (~15 kDa), stable, and highly specific binder  

### Design Pipeline  
1. **Fusion Generation**  
   - Constructed six candidates by varying:  
     - Nanobody orientation (N- vs. C-terminal)  
     - Linker length ((G4S)1–3)  

2. **Structure Prediction & Scoring**  
   - Used **AlphaFold 3** by Google DeepMind to generate predicted 3D models.  
   - Extracted **per-residue confidence (pLDDT)** values and computed **domain-level scores**.  
   - Inspected structures for steric clash or linker intrusion.  

3. **RFdiffusion Integration**  
   - Used **RFdiffusion** to refine linker placement and explore orientation variants.  
   - Generated alternative backbone proposals to minimize steric hindrance.  

4. **pLDDT Extractor**  
   - Implemented a parser to extract pLDDT values from AlphaFold predictions.  
   - Produced **scores.csv** with mean and domain-level folding confidence.  

5. **Candidate Selection**  
   - Choose top-performing constructs with:  
     - Stable mCherry β-barrel  
     - Exposed, well-folded nanobody domain  
     - Mean pLDDT ≥ 80  

### Experimental Plan  
- Expression in *E. coli*  
- Purification via Ni-NTA affinity chromatography  
- Validation by **flow cytometry** and **fluorescence microscopy** (HER2+ vs. HER2– cells)  

---

## Results & Deliverables  

Computational modeling identified fusion proteins with **balanced structural stability** and high-confidence folding scores.  
- **Top candidate**: Maintains robust fluorescence with exposed nanobody binding interface.  
- **Flexible linker**: Prevents β-barrel intrusion and preserves binding accessibility.  

**Deliverables include:**  
- `candidates.fasta` – fusion sequences  
- `results/` – predicted PDBs and structural images  
- `scores.csv` – per-domain pLDDT scores  
- **Wet-lab SOP** – expression → Ni-NTA purification → flow cytometry  
- **Iteration plan** – linker/orientation swaps and alternative nanobody testing  

---

## Impact  

The mCherry–nanobody fusion provides a **fast, scalable, and live-cell compatible method** for identifying HER2+ cancer cells. Applications include:  
1. **Cancer diagnostics** – rapid identification of HER2+ cells by flow cytometry  
2. **Live-cell imaging** – tracking receptor localization and trafficking  
3. **Therapeutic monitoring** – real-time evaluation of HER2-targeted therapies  

By combining nanobody precision with mCherry brightness, this project introduces a **new class of fluorescent probes** that could accelerate both cancer research and translational diagnostics.  

---

## Repository Structure  


├── README.md                                               
│
├── data/
│   ├── AlphaFold inputs            # The 6 sequences + 3 regenerations we submitted to AlphaFold Server
│   └── RFdiffusion input pdb and candidates.zip   # Initial pdb files used as "backbone" of the RFdiffusion
│   
│  
│
└── scripts/                          
    ├── diffusion.ipynb                             # RFdiffsion notebook provided was used
    └── pLDDT_extractor_from_cif.ipynb              # Extraction program used to get the mean pLDDT
