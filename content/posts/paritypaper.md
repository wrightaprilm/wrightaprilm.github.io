Title: Reproducibility and Cutting Yourself Some Slack
Date: 2015-4-3 11:58
Category: science, evolution, squamates
Slug: parity-paper
Authors: April Wright

I recently submitted a paper I'd like to talk about a little bit. We did a reanalysis of a previously-published dataset from Pyron and Burbrink [2014](http://onlinelibrary.wiley.com/doi/10.1111/ele.12168/full). This paper assembled a really impressive dataset of squamate parity modes and performed some comparative methods analysis with them. We wanted to look at how phylogenetic uncertainty and model assumptions affect the conclusion reached. 

Today, I'm writing a little about the reproducibility of the paper.

#Motivation

*In Writing This:* A few people have pointed out that open science has kind of an image problem. And I fully agree. From reading Twitter about open science, you'd get the impression that if you don't use the latest tools and your pipeline isn't perfect, and you can't just type 'make' and have the full paper spit back at you from the command line, then you aren't doing it right. 

Not true, and that's a really alienating message. There's a very tech-y modality to a lot of the discussions of open science, but in my experience, a lot of people are quietly and contentedly practicing openness and are _really happy_ to be nice to new practitioners. I came up in a [lab](http://www.zo.utexas.edu/faculty/antisense/) where it was expected that you provide everything a person would need to reproduce the paper, even if the journal makes no provisions for that. Lab alums have gone on to release free and open source software prodigiously. Many are involved with generating [permissively-licensed](http://treethinkers.org) and [fully archived](https://molevol.mbl.edu/index.php/Main_Page) teaching materials and tutorials. It never occurred to me to do science another way, really. You can do good work, and open work, without breaking your back. This post is fundamentally about *striking the right balance for you.*

*In using the tools I used:* I had never written a Makefile before and wanted to try. That's all really. I had read about using them for [reproducibility](https://ropensci.org/blog/2014/06/09/reproducibility/), and they seemed useful. It's not *full* reproducibility, in the sense that you type make and are left with a figure, but you type make, get some numbers and use an iPython notebook to plot them. As we simplified the paper, the Makefiles got simpler, so the ones attached to the final paper might actually be basic enough for an intro user to grasp. And I'm all about zero-entry resources.

The [iPython Notebook](http://ipython.org/notebook.html) is a really great tool to make code easy-to-use for collaborators and novices. Since I was working with my labmate, Katie Lyons, who was a total novice at computation, I wanted to make sure the scripts were easy for her to follow. In an iPython notebook, code is held in a cell. The user executes the cell and sees the output. This is especially nice for graphics -  you run your code and your graph shows up, in the window, in full color. You can make very easy-to-see, easy-to-use interactive documents in this way.

#What we did

The paper had three main analysis:
1) Running [BiSSE](http://www.zoology.ubc.ca/~fitzjohn/diversitree.docs/) on four time-scaled phylogenetic trees to look at the effect of topology and branch length on the conclusions reached.

2) Running BiSSE on each of these trees with a variety of parameters to look at the effects of the exact model settings on the conclusion reached.

3) Using [PAUP](http://paup.csit.fsu.edu/) to count changes on the tree.


There were also little ancillariy analyses that we did, for example, looking at Robinson-Foulds distances between trees. These aren't the main thrust of the paper and are provided as iPython notebooks.

##Goal One: Run BiSSE on a few trees

Easy enough. We made trees using Examl and garli. The estimations for these trees are quite long - about a week - so we didn't include this step in any of the makefiles. I'm sure I could have beat my head against a wall figuring out a solution to the long estimation problem, but ... well, that really didn't seem worth it. The configuration files for tree-building software can be found in [our materials](http://wrightaprilm.github.io/ParityPaper/) under PhylogenyMaking. 

Then, we time-scale the trees. Pyron and Burbink used [treePL](https://github.com/blackrim/treePL) for this and since we're reproducing their work, we did too. TreePL is kind of finicky about where it compiles. I found that using the Linux instructions in a Vagrant box with Ubuntu 12 is the easiest way to do this. 

If you don't want to bother with these two long steps, the trees are in the Trees directory of the repository.

You can run BiSSE in a couple ways, from my repository. The easiest is to open a terminal, change directories into the repository and type 'make'. This will output for you results of BiSSE's parameter fitting as csv files and newick strings of the trees with the marginal likelihoods of ancestral states written to the nodes. You can then visualize these trees in FigTree or your preferred tree-viewing software.

##Goal Two: Parameter Sampling

Pyron and Burbrink used a sampling parameter we weren't sure we understood the function of. So we did an exercise in which we sampled many values of this parameter and made a heatmap to look at how this changed the probability of the ancestor of all squamates being viviparous. 

If you type 'make -f Makefileheat', this analysis will run on your computer. However, it makes a lot of replicates and takes a long time. I wouldn't actually do it. You can find my heatmap data in the Data directory, and the interactive heatmapping script in the iPython notebooks. This script illustrates well what I meant about iPython notebooks being really nice for graphics earlier.

##Goal Three

We just provided the PAUP file for this. Donezo.


#How I feel about it

This paper was a massive effort. I didn't anticipate how big of an undertaking it would be just to do the research. But I was strongly motivated by pedagogy - a new student in my lab wanted to learn computation, and she really took ownership of this project. She stepped up, and that made it easy for me to step up on a non-dissetation project in my last year of grad school while pregnant.  See her post in the coming days about learning by doing.

About the reproducibility ... I intended to do more. But, right now, I have a paper in review that I'm massively proud of. You can reproduce it. Katie learned a lot. I learned some skills I wanted (make, mostly) and made some resources I think will be helpful for novice users. I'm not a martyr to reproducibility: I'm going to do the best job that I can on it and go home at the end of the day. And that's what I'd like readers, esecially novice readers to take away: your project doesn't need to be perfectly, fully reproducible to be useful. Do your best. Learn something new. Don't get bogged down in the fear that the Twitterverse will chuckle at your puny attempt at a pipeline.

Do good enough. I did. I deserve a beer. Maybe next month.


 
