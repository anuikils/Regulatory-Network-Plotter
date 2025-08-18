# Regulatory-Network-Plotter
Short summary
This repository contains a small R script that reads multiple TSV edge-lists (no header), builds one igraph object per TSV, computes a layout (from the first graph), and exports a comparable figure per input file (PNG + SVG). Node and edge colors / borders are assigned according to the mode flags and whether a node appears in the first column (node1). The script uses the exact color scheme and plotting parameters defined at the top of the code.
Requirements

R (recommended ≥ 4.0) and the following packages:

install.packages(c("igraph", "readr", "dplyr"))
The script uses base R svg() for vector export (no svglite dependency).

Files & layout

Place your input files in one folder_path:
For example: 
└─ input_folder/    # put all .tsv files here
   ├─ sample1.tsv
   ├─ sample2.tsv
   └─ ...
Input format (TSV)

This script expects TSV files without headers and with at least four columns (tab-separated):
col1   col2   col3        col4
node1  node2  node1_mode  node2_mode

col1 (node1) — source node name (string)

col2 (node2) — target node name (string)

col3 (node1_mode) — mode for node1: "1" means ON; any other value (e.g., "2") means OFF

col4 (node2_mode) — mode for node2: same rule as above

Example

A	B	1	2
B	C	2	1
D	A	1	1

Node name matching is exact (case-sensitive). If your files have headers, either remove them or adapt the script to read headers.

Color & styling logic (exact values)

The script defines color constants at the top. These are the exact hex values used:

color_ON = #C6ACD3 — fill color for ON nodes

color_OFF = #A3195B — fill color for OFF nodes

default_first_col_color = #7ee3bd — fill for nodes that appear in node1

default_first_col_border_on = #2ab081 — border for first-col ON nodes

default_border_on = #865bb3 — border for ON nodes (non-first-col)

default_border_off = #6A6C70 — border for OFF nodes

Node fill rule

If node appears in node1 → default_first_col_color.

Else if node mode == "1" → color_ON.

Else → color_OFF.
(Remember: any value other than "1" is considered OFF — e.g., "2".)

Node border rule

If firstCol AND mode == "1" → default_first_col_border_on.

Else if mode == "1" → default_border_on.

Else → default_border_off.

Edge color rule

If source is ON and target is ON:

If the target appears somewhere as a node1 in the file → "red" (ON→ON in edge).

Else → dark gray #6A6C70 (ON→ON out edge).

Otherwise (ON-OFF or OFF-OFF) → "gray".

Edge width logic

#6A6C70 edges → width 3

red edges → width 2

other edges → width 1

The plotting function scales some values for SVG export for visibility (see the script for the exact multipliers).

Quick start — run instructions

Put your .tsv files into the folder referenced by folder_path in the script (default in the script: "carpeta prueba/").

Open Regulatory-Network-Plotter.R in R or RStudio and run it, or run it from the R console:

Script parameters you may want to change

folder_path — path to folder containing TSV files.

set.seed(22) — change for different layout randomness (layout_with_fr is seeded).

layout_with_fr — you can replace with layout_with_kk or another igraph layout if desired.

Color constants at the top — change hex values to customize colors.

show_labels = TRUE/FALSE in plot_network() — disable labels for large networks.

Output files

For each input name.tsv, the script writes:

name.png — raster image (2000 × 1500 px, 300 DPI), transparent background.

name.svg — vector image (SVG). The script scales arrow/width/frame values for the SVG export to keep visibility.

Files are saved in the working directory (or you can edit the file_prefix path inside plot_network() to store them elsewhere).
