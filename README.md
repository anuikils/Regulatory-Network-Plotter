# Regulatory-Network-Plotter
This repository contains a small R script that reads multiple TSV edge-lists (no header), builds one igraph object per TSV, computes a layout (from the first graph), and exports a comparable figure per input file (PNG + SVG). Node and edge colors / borders are assigned according to the mode flags and whether a node appears in the first column (node1). The script uses the exact color scheme and plotting parameters defined at the top of the code.

Usage:
You only need to download the script "Regulatory-Network-Plotter.R" from this repository. Once downloaded, it can be opened through RStudio. The script assumes that all the input files for the networks to be compared are located in the same folder (you will find in the rows an example of the .tsv format, "Tomato_Example.tsv", as well as example outputs in .png and .svg).

Before running the script, you must modify the line that specifies the directory of that folder. The outputs will be automatically saved in the working directory.

