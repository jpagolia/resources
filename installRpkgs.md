# How to install infercnv as an example of installing R packages in the terminal

# Need to load libgit2 to properly install infercnv dependency gert
`module load libgit2`

# Installing R packages in the terminal using BiocManager
`module load R/4.3.3`\
`R`
# Load BiocManager
`if (!requireNamespace("BiocManager", quietly = TRUE))`\
 `   install.packages("BiocManager", lib="/home/jpagolia/James_R_433")`

# Set the library path
`.libPaths("/home/jpagolia/James_R_433")`

# Install a Bioconductor package (e.g., GenomicRanges)
`BiocManager::install("infercnv", lib="/home/jpagolia/James_R_433")`

`q()`
