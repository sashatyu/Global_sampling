This is a project providing the code and input data examples for various global sampling options from the following publication: Tyukavina et al. (2025) "Practical global sampling methods for estimating area and map accuracy of land cover and change" [https://doi.org/10.1016/j.rse.2025.114714](https://doi.org/10.1016/j.rse.2025.114714). For a detailed description of the study please refer to the publicaiton.

For instructions on how to install Anaconda and run Jupyter notebooks on PC [please refer to this guide](https://docs.google.com/document/d/197kGYTGDyz5te9KebEPLCPXVmrubweAzFACW24Qelqc/edit?usp=sharing).

Python 3 code implementing equations from the Appendix (numbering is consistent with sections of Appendix)
* A.1.1 Equal probability sampling.ipynb
* A.1.2 Unequal probability sampling - proportional to unit area.ipynb
* B.1 Regression estimator - simple random sampling.ipynb
* B.2 Regression estimator - stratified sampling.ipynb
* C Continous point sampling.ipynb

**Examples of input data:**

***Sampling design information***
[Number of appendix]Strata_info.txt (for Appendices A.1.1, A.1.2, B.2 and C)

   Columns: 
   * "Stratum": Stratum ID (1-N);
   * (N/A for C, not required for A.1.2) "Count": total number of units (pixels, polygons) in each stratum;
   * (optional for B.2) "Area": Stratum area;
   * (for B.2 only) "Xh": stratum-specific mean of the values of auxiliary class (calculated accross all units in the stratum).
 
   Section B.1 requires the following parameters specified directly in the code:
	* "N": total number of units in the sampling region (population);
	* "X": population mean of the values of auxiliary class (calculated accross all units in the sampling region);
	* (optional, might be needed to convert estimates to % of total area)"Atot" - area of the sampling region (e.g. in km²).

***Input data for each sample unit***
[Number of appendix]Sample_data.txt (for Appendices A.1.1, A.1.2, B.1, B.2 and C)

   Columns for Appendix A:
   * "Stratum": stratum ID, 1 - nstrata;
   * "Pixarea": area of each sample unit (in units that are desired for area reporting);
   * "Map"(for accuracy assessment only): proportion of target class from the map (0-1) for each sample unit;
   * "Reference": proportion of target class from reference sample classification for each sample unit; allowed values are from -1 to 1 for area estimation, and from 0 to 1 for map accuracy assessment;
   * (optional)"RefType": type labels, if the are of target class needs to be estimated separately for multiple sub-types;
   * (optional)"Correct": proportion of sample unit (0-1), which is correctly mapped. This column is necessary for maps with more than two classes. For map with two classes it is computed in the function "estimate_OA_two_classes" directly from "Map" and "Reference" columns.

   Columns for Appendix B:
   * (for B.2 only)"Stratum": Stratum ID (1-N);
   * "yi": area of the target class in sample unit i,derived from sample interpretation (reference classification); should be in the same units as stratum Area and Atot;
   * "xi": value of the auxiliary class for sample unit (e.g. area of land cover class from existing wall-to-wall map or mean spectral index value within sample unit); ould be in any units matching X.

   Columns for Appendix C:
   * "Stratum": stratum ID, 1 - nstrata;
   * "Reference": proportion of target class from reference sample classification for each sample unit; allowed values are from -1 to 1 for area estimation, and from 0 to 1 for map accuracy assessment;
   * (optional)"RefType": type labels, if the are of target class needs to be estimated separately for multiple sub-types.


**Update from May 5, 2025:**

***Functions to estimate overall accuracy in sections A.1.1 and A.1.2 have been modified***

The modified version of the code uses ratio estimator (equation A.11 for equal probability sampling (section A.1.1) and equation A.31 for unequal probability sampling (section A.1.2)) instead of equations A.7 (section A.1.1) and A.26 (section A.1.2) as recommended in Appendix A.2.2 of the paper.

The approach for estimating overall accuracy described in the paper (estimating the area of agreement using equation A.7 (for equal probability sampling) or equation A.26 (for unequal probability sampling) and then dividing by a known total area of the study region) is correct, but might produce estimates of OA over 100% in rare cases when overall accuracy is close to 100% (i.e., the area of agreement between the map and the reference sample is very close to the total area of the study region).

When using a ratio estimator (equation A.11 or A.31), both the correctly classified area (numerator of the ratio) and the total area of the study region (denominator of the ratio) are estimated from the sample, and thus the estimated Overall Accuracy will not exceed 100%.

Functions to estimate standard errors of the overall accuracy have been modified as well, and now use respective variance estimators of the ratio for equal and unequal probability sampling.

