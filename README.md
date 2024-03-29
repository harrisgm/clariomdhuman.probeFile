# clariomdhuman.probeFile
Contains annotated probe-level information for the MTA-1_0 (ClariomD mouse) microarray.  Used by the GCSscore R package for differential gene expression analysis.

# Description
===================

The `clariomdhuman.probeFile` package is an AnnotationForge-generated package containing the probe sequence information for MTA-1_0 (ClariomD mouse) array.  The package contains a `data.frame` containing the necessary probe-level information to run the `GCSscore` differential expression on the following Affymetrix/Thermo-Fisher cchip type:  

ClariomD Human microarray

All probe-level information in this file was pulled from the platform design (pd) annotation package (`pd.clariom.d.human`) on Bioconductor: https://bioconductor.org/packages/release/data/annotation/html/pd.clariom.d.human.html

This probe-level package was created using the `AnnotationForge` package.  The `AnnotationForge` package required the `getProbeDataAffy` function to be modified to correctly read in the `probeFile` file for newer Affymetrix array types.  This modified function was saved as `getProbeDataMTA`.  The customized functions from the `AnnotationForge` package can be found the following github repository: https://github.com/harrisgm/GCSscore-probeFile-functions

Additionally, the compression scheme of the `rda` file was set to `xz` with a compression level of 9.  This level of compression was necessary to keep the `rda` beneath 100Mb.  

The only column that is not directly from the platform design (pd) packages is the `GC.Count` column was generated by running the following commands on the full probe sequences that are pulled from the platform design packages (found in the `XXXpFBuilder.R` functions in the `GCSscore-probeFile-functions` repository:

```
chip.pmfeature[,GC.count := str_count(sequence, "G|C")]
```

The full probe `sequence` column was then removed and replaced just the `GC.count` information for each probe.  The full probe `sequence` column was removed to reduce the resulting packag sizes to under 100Mb.

Installation
------------

`clariomdhuman.probeFile` is an package that is in the process being uploaded to the BioConductor repository. Until it is uploaded to Bioconductor, the recommended way to install it is to load `R` and ensure that all dependencies are install prior to installation.
```

Dependencies from Bioconductor (run commands in Rstudio/R.app):

```r
if (!requireNamespace("BiocManager", quietly = TRUE))
    install.packages("BiocManager")
    
BiocManager::install("AnnotationDbi")
```

Once the dependencies are installed, build and install the `clariomdhuman.probeFile` package from source.

Contact
-------

Guy Harris, M.S.
<harrisgm@vcu.edu>

Michael F. Miles, M.D., Ph.D.
<Michael.Miles@vcuhealth.org>

[1]: https://github.com/harrisgm/GCSscore
