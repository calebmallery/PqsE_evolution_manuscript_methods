#ggmsa
if (!requireNamespace("devtools", quietly=TRUE))
    install.packages("devtools")
devtools::install_github("YuLab-SMU/ggmsa")
library(ggmsa)
luxR_sequence <- "/Users/calebmallery/Desktop/pqse_evol_manuscript/luxR_homologues.txt"
ggmsa(luxR_sequence, start = 1, end = 40, char_width = 0.5, seq_name = TRUE) + geom_seqlogo() + geom_msaBar()

#ggtree + msa
library(Biostrings)
library(ape)
library(ggtree)
protein_sequences <- "/Users/calebmallery/Desktop/pqse_evol_manuscript/luxR_homologues.txt"
x <- readAAStringSet(protein_sequences)
d <- as.dist(stringDist(x, method = "hamming")/width(x)[1])
tree <- bionj(d)
p <- ggtree(tree ) + geom_tiplab()

data = tidy_msa(x, 180, 208)
p + geom_facet(geom = geom_msa, data = data,  panel = 'msa', font = NULL, color = "Chemistry_AA") + 
    geom_facet(geom = ggmsa:::geom_logo, data = data,  panel = 'msa', color = "Chemistry_AA", adaptive = T) + 
      xlim_tree(1)
