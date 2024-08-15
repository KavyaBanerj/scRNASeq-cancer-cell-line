## Key Scientific Question (KSQ)

**How would you explore the use of the following FDA-approved antibody therapies in additional cancers using available scRNA-seq data from cancer cell lines?**

- **Trastuzumab**: Targets HER2 and is used in the treatment of HER2-positive breast and gastric cancers.
- **Bevacizumab**: Targets VEGF and is used for a variety of cancers, including colorectal, lung, glioblastoma, breast, liver, and kidney cancer.

## Background

### 1. **Cancer Cell Lines**

Cancer cell lines are populations of cancer cells that have been cultured in the laboratory (in vivo) and can proliferate indefinitely under controlled conditions. These cell lines are derived from the tumors of cancer patients and are used extensively in cancer research and drug development due to their ability to provide a consistent, cost-effective, reproducible, and unlimited source of biological material for high-throughput experiments (Mirabelli et al., 2019).

Cancer cell lines can differ significantly from the tumors they are derived from. Cell lines generally have more genomic alterations than primary tumors, partly due to the selection pressures and adaptations during immortalization and culturing. The lack of a natural tumor environment, particularly the microenvironmental interactions and cell type diversity present in actual tumors, may cause further differences (Sinha et al., 2021). While they are invaluable for certain types of studies, they may not fully capture the complexity and heterogeneity of actual tumors. Studies should be complemented by models such as patient-derived xenografts and organoids to understand tumor-microenvironment interactions.

### 2. **Single-cell RNA Sequencing (scRNA-seq)**

Single-cell RNA sequencing (scRNA-seq) allows for the capture of the transcriptome (mRNA) at the individual cell level. Unlike conventional bulk RNA-seq, which aggregates gene expression data across a multitude of cells, scRNA-seq offers cell-specific resolution on molecular processes.

**Use Cases (Chang et al., 2023):**
- **Identifying Drug Targets**: scRNA-seq can help in understanding the expression patterns of various cell types within a tumor, aiding in identifying potential drug targets for specific cell populations, including those that are rare or resistant to existing treatments, thereby aiding in the development of personalized cancer therapeutics.
- **Monitoring Treatment Response**: scRNA-seq can be used to observe how different cell types within a tumor respond to treatment, potentially helping to overcome drug resistance.

### 3. **Treatments and Their Targets**

- **Treatment: Trastuzumab -> Target: HER2**
  - **HER2 (Human Epidermal Growth Factor Receptor 2)**: A protein and receptor, member of the epidermal growth factor receptor (EGFR) family, that promotes cell growth and differentiation. When HER2 is overexpressed, it leads to uncontrolled cell growth and division, contributing to the development and progression of certain aggressive cancers, primarily breast cancer and certain types of gastric and ovarian cancers. HER2-positive cancers are characterized by rapid growth and a higher likelihood of recurrence.
  - **Pathway Activation**: Typically results from gene amplification, leading to overexpression of the HER2 protein on the cell surface. This overexpression can cause continuous activation of downstream signaling pathways that promote cell proliferation and survival.
  - **Trastuzumab**: By binding to HER2, trastuzumab inhibits the proliferation of cancer cells that depend on this receptor for growth, through internalization and downregulation of HER2 (Roviello et al., 2021).
  - **Resistance Mechanisms**: Mutations in the HER2 receptor can prevent trastuzumab from binding effectively. Cancer cells may activate other growth factor receptors or downstream signaling pathways (e.g., PI3K/AKT pathway) to bypass the blocked HER2 signaling. Some cancer cells may downregulate or lose HER2 expression over time, making them less susceptible to trastuzumab (Roviello et al., 2021).

