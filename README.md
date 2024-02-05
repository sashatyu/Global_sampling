This is a project providing the code and input data examples for various global sampling options from the following publication: Tyukavina et al. (in review) "Practical global sampling methods for estimating area and map accuracy of land cover and change classes". For a detailed description of the study please refer to the publicaiton.

Python 3 code implementing equations from the Appendix (numbering is consistent with sections of Appendix)
* A1.1.1 Equal probability sampling.ipynb
* A1.1.2 Unequal probability sampling - proportional to unit area.ipynb
* A2.1 Regression estimator - simple random sampling.ipynb
* A2.2 Regression estimator - stratified sampling.ipynb
* A3 Continous point sampling.ipynb

**Examples of input data:**

***Sampling design information***
[Number of appendix]Strata_info.txt (for Appendices A1.1.1, A1.1.2, A2.2 and A3)

   Columns: 
   * "Stratum" - Stratum ID (1-N);
   * (N/A for A3, not required for A.1.2) "Count" - total number of units (pixels, polygons) in each stratum;
   * (optional for A2.2) "Area" - Stratum area;
   * (for A2.2 only) "Xh" - stratum-specific mean of the values of auxiliary class (calculated accross all units in the stratum).
 
   Section 5.2. requires the following parameters specified directly in the code:
	* "N" - total number of units in the sampling region (population);
	* "X" - population mean of the values of auxiliary class (calculated accross all units in the sampling region);
	* (optional, might be needed to convert estimates to % of total area)"Atot" - area of the sampling region (e.g. in km²).

***Input data for each sample unit***
[Number of appendix]Sample_data.txt (for Appendices A1.1.1, A1.1.2, A2.1, A2.2 and A3)

   Columns for Appendix A1:
   * "Stratum" - stratum ID, 1 - nstrata;
   * "Pixarea" - area of each sample unit (in units that are desired for area reporting);
   * "Map"(for accuracy assessment only) - proportion of target class from the map (0-1) for each sample unit;
   * "Reference" - proportion of target class from reference sample classification for each sample unit; allowed values are from -1 to 1 for area estimation, and from 0 to 1 for map accuracy assessment;
   * (optional)"RefType" - type labels, if the are of target class needs to be estimated separately for multiple sub-types;
   * (optional)"Correct" - proportion of sample unit (0-1), which is correctly mapped. This column is necessary for maps with more than two classes. For map with two classes it is computed in the function "estimate_OA_two_classes" directly from "Map" and "Reference" columns.

   Columns for Appendix A2:
   * (for A2.2 only)"Stratum" - Stratum ID (1-N);
   * "yi" - area of the target class in sample unit i,derived from sample interpretation (reference classification); should be in the same units as stratum Area and Atot;
   * "xi" - value of the auxiliary class for sample unit (e.g. area of land cover class from existing wall-to-wall map or mean spectral index value within sample unit); ould be in any units matching X.

   Columns for Appendix A3:
   * "Stratum" - stratum ID, 1 - nstrata;
   * "Reference" - proportion of target class from reference sample classification for each sample unit; allowed values are from -1 to 1 for area estimation, and from 0 to 1 for map accuracy assessment;
   * (optional)"RefType" - type labels, if the are of target class needs to be estimated separately for multiple sub-types.
