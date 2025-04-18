This repository provides scripts for LDSC (Linkage Disequilibrium Score Regression) and MiXeR analysis to estimate heritability and genetic correlations from GWAS summary statistics. It includes files from the LDSC (MIT License) and MiXeR (MIT License) repositories, used with permission as per their licenses. Requirements: Ubuntu 18.04 and Python 3.6.8 for compatibility, along with dependencies listed in the README.
Munging GWAS Files
Before running LDSC, munge your GWAS summary statistics using munge_sumstats.py. Below is an example command to preprocess a GWAS file (e.g., smoking initiation data):
```bash
./munge_sumstats.py \
  --sumstats "/GSCAN_SmkInit_2022_GWAS_SUMMARY_STATS_EUR_without_UKB.txt" \
  --signed-sumstats BETA,0 \
  --snp RSID \
  --a1 EFFECT_ALLELE \
  --a2 OTHER_ALLELE \
  --p P \
  --N-col N \
  --merge-alleles "/mnt/d/bioinformatics_research/LDSC/w_hm3.snplist.txt" \
  --out "/smoking_initiation_munged"
```
  This generates a munged output file (e.g., smoking_initiation_munged.sumstats.gz) for downstream analysis.

  Step 2: Running Genetic Correlation Analysis
After munging, use ldsc.py to estimate genetic correlations between traits. The example below computes the genetic correlation between a munged GWAS file (e.g., cerebellum white matter volume) and another trait, using reference LD scores:
```bash
./ldsc.py \
  --rg /rh_volume_Cerebellum-White-Matter_munged.sumstats.gz \
  --ref-ld-chr /eur_w_ld_chr/ \
  --w-ld-chr /eur_w_ld_chr/ \
  --out /rh_volume_Cerebellum-White-Matter/results
  This command outputs results (e.g., genetic correlation estimates) to the specified directory (/rh_volume_Cerebellum-White-Matter/results).
```
  Notes
File Paths: Update paths (e.g., /GSCAN_SmkInit_2022_GWAS_SUMMARY_STATS_EUR_without_UKB.txt, /eur_w_ld_chr/) to match your directory structure.
Input Files: Ensure required files (e.g., w_hm3.snplist.txt, LD score files) are available.
Documentation: Refer to the LDSC documentation for additional options and troubleshooting.
