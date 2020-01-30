Getting Start
-------------

We will be looking at bike crash data for North Carolina collected by
the North Carolina Department of Transportation between 2007-2018. This
data can be downloaded from the Durham open data website:
<a href="https://live-durhamnc.opendata.arcgis.com/datasets/ncdot-bike-crash-data" class="uri">https://live-durhamnc.opendata.arcgis.com/datasets/ncdot-bike-crash-data</a>.

Now let’s import the data:

``` r
the_file <- "/Users/strykerw/Downloads/bikecrashnew.csv" ## the downloaded file should say NCDOT_Bike_Crash_Data. I changed the file name for personal purposes, but you should import according to how you saved it on your computer. Just make sure the file is CSV format

df <- read.csv(the_file) ## open a CSV

head(df) ## use this function to see the column names and the first six rows of the data.frame (df) we opened
```

    ##           X        Y OBJECTID AmbulanceR BikeAge BikeAgeGrp BikeAlcDrg
    ## 1 -78.88390 36.03949        1        Yes      11     15-Nov          .
    ## 2 -78.78280 35.75112        2        Yes      20      20-24          .
    ## 3 -80.69782 35.08473        3        Yes      37      30-39          .
    ## 4 -80.47932 35.68440        4        Yes      30      30-39          .
    ## 5 -78.90445 34.99943        5        Yes      45      40-49          .
    ## 6 -80.47759 35.66667        6        Yes      58      50-59          .
    ##   BikeAlcFlg        BikeDir BikeInjury                                  BikePos
    ## 1         No   With Traffic          3 Sidewalk / Crosswalk / Driveway Crossing
    ## 2         No Facing Traffic          2 Sidewalk / Crosswalk / Driveway Crossing
    ## 3         No        Unknown          3                              Non-Roadway
    ## 4         No   With Traffic          2                              Travel Lane
    ## 5         No   With Traffic          3                              Travel Lane
    ## 6         No   With Traffic          3 Sidewalk / Crosswalk / Driveway Crossing
    ##   BikeRace BikeSex         City     County CrashAlcoh  CrashDay
    ## 1    Black    Male       Durham     Durham         No   Tuesday
    ## 2 Hispanic    Male         Cary       Wake         No    Friday
    ## 3    Black    Male    Stallings      Union         No    Monday
    ## 4    White    Male    Salisbury      Rowan         No    Friday
    ## 5    Black    Male Fayetteville Cumberland         No    Friday
    ## 6    White    Male    Salisbury      Rowan         No Wednesday
    ##                                              CrashGrp CrashHour
    ## 1                Parallel Paths - Other Circumstances        16
    ## 2  Motorist Failed to Yield - Signalized Intersection         9
    ## 3                                         Non-Roadway        17
    ## 4                          Motorist Left Turn / Merge        17
    ## 5                       Motorist Overtaking Bicyclist        12
    ## 6 Bicyclist Failed to Yield - Signalized Intersection         9
    ##           CrashLoc CrashMonth CrashSevr
    ## 1 Non-Intersection    January         3
    ## 2     Intersection    January         2
    ## 3      Non-Roadway    January         3
    ## 4     Intersection    January         2
    ## 5 Non-Intersection    January         3
    ## 6     Intersection    January         3
    ##                                       CrashType CrashYear  Developmen DrvrAge
    ## 1            Bicyclist Ride Out - Parallel Path      2007 Residential      35
    ## 2        Motorist Drive Out - Right Turn on Red      2007 Residential      64
    ## 3                                   Non-Roadway      2007  Commercial      39
    ## 4       Motorist Left Turn - Opposite Direction      2007  Commercial     999
    ## 5       Motorist Overtaking - Bicyclist Swerved      2007  Commercial      51
    ## 6 Bicyclist Ride Out - Signalized  Intersection      2007 Residential     999
    ##   DrvrAgeGrp DrvrAlcDrg DrvrAlcFlg DrvrInjury        DrvrRace DrvrSex
    ## 1      30-39          .         No          1           White    Male
    ## 2      60-69          .         No          1           White    Male
    ## 3      30-39          .         No          1           White  Female
    ## 4    Unknown          .         No          0 Unknown/Missing Unknown
    ## 5      50-59          .         No          1           Black  Female
    ## 6    Unknown          .         No          0 Unknown/Missing Unknown
    ##      DrvrVehTyp HitRun Latitude LightCond               Locality Longitude
    ## 1 Passenger Car     No 36.03949  Daylight Urban (>70% Developed) -78.88390
    ## 2 Passenger Car     No 35.75112  Daylight Urban (>70% Developed) -78.78280
    ## 3 Passenger Car     No 35.08473      Dusk Urban (>70% Developed) -80.69782
    ## 4 Sport Utility    Yes 35.68440  Daylight Urban (>70% Developed) -80.47932
    ## 5           Van     No 34.99943  Daylight Urban (>70% Developed) -78.90445
    ## 6 Passenger Car    Yes 35.66667  Daylight Urban (>70% Developed) -80.47759
    ##   NumBicsAin NumBicsBin NumBicsCin NumBicsKil NumBicsNoi NumBicsTot NumBicsUin
    ## 1          .          .          .          .          .          .          .
    ## 2          .          .          .          .          .          .          .
    ## 3          .          .          .          .          .          .          .
    ## 4          .          .          .          .          .          .          .
    ## 5          .          .          .          .          .          .          .
    ## 6          .          .          .          .          .          .          .
    ##   NumLanes NumUnits       RdCharacte               RdClass RdConditio
    ## 1   1 lane        2 Straight - Level          Local Street        Dry
    ## 2  3 lanes        2 Straight - Grade          Local Street        Dry
    ## 3  2 lanes        2 Straight - Level Public Vehicular Area        Dry
    ## 4  2 lanes        2 Straight - Grade          Local Street        Dry
    ## 5  2 lanes        2 Straight - Level          Local Street        Dry
    ## 6  2 lanes        2 Straight - Grade          Local Street        Dry
    ##                               RdConfig RdDefects             RdFeature
    ## 1 Two-Way, Divided, Unprotected Median      None    No Special Feature
    ## 2 Two-Way, Divided, Unprotected Median      None Four-Way Intersection
    ## 3                 Two-Way, Not Divided      None    No Special Feature
    ## 4                 Two-Way, Not Divided      None Four-Way Intersection
    ## 5                 Two-Way, Not Divided      None    No Special Feature
    ## 6                 Two-Way, Not Divided      None Four-Way Intersection
    ##        RdSurface   Region RuralUrban   SpeedLimit
    ## 1 Smooth Asphalt Piedmont      Urban 30 - 35  MPH
    ## 2 Smooth Asphalt Piedmont      Urban 30 - 35  MPH
    ## 3 Smooth Asphalt Piedmont      Urban 20 - 25  MPH
    ## 4 Smooth Asphalt Piedmont      Urban 30 - 35  MPH
    ## 5 Coarse Asphalt  Coastal      Urban 30 - 35  MPH
    ## 6 Smooth Asphalt Piedmont      Urban 30 - 35  MPH
    ##                            TraffCntrl Weather Workzone
    ## 1                  No Control Present   Clear       No
    ## 2                  Stop And Go Signal   Clear       No
    ## 3                  No Control Present  Cloudy       No
    ## 4                  No Control Present  Cloudy       No
    ## 5 Double Yellow Line, No Passing Zone   Clear       No
    ## 6                  Stop And Go Signal   Clear       No

When you click the **Knit** button a document will be generated that
includes both content as well as the output of any embedded R code
chunks within the document. You can embed an R code chunk like this:

``` r
summary(cars)
```

    ##      speed           dist       
    ##  Min.   : 4.0   Min.   :  2.00  
    ##  1st Qu.:12.0   1st Qu.: 26.00  
    ##  Median :15.0   Median : 36.00  
    ##  Mean   :15.4   Mean   : 42.98  
    ##  3rd Qu.:19.0   3rd Qu.: 56.00  
    ##  Max.   :25.0   Max.   :120.00

Including Plots
---------------

You can also embed plots, for example:

![](testcrash_files/figure-markdown_github/pressure-1.png)

Note that the `echo = FALSE` parameter was added to the code chunk to
prevent printing of the R code that generated the plot.