- **Treatment: Bevacizumab -> Target: VEGF**
  - **VEGF (Vascular Endothelial Growth Factor)**: VEGF is a signal protein that stimulates the formation of blood vessels (angiogenesis). VEGF binds to its receptors (primarily VEGFR-2) on the surface of endothelial cells, promoting their proliferation and new vessel formation. Tumors hijack this process to ensure an adequate blood supply, facilitating their growth and metastasis (Kieran et al., 2012). VEGF is overexpressed in a variety of cancers, including colorectal, lung, kidney, and glioblastoma.
  - **Pathway Activation**: Often activated by hypoxic conditions within the tumor microenvironment. Tumor cells release VEGF in response to low oxygen levels, binding to VEGF receptors on endothelial cells, triggering angiogenesis (Liu et al., 2023).
  - **Bevacizumab**: By inhibiting VEGF, bevacizumab reduces the blood supply to tumors, thereby inhibiting their growth and spread.
  - **Resistance Mechanisms**: Tumors may activate alternative angiogenic factors (e.g., FGF, PDGF) to continue blood vessel formation despite VEGF inhibition. Some tumors may produce higher levels of VEGF to overcome the inhibitory effects of bevacizumab. Changes in the tumor microenvironment, such as increased pericyte coverage of blood vessels, can make angiogenesis less dependent on VEGF signaling.

## Flip the KSQ

1. From the scRNA-seq data from cancer cell lines, if they express HER2 and VEGF-A, can the data be inferred to understand the molecular mechanisms for tumor-targeting or alternative mechanisms for drug resistance? What are the downstream effects on the pathways?
2. Can we identify subpopulations of cancer cells fit for these antibodies?
3. If we have scRNA-seq data from experiments where cell lines were treated with the specified antibodies or otherwise untreated, can we address the efficacy on untreated cell lines?

## Reference Data

