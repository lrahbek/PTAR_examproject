# Public Transport Access and Reach

Laura Givskov Rahbek 

*Exam Project for Spatial Analytics*

*Bachelor’s Supplementary Subject in Cultural Data Science, Aarhus University*

10-06-2024

## Repository Description and Structure 

This repository contains the code for the preprocessing and analysis of data for the Spatial Analytics (2024) exam at Aarhus University. The analysis aims to investigate differences in reach of public transportation from education instituions in Denmark. Specifically, the differences between the newly and to-be established study programmes positioned in line with the political agreement ['Flere og Bedre Uddannelsesmuligheder i hele Danmark'](https://ufm.dk/lovstof/politiske-aftaler/aftale-om-flere-og-bedre-uddannelsesmuligheder-i-hele-danmark) (*More and Better Education Oppertunities in all of Denmark*, from here FBUM) and their existing counterparts, in terms of distance reach within set time limits. The repository is structured in the following way: 
 
```in``` is were the data should be placed, if the analysis is reproduced. It already contains the following: 

- ```new_ed```, a folder with the new education data and a README file describing the pre-processing. 

- ```preprocessed```, a folder where the code in the markdowns saves pre-processed data. 

- ```GTFS```, a folder where the GTFS data from Rejseplanen should be placed. 

```out``` contains the outputs from the analysis 


```src``` cotains three scripts: 

- ```preprocess_inst_edu.rmd```, where the data related to the locations of the instituions are pre-processed. 

- ```preprocess_rejseplanen.rmd```, where the data related to the public transport data is pre-processed. 

- ```analysis.rmd```, where the data is analysed. 

In this README, the data and aquisition information is given, as well as a detailed walk throughs of the pre-processing and analysis. In pre-processing the locations of the study programmes, many manual tweaks and decisions had to be made, which means that it does not fit other data. However the format of this data is described, so the subsequent pre-processing of public transportation data and the analysis can be conducted on any data. 

## Data 

1. **Instittutionsregisteret [The instituition register]** is a database kept up by different parts of the Government, and contains information on type, name, contact and location for all registered instituions in Denmark (some are not included, but these are not relevant for this analysis). A guideline and format description of the databse can be found [here](https://viden.stil.dk/pages/viewpage.action?pageId=114294882), and a pull from the database can be done from [here](https://data.stil.dk/instreghistorik/). It is updated contiously, but historical pulls are possible, so if the present analysis are to be exactly replicated, date should be specified as April 28, 2024. When pulling the entire database from this date, the file name should be ```Instreg_All_28-04-2024.csv```. The pre-processing of the data is described in a section below, but here the variables used in the pre-processing and in pre-processing of the remaning data is described (note: for the datasets to be able to be easily merged with each other, the shared variables are named the same across the analysis; their names might therefore be slighlty different than those represented in the descriptions in the link above). 

|Variable|Description|Use|
|--------|-----------|---|
|H_INST_NR| Unique ID for an institutions 'main' institution|Identification of individual institutions|
|INST_NR| Unique ID for each individual institution|Identification of individual institutions|
|H_INST_NAME| The name of the 'main' institution|Identification of individual institutions|
|INST_NAME| The name of the individual institution |Identification of individual institutions|
|INST_TYPE|The type of institution | Filtering the types of institutions the FBUM agreement concerns|
|UNIT_TYPE|The type of the institution unit |Filtering and accessing names and ids of main institutions|
|AKTIVE_KODE|Activity key for the institution|Filtering out inactive institutions|
|MUN_NAME|The name of the municipality the institution is located in|Identification of individual institutions, and filtering out institutions in Greenland and the Faroe Islands|
|LAT|The latitude with the geodetic crs: ETRS89| Locating the study programmes of interest|
|LONG|The longitude with the geodetic crs: ETRS89| Locating the study programmes of interest |

2. **New Education** data is described in detail in ```in/new_ed/README.md```, and can be found as a csv file in that same folder. Several choices had to be made, as well as extensive manual pre-processing, why this data has a README.md file dedicated to it. Briefly; the data contains the institutions, names of programmes and rough locations of the original draft of the new study programmes to be started with the FBUM agreement. These, with their already existing counterparts, are used to analyse the difference in public transport acces and reach. 

3. **Uddannelseszoom** is a database manitained by the governement, with the purpose of supplying students with information on the relevance and quality of different programmes, based on student surveys. The data can be found [here](https://ufm.dk/uddannelse/statistik-og-analyser/uddannelseszoom), where further information also is available. For this project, the database is useful in the fact that it contains one row per existing study programme in Denmark, with some of the same key-variables as the Instituition Register. With the data on the new study programmes, this can then be used to find the locations of the existing programmes. A historical pull is as of now not possible, the data used for this analysis is dated March 23, 2024; ```UFM_samlet_23MAR2024.csv```, if when retrieved the data is updated, additional pre-processing might be needed. The variables are described here, for further discussion of the pre-processing see the section below. 

|Variable|Description|Use|
|--------|-----------|---|
|NAME|The title or name of study programme|Differentiating between programmes and matching to the new programmes|
|H_INST_NR| Unique ID for an institutions 'main' institution|Identification of individual institutions, and filtering out rows representing the overall programme (999999)|
|INST_NR| Unique ID for each individual institution|Identification of individual institutions|
|H_INST_NAME| The name of the 'main' institution the programme belongs to|Identification of individual institutions|
|URL|The URL to the study programmes page on www.ug.dk (a page with all available programmes) |The hierachical structure of ug.dk, allows for the extraction of the fields the different studies belong to, which are used in assigning UDD_ARES|
|UDD_AREA|The field the study programme is in|Matching with new study programmes|
|ED_CAT1|The type of institution | Filtering the types of institutions the FBUM agreement concerns|
|ED_CAT2|The type of the institution and programme |Filtering master degrees out, as all new programmes are at the bachelors level|
|MUN_NAME|The name of the municipality the programme is located in|Identification of individual institutions, and filtering out institutions in unnamed municipalities|

4. **GTFS-køreplansdata** is data supplied by [RejseplanenLABS](https://help.rejseplanen.dk/hc/da/categories/201728005) under the [Creative Commons BY 4.0 license](https://creativecommons.org/licenses/by/4.0/legalcode). It contains data on all routes, trips, travel paths, stop locations etc for Danish public transportation, in the standard in General Transit Feed Specification (GTFS) format, which is described [here](https://developers.google.com/transit/gtfs). The data can be accesed by contactign RejseplanenLABS through the site linked above. The data worked with in the current analysis applies in the date range 22/04/2024 to 17/07/2024. If the analysis should be reproduced, the .txt files should be placed in the ```in/GTFS``` folder. The GTFS data contains an enormerous amount of data, in several differemt .txt files. The different files share some variables, and in this way can be merged to acces different combinations of all variables available. The variables used from the original dataset are described here, variables resulting from pre-processing and analysis will be described in the sections below. Variable contains the name of the variable, file contains the names of the file(s) the variable is present in, and description contains a description of the variable. 

|Variable|file|Description|
|--------|----|-----------|
|route_id|routes.txt, trips.txt|The unique ID for each route|
|route_type|routes.txt|The type of route (e.g. 3 = Bus, 2 = Rail)|
|agency_id|routes.txt, agency.txt|The integer representing the agency running the route, the corresponding names can be found in agency.txt|
|trip_id|trips.txt, stop_times.txt|The unique ID for each trip (several trips can belong to the same route, they are differentiated by the travel path (shape) and the days the service is available)|
|service_id|trips.txt, calendar.txt, calendar_dates.txt|Acts as a key to the three files, identifying on what days the trip is in service|
|direction_id|trips.txt|0 or 1, indicating the direction of the trip|    
|shape_id|trips.txt, shapes.txt|Acts as a key between the two files, identifying each unique travel path of the trips|
|departure_time|stop_times.txt|The time of departure from a given stop, for each trip|
|stop_id|stop_times.txt, stops.txt|The unique ID for the stop location|
|stop_sequence|stop_times.txt|Integer describing the order of stops for a given trip (starts at 0)|
|stop_name|stops.txt|The name of the stop (corresponds to a stop_id)|
|stop_lat|stops.txt|The latitude of the stop location, crs: WGS84|
|stop_lon|stops.txt|The longitude of the stop location, crs: WGS84|
|shape_sequence|shapes.txt|The sequence of point locations for each shape_id|
|shape_pt_lat|shapes.txt|The latitude of a point on a shape, following the sequence creates the travel path, crs: WGS84|
|shape_pt_lon|shapes.txt|The longitude of a point on a shape, following the sequence creates the travel path, crs: WGS84|

The type of service of individual trips (service_id) describes how the trips is serviced. This information is stored in calendar.txt and and calendar_dates.txt. calendar.txt has a row for each service_id, columns for each day of the week and a start_date and end_date (22/04/2024 to 17/07/2024 for the current dataset). A preview of the file is shown here: 

|"service_id"|"monday"|"tuesday"|"wednesday"|"thursday"|"friday"|"saturday"|"sunday"|"start_date"|"end_date"|
|------------|--------|---------|-----------|----------|--------|----------|--------|------------|----------|
|1|1|1|1|1|1|0|0|20240422|20240717|
|2|0|0|0|0|1|1|0|20240422|20240717|
|3|1|1|1|1|1|1|1|20240422|20240717|
|4|0|0|0|0|0|1|1|20240422|20240717|
|5|0|0|0|0|0|0|0|20240422|20240717|

A 1 indicates that a trip with the given service_id is available for all of the given week days in the date range. A 0 indicates that the trip is not available for all of the given week days in the date range. To identify the type of exception the 0 indicates, the calendar_dates.txt file is used. A preview is shown here: 

|"service_id"|"date"|"exception_type"|
|------------|------|----------------|
|1|20240520|2|
|1|20240610|2|
|1|20240611|2|
|1|20240612|2|
|1|20240509|2|
|1|20240613|2|
|1|20240614|2|
|2|20240614|2|
|2|20240615|2|
|3|20240610|2|

The combination of the service_id, date and exception_type shows which service_id it applies to, on what date the exception occurs, and the type of exception: 1 if the service has been added to this date and 2 if the service have been removed from this date. 

## Reproducing of Analysis 

As mentioned, the markdown containing the pre-processing of the institution locations called for many manual and case specific tweaks. This process is described in detail in 'Pre-Processing Institution Locations', and the final format of the data is described so it can be replicated on other data. 

### Dependencies and Prerequisites 


tidyverse 
sf 
hms 
difftime

### Pre-Processing Institution Locations 

In ```preprocess_inst_edu.rmd``` the instituion and study programme data is preprocessed. If the neccesary data, as described above, have been placed correctly, all steps can be reproduced. If other data is used in the analysis, a description of the format and makeup of the final data frame is described, so it can be replicated. A few comments are available in the markdown and a complete description of the pre-processing is presented here: 

- The Institution Register data is filtered based on the following conditions: 

    - Inactive institutions are removed (AKTIV_KODE = 3 or 5), as the locations needed are for existing or future institutions. 

    - Institutions located in Greenland or on the Faroe Islands are excluded (BEL_KOMMUNE_TEKST = "Uden for kommunal inddeling (Færøerne og Grønland)"), as the RejseplanenLABS GTFS data does not contains data from either places. 

    - Institutions conduting 'e-learning' are removed (INST_NAVN contains 'e-læring'), as the point of inquiry concerns travel distances, and an e-learning institution does not have the same requirements for attendance etc. 

    - Institutions belonging to any of the five following INST_TYPEs are kept, as these are the ones the new programmes belong to: 
        - 'Maritime uddannelsesinstitutioner' (Maritime Institutions)
        - 'Kunstneriske og kulturelle uddannelsesinstitutioner' (Arts and Cultural Institutions)
        - 'Professionshøjskoler' (University Colleges)
        - 'Universiteter' (Universities)
        - 'Erhvervsakademier' (Business Academies)
    
- Then the INST_NR and the INST_NAME of the 'main' institutions were extracted and appended as the H_INST_NR, to be able to create a H_INST_NAME column for all rows. 

- The data frame was then converted to an ```sf``` object, with crs = 4258, which was transformed to planarcoordinates with crs  = 25832. I have chosen to work with planarcoordinates instead of geodetic, for this project, as distance measurements are less heavy for planarcoordinates, and the distances in question are fairly small. Finally, the data frame was saved to ```in/preprocessed/institutions/InReg.shp``` 

- The choices made for the new study programme data, are discussed in ```in/new_ed/README.md```. Briefly; the new study programmes were read in from ```in/new_ed/new_study.csv```, merged with the pre-processed institution register data and cleaned. 

- The UddannelsesZoom data is filtered on the following conditions, to clean it up before merging with either of the other data frames: 
    
    - The row for each programme, representing the overall data for the country is removed (H_INST_NR = 999999)

    - Institutions located on Greenland and the Faroe Islands are removed (MUN_NAME = "Uoplyst/ukendt"). 

- Then an additional column is made, UDD_AREA, to represent the field each programme is in. The variable is extracted from the URL column, which contains the urls to the pages for each programme. 

- The municipality names are changed, to be able to merge with the Institution Register Data. 'Kommune' is added to each name, for Københavns Kommune and Bornholms Regionekommune the names are edited indivudally. 

- After the initial cleaning, the UdannelsesZoom programmes that match with any of the new programmes are extracted. For all but four of the new programmes, this is conducted on NAME match (same exact programme), for the remaining four the programme field as well as manual inspection lead to the descisions made, this is all dicussed in detail in ```in/new_ed/README.md```. 

- In merging the UddannelsesZoom data with the Institution Register data, some variables had to be corrected: 

    - Several almost identical rows were included, as both bachelors and masters programmes have the same names, the masters programmes were removed, as the new study programmes are at the bachelors level. 

    - A wrong INST_NR was included for an institution in Esbjerg, this was corrected.

    - The Social Worker in Guldborgsund and the Automation Engineering in Hedensted, has been closed, why these were removed. 

- Finally, the new and existing study programmes were merged into one data frame, where a STATUS variable indicates whether a programme is 'new' or 'old' (some of the new programmes were already added to the UddannelsesZoom dataset, creating duplicates, these duplicates were removed keeping the ones with STATUS = 'new'). Grouping 'codes' were also assigned to each programme, these can be found in ```in/new_ed/README.md```. The final data frame is saved to ```in/preprocessed/education/EDU.shp```. Following is an example of the format, note that it should be an sf object. 

|

### Pre-Processing RejseplanenLABS Data 

In ```preprocess_rejseplanen.rmd``` the GTFS data from RejseplanenLABS is pre-processed. If the data has been placed correctly, as described above, and an sf object equivalent to the EDU used here is made, all steps can be reproduced. A few comments are avaialbel in the markdown, and a complete description of the pre-processing is included here: 

- The EDU sf object is loaded in, and a 500 meter buffer is added around each POINT, creating POLYGONS for all study programme locations. If another dataset is used, with the format as described above, this can be loaded in here.

- The next step is to load in all the raw GTFS data, as desrcibed in the 'Data' section above, and perform some pre-processing on it. 

    - ```routes.txt```: "route_id", "agency_id" and "route_type" are used. Rows with the "agency_id" = 401 (Skånetrafikken), is removed as it is outside of Denmark, and "route_type" = 715 & 4 (flextrafik and ferries) are removed, as the timetables work differently to those of more stable types of transports, e.g. busses and trains. 

    - ```trips.txt```: "route_id", "service_id", "trip_id", "direction_id" and "shape_id" are used. The rows with "service_id" corresponding to a service_id in ```routes``` are kept (the ones not filtered out). 

    - ```stop_times.txt```: "trip_id", "departure_time", "stop_id" and "stop_sequence" are used. The column "arrival_time" was excluded, as the point of interest is distance travelled within a given timeframe, which is revealed by the departure time and not the arrival time. The rows with "trip_id" corresponding to a trip_id in ```trips``` are kept. If a given "departure_time" is after midnight, and the given trip started before midnight, the time given is above 24:00, i.e. 02:14 is represented as 26:14. This format cannot be handled in the datetime class, and all "departure_time" values are therefore redone to fit to the conventional notation. Then the variable "time" is added, calculated by subtracting the previous "departure_time" from the current. The value is in the difftime format in seconds. If a row has "stop_sequence" = 0, the corresponding "time" value is also set to 0, as this is the startingpoint of the trip. Additionally, "time" values below 0, are added with 86400 (the number of seconds in 24 hours), as these represent time across midnight. Then the ```stop_times``` data frame is merged with ```trips```, resulting in a data frame with the following variables: "trip_id", "departure_time", "stop_id", "stop_sequence", "time", "route_id", "service_id", "direction_id", "shape_id", which is saved to ```in/preprocessed/GTFS_prep/stop_times.csv```. Then all unique combinations of "stop_id", "stop_sequence", "time", "route_id", "service_id", "direction_id" and "shape_id" are extracted, as ```stops_routes``` and saved to ```in/preprocessed/GTFS_prep/stops_routes.csv```.

    - ```stops.txt```: "stop_id", "stop_name", "stop_lon" and "stop_lat" are used. The geodetic coordinates are in CRS WGS84, and used in converting the dataframe to an sf object with ESPG: 4326, and then transformed to planarcoordinates with ESPG: 25832. Then all stops within any polygon from ```EDU``` (the buffers around the study programme locations) are assigned a 1 and the rest a 0, in the new column "intersect", to be able to distinct between the stops. Lastly, the shapefile is saved to ```in/preprocessed/GTFS_prep/stops.shp```. 

    - ```shapes.txt```: "shape_id", "shape_pt_lon", "shape_pt_lat" and "shape_pt_sequence" were used. The geodetic coordinates are in CRS WGS84, and used in converting the dataframe to an sf object with ESPG: 4326, and then transformed to planarcoordinates with ESPG: 25832. The the POINT geometries are cast to LINESTRING geometries, in the order defined by "shape_pt_sequence". Resulting in an sf object, ```shapes``` with one row per unique "shape_id" and "geometry", which is saved to ```in/preprocessed/GTFS_prep/shapes.shp``` 

    - ```calendar.txt```: "service_id", "start_date", "end_date" as well as "monday" to "sunday" are used. The "service_id"s not present in ```routes_stops``` are removed. 

    - ```calendar_dates.txt```: "service_id", "date" and "exception_type" are used. The The "service_id"s not present in ```routes_stops``` are removed. Then the values in the "date" column are defined as date objects (as.Date) and the "service_id" is converted to character. 

- When the raw data has been pre-processed, further pre-processing is conducted to retrieve; information on when different trips are in service (to be able to identify differences between weekdays and weekends), information on mean waitining time for the individual stops (to get a more accurate look at the distance reached within a time limit) and finally information on the distances possible to travel from the different stops that lie within the 500 meter buffers from all the included study programmes. 

    - The data used for this analysis includes information on trips and service in the date range 22/04/2024 to 17/07/2024 (the first day being a monday). To identify wheter or not each trip is in service on any given day in this range, a matrix is made, ```calendar_matrix```, with one column per "date" in the range and one row per included "service_id". The matrix is populated by 1s and 0s, conditioned on whether a given service_id indicates service on a specific date using ```calendar```. Then the ```calendar_dates``` data frame is used to include the exceptions. For each row in ```calendar_date``` the matrix cells with the corresponding "date" and "service_id" is either filled with a 0, (if the "exception_type" = 2) or a 1 (if "exception_type" = 2). The final matrix is saved as an RData file (at ```in/preprocessed/GTFS_prep/calendar_matrix.RData```), as it is large and takes a while to run. 

    - To approach a nuanced view of the differences from the different study programmes, the waiting times are included when calculating distance traveled within the given time limits. "wait" is calculated and by extracting all rows from the ```stop_times``` data frame, where "stop_id" represents a stop that lies within a buffer around a study program. Then the data fram is arranged by "stop_id", "service_id" and the "departure_time", and grouped by "stop_id" and "service_id", finally the "wait" value is calculated by subtracting "departure_time" from the previous "departure_time". To be able to handle each 24 hours as a 'loop' the first departure of the day has to be related back to the previous (in other words; the latest departure). This is done by extracting the first and last row from all groups, then arranging "departure_time" in descending order, and calculating the "wait", then the first rows from each group are merged with the initial data frame (replacing the duplicate rows). Finally the dataframe is saved to ```in/preprocessed/stop_wait.csv```


    - 




### Analysis 

format: 


|CODE|STATUS|LIMIT|WEEK|DIST|
|----|------|-----|----|--------|
|Description of group (e.g. the programme)|The binary predictor (e.g. new or old)|Time limits(e.g. 5, 20, 45 minutes)|The type of day the service occurs (e.g. weekday or weekend)|The outcome; the maximum distance possibly travelled|