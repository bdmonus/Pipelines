#!/bin/bash

# ----------------SLURM Parameters----------------

#SBATCH -A strauss
#SBATCH -J q2_scikit_tax
#SBATCH -N 1
#SBATCH --time=300:00:00
#SBATCH --mem=90g				#TOTAL RAM PER TASK		
#SBATCH -n 32					#NUMBER OF CPUS PER TASK
#SBATCH -D /ufrc/strauss/antonio.castella/citrus/CRDF/time0/16S 	#PATH OF YOUR WORKING FOLDER
#SBATCH -o logs/q2_scikit_tax_taxa_%j.out	#PATH OF LOG FILE


date;hostname;pwd

################################################################################
#
# Assign taxonomy using a pre-trained scikit classifier version 0.19.1
# 
################################################################################

# ----------------Load Modules--------------------
module load qiime2/2018.8

# ----------------Housekeeping--------------------
cd features

# ----------------Commands------------------------


#qiime feature-classifier classify-sklearn \
#  --p-n-jobs -1 \
#  --i-reads rep-seqs.qza \
#  --o-classification taxonomy.qza \
#  --i-classifier  /ufrc/strauss/nevinsc/BSCjan19/16S2/SILVA_nb_99_V3-V4b.qza


qiime metadata tabulate \
  --m-input-file taxonomy.qza \
  --o-visualization taxonomy.qzv

#qiime taxa barplot \
#  --i-table table.qza \
#  --i-taxonomy taxonomy.qza \
#  --m-metadata-file /ufrc/strauss/antonio.castella/citrus/CRDF/time0/16S/features/Metadata.txt \
#  --o-visualization taxa-bar-plots.qzv

#Unload modules:
module unload qiime2/2018.8

date