This project will use the data from Kinker et al., 2020, available [here](https://www.nature.com/articles/s41588-020-00726-6).  
Data availability: Can be downloaded from [Broad Institute's SCP portal here](https://singlecell.broadinstitute.org/single_cell/study/SCP542/pan-cancer-cell-line-heterogeneity).

### Background

The paper focuses on understanding cellular heterogeneity and plasticity within human tumors, which are crucial for grasping disease progression and treatment resistance. The study aimed to clarify the mechanisms and functional significance of intratumor heterogeneity (ITH), hypothesizing that a substantial part of ITH in malignant cells is due to intrinsic cellular plasticity, independent of the tumor microenvironment. By profiling numerous cancer cell lines from the Cancer Cell Line Encyclopedia (CCLE) collection, the study sought to map the landscape of cellular diversity and identify recurring programs of heterogeneity using scRNA-seq.

The study identified 12 recurrent heterogeneity programs (RHPs), including 2 related to the cell cycle and 10 others associated with diverse biological processes. Notably, 9 of these RHPs closely mirrored heterogeneity programs observed within tumors, suggesting their retention even without a native microenvironment. The additional 10 RHPs were either independent of cell cycle status or predominantly expressed by non-cycling cells. Importantly, each RHP was detected across at least eight different cell lines and from four different pools, underscoring their robustness. The authors argue that the significance of these RHPs stems from their recurrence, as they may influence critical cancer phenotypes like drug resistance and metastasis. 

### Questions to Address

- **How did the authors handle the potential caveat of co-culturing cell lines before profiling by scRNA-seq? Why do you think that caveat was or was not adequately addressed?**

  The study included a control experiment where six cell lines were either co-cultured or combined immediately before profiling for a direct comparison to evaluate the effects of co-culturing. Their findings indicated that while co-culturing had a modest impact on average gene expression, the patterns of heterogeneity within each cell line remained highly consistent across both co-cultured and non-co-cultured conditions based on the pairwise correlations on the NMF programs (Fig. S1C–F).

  In terms of whether this caveat was adequately addressed, the study conducts a controlled and adequate analysis of the scope of the study. However, the modest effects observed could still raise concerns about the potential for co-culturing to influence specific cellular behaviors or interactions if this dataset is used to study cell-cell interactions, which can lead to discrete subpopulations within the co-cultures.

- **The authors identified discrete subpopulations of cells within a subset of individual cell lines (Fig. 2A-B). What might be the reason why some cell lines have these discrete subpopulations while others do not?**

  The study found that discrete clusters were typically cell line specific (Fig. 2B). Only 11% of the cell lines exhibited discrete clusters, suggesting that many cell lines may show homogenous expression patterns. However, differences in experimental conditions, such as the methods used for cell culture and profiling (Strating et al., 2023), as well as inherent biological differences among cell lines, could also play a role in the presence or absence of discrete subpopulations.

- **What are Recurrent Heterogeneous Programs (RHPs) and how were they defined?**

  Recurrent Heterogeneous Programs (RHPs) are clusters of gene expression programs that vary across multiple cell lines. Specifically, an RHP is a set of genes that appeared in at least 25% of the programs within a specific cluster. These were identified by comparing expression programs derived from two methods: DBSCAN and Non-negative Matrix Factorization (NMF).

- **How do the identified RHPs relate to in vivo programs of heterogeneity in tumors, and what evidence supports this relationship?**

  Out of the 12 RHPs identified, 9 were found to be highly similar to programs of heterogeneity present in tumors. The overlap of signature genes between in vitro RHPs and in vivo programs was statistically significant, with FDR-adjusted p-value < 10⁻⁹ (Fig. 4A). The RHPs were characterized by functional enrichment analyses; many of the genes associated with RHPs correspond to known biological processes observed in tumors, such as stress responses and epithelial-mesenchymal transition (EMT) (Fig. 3).

## References

- Mirabelli, P., Coppola, L., & Salvatore, M. (2019). Cancer Cell Lines Are Useful Model Systems for Medical Research. *Cancers, 11*(8), 1098. [https://doi.org/10.3390/cancers11081098](https://doi.org/10.3390/cancers11081098)
- Sinha, R., Luna, A., Schultz, N., & Sander, C. (2021). A pan-cancer survey of cell line tumor similarity by feature-weighted molecular profiles. *Cell Reports Methods, 1*(2), 100039. [https://doi.org/10.1016/j.crmeth.2021.100039](https://doi.org/10.1016/j.crmeth.2021.100039)
- Chang, X., Zheng, Y., & Xu, K. (2023). Single-Cell RNA Sequencing: Technological Progress and Biomedical Application in Cancer Research. *Molecular Biotechnology, 66*(1497–1519). [https://doi.org/10.1007/s12033-023-00777-0](https://doi.org/10.1007/s12033-023-00777-0)
- Roviello, G., Aprile, G., D’Angelo, A., et al. (2021). Human epidermal growth factor receptor 2 (HER2) in advanced gastric cancer: where do we stand? *Gastric Cancer, 24*(765–779). [https://doi.org/10.1007/s10120-021-01182-9](https://doi.org/10.1007/s10120-021-01182-9)
- Kieran, M. W., Kalluri, R., & Cho, Y. J. (2012). The VEGF pathway in cancer and disease: responses, resistance, and the path forward. *Cold Spring Harbor Perspectives in Medicine, 2*(12), a006593. [https://doi.org/10.1101/cshperspect.a006593](https://doi.org/10.1101/cshperspect.a006593)
- Liu, Z. L., Chen, H. H., Zheng, L. L., et al. (2023). Angiogenic signaling pathways and anti-angiogenic therapy for cancer. *Signal Transduction and Targeted Therapy, 8*(198). [https://doi.org/10.1038/s41392-023-01460-1](https://doi.org/10.1038/s41392-023-01460-1)
- Kinker, G. S., Greenwald, A. C., Tal, R., et al. (2020). Pan-cancer single-cell RNA-seq identifies recurring programs of cellular heterogeneity. *Nature Genetics, 52*(1208–1218). [https://doi.org/10.1038/s41588-020-00726-6](https://doi.org/10.1038/s41588-020-00726-6)
- Strating, E., Verhagen, M. P., Wensink, E., et al. (2023). Co-cultures of colon cancer cells and cancer-associated fibroblasts recapitulate the aggressive features of mesenchymal-like colon cancer. *Frontiers in Immunology, 14*, 1053920. [https://doi.org/10.3389/fimmu.2023.1053920](https://doi.org/10.3389/fimmu.2023.1053920)
