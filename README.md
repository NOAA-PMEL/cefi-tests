# Example S3 Storage for Model Output

## The S3 Bucket (s3://noaa3100-oar-pmel-dev-cefi/)

In this folder s3://noaa3100-oar-pmel-dev-cefi/ne_pacific_10km/ there are 12 netCDF files. Each file contains one month's worth of model out for from a 10km model in the Northeast Pacific. There are many parameters in each file. The data are the on model native (curvi-linear) grid.

Also contained in this directory is a single netCDF file (s3://noaa3100-oar-pmel-dev-cefi/ne_pacific_10km/roms_grd_nep.nc) which contains the grids (the 2D lat/lon coordinates and the vertical levels).

Below is another folder (s3://noaa3100-oar-pmel-dev-cefi/ne_pacific_10km/json/) which contains kerchunk files. There are kerchunks of each individual netCDF file and a "combined" file with is a multi-file kerchunk which aggregates the indivdiual files into a single kechunked time series. The kerchunk files were created using a chunck size of 1 time step per chunk.

## The notebooks

[The notebook that was used to create the kerchunk files.](notebooks/mk_goa_kerchunk.ipynb)
[A notebook that reads the combined file and plots a time step.](notebooks/read_goa_kerchunk-s3.ipynb)
Because the grid and the data are separate, you have to read both data sets and merge them (identifying the latitude and longitude variables) to get an xarray dataset which follows the CF Conventions data model.

Note, the notebook that reads the data access the s3 directly via the s3fs. I did try to serve the data via xpublish, but it produced an error. I will report the error to the xpublish developers.
