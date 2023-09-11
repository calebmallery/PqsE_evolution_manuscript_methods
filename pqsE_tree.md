muscle -in pqsE_homolog.faa -out pqsE_homolog_aln.faa
trimal -in pqsE_homolog_aln.faa -out pqsE_homolog_aln_trm.faa -strictplus
iqtree -s pqsE_homolog_aln_trm.faa -m MFP
>Best-fit model according to BIC: WAG+F+G4
iqtree -s pqsE_homolog_aln_trm.faa -m WAG+F+G4 -bb 1000

#for the B.c/PA one:
saved result from burkdb as csv
searched for "," replaced with "\n". Then searched for "(^B)" and replaced with >\1. 
some have messy names so I searched for \s-\sAssembly\s and replaced with "_" and saved the file as .faa

Similar for pseudodb but: \s*\sassembly\s

#Now that our files are on the command line we want to make sure we have what we think we do:
grep ">" Pa_pqsE_orthologues.faa | wc -l
300
grep ">" Bc_pqsE_orthologues.faa | wc -l
462

combine the files 
cat pqsE_orthologues.faa B.c_pqsE_orthologues.faa > pqsE_orthologues.faa

check: grep ">" pqsE_orthologues.faa | wc -l
762

some headers still suck
sed -i 's/ /_/g' pqsE_orthologues.faa
sed -i 's/-/_/g' pqsE_orthologues.faa
sed -i 's/[.]/_/g' pqsE_orthologues.faa
sed -i 's/#/_/g' pqsE_orthologues.faa
sed -i 's/[/]/_/g' pqsE_orthologues.faa
sed -i 's/__/_/g' pqsE_orthologues.faa

muscle -in pqsE_orthologues.faa -out ortho_aln.faa
