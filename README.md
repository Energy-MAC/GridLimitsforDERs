# GridLimitsforDERs

This repository contains script and data files for the project titled 'Grid limits pose equity barriers for distributed energy resources'.

We are in the process of uploading files to this repository.

---------------

CensusDataAggregation.Rmd 
- aggregates demographic features (Supplementary Table S8) and one geographic feature (urban heat, Supplementary Table S7)
- key output: bgCAcensusCES.csv as a cleaned data file

ArcGISprocess.rtf 
- contains a guide to the ArcGIS processes and commands used to perform the spatial data analysis (see Methods section, "Residential households are spatially matched to distribution circuits that provide electric service")
- key output: Figure 1, Supplementary Figure S4

Utility data files are read from ArcGIS outputs and operated on via:

01_utilitydata.Rmd
- pulls in and analyzes circuit and line data
- key SCE inputs: Customer_Type_Breakdown.csv, Substations.csv, ICA__Circuit_Segments_CA_Res.csv (available at: https://berkeley.box.com/s/we2tzo7czvwi0fwt0pc7ecrovz9mrz23), RAM__Circuits.csv, 2012-2017CircuitCustomerBase.xlsx
- key PG&E inputs: FeederDetail_CalAlbers.csv, Substations_CalAlbers.csv, lcr-substation-list_2019-12.csv, LineDetail_CA_Res.csv (available at: https://berkeley.box.com/s/iwg21nyn3pjed7vgpb12k8prqcp63lll)
- key outputs: Supplementary Figure S5(b), PGE_circ.csv, SCE_circ.csv, PGE_subs.csv, SCE_subs.csv

02_cpolys.Rmd
- pulls in circuit polygon data (outputs from ArcGIS) and analyzes outcomes of spatial processing
- key SCE inputs: SCE_ICAall_cspoly.csv, SCE_ICAall_cpolybg_zcta_ghi.csv, SCE_ICAall_ctotpoly.csv
- key PG&E inputs: PGE_ICA19_cspoly.csv, PGE_ICA19_cpolybg_zcta_ghi.csv, PGE_ICA19_cpolybg_ICAavail_zcta_ghi.csv, PGE_ICA19_ctotpoly.csv, PGE_subs.csv
- other key inputs: bgCAcensusCES.csv
- key outputs: Supplementary Figure S5(a), PGE_all.csv, PGE_ICAall.csv, PGE_ICAallreal.csv, SCE_ICAall.csv, SCE_ICAallreal.csv

03_features.Rmd
- assembles and cleans features to be used in random forest and linear and logistic regression runs
- key inputs: PGE_all.csv, PGE_ICAall.csv, PGE_ICAallreal.csv, SCE_ICAall.csv, SCE_ICAallreal.csv, bgCAcensusCES.csv
- key outputs: Supplementary Figure S6, PGE_ICAalldemo.csv, PGE_ICAalldemoreal.csv, SCE_ICAalldemo.csv, SCE_ICAalldemoreal.csv

04_allocation.Rmd
- assigns hosting capacity to households (see Methods section "Available circuit hosting capacity is allocated to residential households by service location")
- key inputs: PGE_ICAalldemo.csv, PGE_ICAalldemoreal.csv, SCE_ICAalldemo.csv, SCE_ICAalldemoreal.csv
- key outputs: Supplementary Table S4, Supplementary Figure S7, PGE_ICAalldemoalloc.csv, SCE_ICAalldemoalloc.csv, PGE_ICAalldemotrees_real.csv, SCE_ICAalldemotrees_real.csv

05_access.Rmd
- calculates grid access for households served by PG&E and SCE (see Methods section "Households need kilowatts of circuit capacity for access to DERs")
- key inputs: PGE_ICAalldemoalloc.csv, SCE_ICAalldemoalloc.csv
- key outputs: Figures 2 and 3; Supplementary Figures S1 and S2; and Supplementary Tables S1, S2, and S3

Machine Learning Models.ipynb
- performs linear regression, logistic regression, and random forest runs (see Methods section "Connecting household access results to infrastructure, service, geographic, and demographic features", Supplementary Note S5, and Supplementary Figure S3)
- key inputs: SCE_ICAalldemotrees_real.csv, PGE_ICAalldemotrees_real.csv

ftfigs.Rmd
- analyzes the relationships between demographic indicators and hosting capacity (see Methods section "Connecting household access results to infrastructure, service, geographic, and demographic features")
