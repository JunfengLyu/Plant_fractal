# Plant Fractal

This repository provides demo pipelines for analyzing and modeling fractal-like structures in plants.

The example script `vein_demo.py` processes a leaf venation image, extracts the binary vein mask and skeleton, estimates fractal and lacunarity metrics, reconstructs the skeleton network, and visualizes graph-theoretic properties such as degree distribution and hierarchy depth.

The script `L-system.py` demonstrates how a deterministic Lindenmayer system (L-system) can generate plant-like branching patterns through iterative string rewriting and turtle-graphics interpretation. It also illustrates how iteration depth and turning angle affect the resulting morphology.

---

## Repository structure

```text
Plant_fractal/
├── vein_demo.py
├── vein_demo/
│   ├── vein.png
│   ├── 00_original.png
│   ├── 01_raw_binary_mask.png
│   ├── 02_skeleton.png
│   ├── 03_porosity_hull.png
│   ├── 04_box_counting_dimension.png
│   ├── 05_lacunarity_curve.png
│   ├── 06_network_nodes_by_degree.png
│   ├── 07_degree_distribution.png
│   ├── 08_hierarchy_depth.png
│   ├── 09_hierarchy_depth_distribution.png
│   ├── summary_metrics.csv
│   ├── node_metrics.csv
│   ├── edge_metrics.csv
│   ├── box_counting_data.csv
│   ├── lacunarity_data.csv
│   └── degree_distribution.csv
├── L-system.py
├── L-system_images/
│   ├── 图_L-system转角参数比较.png
│   └── 图_L-system迭代过程.png
└── README.md
```

---

## Usage

### Leaf venation analysis

Run the venation demo script from the project root:

```bash
python vein_demo.py
```

The script reads the input image:

```text
vein_demo/vein.png
```

and saves all output figures and tables into:

```text
vein_demo/
```

### L-system plant generation

Run the L-system script from the project root:

```bash
python L-system.py
```

By default, the script uses the `classic` preset and saves the generated plant as `l_system_plant.svg`. It uses only the Python standard library. Presets, iteration depth, turning angle, and output path can be customized from the command line:

```bash
python L-system.py --preset bushy --iterations 5 --angle 30 --output bushy.svg
```

Available presets are `classic`, `bushy`, and `binary`. The iteration number must be between 1 and 9.

The L-system model begins with an axiom and repeatedly applies production rules in parallel. The resulting command string is interpreted using turtle graphics: `F` draws a branch segment, `+` and `-` change the heading, and `[` and `]` save and restore branching states.

---

## Image processing workflow

The raw venation image is converted into a binary vein mask and then skeletonized into a one-pixel-wide network representation. This workflow preserves the major topological structure of the venation network while simplifying the structure for graph analysis.

<p align="center">
  <img src="vein_demo/00_original.png" width="30%">
  <img src="vein_demo/01_raw_binary_mask.png" width="30%">
  <img src="vein_demo/02_skeleton.png" width="30%">
</p>

---

## Fractal and lacunarity analysis

The box-counting dimension estimates the spatial filling complexity of the venation network across scales. Lacunarity measures the heterogeneity of the pore or gap distribution across different window sizes.

<p align="center">
  <img src="vein_demo/04_box_counting_dimension.png" width="45%">
  <img src="vein_demo/05_lacunarity_curve.png" width="45%">
</p>

---

## Network topology analysis

After skeletonization, the vein network is represented as a graph composed of nodes and edges. Nodes are colored by graph degree to show local branching complexity. The degree distribution summarizes the abundance of endpoints, simple branch points, and higher-order junctions.

<p align="center">
  <img src="vein_demo/06_network_nodes_by_degree.png" width="45%">
  <img src="vein_demo/07_degree_distribution.png" width="45%">
</p>

---

## Hierarchical organization

The hierarchy depth is estimated by breadth-first search from an approximate basal or petiole node. This provides a simple topological measure of how the network expands from the primary vein toward higher-order peripheral branches.

<p align="center">
  <img src="vein_demo/08_hierarchy_depth.png" width="45%">
  <img src="vein_demo/09_hierarchy_depth_distribution.png" width="45%">
</p>

---

## L-system plant morphology

L-systems provide a concise, rule-based description of plant development. Starting from a simple initial string, repeated rewriting produces increasingly complex branching structures. The iteration number controls the developmental depth and structural complexity of the generated plant.

<p align="center">
  <img src="L-system_images/图_L-system迭代过程.png" width="75%">
</p>

The turning angle is a key morphological parameter in turtle-graphics interpretation. Changing this angle while keeping the production rules fixed alters branch orientation, crown width, compactness, and the overall appearance of the simulated plant.

<p align="center">
  <img src="L-system_images/图_L-system转角参数比较.png" width="75%">
</p>

---

## Main methods

The current demos include:

- CLAHE contrast enhancement
- Otsu thresholding
- Skeletonization
- Box-counting fractal dimension
- Lacunarity analysis
- Skeleton-to-graph reconstruction
- Degree distribution
- Connected component analysis
- Cycle rank / loop number
- BFS-based hierarchy depth
- Deterministic L-system string rewriting
- Stack-based turtle-graphics interpretation
- Iteration-depth and turning-angle comparison

---

## Citation notes

- Otsu, N. (1979). A threshold selection method from gray-level histograms.
- Zhang, T. Y., & Suen, C. Y. (1984). A fast parallel algorithm for thinning digital patterns.
- Falconer, K. J. (2003). *Fractal geometry: Mathematical foundations and applications*.
- Plotnick, R. E., Gardner, R. H., Hargrove, W. W., Prestegaard, K., & Perlmutter, M. (1996). Lacunarity analysis.
- Hagberg, A. A., Schult, D. A., & Swart, P. J. (2008). Exploring network structure, dynamics, and function using NetworkX.
- Lindenmayer, A. (1968). Mathematical models for cellular interactions in development.
- Prusinkiewicz, P., & Lindenmayer, A. (1990). *The algorithmic beauty of plants*.
