This is a project providing the code and input data examples for various global sampling options from the following publication: Tyukavina et al. (in review) "Options for global sampling of geographic data". For a detailed description of the study please refer to the publicaiton.

Python 3 code implementing equations from the Appendix (numbering is consistent with sections of Appendix)
* 2. Sampling of equal area units, strata weighted by number of units.ipynb
* 3. Sampling of equal area units, strata weighted by area.ipynb
* 4. Sampling weighted by unit area.ipynb
* 5.2. Regression estimator - simple random sampling.ipynb
* 5.3. Regression estimator - stratified sampling.ipynb

**Examples of input data:**

***Sampling design information***
* 2-3.strata_info.txt (for Sections 2 and 3)
* 4.strata_info.txt (for Section 4)
* 5.3.strata_info.txt (for Section 5.3)

   Columns: 
   * "Stratum" - Stratum ID (1-N)
   * "Area_km2" - Stratum area
   * (for Sections 2, 3 and 5.3) "Count" - total number of units (pixels, polygons) in each stratum
   * (for Section 4 only) "Sample size" - Number of pixels sampled in each stratum
   * (for sampling without replacement only, Section 4)"SumPixareaSq" - sum of squared areas of all (not only sampled) units (pixels/polygons) within each stratum
   * (for Section 5.3. only) "Xh" - stratum-specific mean of the proportion (from 0 to 1) of auxiliary class (calculated accross all units in the stratum)
 
   Section 5.2. requires the following parameters specified:
     * "Atot" - area of the sampling region (e.g. in km²)
     * "N" - total number of sampling units in the sampling region
     * "X" - population mean of the proportion (from 0 to 1, or from -1 to 1 for net change area estimation) of auxiliary class

***Input data for each sample unit***
* 2-3.Sample_data.txt (for Sections 2 and 3)
* 4.Sample_data.txt (for Section 4)
* 5.2.Sample_data.txt (for Section 5.2)
* 5.3.Sample_data.txt (for Section 5.3)

   Columns for Sections 2-4:
   * "Stratum" - Stratum ID (1-N)
   * "Map"(for accuracy assessment only) - proportion of target class from the map (from 0 to 1) for each sample unit
   * "Reference" - proportion of target class from reference sample classification for each sample unit; allowed values are from -1 to 1 for area estimation, and from 0 to 1 for map accuracy assessment.
   * (optional)"RefType" - type labels, if the are of target class needs to be estimated separately for multiple sub-types
   * (optional)"Correct" - proportion of sample unit (0-1), which is correctly mapped. This column is necessary for maps with more than two classes. For map with two classes it is computed in the function "estimate_OA_two_classes" directly from "Map" and "Reference" columns.
   * (for Section 4 only) "Pixarea" - area of each sampled pixel/polygon in units consistent with strata area from the sample table (e.g. km2)

   Columns for Sections 5.2 and 5.3:
   * (for Section 5.3 only)"Stratum" - Stratum ID (1-N)
   * "yi" - proportion (from 0 to 1 or from -1 to 1 for net change area estimation) of the target class from the area of the sampled unit (derived from sample interpretation)
   * "xi" - proportion (from 0 to 1 or from -1 to 1 for net change area estimation) of the auxiliary class from the area of the sampled unit (derived from a wall-to-wall map)
