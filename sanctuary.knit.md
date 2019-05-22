
# Extract data within a boundary {#sanctuary}
>notebook filename | 02-sanctuary.Rmd    
history | converted to R notebook from sanctuary.R  

In this exercise, you will download data from within the boundaries of the Monterey Bay National Marine Sanctuary (MBNMS) and visualize the data in a map. 

The exercise demonstrates the following skills:  

* Loading data from a CSV file  
* Using **rerddap** to retrieve information about a dataset from ERDDAP 
* Using the **rxtractogon** function to extract satellite data within an polygon over time  
* Mapping satellite data  

## Install packages and load libraries

```r
# Function to check if pkgs are installed, install missing pkgs, and load
pkgTest <- function(x)
{
  if (!require(x,character.only = TRUE))
  {
    install.packages(x,dep=TRUE)
    if(!require(x,character.only = TRUE)) stop(x, " :Package not found")
  }
}

# create list of required packages
list.of.packages <- c("ncdf4", "parsedate", "rerddap", "sp", "devtools", "ggplot2", "RColorBrewer", 
                      "reshape2", "maps", "mapdata", "jsonlite")

# Run install and load function
for (pk in list.of.packages) {
  pkgTest(pk)
}

# create list of installed packages
pkges = installed.packages()[,"Package"]

# Check if devtools pkgs are install. Install missing pkgs.
if(!('rerddapXtracto' %in% pkges)) {
  devtools::install_github("rmendels/rerddapXtracto")}
if(!('plotdap' %in% pkges)) {
  devtools::install_github('ropensci/plotdap')} 
if(!('rerddap' %in% pkges)) {
  devtools::install_github("ropensci/rerddap")}

library(rerddap)
library(rerddapXtracto)
library(mapdata)
```

## Load sanctuary boundary coordinates
For this example, the sanctuary boundary is definded within a comma separated file (mbnms.txt) in the shapes folder. The file contains a series of longitude and latitude coordinates the together draw the the boundry of the sanctuary on a map, like tracing a dot-to-dot drawing.  

>Longitude, Latitude  
-120, 52.0  
-120, 52.0  
-120, 52.0  
'...  
-120, 52.0  

A boundary file for Olympic Coast National Marine Sanctuary (OCNMS) is also availaible in the shapes folder. Additional sanctuary boundaries may be obtained at   [http://sanctuaries.noaa.gov/library/imast_gis.html](http://sanctuaries.noaa.gov/library/imast_gis.html).

**The script below:**   

* Loads the boudary data from the CSV file into a dataframe  
* Extracts the longitude and latitude data into vector variables  















