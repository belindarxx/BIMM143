Class 12: Structural Bioinformatics II
================
Belinda Xue
11/7/2019

## Prep for docking

WE weant to produce a protein-only PDB file and a drug only PFB file.

Workbook LAB 12 1.1-1.2

``` r
library(bio3d)

# download the PDB file, will show on the right side bar
get.pdb("1hsg")
```

    ## Warning in get.pdb("1hsg"): ./1hsg.pdb exists. Skipping download

    ## [1] "./1hsg.pdb"

``` r
pdb <- read.pdb("1hsg.pdb")
protein <- atom.select(pdb, "protein", value=TRUE)
write.pdb(protein,file="1hsg_protein.pdb")
```

and for the ligand

``` r
ligand <- atom.select(pdb,"ligand", value=TRUE)
write.pdb(ligand, file="1hsg_ligand.pdb")
# make sure we have no protein in the ligand
```

LAB 12 Section 2.3

``` r
library(bio3d)
res <- read.pdb("all.pdbqt", multi=TRUE)
write.pdb(res, "results.pdb")
```

``` r
# res <- read.pdb("all.pdbqt", multi=TRUE)
ori <- read.pdb("ligand.pdbqt")
rmsd(ori,res)
```

    ##  [1]  0.590 11.163 10.531  4.364 11.040  3.682  5.741  3.864  5.442 10.920
    ## [11]  4.318  6.249 11.084  8.929

result.pdb ran in VMD, shows 14 frames–\> meaning total 14 frames of
docking and the first one is the lowest energy one (more preferred one)

Section 3

``` r
library(bio3d)
pdb <- read.pdb("1HEL")
```

    ##   Note: Accessing on-line PDB file

``` r
modes <- nma(pdb)
```

    ##  Building Hessian...     Done in 0.025 seconds.
    ##  Diagonalizing Hessian...    Done in 0.114 seconds.

``` r
plot(modes, sse=pdb)
```

![](class12_files/figure-gfm/unnamed-chunk-6-1.png)<!-- -->

``` r
# visualize NMA results
mktrj(modes,mode=7, file="nma_7.pdb")
```
