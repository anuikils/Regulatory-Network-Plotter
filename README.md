# Regulatory-Network-Plotter
This repository contains a small R script that reads multiple TSV edge-lists (no header), builds one igraph object per TSV, computes a layout (from the first graph), and exports a comparable figure per input file (PNG + SVG). Node and edge colors / borders are assigned according to the mode flags and whether a node appears in the first column (node1). The script uses the exact color scheme and plotting parameters defined at the top of the code.

