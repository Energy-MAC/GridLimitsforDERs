# GridLimitsforDERs

This repository contains script and data files for the project titled 'Grid limits pose equity barriers for distributed energy resources'.

Additionally, we include three files here that provide results for circuit capacity per household across the utility territories of PG&E and SCE in California. These are higher-resolution versions of Figure 1a, 1b, and 1c, and show circuit capacity for PV, PV with operational flexibility limits, and load, respectively. Files: BrockwayCondeCallaway_GridLimitsforDERs_PV.pdf, BrockwayCondeCallaway_GridLimitsforDERs_PVOF.pdf, and BrockwayCondeCallaway_GridLimitsforDERs_Load.pdf.

---------------

Files located in this repository include script files (described below) and some key data files (listed below in key input/output sections).

**Data preparation**

CensusDataAggregation.Rmd 
- Aggregates demographic features (Supplementary Table S8) and one geographic feature (urban heat, Supplementary Table S7)
- Key output: bgCAcensusCES.csv as a cleaned data file

ArcGISprocess.rtf 
- Contains a guide to the ArcGIS processes and commands used to perform the spatial data analysis (see Methods section, "Residential households are spatially matched to distribution circuits that provide electric service")
- Key output: Figure 1, Supplementary Figure S4

**Utility data files are read from ArcGIS outputs and operated on via:**

01_utilitydata.Rmd
- Pulls in and analyzes circuit and line data
- Key SCE inputs: Customer_Type_Breakdown.csv, Substations.csv, ICA__Circuit_Segments_CA_Res.csv (available at: https://berkeley.box.com/s/we2tzo7czvwi0fwt0pc7ecrovz9mrz23), RAM__Circuits.csv, 2012-2017CircuitCustomerBase.xlsx
- Key PG&E inputs: FeederDetail_CalAlbers.csv, Substations_CalAlbers.csv, lcr-substation-list_2019-12.csv, LineDetail_CA_Res.csv (available at: https://berkeley.box.com/s/iwg21nyn3pjed7vgpb12k8prqcp63lll)
- Key outputs: Supplementary Figure S5(b), PGE_circ.csv, SCE_circ.csv, PGE_subs.csv, SCE_subs.csv

02_cpolys.Rmd
- Pulls in circuit polygon data (outputs from ArcGIS) and analyzes outcomes of spatial processing
- Key SCE inputs: SCE_ICAall_cspoly.csv, SCE_ICAall_cpolybg_zcta_ghi.csv, SCE_ICAall_ctotpoly.csv
- Key PG&E inputs: PGE_ICA19_cspoly.csv, PGE_ICA19_cpolybg_zcta_ghi.csv, PGE_ICA19_cpolybg_ICAavail_zcta_ghi.csv, PGE_ICA19_ctotpoly.csv, PGE_subs.csv
- other key inputs: bgCAcensusCES.csv
- Key outputs: Supplementary Figure S5(a), PGE_all.csv, PGE_ICAall.csv, PGE_ICAallreal.csv, SCE_ICAall.csv, SCE_ICAallreal.csv

03_features.Rmd
- Assembles and cleans features to be used in random forest and linear and logistic regression runs
- Key inputs: PGE_all.csv, PGE_ICAall.csv, PGE_ICAallreal.csv, SCE_ICAall.csv, SCE_ICAallreal.csv, bgCAcensusCES.csv
- Key outputs: Supplementary Figure S6, PGE_ICAalldemo.csv, PGE_ICAalldemoreal.csv, SCE_ICAalldemo.csv, SCE_ICAalldemoreal.csv

04_allocation.Rmd
- Assigns hosting capacity to households (see Methods section "Available circuit hosting capacity is allocated to residential households by service location")
- Key inputs: PGE_ICAalldemo.csv, PGE_ICAalldemoreal.csv, SCE_ICAalldemo.csv, SCE_ICAalldemoreal.csv
- Key outputs: Supplementary Table S4, Supplementary Figure S7, PGE_ICAalldemoalloc.csv, SCE_ICAalldemoalloc.csv, PGE_ICAalldemotrees_real.csv, SCE_ICAalldemotrees_real.csv

05_access.Rmd
- Calculates grid access for households served by PG&E and SCE (see Methods section "Households need kilowatts of circuit capacity for access to DERs")
- Key inputs: PGE_ICAalldemoalloc.csv, SCE_ICAalldemoalloc.csv
- Key outputs: Figures 2 and 3; Supplementary Figures S1 and S2; and Supplementary Tables S1, S2, and S3

**Analysis of results**

Machine Learning Models.ipynb
- Performs linear regression, logistic regression, and random forest runs (see Methods section "Connecting household access results to infrastructure, service, geographic, and demographic features", Supplementary Note S5, and Supplementary Figure S3)
- Key inputs: SCE_ICAalldemotrees_real.csv, PGE_ICAalldemotrees_real.csv

ftfigs.Rmd
- Analyzes the relationships between demographic indicators and hosting capacity (see Methods section "Connecting household access results to infrastructure, service, geographic, and demographic features")
- Key inputs: PGE_ICAalldemoalloc.csv, SCE_ICAalldemoalloc.csv
- Key outputs: Figures 4 and 5
