# Stanford CS230 Project

More documentaton is coming soon to this README. The following is brief but hopefully still illustrative:

## Project Goal
The goal of this project is to explore the use of autoencoders for metagenome binning. Specifically, the goal is to explore how assembled contigs can be clustered (i.e. "binned") in a lower dimensional encoding space and how these bins map back to the source genomes that those contigs represent. I am building upon important and recent work published by Nissen et all describing VAMB which uses a variational autoencoder to improve binning. In extention of those efforts, I am exploring the use of the Beta-VAE and disentanglement with the hypothesis that making the encoding space dimensions less correlated will improve the clustering resolution of contigs as they are assigned to bins. This can have many uses especially when a metagenome sample may represent source genomes that are similar to one another.

## Repository Components
As with most life scienses projects, there are MANY steps in data pre- and post- processig that have to be accomplished in order for model experimentation to work. These include the acqusition or creation of source data in the form of short read metagenome shotgun sequencing data for which the input source genomes are known. This is followed by assembly into contigs and quantitation fo contig abundance as well as--at least in many standard cases--calculation of tetranucleotide frequencies all in order to make input data ready for modeling.

The model itself is, of course, a required component both as a baseline for which I will be using VAMB and as a replacement model for tweaking. 

Finally, model outputs are encoding vectors which have to be clustered and those clusters have to be scored in terms of the precision/contamination and recall/completeness in their ability to capture the souce genomes.

This repository contains several important notebooks detailing each aspect of this process. The figure below provides an overall schematic of model training and its related pre- and post-processing steps. The numbered elements in the schematic correspond to the numbered subtitles for corresponding notebooks below:

![alt text](annotated_Stanford_schematic.png "Model Workflow to Include Pre- and Post-Processing")

### 1. Acquiring Data
Thos notebook walks through the process of simulating short read metagenome shotgun sequencing datasets from a collection of input source genomes and both describes and demonstrates how to use the CAMISIM package to simulate our input data.

### 2. Preparing Data
This notebook describes and demonstrates the process of taking short read input data such as that produced in the previous notebook and creating the assembled contigs along with abundance and tetranucleotide frequency data. Note that there are multiple ways that one could do this but I use minimap2 and certain utilities from the VAMB package which I have more or less "hotwired" into the repository.

### 3. Running VAMB
This notebook described the baseline process of running the VAMB model as described by Nissen et al. and is incorporated from their repository.

### 4. Beta VAE
This repository contains the encoder model specific to this project which is build to fit into the workflow in place of VAMB while still being able to rely on some of VAMB's data ingestion utilizies. This is where we define and tweak the beta parameter.

### 5. Benchmarking Bins
This notebook contains the steps to take bins clustered in the encoding space and to score their completeness and contamination which is analogous to recall and precision. This also contains the code to generate tSNE plots in the encoding space to better visualize this specific step and the impact of the beta parameter on clustering here.