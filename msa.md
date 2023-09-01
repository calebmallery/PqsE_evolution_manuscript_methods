#ggmsa
if (!requireNamespace("devtools", quietly=TRUE))
    install.packages("devtools")
devtools::install_github("YuLab-SMU/ggmsa")
library(ggmsa)
luxR_sequence <- "/Users/calebmallery/Desktop/pqse_evol_manuscript/luxR_homologues.txt"
ggmsa(luxR_sequence, start = 1, end = 40, char_width = 0.5, seq_name = TRUE) + geom_seqlogo() + geom_msaBar()

#ggtree + msa
library(Biostrings)
x <- readAAStringSet(protein_sequences)
d <- as.dist(stringDist(x, method = "hamming")/width(x)[1])
library(ape)
tree <- bionj(d)
library(ggtree)
p <- ggtree(tree) + geom_tiplab()
data = tidy_msa(x, 164, 213)
p + geom_facet(geom = geom_msa, data = data,  panel = 'msa',
               font = "DroidSansMono", color = "Chemistry_AA", char_width = 0.5) +
    xlim_tree(1)
