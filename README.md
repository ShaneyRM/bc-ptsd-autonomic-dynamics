# Analysis code: Autonomic Dynamics in Breast Cancer Patients with PTSD

**Study:** *Autonomic Dynamics in Breast Cancer Patients with PTSD Using Sympathetic and Parasympathetic Activity Indices and Emotional Dimensions*  
**Authors:** Francesca Cotardo, Shane R. McClafferty, Xinzhu Chai, Luca Ostacoli, Sara Carletto, and Bruce H. Friedman  
**Affiliation:** Department of Clinical and Biological Sciences, University of Turin, Italy

This repository contains analysis code for the study. Results and publication figures are omitted pending acceptance. It does not contain participant-level data or the clinical source spreadsheets.

## Citing this repository

Use the metadata in [`CITATION.cff`](CITATION.cff) when citing this software.

## License

This repository is licensed under the [PolyForm Noncommercial License 1.0.0](LICENSE). The license permits use for noncommercial purposes and includes only the patent license stated in its terms. Commercial use is not permitted under this license.

## Repository contents

| Path | Contents |
| --- | --- |
| [`src/Statistical_Analysis.Rmd`](src/Statistical_Analysis.Rmd) | R analysis code for SAI, PAI, NerMI valence, and motivation. |
| [`src/ECG_Processing.ipynb`](src/ECG_Processing.ipynb) | ECG processing record, SAI/PAI preparation, and a Figure 4 workflow from previously processed NerMI data. |

## Data and reproducibility

The required input data are not included. Use only data you are authorized to access, and keep identifiable or participant-level data and generated files out of public version control.

### R analyses

The R Markdown report expects these four files in one private input directory:

- `functional_cleaned_long.csv`
- `functional_cleaned_long_nermi.csv`
- `Participant data.xlsx`
- `Dataset for IES-R, STAI Y1 e 2, BDI.xlsx`

Install R and the `rmarkdown` package, set `BHI_INPUT_DIR` to the private input directory, then render `src/Statistical_Analysis.Rmd` from the repository root. For example, in PowerShell:

```powershell
Rscript -e "install.packages('rmarkdown')"
$env:BHI_INPUT_DIR = "D:\path\to\authorized\analysis-inputs"
Rscript -e "rmarkdown::render('src/Statistical_Analysis.Rmd')"
```

The report checks for and installs missing analysis packages from CRAN when run, so internet access may be required. The local R 4.4.3 package versions are recorded in [`environment/R-4.4.3-packages.txt`](environment/R-4.4.3-packages.txt). These are version references, not a lockfile; the report does not pin package versions. Rendering can create reports and analysis artifacts, so review generated files before adding them to version control.

### ECG and Figure 4 notebook

The notebook includes optional upstream EDF processing and a separate Figure 4 route that uses saved processed data. Set the `DATA_DIR` path in the setup cell to the authorized local study-data directory before using the upstream cells. For Figure 4 alone, set `PROJECT_DIR` and choose either the processed-file or combined-CSV source described in the notebook; the saved inputs must contain NerMI valence, motivation, and activation. The notebook is not required for the R analysis workflow.

The available local Python environments are documented in [`environment/`](environment/). They are **not a single complete environment**: `updated` contains the author-controlled, proprietary NerMI and SAI/PAI implementations but not MNE, while `mne-env` contains MNE but not those packages. Their version numbers in the inventory are identification only, not public install instructions. Thus, the complete EDF-to-feature workflow is not reproducible from either environment as currently installed. Figure 4 from saved data does not require running the upstream feature extraction. The implementations are not distributed in this repository; see [Method licensing and access](#method-licensing-and-access) for available analysis and licensing options. Output files are configured not to overwrite existing files.

## Analysis overview

**SAI/PAI phase summaries.** Phase-level median, area under the curve (AUC), peak, and slope features were used to describe baseline, script, and post-script recovery. Mixed-effects models included condition (EMDR vs. TAU), assessment (T0 vs. T1), phase, their interactions, and participant random intercepts.

**SAI/PAI change scores.** T1 - T0 changes were calculated for phase-level features. Reactivity and recovery represented baseline-to-script and script-to-recovery changes. Between-group comparisons used Welch two-sample t tests; associations with CAPS-5 and IES-R symptom changes used Spearman correlations. Broader feature associations were exploratory.

**Exploratory mLFPCA.** Multilevel functional principal component analysis was applied separately by phase and measure to characterize between-subject and visit-related trajectory variation. Screened components were explored in treatment-adjusted regressions. These analyses are hypothesis-generating.

Statistical results and figures are omitted pending acceptance.

## Method licensing and access

NerMI (valence, motivation, and activation) and SAI/PAI are distinct methods with different rights holders.

- **NerMI:** Owned by McClafferty Innovations, LLC; associated U.S. patent application **19/227,299** is unpublished. The implementation is not included in this repository. For background on the dynamic-architecture method and its initial validation, see the [associated article](https://doi.org/10.1111/psyp.70359) and the [Dynamic Architecture Experiment repository](https://github.com/ShaneyRM/dynamic-architecture-experiment). The experiment repository describes its collection and processing pipeline; it does not contain the code that estimates the article's models or implements the real-time monitoring system. To request NerMI licensing or analysis services, visit [nermi.info](https://nermi.info/) or email [srmcclafferty@gmail.com](mailto:srmcclafferty@gmail.com).
- **SAI/PAI:** The indices used here follow the SAI/PAI formulation described by Nardelli et al. (2023; see [reference](#references)). They are covered by U.S. Patent **11,075,009 B2**. The third-party implementation and the repository authors' own implementation are not released here; non-commercial processing may be requested from the authors. An online SAI/PAI calculator is available at [saipai-hrv.com](https://www.saipai-hrv.com/index.html). Its site states that uploads are not encrypted and files may remain on the server between reboots; **do not upload identifiable, confidential, or otherwise sensitive participant data.** Review the site's [disclaimer](https://www.saipai-hrv.com/disclaimer.txt) and the rights holder's terms before use.

The implementations of NerMI and SAI/PAI are not included in this repository. This repository is licensed under the terms in [`LICENSE`](LICENSE); those terms govern any patent license for the software they cover. Contact the respective rights holders for permissions to use implementations or services that are not included here.

## References

- Lin, W., Zou, J., Di, C., Rock, C. L., & Natarajan, L. (2024). Multilevel longitudinal functional principal component model. *Statistics in Medicine, 43*(25), 4781-4795. https://doi.org/10.1002/sim.10207
- McClafferty, S. R. (n.d.). *Dynamic Architecture Experiment* [Software repository]. GitHub. https://github.com/ShaneyRM/dynamic-architecture-experiment
- McClafferty, S. R., & Friedman, B. H. (2026). A Dynamic Architecture Linking Autonomic Activity to Emotional Dimensions: Real-Time Estimation From Photoplethysmography. *Psychophysiology, 63*(7). https://doi.org/10.1111/psyp.70359
- Nardelli, M., Citi, L., Barbieri, R., & Valenza, G. (2023). Characterization of autonomic states by complex sympathetic and parasympathetic dynamics. *Physiological Measurement, 44*(3), 035004. https://doi.org/10.1088/1361-6579/acbc07
