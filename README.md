# Cloud_morphologies2024
Anna Hall (ESS 569), Je-Yun Chun (ESS 569), Katherine Mifsud (ESS 569), and Vlad Munteanu(ESS 469)

The objective of this geoscience machine learning project is to attempt to correctly identify cloud types/cloud morphologies through image based classification, such as a convolutional neural network. 

The premise of this project could be completed or replicated using various data sources. For this specific project, only data from geostationary weather satellite, GOES-R 16 is used for cloud identification. We use three data products from the GOES-16 Satellite Series; a cloud image and moisture product, a cloud optical depth product, and a reflected shortwave radiation product.

We chose to use a deep learning convolutional neural network (CNN) to identify and classify satellite images of clouds because this will allow us to automatically look for patterns, textures, and shapes in the images; sort and label them efficiently. Our CNN will process our satellite images that we input from GOES-R 16, and look for cloud formation, shape, and brightness. These features will aid in the classification process. CNNs are composed of several layers. The input layer is coomprised of the GOES-R 16 satellite images. The convolutional layer, will process the image and identify features and patterns. The output layer will provide the final morphology classification. 

These notebooks and scripts are created in python through the VS Code platform. 
Before running any scripts or notebooks, the user should import the necessary packages listed below, should the necessary packages not be available you can try a 'pip install **package name**' 

Relevant packages and libraries to install include :

```python
from goes2go import GOES
import pandas as pd
from datetime import datetime
import xarray as xr
import subprocess
from netCDF4 import Dataset
import cartopy.crs as ccrs
import cartopy.feature as cfeature
import matplotlib.pyplot as plt
import numpy as np
```
There are a couple of packages that may be unfamiliar to the every day python user **goes2go** and **subprocess**.

The **goes2go** package is developed as an easy and efficient way to access GOES satellite data on the AWS server. This package is developed by **Brian Blaylock**. Instructions on installing and using the goes2go package can be found on this GitHub page:

https://github.com/blaylockbk/goes2go?tab=readme-ov-file#download-data 

Other important links pertaining to the goes2go python package and the man, the myth, the legend, himself can be found here:

Brian's Homepage
(https://home.chpc.utah.edu/~u0553130/Brian_Blaylock/home.html)

Brian's Github
(https://github.com/blaylockbk/pyBKB_v3/blob/master/BB_GOES/mapping_GOES16_TrueColor.ipynb)

Brian's Bulk download github (GOES2go)
(https://github.com/blaylockbk/goes2go?tab=readme-ov-file)

Brian's ABI field of view
(https://goes2go.readthedocs.io/en/latest/user_guide/notebooks/field-of-view_ABI.html)

The next package that may be unfamiliar is subprocess. We use the subprocess package to access the GOES data stored on the AWS server.

To set-up the AWS CLI on your own please follow these written instructions:

NASA github for accessing GOES data
(https://github.com/awslabs/open-data-docs/tree/main/docs/noaa/noaa-goes16)

To read more about the satellite data housed on the AWS server you can follow these links:

NOAA GOES on AWS
(https://docs.opendata.aws/noaa-goes16/cics-readme.html)

Base AWS registry
(https://registry.opendata.aws/noaa-goes/)

for debugging AWS CLI follow this link:
(https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-troubleshooting.html#general-formatting)

For more information about the GOES Series:

Satellite Data Information from NESDIS
(https://www.star.nesdis.noaa.gov/atmospheric-composition-training/satellite_data.php#abi_aws)

GOES Image Viewer
(https://www.star.nesdis.noaa.gov/goes/sector.php?sat=G16&sector=gm)

Beginner's guide to GOES data
(https://www.goes-r.gov/downloads/resources/documents/Beginners_Guide_to_GOES-R_Series_Data.pdf)

GOES documents -- PUG v5 for converting to lat/lon grid
(https://www.goes-r.gov/resources/docs.html)

Imager Projector 
(https://www.star.nesdis.noaa.gov/atmospheric-composition-training/satellite_data_goes_imager_projection.php#:~:text=If%20you%20want%20to%20work,in%20the%20GOES%2DR%20PUG.)

NESDIS STAR code for converting between ABI Grid and Lat/Lon
(https://www.star.nesdis.noaa.gov/atmospheric-composition-training/python_abi_lat_lon.php)


Other links that may be helpful:

Leif's Github
(https://github.com/leifdenby/convml-tt?tab=readme-ov-file)

geostationary projection documentation
(https://proj4.org/en/9.5/operations/projections/geos.html)

funny Basemap Thread
(https://github.com/matplotlib/basemap/issues/361)


## References and Resources

- **Brian Blaylock’s Resources**: For accessing GOES satellite data and `goes2go` details:
  - [Brian's GitHub](https://github.com/blaylockbk/goes2go)
  - [Brian's Homepage](https://home.chpc.utah.edu/~u0553130/Brian_Blaylock/home.html)
  - [Mapping GOES16 TrueColor](https://github.com/blaylockbk/pyBKB_v3/blob/master/BB_GOES/mapping_GOES16_TrueColor.ipynb)
  - [GOES Image Viewer](https://www.star.nesdis.noaa.gov/goes/sector.php?sat=G16&sector=gm)
  - [GOES ABI Field of View](https://goes2go.readthedocs.io/en/latest/user_guide/notebooks/field-of-view_ABI.html)

- **Further Reading**:
  - [NOAA GOES on AWS](https://docs.opendata.aws/noaa-goes16/cics-readme.html)
  - [GOES Series Documentation](https://www.goes-r.gov/resources/docs.html)
  - [AWS CLI Troubleshooting](https://docs.aws.amazon.com/cli/latest/userguide/cli-chap-troubleshooting.html#general-formatting)
  - [Beginner's Guide to GOES Data](https://www.goes-r.gov/downloads/resources/documents/Beginners_Guide_to_GOES-R_Series_Data.pdf)
  - [NASA GitHub for Accessing GOES Data](https://github.com/awslabs/open-data-docs/tree/main/docs/noaa/noaa-goes16)
  - [Satellite Data Information from NESDIS](https://www.star.nesdis.noaa.gov/atmospheric-composition-training/satellite_data.php#abi_aws)
  - [GOES Imager Projection](https://www.star.nesdis.noaa.gov/atmospheric-composition-training/satellite_data_goes_imager_projection.php#:~:text=If%20you%20want%20to%20work,in%20the%20GOES%2DR%20PUG.)
  - [GOES Lat/Lon Conversion Code](https://www.star.nesdis.noaa.gov/atmospheric-composition-training/python_abi_lat_lon.php)
  - [Leif’s GitHub for convml-tt](https://github.com/leifdenby/convml-tt?tab=readme-ov-file)
  - [Geostationary Projection Documentation](https://proj4.org/en/9.5/operations/projections/geos.html)
  - [Basemap Documentation](https://matplotlib.org/basemap/stable/users/geography.html)
  - [Funny Basemap Thread](https://github.com/matplotlib/basemap/issues/361)


Basemap Documentation (I did not use this, however, Brian does.)
(https://matplotlib.org/basemap/stable/users/geography.html)


**High-level descriptions of each added notebook and scripts in this repository will be updated frequently, as new files are added. 
