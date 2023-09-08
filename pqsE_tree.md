muscle -in pqsE_homolog.faa -out pqsE_homolog_aln.faa
trimal -in pqsE_homolog_aln.faa -out pqsE_homolog_aln_trm.faa -strictplus
iqtree -s pqsE_homolog_aln_trm.faa -m MFP
>Best-fit model according to BIC: WAG+F+G4
iqtree -s pqsE_homolog_aln_trm.faa -m WAG+F+G4 -bb 1000
