if (!requireNamespace("devtools", quietly=TRUE))
    install.packages("devtools")
devtools::install_github("YuLab-SMU/ggmsa")
library(ggmsa)
luxR_sequence <- "/Users/calebmallery/Desktop/pqse_evol_manuscript/luxR_homologues.txt"
ggmsa(luxR_sequence, start = 1, end = 40, char_width = 0.5, seq_name = TRUE) + geom_seqlogo() + geom_msaBar()
