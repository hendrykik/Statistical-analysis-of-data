# opis danych
Dane zostały pobrane 15 marca 2024 ze strony https://www.kaggle.com/datasets/schnell18/golang-github-repositories-and-gomod-of-all-vers/data (wymagane zalogowanie)

# licencja
https://cdla.dev/sharing-1-0/

# opis zawartości (w języku angielskim)


This is a update-to-date golang repositories on github with creation date before 2023-08-11. This dataset excludes toy project with stars below 10. The most distinct feature of this dataset is that it include the go.mod file for all published versions of each repository that use go module system. The go.mod files are packed in the gomod.parquet to save space and lend itself to analysis by big data tools.

# file commits-go-awesome.csv

Commit summary dataset as of 2023-09-05 for repositories listed in the go-awesome project.
Columns are as follows:

full_name: repository name in owner/repo format
branch: the branch where the commits come from, the default branch of repository
sha: commit id in sha1 format
author_name: name of author
author_date: date of the commit was made
verified: indicate if the commit is signed and verified
