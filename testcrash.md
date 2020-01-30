Getting Started
---------------

We will be looking at bike crash data for North Carolina collected by
the North Carolina Department of Transportation between 2007-2018. This
data can be downloaded from the Durham open data website:
<a href="https://live-durhamnc.opendata.arcgis.com/datasets/ncdot-bike-crash-data" class="uri">https://live-durhamnc.opendata.arcgis.com/datasets/ncdot-bike-crash-data</a>.

Now let’s import the data:

``` r
the_file <- "/Users/strykerw/Downloads/bikecrashnew.csv" ## the downloaded file should say NCDOT_Bike_Crash_Data. I changed the file name for personal purposes, but you should import according to how you saved it on your computer. Just make sure the file is in CSV format

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

As you can see, the column headings are straight forward. You can change
them if you’d like using the names(df)function: names(df) \<- c(“insert
column name here”,“insert column name here”…). I am going to keep my
columns as they are.

We must now install the ggplot2 and RColorBrewer libraries. We will need
them later.

``` r
#install.packages("ggplot2") ## take out the hash-symbol at the beginning of this line if you want to run this line in R. 
#install.packages("RColorBrewer")
#After installing the packages you need to open the libraries.
library(ggplot2)
library(RColorBrewer)
```

Density
-------

When first looking at the data, I just wanted to see a general trend of
when bike crashes were happening per hour. The density function allows
us to look at the percent occurrence of all data points across one
variable. In this instance I wanted to look at the data (which was 11266
NC bike crash incidents that ocurred between 2007-2018) by the hour time
dimension within a day.

``` r
p <- ggplot(df, aes(x=CrashHour)) + 
  geom_density() ##the x value should be equal to the CrashHour column because that indicates what time of day the crash ocurred. The geom_density() function will then plot all points in the data frame (the crash incidents) corresponding to that variable
p ## we set p equal to the density function so this will now plot p
```

![](testcrash_files/figure-markdown_github/unnamed-chunk-3-1.png)

As you can see, most crashes occur around afternoon rush hour (around
the 17th hour of the day, or 5pm). It is interesting, however, that
there are not two peaks— one being for the morning rush hour as well.
This can indicate that policy makers may need to focus safety efforts on
afternoon rush hour commute times.

Frequency Polygon
-----------------

This graph is interesting, but let’s add another variable: the race of
the cyclist in the accident. Perhaps differences in crashes throughout
the day among races may indicate different patterns in travel behavior
(for example, different races may be commuting more frequently at
different hours of the day). To incorporate this other variable, we will
need to use the frequency polygon function.

``` r
p <- ggplot(df, aes(x=CrashHour, colour=BikeRace)) + geom_freqpoly(binwidth=1) +
  scale_x_continuous(breaks=c(0,2,4,6,8,10,12,14,16,18,20,22,24))+ labs (title = "Crash Frequency per Hour by Race of NC Cyclists", x = "Crash Hour", y = "Number of Crashes")
p ## you can see the process of the code explained below the graphic
```

![](testcrash_files/figure-markdown_github/unnamed-chunk-4-1.png)

``` r
## We continued to use the CrashHour column as the x variable (because it is the time element). We can also differentiate the frequency lines of crash incidents by race, and make them visibly different by default colors by setting colour = Bike Race. Note: bike race is the column in the data set that corresponds with the race of the cyclist who crashed.

## binwidth deals with the scale of the x value. I played with changing the binwidth to best display the data, but let's choose a bandwidth of 1 for now. Unlike the density function, the geom_freqpoly function shows the raw frequency of crashes, and I categorized this by race over the time variable of crash hour.

## the scale_x function_continous() function allows you to manually change the breaks on the axes. I manually changed the breaks to show numbers for every two hours within a day along the x-axis. The labs function then allows you to specify the title of the visualization (title = "name  here"), the title of the x-axis (x = "namehere"), and the title of the y-axis ("name here")

## then plot p (what we assigned the function to)
```

This visualization provides us with a better idea of how bike crash
occurences within the last decade have been distributed across the day
by race, and the comprehensiveness of the data set allow us to see a
clearer trend. Crashes for almost every race peak at the 5pm rush hour
time, but it also gives you an idea of bike ridership: Whites and Blacks
get in more crashes, and this is likely because more of them ride bikes.
It would be interesting in the future to look at this data
proportionally in order to compare crash occurrence by race vs the
number of active cyclists within that race.

This data can continue to be manipulated, but let’s look at what my
project partners have visualized with the same data!

Note: you can also use the csv file to filter the data by city, county,
etc. I saved the data into a new csv file that only included bike
crashes within Orange County to see if crash incidences by race across
the day vary from the state-level data.
