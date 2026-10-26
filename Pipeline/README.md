# Pipeline backup

This folder contains the exported `Retail_Data_Quality_Pipeline` definition and manifest.

The JSON definition contains one `TridentNotebook` activity. In the Fabric settings screenshot, that activity is configured to run `Day04_Data_Quality_Checks` in the `Retail Demand Intelligence` workspace. The JSON itself stores Fabric notebook and workspace IDs rather than a portable notebook package.

This pipeline runs the data-quality notebook. It is separate from `Retail_ETL_Transformations` and does not document or run the ETL transformations. The referenced Day 4 notebook export is not included in this backup, so add it to `Notebooks/` if you need an independently restorable copy.
