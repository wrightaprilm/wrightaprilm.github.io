Title: PyRAD and TACC
Date: 2014-01-27 11:20

Category: Next-gen sequencing
Tags: bioinformatics
Slug: pyrad-and-tacc
Authors: April Wright
Summary: Making PyRAD work on TACC
#Running PyRAD on TACC

I needed to write this all out and put it somewhere, mostly so I don't forget it. Also so we can all stop whispering dark, apocryphal tales of memory limits in the halls.

I'm trying out the [PyRAD pipeline](http://dereneaton.com/software/pyrad/) for the next-gen data I'm currently working with. My colleagues and I are looking to assemble data matrices that can be used for [Structure](http://pritchardlab.stanford.edu/structure.html), phylogenetics and maybe species delimitation. We're working with _Eurycea_ [salamanders](http://www.amphibiaweb.org/cgi/amphib_query?where-genus=Eurycea&where-species=waterlooensis), which are contentious taxonomically.

To answer questions about their evolutionary history, we're using restriction site data. RADseq data is often very rich at the level of one or a few populations, but the number of recovered orthologous loci may taper off above the species level. Some of our divergences are potentially quite deep relative to many RADseq datasets, and PyRAD uses a clustering algorithm to identify homology among sequences. This should result in less data loss among different species, particularly among more distantly-related samples. PyRAD can also accomodate indels, which is unique among RADseq processing software.

#Getting the software

Developer [Deren Eaton]((http://dereneaton.com) has done a really nice job of making code available via his [GitHub](http://dereneaton.com) with prety much continual changelogging. So, log into TACC, and in your home, type:

```unix

git clone https://github.com/dereneaton/pyrad.git
```

To fetch the latest development version. Note: you can, of course, go to the [PyRAD site](http://dereneaton.com/software/pyrad/) and download a zip file of the sofware. But I'm lazy and would rather just clone it at the command line.

PyRAD will demultiplex the data and remove adapters and restriction recognition sites and adapters. But in order to do PyRAD's clustering, you will need [VSEARCH](https://github.com/torognes/vsearch). You can use USEARCH, but VSEARCH is much faster and more memory efficient. We have 300 samples, so this is important for us. In your home directory, type:

```unix
git clone https://github.com/torognes/vsearch.git
```

Change directories into the VSEARCH folder and type:

```UNIX
make -f Makefile 
```

to compile the software. 

So that's the ancillary software. 

PyRAD is controlled via a parameter file, params.txt. It looks like this:

```UNIX
==** parameter inputs for pyRAD version 3.0a  **==========================  affected step ==
/scratch/user/my_working_dir       ## 1. Working directory                                 (all)
/scratch/user/my_data/*.fastq.gz   ## 2. Loc. of non-demultiplexed files (if not line 16)  (s1)
/scratch/user/my_barcodes.txt      ## 3. Loc. of barcode file (if not line 16)             (s1)
/home1/user/vsearch/vsearch  ## 4. command (or path) to call vsearch (or usearch)    (s3,s6)
muscle                 ## 5. command (or path) to call muscle                  (s3,s7)
CATG,TGCA              ## 6. Restriction overhang (e.g., C|TGCAG -> TGCAG)     (s1,s2)
16                     ## 7. N processors (parallel)                           (all)
6                      ## 8. Mindepth: min coverage for a cluster              (s4,s5)
4                      ## 9. NQual: max # sites with qual < 20 (line 18)       (s2)
.8                     ## 10. Wclust: clustering threshold as a decimal         (s3,s6)
rad                    ## 11. Datatype: rad,gbs,ddrad,pairgbs,pairddrad,merge   (all)
4                      ## 12. MinCov: min samples in a final locus             (s7)
3                      ## 13. MaxSH: max inds with shared hetero site          (s7)
rad_tes                ## 14. Prefix name for final output (no spaces)         (s7)
==== optional params below this line ===================================  affected step ==
                       ## 15.opt.: select subset (prefix* only selector)            (s2-s7)
                       ## 16.opt.: add-on (outgroup) taxa (list or prefix*)         (s6,s7)
                       ## 17.opt.: exclude taxa (list or prefix*)                   (s7)
                       ## 18.opt.: loc. of de-multiplexed data                      (s2)
                       ## 19.opt.: maxM: N mismatches in barcodes (def= 1)          (s1)
                       ## 20.opt.: phred Qscore offset (def= 33)                    (s2)
                       ## 21.opt.: filter: def=0=NQual 1=NQual+adapters. 2=strict   (s2)
                       ## 22.opt.: a priori E,H (def= 0.001,0.01, if not estimated) (s5)
                       ## 23.opt.: maxN: max Ns in a cons seq (def=5)               (s5)
                       ## 24.opt.: maxH: max heterozyg. sites in cons seq (def=5)   (s5)
                       ## 25.opt.: ploidy: max alleles in cons seq (def=2;see docs) (s4,s5)
                       ## 26.opt.: maxSNPs: (def=100). Paired (def=100,100)         (s7)
                       ## 27.opt.: maxIndels: within-clust,across-clust (def. 3,99) (s3,s7)
                       ## 28.opt.: random number seed (def. 112233)              (s3,s6,s7)
                       ## 29.opt.: trim overhang left,right on final loci, def(0,0) (s7)
                       ## 30.opt.: output formats: p,n,a,s,v,u,t,m,k,g,* (see docs) (s7)
                       ## 31.opt.: call maj. consens if depth < stat. limit (def=0) (s5)
                       ## 32.opt.: keep trimmed reads (def=0). Enter min length.    (s2)
                       ## 33.opt.: max stack size (int), def= max(500,mean+2*SD)    (s3)
                       ## 34.opt.: minDerep: exclude dereps with <= N copies, def=1 (s3)
                       ## 35.opt.: use hierarchical clustering (def.=0, 1=yes)      (s6)
                       ## 36.opt.: repeat masking (def.=1='dust' method, 0=no)      (s3,s6)
                       ## 37.opt.: vsearch threads per job (def.=6; see docs)       (s3,s6)
==== optional: list group/clade assignments below this line (see docs) ==================

```

I'm not going to talk here about parameters, since parameter fitting is something we're working on now. Edit this file to your heart's content. Save it somewhere smart. 

Lastly, assemble your job control file (either qsub or slurm). Here is an example of a qsub file like the one I use:

```UNIX

#!/bin/bash
#$-A My_allocation                 #TACC allocation against which to charge your computation time.
#$ -V                              # Inherit submission environment 
#$ -cwd                            # Use current working directory 
#$ -N my_awesome_name              # Job name 
#$ -o $JOB_NAME.o$JOB_ID           # Name of the output file (eg. myMPI.oJobID) 
#$ -e $JOB_NAME.e$JOB_ID
#$ -pe 1way 24                    # Request 24 processors, at a rate of 24 proc/node (so 1 node) 
#$ -q largemem                    # Use 'normal' queue ('development' for testing, 'largemem' for lots-o-memory) 
#$ -l h_rt=12:00:00               # Run time (hh:mm:ss) 
#$ -M me@email.com                # Email 
#$ -m baes                        # Notifications at beginning and end of job


module load python
module load muscle

/home/user/pyRAD -p ./path/to/params.txt

```

I'll edit this with a slurm file once we've migrated to Stampede.

PyRAD is built with python, so we must load this in order to use PyRAD. PyRAD also requires MUSCLE to align within-individual stacks before estimating heterozygosity and sequencing error. TACC has this installed. We must also load this to use PyRAD.

Depending on your dataset size, you might need to use TACC's largemem node. With my number of samples, I needed the memory. If you do not, replace largemem with normal. Largemem charges against allocations more and the queue is often longer, so don't use it if not needed.

Stay tuned. We'll have more good stuff about PyRAD soon.


Special thanks to Edgardo Ortiz Valencia for useful insight USEARCH vs VSEARCH.

