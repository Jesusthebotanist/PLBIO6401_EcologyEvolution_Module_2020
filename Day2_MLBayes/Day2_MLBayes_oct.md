# Model Based Phylogenetics on the Linux server
___
## Remote Login
First we will need to log into the server. Refer to Day1 worksheet on how to do this. Remember your user name is your netid, the server is the IP address of the computer and your password is your first name, capital first letter plus 6410 (except for Han let me know if you forgot). 

As a short reminder, Windows user will need to open Putty or Mobaxterm but Mac user can simply open terminal and ssh
```bash
ssh
```

## Update project folder with git
First everyone needs to change directory to the project file. When you first login to the server you will be put in the "username" folder. This is analogous to when you turn on your computer you go to your Desktop. Typing 'cd' with out any argument will take you to the "username" folder immediately. Once there cd to the class folder. 
```bash
cd 
cd PLBIO6401_EcologyEvolution_Module_2020
```

The next thing we are going to do is update our folder. We've added the new material for Day2 as well as made a slight adjustment to the Day 1 lecture. We do this using git up. 
```bash
git pull origin master PLBIO6401_EcologyEvolution_Module_2020
ls
```

Now that we have updated our file, we can see there is a new folder 'Day2_MLBayes'. This folder is empty because there is no new material here. Lets make two directories for our Likelihood and Bayesian analysis. 
```bash
mkdir Day2_MLBayes
mkdir Day2_MLBayes/ML
mkdir Day2_MLBayes/Bayes
```

## Maximum Likelihood with RAxML
RAxML is one of the most commonly used Maximum likelihood inference programs. While it is the program we will use,  in the past recent years there have been a number of new Likelihood programs including IQ-Tree, GARLi, FAST ML, and others. Certain programs are more common in certain fields, (IQ-Tree in viral work and RAxML in phylogenetic). If you ever use phylogenetics in your own research, make sure you look into these various programs.  

We will used the aligned fasta file we generated in Day 1. Our first step is to make a copy of this file into both our ML folder.
```bash
cp Day1_LinuxAlignmentParsimony/My_first_Parsimony_Analysis/ruhf_32_by_5000_aligned.fas \
/ML
```

Again we have RAxML preinstalled, to run it simply type 'raxmlHPC'. Unlike TNT which opens up a scripter and you type commands, many Linux programs have 'arguments' denoted by a dash '-' which can be be include in the terminal line when you run the program. The dash '-' is sometimes called a flag. The argument are different for different programs but one commonly shared one is the -h flag which pull up a help menu. Let try this out with RAxML 
```bash
raxmlHPC -h
```

As you can see RAxML has quite a number of different options. Often times there is a pdf manual where it is easier to read these options. You can find the [RAxML manual here](sco.h-its.org/exelixis/resource/download/NewManual.pdf). We do not need to specify all argument in order to run a program, in our analysis we will specify the following. 

* -s The input sequence file name
* -m The substitution model
* -o The outgroups
* -p A random parsimony seed, this is for reproducibility purposes
* -n The output file name
```bash
raxmlHPC \
-s ruhf_32_by_5000_aligned.fas \
-m GTRGAMMA \
-o Pedinomonas_minor \
-p $RANDOM \
-n ruhf_32_by_5000.phy
```



```bash
raxmlHPC -s ruhf_32_by_5000.phy -m GTRGAMMA -o Pedinomonas_minor -p $RANDOM -n

32_outgroup
```
## MrBayes

```bash
cp /Day1_LinuxAlignmentParsimony/My_first_Parsimony_Analysis/ruhf_32_by_5000_aligned.fas /
/ML
```

```bash
mb
```

## Visualize 

# Model Based Phylogenetics on CIPRES
___
1. Make an account on [CIPRES](https://www.phylo.org/).
2. Log in (you may not have too I forget)
3. First thing is you are going to download a local copied of the **aligned** ruhf_32_by_5000_aligned.fas using Cyberduck
4. On CIPRES go to "Create New Folder"
5. Under "Label" give this project a name, "PLDay2" and click "Save"
6. On the left hand side your folder should appear with two subfolder, "Data" and "Tasks"

## Make a CIPRES Account

## RAxML

## MrBayes

## Visualize 

## A note

# Homework
# About This Doucment
This document was written in markdown and knitted into a PDF with Pandoc, using the following code. 
```bash
pandoc Day2_MLBayes_oct.md\
-f gfm \
-t latex \
--toc \
-V toc-title:"Table of Contents" \
-V linkcolor:blue \
-M title="Day 2: Maximum Likelihood and Baysien Methods" \
-M author="Jesus Martinez-Gomez" \
-M date="October 19th, 2020" \
-M abstrac="In today's worksheet we will analyze the data sheet we analyzed in Day1 using a Maximum Likelihood and Bayesian approach using the programs RAxML and MrBayes. We will do these two ways, the first will be on the serve similar to day one. The second way will be using the online CIPRES Science Gateway . CIPRES is an amazing resource for phylogenetic. Essentially, it is a super computer that has a number of phylogenetic programs pre-installed. Instead of accessing through linux it has an easy to use GUI. Practically speaking, if you are interested"
--extract-media ./images \
--highlight-style tango \
-o Day1_Worksheet_LinuxAlignmentParsimony_Oct2020.pdf
```
