# FinalProject
This is the repository for my final project

The goal of this project is to examine the evolutionary timeline of the rabbit, and detemining its relationship to other pet animals. I will root the tree using the armadillo, something which diverged before mammals.

My workflow for the final project is as follows, scripts are designated with excessively large letters as github is hard

1. download full sequence data for each species used for tree generation

  -Rabbit genome
ftp://ftp.ensembl.org/pub/release-100/fasta/oryctolagus_cuniculus/pep/Oryctolagus_cuniculus.OryCun2.0.pep.all.fa.gz

-Guinea Pig genome 
ftp://ftp.ensembl.org/pub/release-99/fasta/cavia_porcellus/pep/Cavia_porcellus.Cavpor3.0.pep.all.fa.gz

-Mouse genome 
ftp://ftp.ensembl.org/pub/release-100/fasta/mus_musculus/pep/Mus_musculus.GRCm38.pep.all.fa.gz

-Dog genome
ftp://ftp.ensembl.org/pub/release-100/fasta/canis_lupus_familiaris/pep/Canis_lupus_familiaris.CanFam3.1.pep.all.fa.gz

-Cat genome
ftp://ftp.ensembl.org/pub/release-100/fasta/felis_catus/pep/Felis_catus.Felis_catus_9.0.pep.all.fa.gz 

-Gerbil genome
ftp://ftp.ensembl.org/pub/release-100/fasta/meriones_unguiculatus/pep/Meriones_unguiculatus.MunDraft-v1.0.pep.all.fa.gz

-Armadillo genome
ftp://ftp.ensembl.org/pub/release-100/fasta/dasypus_novemcinctus/pep/Dasypus_novemcinctus.Dasnov3.0.pep.all.fa.gz

# wget filename.fa.gz

2. Unwrapping files for access

# gzip -d filename.fa.gz

3. Pull desired sequence from FASTA file

# grep -A 1 "sonic" filename.fa > output filename.fa

4. Neaten up file headers

# awk '/^>/{print ">animal_" ++i; next}{print}' animal_sonic.fa > header_animal_sonic.fa  

5. Concatenate files into one input for Multiple Sequence Alignment

# cat filename_1 filename_2 filename_3... > output filename.fa

6. Multiple Sequence Alignment

# mafft --auto input.fa > output.fa

7. Tree assembly

# iqtree -s input.fa -m LG -bb 1000 -pre output

The tree is now viewable in FigTree

#NEXUS
begin trees;
	tree tree_1 = [&R] ((rabbit_1:0.03006,(((cat_1:0.003048,cat_2:0.175259)[&label=63]:0.011901,((dog_1:0.002587,dog_3:0.076947)[&label=51]:0.003137,dog_2:0.079193)[&label=72]:0.015421)[&label=92]:0.01686,((guinea_pig_1:2.0E-6,guinea_pig_2:2.0E-6)[&label=100]:0.036475,(gerbil_1:0.022585,mouse_1:0.031035)[&label=100]:0.042328)[&label=77]:0.0144)[&label=59]:0.006886):0.034014,armadillo_1:0.034014);
end;

