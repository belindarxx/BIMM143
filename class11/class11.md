Class 11: Structural Bioinformatics
================

## The PDB database for biomolecular structural data

Download a CSV file from the PDB site (“Analyze” -\> “PDB Statistics” \>
“by Experimental Method and Molecular Type”)

> Q1: Determine the percentage of PFB structures solved by X-ray and
> Electron Microscopy.

``` r
# Read CSV
data <- read.csv("Data Export Summary.csv")
data
```

    ##   Experimental.Method Proteins Nucleic.Acids Protein.NA.Complex Other
    ## 1               X-Ray   131278          2059               6759     8
    ## 2                 NMR    11235          1303                261     8
    ## 3 Electron Microscopy     2899            32                999     0
    ## 4               Other      280             4                  6    13
    ## 5        Multi Method      144             5                  2     1
    ##    Total
    ## 1 140104
    ## 2  12807
    ## 3   3930
    ## 4    303
    ## 5    152

Total number of entries

``` r
sum(data$Total)
```

    ## [1] 157296

Proportion of entries from each method

``` r
round((data$Total/sum(data$Total)) * 100, 2)
```

    ## [1] 89.07  8.14  2.50  0.19  0.10

Vast majority of protein is done by X-ray: 89% Electron Microscopy is
only 2.49%

> Determine what proportion of structures are protein?

Proportion that are protein

``` r
round (sum(data$Proteins) / sum(data$Total) * 100 , 2)
```

    ## [1] 92.71

## HIV-Pr structure analysis

Here we will read the 1HSG PDB structure and select the protein
component and write out a new **protein-only** PDB format file. We then
do the same for the ligand (i.e. known drug molecule) creating a
**ligand-only** PDB file.

``` r
library(bio3d)
# R package: biological sutructure analysis
pdb<- read.pdb("1hsg.pdb")
pdb
```

    ## 
    ##  Call:  read.pdb(file = "1hsg.pdb")
    ## 
    ##    Total Models#: 1
    ##      Total Atoms#: 1686,  XYZs#: 5058  Chains#: 2  (values: A B)
    ## 
    ##      Protein Atoms#: 1514  (residues/Calpha atoms#: 198)
    ##      Nucleic acid Atoms#: 0  (residues/phosphate atoms#: 0)
    ## 
    ##      Non-protein/nucleic Atoms#: 172  (residues: 128)
    ##      Non-protein/nucleic resid values: [ HOH (127), MK1 (1) ]
    ## 
    ##    Protein sequence:
    ##       PQITLWQRPLVTIKIGGQLKEALLDTGADDTVLEEMSLPGRWKPKMIGGIGGFIKVRQYD
    ##       QILIEICGHKAIGTVLVGPTPVNIIGRNLLTQIGCTLNFPQITLWQRPLVTIKIGGQLKE
    ##       ALLDTGADDTVLEEMSLPGRWKPKMIGGIGGFIKVRQYDQILIEICGHKAIGTVLVGPTP
    ##       VNIIGRNLLTQIGCTLNF
    ## 
    ## + attr: atom, xyz, seqres, helix, sheet,
    ##         calpha, remark, call

``` r
#read.pdb()
#atom.select()
#write.pdb()
#trim.pdb()
```

``` r
ligand <- atom.select(pdb, "ligand", value=TRUE)
write.pdb(ligand, file="1hsg_ligand.pdb")
# only give the 1hsg 里的 ligand 里的protein, only give you MK1
```

> Q2: Type HIV in the PDB website search box on the home page and
> determine how many HIV-1 protease structures are in the current PDB?

L ColorId 4 resid25 newcar chain protein Pdw Name not protein and not
water
