# Real-time-air-temperature-mapping---Australia

SUMMARY
This repository hosts the source code for http://austemperature.live/.
This mapping application displays spatially interpolated air temperature and accumulated rainfall maps generated from recordings provided by Automatic Weather Stations of the Australian Bureau of Meteorology (BoM). Maps are generated using thin-plate spline interpolation along with covariate information (9 second Digital Elevation Model) to account for the lapse rates (for temperature based maps only). Main features  of this web mapping application include:
-	Web maps presented at ~285m spatial resolution for the entire spatial extent of Australia showcasing air temperature (°C) and accumulated rainfall (i.e. accumulated mm from 9am AEST);
-	Maps updated every 30 mins displaying the most recent observations as a continuous geotiff surface;
-	BoM automatic weather stations locations (presenting 'live' observations of temperature and rainfall - simply toggle on/off this layer in the table of contents then click on the map icons to access the latest recordings);
-	Zoom in/out functionality (to any site location in Australia); 
-	Map query functionality to provide site specific information for any location in Australia (simply click on a location within the map extent to derive site specific information for the previous 3 hours for temperature and rainfall);
Please note that this map application is a PhD experiment and continually evolving. A journal article detailing the major findings of this study is currently in production.

SPECIFICATIONS
The source code presented in this repository requires:
-	High-end CPU specifications, preferably with at least 12VCPU’s and plenty of RAM. 
-	Software R (ver 3.6.1 or higher, visit https://www.r-project.org/) installed and operating. In addition, the following R packages will also need to be installed and operating: httr, RNetCDF, ncdf4, epiR, plyr, gstat, sp, automap, rgdal, raster, MASS, doParallel, foreach, snow, Cubist, fields, leaflet, htmwidgets, leaflet.extras, shiny.
-	Geoserver (ver 2.15.1 or higher, visit: http://geoserver.org/) installed and operating and deployed on port 8080.
-	Shiny server (ver 1.5.13 or higher, visit: https://rstudio.com/products/shiny/shiny-server/) installed and operating and deployed on port 3838. 

REPOSITORY DETAILS
The repository (RTmap_source_code_and_data_structure.zip) can be unzipped to find the following directories:

Rcode – Possesses the source code to run the application including:
-	‘RealTime_MappingCode_00minutes.R’ - A nationwide air temperature and rainfall map is produced based from 'near real-time' BoM AWS data relevant for observations at 00 minutes (past the hour of interest). It is recommended this script be run at 20 minutes past the hour of interest (e.g. 12.20am AEST). Note that the script requires configuration under the ‘INPUT PARAMETERS’ (these are explained in the script itself). Also note that if GeoServer and Shiny are not installed the script can still be executed to produce maps – they will just not be deployed on GeoServer or Shiny. To do this, ensure to enter ‘GEOSERVER<- "n"’ in the script setting for this feature. 
-	‘RealTime_MappingCode_00minutes.R’ - A nationwide air temperature and rainfall map is produced based from 'near real-time' BoM AWS data relevant for observations at 30 minutes (past the hour of interest). It is recommended this script be run at 50 minutes past the hour of interest (e.g. 12.50am AEST). Note that the script requires configuration under the ‘INPUT PARAMETERS’ (these are explained in the script itself). Also note that if GeoServer and Shiny are not installed the script can still be executed to produce maps – they will just not be deployed on GeoServer or Shiny. To do this, ensure to enter ‘GEOSERVER<- "n"’ in the script setting for this feature.
-	‘DeployWebMaps.R’- A nationwide temperature and rainfall map is deployed to the shiny web app based on surfaces produced from the Real time mapping code (‘RealTime_MappingCode_00minutes.R’ or ‘RealTime_MappingCode_00minutes.R’). Note that the script requires configuration under the ‘INPUT PARAMETERS’ (these are explained in the script itself). GeoServer and Shiny server must be installed and operating for this feature to work.

Mapping_system_DATAMODEL – The data model for the above Rcode where outputs will be written and referred to. 
-	This folder structure ought to be placed in a high-level root directory, e.g. " C:/Mapping_system_DATAMODEL". Be sure to adjust the ‘INPUT PARAMETERS’ in ‘RealTime_MappingCode_00minutes.R’ and ‘RealTime_MappingCode_00minutes.R’ to define the ROOT_DIR parameter, accordingly. 
-	Also note that the data model requires the 9 second DEM to be placed in the DATA MODEL in the following location: Mapping_system_DATAMODEL/INTERMEDIATE_CovariateData/TAS
This DEM can be downloaded from:
https://data.gov.au/data/dataset/ebcf6ca2-513a-4ec7-9323-73508c5d7b93  
NB: It is vitally important (!) that this DEM is reprojected to ‘GDA94_Geoscience_Australia_Lambert’ and saved as a SAGA grid file (.sdat) and placed in the directory as defined above.

GeoserverStyleFiles – Style files to be added into Geoserver to render incoming air temperature and rainfall maps for display in the shiny application. Style files include:
-	Air_temperature_degC.sld – style file for air temperature maps.
-	Rainfall_mm.sld – style file for rainfall maps.
NB: This will need to be manually configured in GeoServer.

GEOSERVER CONFIGURATION
Ensure the following workspaces are created in GeoServer: 
-	TempPred
-	RainPred

Ensure the following style files are created in GeoServer and the sld contents pasted into style content accordingly (as mentioned previously):
-	Air_temperature_degC – style file for air temperature maps (refer to Air_temperature_degC.sld).
-	Rainfall_mm – style file for rainfall maps (refer to Rainfall_mm).

FURTHER INFORMATION
For further information about this application please email:
mweb7041@uni.sydney.edu.au
Mathew Webb (PhD student, University of Sydney)
School of Life and Environmental Sciences & Sydney Institute of Agriculture, The University of Sydney, Eveleigh, NSW, Australia

