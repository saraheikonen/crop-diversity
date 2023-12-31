Code from manuscript: 'Diverging impacts of climate change on the global potential diversity of food crops'
By:Sara Heikonen, Matias Heino, Mika Jalava, Stefan Siebert, Daniel Viviroli, Matti Kummu

The ananlysis is composed of five MATLAB scripts and five R scripts:

1) step1_crop_calendar_filters.R
	- Create monthly filter rasters for filtering climate parameter only within the cropping season (1),
	  for limited number of crops. Used for supplementary, seasonal SCS analysis.

2) step2_create_ref_data.R
	- Create Shapefiles and rasters of World Bank regions (2), latitude zones and elevation (3) zones
	- Create total cropland mask rasters for main analysis with SPAM 2010 crop producion data (4),
	  for analysis with SPAM 2005 crop production data (5), and seasonal Safe Climatic Space (SCS) (6)
	  analysis
	- Create crop production rasters for maize and soybean with matching coverage for
	  seasonal SCS analysis

3) step3_holdridge_download_data_missing_removed.m
	- Modified from code from Kummu et al. (6). Downloads present and future climate parameter data
	  datafrom Worldclim (7) and preprocess for next analysis steps. Data can be preprosessed either
	  for main, annual SCS analysis or for supplementry analaysis with seasonal SCS.

4) step4_holdridge_define_classes.m
	-  Modified from code from Kummu et al. (6). Classifies global land area into Holdridge life zones.

5) step5_holdridge_calculate_change.m
	-  Modified from code from Kummu et al. (6). Calculates future shifts in Holdridge life zones.

6) step6_holdridge_analyses_main.m
	-  Modified from code from Kummu et al. (6). Combines Holdridge data with crop production data.
	   Delineates crop specific SCSs and share of production and cropland area within and outside the SCS.
	   Also needs data on resilience (8).These scripts require four external MATLAB packages: cbarrow, export_fig,
	   crameri, wprctile. The script performs the analysis for one crop at a time with the following input parameters: env = 'local',
	   spamcrop_name = (crop raster filename here without the '.tif'), res_yes = false, scenarios = 'warming', spam_year = '2010' or '2005'.
	   

7) step7_reorganize_step6_results.m
	- Reorganizes results collected from the parfor loop in step 6 for further analyses

8) step8_crop_diversity.R
	- Combines results of production and area outside the SCS for individual crops (from step 6)
	  at the level of crop groups for visualisation. Determines the lowest warming level that would
	  push 25%, 50%, and 75% of local crop production outside the SCS & produces regional summaries. Calculates total
	  potential crop diversity and change in potential crop diversity at warming levels, summarize within geographic
	  regions as well as latitude and elevation zones.

9) step9_figures_tables.R
	- Produces all figures and reformats some output tables from previous steps

10) step10_seasonal_vs_annual_SCS.R
	- Comparison of results from seasonal and annual SCS approaches. Before running this script, the steps 3-8 should be run with
	  annual SCS approach and seasonal SCS approach. The selction between approaches is made in step 3, and the steps after that are the
	  same with both approaches.

Modified from code from Kummu et al. (6): Functions (apart from those that are from external packages) required for running the MATLAB scripts are
in the 'functions' folder. The data used for downloading the data and creating the Holdridge life zones are in the 'input' folder. In addition,
in the 'input' folder, there is the land mask file that was used for these analyses, and in the 'ref_data' folder, the country code file and raster,
and the crop group code file that were used in these analyses.

The scripts have coherent file structure and external data needed to perform the analyses are listed in References, (1-5, 7, 8).

Used MATLAB version: 9.14.0.2239454 (R2023a)

Used R version: 4.3.1

Used R base packages: stats, graphics, grDevices, utils, datasets, methods, base

Used other R packages and their versions:
ncdf4_1.21          rgeos_0.6-3         rnaturalearth_0.3.3 RColorBrewer_1.1-3  scico_1.4.0        
colorspace_2.1-0    tmap_3.3-3          lubridate_1.9.2     forcats_1.0.0       stringr_1.5.0      
purrr_1.0.1         readr_2.1.4         tibble_3.2.1        tidyverse_2.0.0     ggplot2_3.4.2      
tidyr_1.3.0         matrixStats_1.0.0   sf_1.0-14           raster_3.6-23       sp_2.0-0           
terra_1.7-39        dplyr_1.1.2         readxl_1.4.3        openxlsx_4.2.5.2    rstudioapi_0.15.0  
raveio_0.1.0

Refrerences

(1) Jägermeyr, J., Müller, C., Minoli, S., Ray, D. & Siebert, S. GGCMI Phase 3 crop calendar. (2021) doi:10.5281/zenodo.5062513.

(2) The World Bank Group. World Bank Country and Lending Groups – World Bank Data Help Desk. 
https://datahelpdesk.worldbank.org/knowledgebase/articles/906519-world-bank-country-and-lending-groups.

(3) Lehner, B., Verdin, K. & Jarvis, A. New Global Hydrography Derived From Spaceborne Elevation Data. 
Eos, Transactions American Geophysical Union 89, 93–94 (2008).

(4) Yu, Q. et al. A cultivated planet in 2010 – Part 2: The global gridded agricultural-production maps.
Earth System Science Data 12, 3545–3572 (2020).

(5) Wood-Sichra, Ulrike, Joglekar, Alison B., & You, Liangzhi. Spatial production allocation model (SPAM) 2005: Technical documentation. (2016).

(6) Kummu, M., Heino, M., Taka, M., Varis, O. & Viviroli, D. Climate change risks pushing one-third of global food production outside the safe climatic space.
One Earth 4, 720–729 (2021).

(7) Fick, S. E. & Hijmans, R. J. WorldClim 2: new 1-km spatial resolution climate surfaces for global land areas.
International Journal of Climatology 37, 4302–4315 (2017).

(8) Varis, O., Taka, M. & Kummu, M. The Planet’s Stressed River Basins: Too Much Pressure or Too Little Adaptive Capacity? Earth’s Future 7, 1118–1135 (2019).
