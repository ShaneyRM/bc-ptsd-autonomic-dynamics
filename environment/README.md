# Environment version references

These files record package versions from the local environments used during repository preparation. They are **inventories, not lockfiles or installation instructions**. `NerMI` and `psychological_monitoring` are author-controlled proprietary packages, not public dependencies; their listed versions are for identification only. Neither implementation is included in this repository. NerMI licensing or analysis services may be requested through [nermi.info](https://nermi.info/) or by emailing [srmcclafferty@gmail.com](mailto:srmcclafferty@gmail.com). Non-commercial SAI/PAI processing may be requested from the corresponding author. No private package source paths, credentials, or package code are included.

## R analysis environment

[`R-4.4.3-packages.txt`](R-4.4.3-packages.txt) records the R version and versions of the packages used by `src/Statistical_Analysis.Rmd`. The report may install missing packages from CRAN, and this inventory does not lock transitive dependencies or platform-specific binaries.

## Python environments

- [`python-updated-packages.txt`](python-updated-packages.txt): Python 3.13.2 environment containing the proprietary internal NerMI and `psychological_monitoring` packages, but not MNE.
- [`python-mne-env-packages.txt`](python-mne-env-packages.txt): Python 3.11.14 environment containing MNE, but not the proprietary internal packages NerMI or `psychological_monitoring`.

Neither environment alone contains all packages for the optional upstream EDF-to-feature workflow. Do not combine these version lists into a new environment without compatibility testing. The private packages are not available for public installation from this repository. The saved-data Figure 4 workflow does not require those feature-extraction packages.

For a fully reproducible software environment, create and validate a project-specific lockfile after the licensed package sources and a compatible Python version are available.
