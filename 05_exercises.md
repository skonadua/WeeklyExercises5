---
title: 'Weekly Exercises #5'
author: "Stephanie Konadu-Acheampong with help from Jennifer Huang"
output: 
  html_document:
    keep_md: TRUE
    toc: TRUE
    toc_float: TRUE
    df_print: paged
    code_download: true
    code_folding: hide 
---





```r
library(tidyverse)     # for data cleaning and plotting
```

```
## -- Attaching packages --------------------------------------- tidyverse 1.3.0 --
```

```
## v ggplot2 3.3.3     v purrr   0.3.4
## v tibble  3.0.5     v dplyr   1.0.3
## v tidyr   1.1.2     v stringr 1.4.0
## v readr   1.4.0     v forcats 0.5.0
```

```
## -- Conflicts ------------------------------------------ tidyverse_conflicts() --
## x dplyr::filter() masks stats::filter()
## x dplyr::lag()    masks stats::lag()
```

```r
library(gardenR)       # for Lisa's garden data
library(lubridate)     # for date manipulation
```

```
## 
## Attaching package: 'lubridate'
```

```
## The following objects are masked from 'package:base':
## 
##     date, intersect, setdiff, union
```

```r
library(openintro)     # for the abbr2state() function
```

```
## Loading required package: airports
```

```
## Loading required package: cherryblossom
```

```
## Loading required package: usdata
```

```r
library(palmerpenguins)# for Palmer penguin data
library(maps)          # for map data
```

```
## 
## Attaching package: 'maps'
```

```
## The following object is masked from 'package:purrr':
## 
##     map
```

```r
library(ggmap)         # for mapping points on maps
```

```
## Google's Terms of Service: https://cloud.google.com/maps-platform/terms/.
```

```
## Please cite ggmap if you use it! See citation("ggmap") for details.
```

```r
library(gplots)        # for col2hex() function
```

```
## 
## Attaching package: 'gplots'
```

```
## The following object is masked from 'package:stats':
## 
##     lowess
```

```r
library(RColorBrewer)  # for color palettes
library(sf)            # for working with spatial data
```

```
## Linking to GEOS 3.8.0, GDAL 3.0.4, PROJ 6.3.1
```

```r
library(leaflet)       # for highly customizable mapping
library(ggthemes)      # for more themes (including theme_map())
library(plotly)        # for the ggplotly() - basic interactivity
```

```
## 
## Attaching package: 'plotly'
```

```
## The following object is masked from 'package:ggmap':
## 
##     wind
```

```
## The following object is masked from 'package:ggplot2':
## 
##     last_plot
```

```
## The following object is masked from 'package:stats':
## 
##     filter
```

```
## The following object is masked from 'package:graphics':
## 
##     layout
```

```r
library(gganimate)     # for adding animation layers to ggplots
library(transformr)    # for "tweening" (gganimate)
```

```
## 
## Attaching package: 'transformr'
```

```
## The following object is masked from 'package:sf':
## 
##     st_normalize
```

```r
library(gifski)        # need the library for creating gifs but don't need to load each time
library(shiny)         # for creating interactive apps
theme_set(theme_minimal())
```


```r
# SNCF Train data
small_trains <- read_csv("https://raw.githubusercontent.com/rfordatascience/tidytuesday/master/data/2019/2019-02-26/small_trains.csv") 
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   year = col_double(),
##   month = col_double(),
##   service = col_character(),
##   departure_station = col_character(),
##   arrival_station = col_character(),
##   journey_time_avg = col_double(),
##   total_num_trips = col_double(),
##   avg_delay_all_departing = col_double(),
##   avg_delay_all_arriving = col_double(),
##   num_late_at_departure = col_double(),
##   num_arriving_late = col_double(),
##   delay_cause = col_character(),
##   delayed_number = col_double()
## )
```

```r
# Lisa's garden data
data("garden_harvest")

# Lisa's Mallorca cycling data
mallorca_bike_day7 <- read_csv("https://www.dropbox.com/s/zc6jan4ltmjtvy0/mallorca_bike_day7.csv?dl=1") %>% 
  select(1:4, speed)
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   ele.num = col_double(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = ""),
##   time_hr = col_double(),
##   dist_km = col_double(),
##   speed = col_double()
## )
```

```r
# Heather Lendway's Ironman 70.3 Pan Am championships Panama data
panama_swim <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_swim_20160131.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   ele = col_logical(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
panama_bike <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_bike_20160131.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
panama_run <- read_csv("https://raw.githubusercontent.com/llendway/gps-data/master/data/panama_run_20160131.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   lon = col_double(),
##   lat = col_double(),
##   ele = col_double(),
##   time = col_datetime(format = ""),
##   extensions = col_double(),
##   event = col_character(),
##   date = col_date(format = ""),
##   hrminsec = col_datetime(format = "")
## )
```

```r
#COVID-19 data from the New York Times
covid19 <- read_csv("https://raw.githubusercontent.com/nytimes/covid-19-data/master/us-states.csv")
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   date = col_date(format = ""),
##   state = col_character(),
##   fips = col_character(),
##   cases = col_double(),
##   deaths = col_double()
## )
```

## Put your homework on GitHub!

Go [here](https://github.com/llendway/github_for_collaboration/blob/master/github_for_collaboration.md) or to previous homework to remind yourself how to get set up. 

Once your repository is created, you should always open your **project** rather than just opening an .Rmd file. You can do that by either clicking on the .Rproj file in your repository folder on your computer. Or, by going to the upper right hand corner in R Studio and clicking the arrow next to where it says Project: (None). You should see your project come up in that list if you've used it recently. You could also go to File --> Open Project and navigate to your .Rproj file. 

## Instructions

* Put your name at the top of the document. 

* **For ALL graphs, you should include appropriate labels.** 

* Feel free to change the default theme, which I currently have set to `theme_minimal()`. 

* Use good coding practice. Read the short sections on good code with [pipes](https://style.tidyverse.org/pipes.html) and [ggplot2](https://style.tidyverse.org/ggplot2.html). **This is part of your grade!**

* **NEW!!** With animated graphs, add `eval=FALSE` to the code chunk that creates the animation and saves it using `anim_save()`. Add another code chunk to reread the gif back into the file. See the [tutorial](https://animation-and-interactivity-in-r.netlify.app/) for help. 

* When you are finished with ALL the exercises, uncomment the options at the top so your document looks nicer. Don't do it before then, or else you might miss some important warnings and messages.

## Warm-up exercises from tutorial

  1. Choose 2 graphs you have created for ANY assignment in this class and add interactivity using the `ggplotly()` function.
  
*Original Plot*


```r
garden_harvest %>%
  filter(vegetable == "tomatoes") %>% 
  ggplot(mapping = aes(y = variety, x = weight, color=months(date))) +
    geom_jitter(height = .25, width = .25, size = .80) + 
    ggtitle("Tomato Weight by Variety and Date Harvested") + 
    labs(x = " " , y = " ") + theme_solarized_2()
```

![](05_exercises_files/figure-html/unnamed-chunk-1-1.png)<!-- -->


*Plotly Plot*
  

```r
mygardengraph2 <- garden_harvest %>%
  filter(vegetable == "tomatoes") %>% 
  ggplot(mapping = aes(y = variety, x = weight, color=months(date))) +
    geom_jitter(height = .25, width = .25, size = .80) + 
    ggtitle("Tomato Weight by Variety and Date Harvested") + 
    labs(x = " " , y = " ") + theme_solarized_2()

ggplotly(mygardengraph2, 
         tooltip = c("text", "x"))
```

```{=html}
<div id="htmlwidget-05893077a741860ff24f" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-05893077a741860ff24f">{"x":{"data":[{"x":[435.094280529418,320.057731800945,618.968493177672,96.971514801844,435.869913148228,167.867742575705,508.970329862321,856.942270911997,335.944676799467,156.217311267043,211.034212295432,102.24671179289,307.956903322367,387.204171739519,230.775810366031,73.0821549193934,339.111189337214,118.149933382636,563.123564162175,290.233268668526,781.193422033451,222.84984226618,381.910908191116,217.051941786311,66.8653986805584,393.080392659176,306.774875372066,174.786225941731,302.903571320116,359.108796688379,355.76267248881,233.045793548692,364.064561115461,1045.05537033977,562.024618845549,292.081329772249,161.955651271623,81.0960951548768,564.102908896981,183.968197101378,178.923551422544,590.839224590571,1101.84959789843,308.245537270908,53.7666127366247,63.9509957747068,215.808937019669,240.866014886997,301.779241710086,306.799454928376,160.205158194294,217.75931891927,801.898306787712,353.995932776132,359.177601843025,505.84732133348,420.877349848859,332.23516278551,726.963534200564,641.937149345526,413.150177186588,710.896955110831,237.794430160546,525.109415867599,180.76672816521,266.139838921605,489.868924945244,126.240911550587,476.786602888373,328.166344071273,543.102698351024,599.170774270548,560.047639987548,291.237605143688,237.932673659758,396.985766558908,364.002799137728,305.056394267944,588.228941332083,764.004103341606,435.833195131388,305.975380174932,608.073962247698,135.982857761206,148.105770393508,317.027811976965,104.915646711015,271.016470192466,872.117741366616,578.859267688589,615.216317786602,996.84678671218,334.984669086756,264.195886100177,451.176767139928,306.125719303731,332.80758825806,483.175486270222,631.927527722437,359.968876369298,230.162256549811,343.856906424859,1009.85244377819,492.754190838197,1600.98980790703,842.07687213819,1537.89826930559,427.843449232983,243.072638147743,329.867049783119,264.993353728554,561.930541168549,1541.93518035999,800.928055254626,436.18624658999,1573.1440680183,703.964707756299,445.966756601469,268.946124799317,75.1770781273954,578.182703186409,871.084154246841,115.133948891773,629.218608872732,487.916900795884,505.840689190663,1400.08717336832,993.124943384435,1026.20792762248,1885.95543602819,665.763069024542,1042.01662130083,592.785765808891,215.789782592328,308.971160255838,497.198214632459,260.866968815564,819.15666435007,379.817768226727,736.937729625613,1033.12846517097,1096.86868814623,566.127479361719,860.759283541236,459.882519417792,2933.82203945995,599.012716899393,154.784071669099,822.146140077501,588.938334477716,392.767005997826,751.770903358352,833.029995134915],"y":[5.14431442506611,6.06828391249292,7.20195466163568,0.840247295564041,3.75263821089175,8.11062358738855,0.861322251032107,4.15930470416788,11.1089243328897,5.19750416534953,2.01305294572376,7.91422142763622,1.95696860714816,4.86277266091201,5.82617858145386,11.774926101556,10.1314587024972,7.9966015603859,4.95071510830894,6.17724902182817,10.0857334861066,3.22108212392777,1.21644162305165,8.15744309267029,12.008879214176,4.14813083666377,2.79393179086037,0.75625215144828,6.89441617217381,5.19341225782409,6.09230206033681,11.0053996780189,10.2217011122266,1.76309679797851,9.03635636775289,7.83959511318244,2.79786039388273,7.9457497401163,5.11259625200182,8.75164987239987,5.06620547338389,8.83027086697984,2.02540623885579,6.97756306023803,12.1069863796001,7.84793707577046,6.76828502130229,9.21727637690492,7.94293509039562,5.05573180434294,11.9996434361674,5.98841331235599,7.19611378281843,1.96307064278517,4.02830124704633,0.866280615329742,8.22672608820722,4.95113604923245,1.78612072090618,0.939646876766346,2.87762738426682,5.21513900614809,10.8536008539377,0.958742050570436,9.04401114757638,2.81831960484851,12.1152249806328,7.86680938431527,8.16451782814693,11.9141358876368,5.10161564964801,11.1815189179033,0.996484608505853,4.166810690891,2.12561759736855,2.85078685719054,5.18765382911079,6.24494106287602,1.24850690260064,1.85465878620744,7.76933009503409,12.0327680585906,9.87684344814625,8.20260634273291,11.798427869915,4.13623473513871,10.8186813411303,4.92667086236179,6.97445658920333,3.76885913382284,2.18762323458213,0.850531409727409,6.15512091584969,3.1072691072477,8.03438064001966,12.1085524427472,12.2079950317275,6.16967618127819,4.77461128961295,8.89416424860246,2.08637658529915,2.97790248109959,1.07110319531057,8.2364440667443,7.01824341248721,3.23148790502455,4.16600781236775,0.85714552400168,10.8821799471043,4.76896195765585,7.79130285722204,12.2023692922667,0.860205946373753,11.0255850118119,8.14361952291802,4.02682526083663,9.88459510274697,5.90069815027528,5.21052260021679,8.18822773755528,8.92193489836063,5.8749989727512,10.9063435443677,4.96266873145942,12.1983672238421,8.00609851290938,1.08104981936049,2.9345877468586,9.84840909997001,0.898267512326129,10.9710228405893,5.86835503368638,7.19398310978431,3.93632713227998,1.88253298855852,3.05900090164505,12.0020822916413,8.22050687437877,7.92322029056959,12.0964730384294,2.87816048704553,10.0281316603068,12.08520153258,11.1073881655466,6.06349358684383,0.835306831286289,6.98289952450432,5.24099591188133,11.9119955373462,10.0650941906497,2.13688845804427,9.02104231633712,8.08480917778797],"text":["weight:  435","weight:  320","weight:  619","weight:   97","weight:  436","weight:  168","weight:  509","weight:  857","weight:  336","weight:  156","weight:  211","weight:  102","weight:  308","weight:  387","weight:  231","weight:   73","weight:  339","weight:  118","weight:  563","weight:  290","weight:  781","weight:  223","weight:  382","weight:  217","weight:   67","weight:  393","weight:  307","weight:  175","weight:  303","weight:  359","weight:  356","weight:  233","weight:  364","weight: 1045","weight:  562","weight:  292","weight:  162","weight:   81","weight:  564","weight:  184","weight:  179","weight:  591","weight: 1102","weight:  308","weight:   54","weight:   64","weight:  216","weight:  241","weight:  302","weight:  307","weight:  160","weight:  218","weight:  802","weight:  354","weight:  359","weight:  506","weight:  421","weight:  332","weight:  727","weight:  642","weight:  413","weight:  711","weight:  238","weight:  525","weight:  181","weight:  266","weight:  490","weight:  126","weight:  477","weight:  328","weight:  543","weight:  599","weight:  560","weight:  291","weight:  238","weight:  397","weight:  364","weight:  305","weight:  588","weight:  764","weight:  436","weight:  306","weight:  608","weight:  136","weight:  148","weight:  317","weight:  105","weight:  271","weight:  872","weight:  579","weight:  615","weight:  997","weight:  335","weight:  264","weight:  451","weight:  306","weight:  333","weight:  483","weight:  632","weight:  360","weight:  230","weight:  344","weight: 1010","weight:  493","weight: 1601","weight:  842","weight: 1538","weight:  428","weight:  243","weight:  330","weight:  265","weight:  562","weight: 1542","weight:  801","weight:  436","weight: 1573","weight:  704","weight:  446","weight:  269","weight:   75","weight:  578","weight:  871","weight:  115","weight:  629","weight:  488","weight:  506","weight: 1400","weight:  993","weight: 1026","weight: 1886","weight:  666","weight: 1042","weight:  593","weight:  216","weight:  309","weight:  497","weight:  261","weight:  819","weight:  380","weight:  737","weight: 1033","weight: 1097","weight:  566","weight:  861","weight:  460","weight: 2934","weight:  599","weight:  155","weight:  822","weight:  589","weight:  393","weight:  752","weight:  833"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(248,118,109,1)","opacity":1,"size":3.02362204724409,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(248,118,109,1)"}},"hoveron":"points","name":"August","legendgroup":"August","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[23.9361048807623,86.1509691016981,137.226692526368,338.819746675435,30.9537531144451,139.773128248868,246.951568421558,220.048560420517,463.122395985527,106.033353237901,147.750556233223,800.792682181578,611.145458532614,203.177800054778,311.956372377812,314.793987003388,131.218497830094,152.767597487895,442.061847938574,239.809430978028,209.225780234556,40.1755306002451,90.8012302845018,307.04549230088,197.125354541466,633.024636042537,289.799933310249,99.9268246109132],"y":[8.11835451843217,8.07597969565541,2.77286173403263,5.22861737001222,8.09291643893812,5.12719293695409,6.93380740156863,2.24896137835458,1.24995980784297,8.22077897202689,5.01486996246967,10.2054316030117,11.0598663922865,2.85520785080735,1.78470168926287,8.76441758265719,7.96031683357432,4.88660618301947,1.77708240854554,7.07205170649104,0.85696107824333,8.20592678897083,8.19475732778665,7.10498413734604,1.20650164189283,11.0407634137664,2.20786690863315,7.7704323863145],"text":["weight:   24","weight:   86","weight:  137","weight:  339","weight:   31","weight:  140","weight:  247","weight:  220","weight:  463","weight:  106","weight:  148","weight:  801","weight:  611","weight:  203","weight:  312","weight:  315","weight:  131","weight:  153","weight:  442","weight:  240","weight:  209","weight:   40","weight:   91","weight:  307","weight:  197","weight:  633","weight:  290","weight:  100"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(124,174,0,1)","opacity":1,"size":3.02362204724409,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(124,174,0,1)"}},"hoveron":"points","name":"July","legendgroup":"July","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[252.190891568898,213.088494077092,346.139470193069,254.00575048395,362.892311161151,715.237542264746,272.052413343103,63.9527065451257,1376.91854425427,1977.2009660909,2477.93814053584,200.21745704941,374.94964904408,316.084955479484,898.139424170135,525.954303067643,385.809412813163,230.030329272267,859.231800053036,791.056646626792,1174.96965619037,417.856638716301,483.798152924632,219.081591851776,646.179638157249,2838.15752082551],"y":[1.23517420317512,9.8532392308116,8.79303703689948,9.93074041884392,10.8014295973117,0.953294326085597,2.91680617735256,11.8736202985747,7.80458001059014,12.0219898145879,0.883703049621545,10.0223093288951,4.23035585030448,2.98383689904585,11.1152775809169,1.75288124021608,5.13318755640648,12.1015220296104,10.0866477990057,2.89715789002366,0.983166012214497,6.22387587069534,11.1259187064134,7.02509269176517,1.8133425519336,11.975980603951],"text":["weight:  252","weight:  213","weight:  346","weight:  254","weight:  363","weight:  715","weight:  272","weight:   64","weight: 1377","weight: 1977","weight: 2478","weight:  200","weight:  375","weight:  316","weight:  898","weight:  526","weight:  386","weight:  230","weight:  859","weight:  791","weight: 1175","weight:  418","weight:  484","weight:  219","weight:  646","weight: 2838"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(0,191,196,1)","opacity":1,"size":3.02362204724409,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(0,191,196,1)"}},"hoveron":"points","name":"October","legendgroup":"October","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[1953.14793087414,805.191933275084,178.097031294368,201.093606977141,1536.92197817599,773.214674736955,1202.07478949381,1131.0986173806,610.138089727028,1264.97385835741,2160.14203951287,2899.2394195667,441.97163364361,1234.14619305544,1177.75328470359,254.902857688488,430.133972568787,2377.11982794781,709.882155840634,1317.14611498371,1648.84492186457,614.927278789342,692.094997587381,674.027682128013,1392.05707001023,315.905520234141,754.214473073953,413.100391184329,509.0632823325,258.034912248026,725.054928495316,212.039303577505,713.885915520368,227.758804828511,670.003649830585,1052.15743017406,1630.9229639601,2933.97288766829,303.837926766486,1058.02780063322,713.807152020279,94.8668306702748,476.895503478125,2737.80036507372,236.088305506157,1822.86099125119,818.761667723651,2006.23708253412,658.827615991817,1239.16017533338,1977.95767919032,1447.14647620963,494.213991272962,678.00163548789,70.0715659430716,326.931299546501],"y":[12.0610953755677,11.18910890806,6.14579709107056,6.85744525282644,1.01017269201111,8.82625351333991,9.78199010086246,8.13389026373625,11.8930196567671,3.2350485122297,0.917745469370857,2.04208056186326,8.03165016963612,11.8694529870991,9.16744035598822,9.90445101063233,5.92008167738095,12.0618378379149,4.82498391054105,1.03355011309031,3.19333412416745,7.99763864872511,1.16029510390945,11.094110566075,2.2113968989579,9.88581795641221,8.95118379371706,12.0179183839355,8.06893041089643,7.90085972042289,11.9390449166531,11.8298418518389,6.15692648210097,1.10574815922882,2.05211220460478,4.87133739329875,11.0868701165309,11.908577872673,3.17341409926303,7.80692255601753,4.90141821245197,12.0017898081569,5.16743303916883,1.11085093999282,4.21737788908649,10.882401993731,7.83683725027367,10.1753677832894,3.23056652303785,2.04726039618254,12.1632109901402,1.02784006029833,1.85713656817097,8.19547092681751,12.0441445594188,9.80852841422893],"text":["weight: 1953","weight:  805","weight:  178","weight:  201","weight: 1537","weight:  773","weight: 1202","weight: 1131","weight:  610","weight: 1265","weight: 2160","weight: 2899","weight:  442","weight: 1234","weight: 1178","weight:  255","weight:  430","weight: 2377","weight:  710","weight: 1317","weight: 1649","weight:  615","weight:  692","weight:  674","weight: 1392","weight:  316","weight:  754","weight:  413","weight:  509","weight:  258","weight:  725","weight:  212","weight:  714","weight:  228","weight:  670","weight: 1052","weight: 1631","weight: 2934","weight:  304","weight: 1058","weight:  714","weight:   95","weight:  477","weight: 2738","weight:  236","weight: 1823","weight:  819","weight: 2006","weight:  659","weight: 1239","weight: 1978","weight: 1447","weight:  494","weight:  678","weight:   70","weight:  327"],"type":"scatter","mode":"markers","marker":{"autocolorscale":false,"color":"rgba(199,124,255,1)","opacity":1,"size":3.02362204724409,"symbol":"circle","line":{"width":1.88976377952756,"color":"rgba(199,124,255,1)"}},"hoveron":"points","name":"September","legendgroup":"September","showlegend":true,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null}],"layout":{"margin":{"t":46.2864259028643,"r":7.97011207970112,"b":43.8356164383562,"l":123.536737235367},"plot_bgcolor":"rgba(238,232,213,1)","paper_bgcolor":"rgba(253,246,227,1)","font":{"color":"rgba(147,161,161,1)","family":"","size":15.9402241594022},"title":{"text":"Tomato Weight by Variety and Date Harvested","font":{"color":"rgba(101,123,131,1)","family":"","size":19.1282689912827},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-121.565734258614,3079.47472680767],"tickmode":"array","ticktext":["0","1000","2000","3000"],"tickvals":[0,1000,2000,3000],"categoryorder":"array","categoryarray":["0","1000","2000","3000"],"nticks":null,"ticks":"outside","tickcolor":"rgba(147,161,161,1)","ticklen":3.98505603985056,"tickwidth":0.724555643609193,"showticklabels":true,"tickfont":{"color":"rgba(147,161,161,1)","family":"","size":12.7521793275218},"tickangle":-0,"showline":true,"linecolor":"transparent","linewidth":0.724555643609193,"showgrid":true,"gridcolor":"rgba(253,246,227,1)","gridwidth":0.724555643609193,"zeroline":false,"anchor":"y","title":{"text":" ","font":{"color":"rgba(101,123,131,1)","family":"","size":15.9402241594022}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,12.6],"tickmode":"array","ticktext":["Amish Paste","Better Boy","Big Beef","Black Krim","Bonny Best","Brandywine","Cherokee Purple","grape","Jet Star","Mortgage Lifter","Old German","volunteers"],"tickvals":[1,2,3,4,5,6,7,8,9,10,11,12],"categoryorder":"array","categoryarray":["Amish Paste","Better Boy","Big Beef","Black Krim","Bonny Best","Brandywine","Cherokee Purple","grape","Jet Star","Mortgage Lifter","Old German","volunteers"],"nticks":null,"ticks":"outside","tickcolor":"rgba(147,161,161,1)","ticklen":3.98505603985056,"tickwidth":0.724555643609193,"showticklabels":true,"tickfont":{"color":"rgba(147,161,161,1)","family":"","size":12.7521793275218},"tickangle":-0,"showline":true,"linecolor":"transparent","linewidth":0.724555643609193,"showgrid":true,"gridcolor":"rgba(253,246,227,1)","gridwidth":0.724555643609193,"zeroline":false,"anchor":"x","title":{"text":" ","font":{"color":"rgba(101,123,131,1)","family":"","size":15.9402241594022}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":true,"legend":{"bgcolor":"rgba(253,246,227,1)","bordercolor":"transparent","borderwidth":2.06156048675734,"font":{"color":"rgba(147,161,161,1)","family":"","size":12.7521793275218},"y":0.929133858267717},"annotations":[{"text":"months(date)","x":1.02,"y":1,"showarrow":false,"ax":0,"ay":0,"font":{"color":"rgba(101,123,131,1)","family":"","size":15.9402241594022},"xref":"paper","yref":"paper","textangle":-0,"xanchor":"left","yanchor":"bottom","legendTitle":true}],"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"300c2e55e98":{"x":{},"y":{},"colour":{},"type":"scatter"}},"cur_data":"300c2e55e98","visdat":{"300c2e55e98":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```
  
  *Original Plot* 
  

```r
garden_med3 <- garden_harvest %>%
  filter(vegetable == "tomatoes") %>% 
  group_by(variety) %>% 
  mutate(pounds = (weight * .0022046)) %>% 
  mutate(medweight = sum(pounds))
  

garden_med3 %>%
  mutate(uppercase = str_to_title(variety))%>%
  arrange(medweight.by_group = variety) %>%
  ggplot(mapping = aes(x = pounds, y = fct_reorder(uppercase, medweight))) +
  geom_bar(stat="identity", aes(fill=month(date), label = TRUE)) +
  ggtitle("Cumulative Tomato Weight (Grams) by Variety and Date Harvested") +
  labs(x = "" ,
       y = "") +
  theme_minimal() +
  theme(plot.title.position= "plot", panel.grid.major = element_blank(), panel.grid.minor = element_blank()) 
```

```
## Warning: Ignoring unknown aesthetics: label
```

![](05_exercises_files/figure-html/unnamed-chunk-3-1.png)<!-- -->
  
  
*Plotly Plot*   
  

```r
garden_med3 <- garden_harvest %>%
  filter(vegetable == "tomatoes") %>% 
  group_by(variety) %>% 
  mutate(pounds = (weight * .0022046)) %>% 
  mutate(medweight = sum(pounds))
  

mygardengraph <- garden_med3 %>%
  mutate(uppercase = str_to_title(variety))%>%
  arrange(medweight.by_group = variety) %>%
  ggplot(mapping = aes(x = pounds, y = fct_reorder(uppercase, medweight))) +
  geom_bar(stat="identity", aes(fill=month(date), label = TRUE)) +
  ggtitle("Cumulative Tomato Weight (Grams) by Variety and Date Harvested") +
  labs(x = "" ,
       y = "") +
  theme_minimal() +
  theme(plot.title.position= "plot", panel.grid.major = element_blank(), panel.grid.minor = element_blank()) 
```

```
## Warning: Ignoring unknown aesthetics: label
```

```r
ggplotly(mygardengraph,
         tooltip = c("text", "x"))
```

```{=html}
<div id="htmlwidget-6721bedc10c10fd4096d" style="width:672px;height:480px;" class="plotly html-widget"></div>
<script type="application/json" data-for="htmlwidget-6721bedc10c10fd4096d">{"x":{"data":[{"orientation":"v","width":[1.0207298,0.4607614,0.4343062,0.485012,0.6878352,0.9744332,0.639334,0.3020302,0.4475338,0.7473594,0.308644,0.3262808,0.3373038,0.5445362,0.529104,0.6768122,0.0529104,0.1895956,0.0683426,0.2336876,0.2888026,0.088184,0.2006186,0.22046,0.694449,1.7658846,1.3470106,1.3955118],"base":[11.55,11.55,11.55,9.55,9.55,9.55,9.55,5.55,5.55,4.55,4.55,4.55,4.55,2.55,2.55,2.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,0.55,6.55,7.55,7.55],"x":[0.5103649,1.2511105,1.6986443,0.242506,0.8289296,1.6600638,2.4669474,0.1510151,0.5257971,0.3736797,0.9016814,1.2191438,1.5509361,0.2722681,0.8090882,1.4120463,0.0264552,0.1477082,0.2766773,0.4276924,0.6889375,0.8774308,1.0218321,1.2323714,0.3472245,0.8829423,0.6735053,2.0447665],"y":[0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.9,0.9,0.899999999999999,0.899999999999999],"text":["pounds: 1.0207298","pounds: 0.4607614","pounds: 0.4343062","pounds: 0.4850120","pounds: 0.6878352","pounds: 0.9744332","pounds: 0.6393340","pounds: 0.3020302","pounds: 0.4475338","pounds: 0.7473594","pounds: 0.3086440","pounds: 0.3262808","pounds: 0.3373038","pounds: 0.5445362","pounds: 0.5291040","pounds: 0.6768122","pounds: 0.0529104","pounds: 0.1895956","pounds: 0.0683426","pounds: 0.2336876","pounds: 0.2888026","pounds: 0.0881840","pounds: 0.2006186","pounds: 0.2204600","pounds: 0.6944490","pounds: 1.7658846","pounds: 1.3470106","pounds: 1.3955118"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(19,43,67,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[0.2138462,1.1221414,0.842157199999999,0.385805,1.1155276,1.4153532,1.157415,1.234576,1.2963048,2.1979862,2.226646,0.943568800000001,3.3994932,3.08644,4.1578756,6.4682964,0.4651706,0.6790168,2.303807,2.4294692,0.7804284,1.6027442,0.524694800000001,1.6843144,1.355829,0.507058000000001,0.6812214,0.866407800000001,0.4916258,0.6768122,0.3571452,0.9104998,0.5864236,0.8752262,0.5820144,0.758382399999999,1.8562732,2.1891678,1.0956862,2.2773518,0.9612056,1.8893422,0.8664078,0.7914514,0.641538600000001,0.6988582,1.2764634,3.3906748,3.4678358,0.4761936,0.959001,0.3439176,0.8531802,1.2411898,0.791451400000001,1.2433944,0.3946234,0.676812200000001,0.731927199999999,1.5674706,1.1970978,0.802474399999999,0.597446600000001,1.3933072,0.727518,0.5930374,1.3866934,0.341713000000002,0.705472,0.5092626,0.639334,0.7848376,0.4806028,0.672403,0.738541,1.0648218,0.9832516,1.9202066,2.2971932,1.014116,1.3646474,0.6679938,0.6790168,0.4761936,1.7680892,1.9224112,3.5295646,1.3073278,1.3205554,0.3703728,0.2248692,0.2601428,0.4783982,0.6437432,0.1785726,0.1410944,0.6657892,0.9281366,0.277779600000001,1.0515942,0.9612056,0.2998256,0.9942746,1.0868678,0.584218999999999,0.961205600000001,0.165345,1.1155276,1.8055674,0.837747999999999,1.8364318,1.2389852,0.4056464,1.3029186,0.5313086,0.3990326,0.793655999999999,1.2742588,1.6578592,0.7473594,1.7217926,0.8024744,1.3403968,1.5520384,2.2619196,2.4184462,1.2985094,0.7407456,0.5136718,0.5246948,1.3205554,0.231483,0.5357178,1.7658846,0.253528999999999,1.4682636,1.8981606,0.1609358,0.1477082,0.1190484,0.352736,1.080254,0.7231088,0.6746076,0.3262808,0.6746076,0.7341318,1.2389852,1.0758448,0.5754006,1.6247902,1.2478036,1.8121812],"base":[11.55,11.55,11.55,11.55,11.55,11.55,11.55,11.55,11.55,11.55,11.55,11.55,11.55,11.55,11.55,11.55,9.55,9.55,9.55,9.55,9.55,9.55,9.55,9.55,9.55,9.55,9.55,9.55,5.55,5.55,5.55,5.55,5.55,5.55,5.55,5.55,5.55,5.55,5.55,5.55,3.55,3.55,3.55,3.55,3.55,3.55,3.55,3.55,3.55,3.55,4.55,4.55,4.55,4.55,4.55,4.55,4.55,4.55,4.55,4.55,4.55,4.55,4.55,4.55,4.55,4.55,4.55,4.55,1.55,1.55,1.55,1.55,1.55,1.55,1.55,1.55,1.55,1.55,1.55,1.55,2.55,2.55,2.55,2.55,2.55,2.55,2.55,2.55,2.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,0.55,0.55,0.55,0.55,0.55,0.55,0.55,0.55,6.55,6.55,6.55,6.55,6.55,6.55,6.55,6.55,7.55,7.55,7.55,7.55,7.55,7.55,7.55,7.55,7.55,7.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55],"x":[2.0227205,2.6907143,3.6728636,4.2868447,5.037511,6.3029514,7.5893355,8.785331,10.0507714,11.7979169,14.010233,15.5953404,17.7668714,21.009838,24.6319958,29.9450818,3.0191997,3.5912934,5.0827053,7.4493434,9.0542922,10.2458785,11.309598,12.4141026,13.9341743,14.8656178,15.4597575,16.2335721,0.9953769,1.5795959,2.0965746,2.7303971,3.4788588,4.2096837,4.938304,5.6085024,6.9158302,8.9385507,10.5809777,12.2674967,0.4806028,1.9058767,3.2837517,4.1126813,4.8291763,5.4993747,6.4870355,8.8206046,12.2498599,14.2218746,2.1990885,2.8505478,3.4490967,4.4962817,5.5126023,6.5300252,7.3490341,7.8847519,8.5891216,9.7388205,11.1211047,12.1208908,12.8208513,13.8162282,14.8766408,15.5369185,16.5267839,17.3909871,0.352736,0.9601033,1.5344016,2.2464874,2.8792076,3.4557105,4.1611825,5.0628639,6.0869006,7.5386297,9.6473296,11.3029842,2.4327761,3.4490967,4.122602,4.7002072,5.8223486,7.6675988,10.3935867,12.8120329,14.1259745,1.5277878,1.8254088,2.0679148,2.4371853,2.998256,3.4094139,3.5692474,3.9726892,4.7696521,5.3726102,6.0372971,7.043697,7.6742126,8.3212627,9.3618339,10.1973773,10.9700896,11.5333649,12.1738012,13.6343487,14.9560064,16.2930963,1.3139416,2.1362574,2.9905399,3.9076535,4.3728241,4.9691684,6.0031258,7.4691848,2.1395643,3.3741403,4.6362738,5.7077094,7.153927,9.060906,11.4010889,13.2595667,3.1128952,3.7401039,4.2592872,5.1819123,5.9579315,6.3415319,7.4923331,8.5020399,9.3629362,11.0461483,0.0804679,0.2347899,0.3681682,0.6040604,1.3205554,2.2222368,2.921095,3.4215392,3.9219834,4.6263531,5.6129116,6.7703266,7.5959493,8.6960447,10.1323416,11.662334],"y":[0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999],"text":["pounds: 0.2138462","pounds: 1.1221414","pounds: 0.8421572","pounds: 0.3858050","pounds: 1.1155276","pounds: 1.4153532","pounds: 1.1574150","pounds: 1.2345760","pounds: 1.2963048","pounds: 2.1979862","pounds: 2.2266460","pounds: 0.9435688","pounds: 3.3994932","pounds: 3.0864400","pounds: 4.1578756","pounds: 6.4682964","pounds: 0.4651706","pounds: 0.6790168","pounds: 2.3038070","pounds: 2.4294692","pounds: 0.7804284","pounds: 1.6027442","pounds: 0.5246948","pounds: 1.6843144","pounds: 1.3558290","pounds: 0.5070580","pounds: 0.6812214","pounds: 0.8664078","pounds: 0.4916258","pounds: 0.6768122","pounds: 0.3571452","pounds: 0.9104998","pounds: 0.5864236","pounds: 0.8752262","pounds: 0.5820144","pounds: 0.7583824","pounds: 1.8562732","pounds: 2.1891678","pounds: 1.0956862","pounds: 2.2773518","pounds: 0.9612056","pounds: 1.8893422","pounds: 0.8664078","pounds: 0.7914514","pounds: 0.6415386","pounds: 0.6988582","pounds: 1.2764634","pounds: 3.3906748","pounds: 3.4678358","pounds: 0.4761936","pounds: 0.9590010","pounds: 0.3439176","pounds: 0.8531802","pounds: 1.2411898","pounds: 0.7914514","pounds: 1.2433944","pounds: 0.3946234","pounds: 0.6768122","pounds: 0.7319272","pounds: 1.5674706","pounds: 1.1970978","pounds: 0.8024744","pounds: 0.5974466","pounds: 1.3933072","pounds: 0.7275180","pounds: 0.5930374","pounds: 1.3866934","pounds: 0.3417130","pounds: 0.7054720","pounds: 0.5092626","pounds: 0.6393340","pounds: 0.7848376","pounds: 0.4806028","pounds: 0.6724030","pounds: 0.7385410","pounds: 1.0648218","pounds: 0.9832516","pounds: 1.9202066","pounds: 2.2971932","pounds: 1.0141160","pounds: 1.3646474","pounds: 0.6679938","pounds: 0.6790168","pounds: 0.4761936","pounds: 1.7680892","pounds: 1.9224112","pounds: 3.5295646","pounds: 1.3073278","pounds: 1.3205554","pounds: 0.3703728","pounds: 0.2248692","pounds: 0.2601428","pounds: 0.4783982","pounds: 0.6437432","pounds: 0.1785726","pounds: 0.1410944","pounds: 0.6657892","pounds: 0.9281366","pounds: 0.2777796","pounds: 1.0515942","pounds: 0.9612056","pounds: 0.2998256","pounds: 0.9942746","pounds: 1.0868678","pounds: 0.5842190","pounds: 0.9612056","pounds: 0.1653450","pounds: 1.1155276","pounds: 1.8055674","pounds: 0.8377480","pounds: 1.8364318","pounds: 1.2389852","pounds: 0.4056464","pounds: 1.3029186","pounds: 0.5313086","pounds: 0.3990326","pounds: 0.7936560","pounds: 1.2742588","pounds: 1.6578592","pounds: 0.7473594","pounds: 1.7217926","pounds: 0.8024744","pounds: 1.3403968","pounds: 1.5520384","pounds: 2.2619196","pounds: 2.4184462","pounds: 1.2985094","pounds: 0.7407456","pounds: 0.5136718","pounds: 0.5246948","pounds: 1.3205554","pounds: 0.2314830","pounds: 0.5357178","pounds: 1.7658846","pounds: 0.2535290","pounds: 1.4682636","pounds: 1.8981606","pounds: 0.1609358","pounds: 0.1477082","pounds: 0.1190484","pounds: 0.3527360","pounds: 1.0802540","pounds: 0.7231088","pounds: 0.6746076","pounds: 0.3262808","pounds: 0.6746076","pounds: 0.7341318","pounds: 1.2389852","pounds: 1.0758448","pounds: 0.5754006","pounds: 1.6247902","pounds: 1.2478036","pounds: 1.8121812"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(40,84,122,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[3.3884702,4.761936,2.9034582,1.5255832,0.502648799999996,6.0361948,3.1900562,6.3911354,3.0688032,1.477082,2.7314994,1.0890724,2.788819,3.6353854,0.6701984,1.4528314,0.520285600000001,1.565266,2.3192392,1.5740844,1.0515942,0.3924188,0.947977999999999,1.5740844,0.443124599999999,2.4934026,0.9744332,1.355829,1.1221414,0.568786800000002,2.3324668,1.8055674,1.4947188,1.7041558,2.5970188,1.6622684,2.6499292,0.562173000000001,0.696653600000001,4.4224276,0.7209042,1.774703,1.4859004,3.5957026,4.0189858,4.3055838,1.344806,2.7204764,5.2403342,0.9104998,1.598335,0.467375200000003,6.4682964,0.209437000000001,4.3606988,0.154322000000001],"base":[11.55,11.55,11.55,11.55,11.55,11.55,11.55,9.55,9.55,9.55,9.55,9.55,5.55,5.55,5.55,5.55,3.55,4.55,4.55,4.55,4.55,1.55,1.55,1.55,2.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,8.55,0.55,0.55,0.55,6.55,6.55,6.55,6.55,6.55,7.55,7.55,7.55,7.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55,10.55],"x":[34.8734651,38.9486682,42.7813653,44.995886,46.010002,49.2794238,53.8925493,19.8623437,24.592313,26.8652556,28.9695463,30.8798322,14.8005821,18.0126843,20.1654762,21.2269911,14.7201142,18.3444766,20.2867292,22.233391,23.5462303,12.0062516,12.67645,13.9374812,15.0078145,18.4580135,20.1919314,21.3570625,22.5960477,23.4415118,24.8921386,26.9611557,28.6112988,9.1501923,11.3007796,13.4304232,15.233786,16.8398371,17.4692504,20.028791,22.6004569,12.8825801,14.5128818,17.0536833,20.8610275,14.7212165,17.5464114,19.5790526,23.5594579,26.6348749,27.8892923,28.9221474,32.3899832,35.7288499,38.0139178,40.2714282],"y":[0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999],"text":["pounds: 3.3884702","pounds: 4.7619360","pounds: 2.9034582","pounds: 1.5255832","pounds: 0.5026488","pounds: 6.0361948","pounds: 3.1900562","pounds: 6.3911354","pounds: 3.0688032","pounds: 1.4770820","pounds: 2.7314994","pounds: 1.0890724","pounds: 2.7888190","pounds: 3.6353854","pounds: 0.6701984","pounds: 1.4528314","pounds: 0.5202856","pounds: 1.5652660","pounds: 2.3192392","pounds: 1.5740844","pounds: 1.0515942","pounds: 0.3924188","pounds: 0.9479780","pounds: 1.5740844","pounds: 0.4431246","pounds: 2.4934026","pounds: 0.9744332","pounds: 1.3558290","pounds: 1.1221414","pounds: 0.5687868","pounds: 2.3324668","pounds: 1.8055674","pounds: 1.4947188","pounds: 1.7041558","pounds: 2.5970188","pounds: 1.6622684","pounds: 2.6499292","pounds: 0.5621730","pounds: 0.6966536","pounds: 4.4224276","pounds: 0.7209042","pounds: 1.7747030","pounds: 1.4859004","pounds: 3.5957026","pounds: 4.0189858","pounds: 4.3055838","pounds: 1.3448060","pounds: 2.7204764","pounds: 5.2403342","pounds: 0.9104998","pounds: 1.5983350","pounds: 0.4673752","pounds: 6.4682964","pounds: 0.2094370","pounds: 4.3606988","pounds: 0.1543220"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(62,129,183,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"orientation":"v","width":[0.555559199999998,1.576289,5.4629988,2.59040499999999,1.1596196,1.42417159999999,0.5996512,0.696653600000001,1.7438386,0.826725,0.850975599999998,0.9215228,0.4828074,3.0357342,0.7627916,0.469579800000002,0.559968399999999,0.440920000000002,1.8937514,0.800269800000002,1.9797308,1.0670264,0.1410944,4.3584942,0.507058000000001,6.2566548],"base":[11.55,11.55,11.55,11.55,9.55,9.55,5.55,5.55,5.55,3.55,4.55,1.55,2.55,8.55,0.55,6.55,6.55,6.55,6.55,7.55,7.55,7.55,10.55,10.55,10.55,10.55],"x":[55.765357,56.8312811,60.350925,64.3776269,32.0041782,33.2960738,22.2532324,22.9013848,24.1216309,15.3936195,24.4975152,15.1852848,15.4707805,30.8765253,14.6429532,23.1956989,23.710473,24.2109172,25.3782529,23.2706553,24.6606556,26.1840342,40.4191364,42.6689307,45.1017068,48.4835632],"y":[0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.9,0.9,0.9,0.9,0.9,0.9,0.9,0.899999999999999,0.9,0.9,0.9,0.9,0.9,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999,0.899999999999999],"text":["pounds: 0.5555592","pounds: 1.5762890","pounds: 5.4629988","pounds: 2.5904050","pounds: 1.1596196","pounds: 1.4241716","pounds: 0.5996512","pounds: 0.6966536","pounds: 1.7438386","pounds: 0.8267250","pounds: 0.8509756","pounds: 0.9215228","pounds: 0.4828074","pounds: 3.0357342","pounds: 0.7627916","pounds: 0.4695798","pounds: 0.5599684","pounds: 0.4409200","pounds: 1.8937514","pounds: 0.8002698","pounds: 1.9797308","pounds: 1.0670264","pounds: 0.1410944","pounds: 4.3584942","pounds: 0.5070580","pounds: 6.2566548"],"type":"bar","marker":{"autocolorscale":false,"color":"rgba(86,177,247,1)","line":{"width":1.88976377952756,"color":"transparent"}},"showlegend":false,"xaxis":"x","yaxis":"y","hoverinfo":"text","frame":null},{"x":[0],"y":[1],"name":"99_d3329ee74a04841f15614ed527df577b","type":"scatter","mode":"markers","opacity":0,"hoverinfo":"skip","showlegend":false,"marker":{"color":[0,1],"colorscale":[[0,"#132B43"],[0.00334448160535109,"#132B44"],[0.00668896321070249,"#132C44"],[0.0100334448160536,"#142C45"],[0.0133779264214047,"#142D45"],[0.0167224080267558,"#142D46"],[0.0200668896321072,"#142D46"],[0.0234113712374583,"#142E47"],[0.0267558528428093,"#152E47"],[0.0301003344481604,"#152F48"],[0.0334448160535118,"#152F48"],[0.0367892976588629,"#152F49"],[0.040133779264214,"#153049"],[0.0434782608695651,"#16304A"],[0.0468227424749165,"#16304A"],[0.0501672240802676,"#16314B"],[0.0535117056856187,"#16314B"],[0.0568561872909698,"#16324C"],[0.0602006688963212,"#17324D"],[0.0635451505016723,"#17324D"],[0.0668896321070234,"#17334E"],[0.0702341137123745,"#17334E"],[0.0735785953177259,"#17344F"],[0.0769230769230769,"#18344F"],[0.080267558528428,"#183450"],[0.0836120401337791,"#183550"],[0.0869565217391305,"#183551"],[0.0903010033444816,"#183651"],[0.0936454849498327,"#193652"],[0.0969899665551838,"#193652"],[0.100334448160535,"#193753"],[0.103678929765886,"#193754"],[0.107023411371237,"#193854"],[0.110367892976589,"#1A3855"],[0.11371237458194,"#1A3955"],[0.117056856187291,"#1A3956"],[0.120401337792642,"#1A3956"],[0.123745819397993,"#1A3A57"],[0.127090301003345,"#1B3A57"],[0.130434782608696,"#1B3B58"],[0.133779264214047,"#1B3B59"],[0.137123745819398,"#1B3B59"],[0.140468227424749,"#1C3C5A"],[0.1438127090301,"#1C3C5A"],[0.147157190635451,"#1C3D5B"],[0.150501672240803,"#1C3D5B"],[0.153846153846154,"#1C3D5C"],[0.157190635451505,"#1D3E5C"],[0.160535117056856,"#1D3E5D"],[0.163879598662207,"#1D3F5D"],[0.167224080267559,"#1D3F5E"],[0.17056856187291,"#1D3F5F"],[0.173913043478261,"#1E405F"],[0.177257525083612,"#1E4060"],[0.180602006688963,"#1E4160"],[0.183946488294314,"#1E4161"],[0.187290969899665,"#1E4261"],[0.190635451505017,"#1F4262"],[0.193979933110368,"#1F4263"],[0.197324414715719,"#1F4363"],[0.20066889632107,"#1F4364"],[0.204013377926421,"#1F4464"],[0.207357859531773,"#204465"],[0.210702341137124,"#204465"],[0.214046822742475,"#204566"],[0.217391304347826,"#204566"],[0.220735785953177,"#214667"],[0.224080267558528,"#214668"],[0.22742474916388,"#214768"],[0.230769230769231,"#214769"],[0.234113712374582,"#214769"],[0.237458193979933,"#22486A"],[0.240802675585284,"#22486A"],[0.244147157190636,"#22496B"],[0.247491638795987,"#22496C"],[0.250836120401338,"#224A6C"],[0.254180602006689,"#234A6D"],[0.25752508361204,"#234A6D"],[0.260869565217391,"#234B6E"],[0.264214046822742,"#234B6E"],[0.267558528428094,"#244C6F"],[0.270903010033445,"#244C70"],[0.274247491638796,"#244C70"],[0.277591973244147,"#244D71"],[0.280936454849498,"#244D71"],[0.28428093645485,"#254E72"],[0.287625418060201,"#254E72"],[0.290969899665552,"#254F73"],[0.294314381270903,"#254F74"],[0.297658862876254,"#254F74"],[0.301003344481605,"#265075"],[0.304347826086956,"#265075"],[0.307692307692308,"#265176"],[0.311036789297659,"#265176"],[0.31438127090301,"#275277"],[0.317725752508361,"#275278"],[0.321070234113712,"#275278"],[0.324414715719064,"#275379"],[0.327759197324415,"#275379"],[0.331103678929766,"#28547A"],[0.334448160535117,"#28547B"],[0.337792642140469,"#28557B"],[0.341137123745819,"#28557C"],[0.344481605351171,"#28567C"],[0.347826086956522,"#29567D"],[0.351170568561873,"#29567D"],[0.354515050167224,"#29577E"],[0.357859531772575,"#29577F"],[0.361204013377926,"#2A587F"],[0.364548494983277,"#2A5880"],[0.367892976588629,"#2A5980"],[0.37123745819398,"#2A5981"],[0.374581939799331,"#2A5982"],[0.377926421404682,"#2B5A82"],[0.381270903010034,"#2B5A83"],[0.384615384615384,"#2B5B83"],[0.387959866220736,"#2B5B84"],[0.391304347826087,"#2C5C85"],[0.394648829431438,"#2C5C85"],[0.397993311036789,"#2C5D86"],[0.401337792642141,"#2C5D86"],[0.404682274247492,"#2C5D87"],[0.408026755852843,"#2D5E87"],[0.411371237458194,"#2D5E88"],[0.414715719063545,"#2D5F89"],[0.418060200668897,"#2D5F89"],[0.421404682274247,"#2E608A"],[0.424749163879599,"#2E608A"],[0.42809364548495,"#2E618B"],[0.431438127090301,"#2E618C"],[0.434782608695652,"#2E618C"],[0.438127090301003,"#2F628D"],[0.441471571906354,"#2F628D"],[0.444816053511706,"#2F638E"],[0.448160535117057,"#2F638F"],[0.451505016722408,"#30648F"],[0.45484949832776,"#306490"],[0.45819397993311,"#306590"],[0.461538461538462,"#306591"],[0.464882943143812,"#306592"],[0.468227424749164,"#316692"],[0.471571906354515,"#316693"],[0.474916387959866,"#316793"],[0.478260869565217,"#316794"],[0.481605351170568,"#326895"],[0.48494983277592,"#326895"],[0.488294314381271,"#326996"],[0.491638795986622,"#326996"],[0.494983277591973,"#326997"],[0.498327759197325,"#336A98"],[0.501672240802675,"#336A98"],[0.505016722408027,"#336B99"],[0.508361204013378,"#336B99"],[0.511705685618729,"#346C9A"],[0.51505016722408,"#346C9B"],[0.518394648829432,"#346D9B"],[0.521739130434783,"#346D9C"],[0.525083612040134,"#346E9D"],[0.528428093645485,"#356E9D"],[0.531772575250836,"#356E9E"],[0.535117056856187,"#356F9E"],[0.538461538461538,"#356F9F"],[0.54180602006689,"#3670A0"],[0.545150501672241,"#3670A0"],[0.548494983277592,"#3671A1"],[0.551839464882943,"#3671A1"],[0.555183946488294,"#3772A2"],[0.558528428093645,"#3772A3"],[0.561872909698997,"#3773A3"],[0.565217391304348,"#3773A4"],[0.568561872909699,"#3773A4"],[0.57190635451505,"#3874A5"],[0.575250836120401,"#3874A6"],[0.578595317725753,"#3875A6"],[0.581939799331103,"#3875A7"],[0.585284280936455,"#3976A8"],[0.588628762541806,"#3976A8"],[0.591973244147157,"#3977A9"],[0.595317725752508,"#3977A9"],[0.59866220735786,"#3978AA"],[0.602006688963211,"#3A78AB"],[0.605351170568562,"#3A79AB"],[0.608695652173913,"#3A79AC"],[0.612040133779264,"#3A79AC"],[0.615384615384616,"#3B7AAD"],[0.618729096989966,"#3B7AAE"],[0.622073578595318,"#3B7BAE"],[0.625418060200669,"#3B7BAF"],[0.62876254180602,"#3C7CB0"],[0.632107023411371,"#3C7CB0"],[0.635451505016723,"#3C7DB1"],[0.638795986622073,"#3C7DB1"],[0.642140468227425,"#3C7EB2"],[0.645484949832776,"#3D7EB3"],[0.648829431438127,"#3D7FB3"],[0.652173913043478,"#3D7FB4"],[0.655518394648829,"#3D7FB5"],[0.658862876254181,"#3E80B5"],[0.662207357859531,"#3E80B6"],[0.665551839464883,"#3E81B6"],[0.668896321070234,"#3E81B7"],[0.672240802675585,"#3F82B8"],[0.675585284280936,"#3F82B8"],[0.678929765886288,"#3F83B9"],[0.682274247491639,"#3F83BA"],[0.68561872909699,"#4084BA"],[0.688963210702341,"#4084BB"],[0.692307692307692,"#4085BB"],[0.695652173913044,"#4085BC"],[0.698996655518395,"#4086BD"],[0.702341137123746,"#4186BD"],[0.705685618729097,"#4186BE"],[0.709030100334448,"#4187BF"],[0.712374581939799,"#4187BF"],[0.71571906354515,"#4288C0"],[0.719063545150502,"#4288C1"],[0.722408026755853,"#4289C1"],[0.725752508361204,"#4289C2"],[0.729096989966555,"#438AC2"],[0.732441471571907,"#438AC3"],[0.735785953177257,"#438BC4"],[0.739130434782609,"#438BC4"],[0.74247491638796,"#438CC5"],[0.745819397993311,"#448CC6"],[0.749163879598662,"#448DC6"],[0.752508361204014,"#448DC7"],[0.755852842809364,"#448EC8"],[0.759197324414716,"#458EC8"],[0.762541806020067,"#458FC9"],[0.765886287625418,"#458FC9"],[0.769230769230769,"#458FCA"],[0.77257525083612,"#4690CB"],[0.775919732441472,"#4690CB"],[0.779264214046822,"#4691CC"],[0.782608695652174,"#4691CD"],[0.785953177257525,"#4792CD"],[0.789297658862876,"#4792CE"],[0.792642140468227,"#4793CF"],[0.795986622073579,"#4793CF"],[0.79933110367893,"#4894D0"],[0.802675585284281,"#4894D0"],[0.806020066889632,"#4895D1"],[0.809364548494983,"#4895D2"],[0.812709030100335,"#4896D2"],[0.816053511705686,"#4996D3"],[0.819397993311037,"#4997D4"],[0.822742474916388,"#4997D4"],[0.826086956521739,"#4998D5"],[0.82943143812709,"#4A98D6"],[0.832775919732441,"#4A99D6"],[0.836120401337793,"#4A99D7"],[0.839464882943144,"#4A9AD8"],[0.842809364548495,"#4B9AD8"],[0.846153846153846,"#4B9BD9"],[0.849498327759198,"#4B9BDA"],[0.852842809364548,"#4B9BDA"],[0.8561872909699,"#4C9CDB"],[0.859531772575251,"#4C9CDB"],[0.862876254180602,"#4C9DDC"],[0.866220735785953,"#4C9DDD"],[0.869565217391305,"#4D9EDD"],[0.872909698996655,"#4D9EDE"],[0.876254180602007,"#4D9FDF"],[0.879598662207358,"#4D9FDF"],[0.882943143812709,"#4DA0E0"],[0.88628762541806,"#4EA0E1"],[0.889632107023411,"#4EA1E1"],[0.892976588628763,"#4EA1E2"],[0.896321070234113,"#4EA2E3"],[0.899665551839465,"#4FA2E3"],[0.903010033444816,"#4FA3E4"],[0.906354515050167,"#4FA3E5"],[0.909698996655518,"#4FA4E5"],[0.91304347826087,"#50A4E6"],[0.916387959866221,"#50A5E7"],[0.919732441471572,"#50A5E7"],[0.923076923076923,"#50A6E8"],[0.926421404682274,"#51A6E8"],[0.929765886287626,"#51A7E9"],[0.933110367892977,"#51A7EA"],[0.936454849498328,"#51A8EA"],[0.939799331103679,"#52A8EB"],[0.94314381270903,"#52A9EC"],[0.946488294314381,"#52A9EC"],[0.949832775919732,"#52AAED"],[0.953177257525084,"#53AAEE"],[0.956521739130435,"#53ABEE"],[0.959866220735786,"#53ABEF"],[0.963210702341137,"#53ACF0"],[0.966555183946488,"#54ACF0"],[0.969899665551839,"#54ADF1"],[0.973244147157191,"#54ADF2"],[0.976588628762542,"#54AEF2"],[0.979933110367893,"#55AEF3"],[0.983277591973244,"#55AFF4"],[0.986622073578596,"#55AFF4"],[0.989966555183946,"#55B0F5"],[0.993311036789298,"#56B0F6"],[0.996655518394649,"#56B1F6"],[1,"#56B1F7"]],"colorbar":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"thickness":23.04,"title":"month(date)","titlefont":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"tickmode":"array","ticktext":["7","8","9","10"],"tickvals":[0,0.333333333333333,0.666666666666667,1],"tickfont":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895},"ticklen":2,"len":0.5}},"xaxis":"x","yaxis":"y","frame":null}],"layout":{"margin":{"t":43.7625570776256,"r":7.30593607305936,"b":25.5707762557078,"l":98.6301369863014},"font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187},"title":{"text":"Cumulative Tomato Weight (Grams) by Variety and Date Harvested","font":{"color":"rgba(0,0,0,1)","family":"","size":17.5342465753425},"x":0,"xref":"paper"},"xaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[-3.28364147,68.95647087],"tickmode":"array","ticktext":["0","20","40","60"],"tickvals":[0,20,40,60],"categoryorder":"array","categoryarray":["0","20","40","60"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"y","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"yaxis":{"domain":[0,1],"automargin":true,"type":"linear","autorange":false,"range":[0.4,12.6],"tickmode":"array","ticktext":["Jet Star","Brandywine","Cherokee Purple","Black Krim","Bonny Best","Big Beef","Mortgage Lifter","Old German","Grape","Better Boy","Volunteers","Amish Paste"],"tickvals":[1,2,3,4,5,6,7,8,9,10,11,12],"categoryorder":"array","categoryarray":["Jet Star","Brandywine","Cherokee Purple","Black Krim","Bonny Best","Big Beef","Mortgage Lifter","Old German","Grape","Better Boy","Volunteers","Amish Paste"],"nticks":null,"ticks":"","tickcolor":null,"ticklen":3.65296803652968,"tickwidth":0,"showticklabels":true,"tickfont":{"color":"rgba(77,77,77,1)","family":"","size":11.689497716895},"tickangle":-0,"showline":false,"linecolor":null,"linewidth":0,"showgrid":false,"gridcolor":null,"gridwidth":0,"zeroline":false,"anchor":"x","title":{"text":"","font":{"color":"rgba(0,0,0,1)","family":"","size":14.6118721461187}},"hoverformat":".2f"},"shapes":[{"type":"rect","fillcolor":null,"line":{"color":null,"width":0,"linetype":[]},"yref":"paper","xref":"paper","x0":0,"x1":1,"y0":0,"y1":1}],"showlegend":false,"legend":{"bgcolor":null,"bordercolor":null,"borderwidth":0,"font":{"color":"rgba(0,0,0,1)","family":"","size":11.689497716895}},"hovermode":"closest","barmode":"relative"},"config":{"doubleClick":"reset","showSendToCloud":false},"source":"A","attrs":{"300c40d9431d":{"fill":{},"label":{},"x":{},"y":{},"type":"bar"}},"cur_data":"300c40d9431d","visdat":{"300c40d9431d":["function (y) ","x"]},"highlight":{"on":"plotly_click","persistent":false,"dynamic":false,"selectize":false,"opacityDim":0.2,"selected":{"opacity":1},"debounce":0},"shinyEvents":["plotly_hover","plotly_click","plotly_selected","plotly_relayout","plotly_brushed","plotly_brushing","plotly_clickannotation","plotly_doubleclick","plotly_deselect","plotly_afterplot","plotly_sunburstclick"],"base_url":"https://plot.ly"},"evals":[],"jsHooks":[]}</script>
```

  
  2. Use animation to tell an interesting story with the `small_trains` dataset that contains data from the SNCF (National Society of French Railways). These are Tidy Tuesday data! Read more about it [here](https://github.com/rfordatascience/tidytuesday/tree/master/data/2019/2019-02-26).


```r
cum_trips <- small_trains %>% 
  group_by(year, departure_station) %>% 
  summarise(yearly_trips = sum(total_num_trips)) %>% 
  ungroup() %>% 
  complete(year, departure_station) %>% 
  arrange(departure_station, year) %>% 
  group_by(departure_station) %>% 
  replace_na(list(yearly_trips = 0)) %>% 
  mutate(cum_trips = cumsum(yearly_trips)) %>% 
  filter(cum_trips > 0)


zoomingtrains <- cum_trips %>% 
  group_by(year) %>% 
  top_n(n = 10, wt = cum_trips) %>% 
  arrange(year, cum_trips) %>% 
  mutate(rank = 1:n()) %>% 
  ggplot(aes(x = cum_trips,
             y = factor(rank),
             fill = departure_station,
             group = departure_station)) +
  geom_col() +
  geom_text(aes(label = departure_station),
            x = -10,
            hjust = "right") +
  labs(title = "Cumulative Number of Trips Taken from Each Departure Station",
       subtitle = "year: {frame_time}",
       x = "", 
       y = "") +
  theme(axis.line = element_blank(), 
        panel.grid = element_blank(),
        axis.text.y = element_blank(),
        legend.position = "none") +
  scale_fill_viridis_d() +
  transition_time(year) #added instead of facet-ing

animate(zoomingtrains)
#changed frame number and duration
anim_save("departures.gif")


# can I make a variable for date so that the year isn't so annoying to look at? 
# can I make the y axis a little larger, so I can see the full names of the stations?
```



```r
knitr:: include_graphics("departures.gif")
```

![](departures.gif)<!-- -->



## Garden data

  3. In this exercise, you will create a stacked area plot that reveals itself over time (see the `geom_area()` examples [here](https://ggplot2.tidyverse.org/reference/position_stack.html)). You will look at cumulative harvest of tomato varieties over time. You should do the following:
  * From the `garden_harvest` data, filter the data to the tomatoes and find the *daily* harvest in pounds for each variety.  
  * Then, for each variety, find the cumulative harvest in pounds.  
  * Use the data you just made to create a static cumulative harvest area plot, with the areas filled with different colors for each vegetable and arranged (HINT: `fct_reorder()`) from most to least harvested (most on the bottom).  
  * Add animation to reveal the plot over date. 

I have started the code for you below. The `complete()` function creates a row for all unique `date`/`variety` combinations. If a variety is not harvested on one of the harvest dates in the dataset, it is filled with a value of 0.


```r
garden_cum <- garden_harvest %>% 
  filter(vegetable == "tomatoes") %>% 
  group_by(date, variety) %>% 
  summarize(daily_harvest_lb = sum(weight)*0.00220462) %>% 
  ungroup() %>% 
  complete(variety, date, fill = list(daily_harvest_lb = 0)) %>% 
  group_by(variety) %>% 
  mutate(cum_harvest_lb = cumsum(daily_harvest_lb)) %>%
  ungroup() %>% 
  mutate(variety = fct_reorder(variety, daily_harvest_lb, sum))
```

```
## `summarise()` has grouped output by 'date'. You can override using the `.groups` argument.
```

```r
  # mutate(rank = 1:n())
```


```r
# garden_cum_plot <- 
garden_cum %>% 
  ggplot(aes(x = date, 
             y = cum_harvest_lb, 
             # y = fct_reorder(cum_harvest_lb), 
             # factor(cum_harvest_lb, variety), 
             fill = variety)) +
  geom_area(position = "stack") +
  labs(title = "Cumulative Tomato Harvest by Variety", 
       subtitle = "date: {frame_along}",
       x = "", 
       y = "", 
       color = "variety") +
  theme(panel.grid.major = element_blank(),
        panel.grid.minor = element_blank(),
        axis.line = element_line(color = "black",
                                 linetype = "solid"), 
        axis.ticks = element_line(color = "black")) +
  transition_reveal(date)

anim_save("cumveggies.gif")
```




```r
knitr::include_graphics("cumveggies.gif")
```

![](cumveggies.gif)<!-- -->


## Maps, animation, and movement!

  4. Map my `mallorca_bike_day7` bike ride using animation! 
  Requirements:
  * Plot on a map using `ggmap`.  
  * Show "current" location with a red point. 
  * Show path up until the current point.  
  * Color the path according to elevation.  
  * Show the time in the subtitle.  
  * CHALLENGE: use the `ggimage` package and `geom_image` to add a bike image instead of a red point. You can use [this](https://raw.githubusercontent.com/llendway/animation_and_interactivity/master/bike.png) image. See [here](https://goodekat.github.io/presentations/2019-isugg-gganimate-spooky/slides.html#35) for an example. 
  * Add something of your own! And comment on if you prefer this to the static map and why or why not.
  

```r
mallorca_map <- get_stamenmap(
    bbox = c(left = 2.28, bottom = 39.41, right = 3.03, top = 39.8), 
    maptype = "terrain",
    zoom = 11
)
ggmap(mallorca_map) +
  geom_path(data = mallorca_bike_day7, 
             aes(x = lon, 
                 y = lat, 
                 color = ele),
             size = .5) +
  geom_point(data = mallorca_bike_day7, 
             aes(x = lon,
                 y = lat), 
             size = .3, 
             color = "red") +
  annotate("text", 
           x = 2.57, 
           y = 39.65, 
           color = "red", 
           label = "City of Origin: Palma",
           size = 2.5) +
  scale_color_viridis_c(option = "magma") +
  theme_map() +
  theme(legend.background = element_blank()) +
  #include label or something for a red dot geom_text(aes(label = vegetable)) +
  labs(title = "Mallorca Bike Path", 
       subtitle = "time: {frame_along}",
       x = "", 
       y = "") +
  transition_reveal(time)

anim_save("bikepath.gif")


#how do I do this: * Show "current" location with a red point. 
```


```r
knitr::include_graphics("bikepath.gif")
```

![](bikepath.gif)<!-- -->

  
  
  5. In this exercise, you get to meet my sister, Heather! She is a proud Mac grad, currently works as a Data Scientist at 3M where she uses R everyday, and for a few years (while still holding a full-time job) she was a pro triathlete. You are going to map one of her races. The data from each discipline of the Ironman 70.3 Pan Am championships, Panama is in a separate file - `panama_swim`, `panama_bike`, and `panama_run`. Create a similar map to the one you created with my cycling data. You will need to make some small changes: 1. combine the files (HINT: `bind_rows()`, 2. make the leading dot a different color depending on the event (for an extra challenge, make it a different image using `geom_image()!), 3. CHALLENGE (optional): color by speed, which you will need to compute on your own from the data. You can read Heather's race report [here](https://heatherlendway.com/2016/02/10/ironman-70-3-pan-american-championships-panama-race-report/). She is also in the Macalester Athletics [Hall of Fame](https://athletics.macalester.edu/honors/hall-of-fame/heather-lendway/184) and still has records at the pool. 
  

```r
full_panama <- bind_rows(panama_swim, panama_bike, panama_run) 

panama_map <- get_stamenmap(
    bbox = c(left = -79.60, bottom = 8.9059, right = -79.44, top = 8.9946), 
    maptype = "terrain",
    zoom = 13)

ggmap(panama_map) +
  geom_path(data = full_panama, 
             aes(x = lon, 
                 y = lat, 
                 color = event),
             size = .5) +
  scale_color_viridis_d(option = "magma") +
  geom_point(data = full_panama, 
             aes(x = lon, 
                 y = lat, 
                 color = event)) +
  theme_map() +
  theme(legend.background = element_blank()) +
  labs(title = "Panama Bike Path",
       subtitle = "hrminsec: {frame_along}",
       x = "",
       y = "") +
  transition_reveal(hrminsec)

anim_save("triathlon.gif")
```



```r
knitr::include_graphics("triathlon.gif")
```

![](triathlon.gif)<!-- -->

  
## COVID-19 data

  6. In this exercise, you are going to replicate many of the features in [this](https://aatishb.com/covidtrends/?region=US) visualization by Aitish Bhatia but include all US states. Requirements:
 * Create a new variable that computes the number of new cases in the past week (HINT: use the `lag()` function you've used in a previous set of exercises). Replace missing values with 0's using `replace_na()`.  
  * Filter the data to omit rows where the cumulative case counts are less than 20.  
  * Create a static plot with cumulative cases on the x-axis and new cases in the past 7 days on the y-axis. Connect the points for each state over time. HINTS: use `geom_path()` and add a `group` aesthetic.  Put the x and y axis on the log scale and make the tick labels look nice - `scales::comma` is one option. This plot will look pretty ugly as is.
  * Animate the plot to reveal the pattern by date. Display the date as the subtitle. Add a leading point to each state's line (`geom_point()`) and add the state name as a label (`geom_text()` - you should look at the `check_overlap` argument).  
  * Use the `animate()` function to have 200 frames in your animation and make it 30 seconds long. 
  * Comment on what you observe.
  
  

```r
weeklycovid19 <- covid19 %>% 
  filter(cases >= 20) %>% 
  group_by(state) %>% 
  mutate(perweek = lag(cases, 7, order_by = date)) %>% 
  replace_na(list(perweek= 0)) %>% 
  mutate(newperweek = cases - perweek,
         state_ordered = fct_reorder2(state,
                                      date,
                                      cases)) %>% 
  group_by(state_ordered) %>% 
  arrange(state_ordered, date)
```



```r
COVID19plot <- weeklycovid19 %>% 
  ggplot(aes(x = cases, 
             y = newperweek,
             group = state_ordered)) +
  geom_path() +
  geom_point(color = "red") +
scale_y_log10(breaks = 
                  scales::trans_breaks(
                    "log10", function(x)10^x),
                labels = scales::comma) +
  scale_x_log10(breaks = 
                  scales::trans_breaks(
                    "log10", function(x)10^x),
                labels = scales::comma) +
  geom_text(aes(label = state), 
            check_overlap = T) +
  labs(title = "Cumulative Number of COVID19 Cases per Week as Shown by State",
       subtitle = "date: {frame_along}",
       x = "", 
       y = "") +
  theme(panel.grid.major = element_blank(),
        panel.grid.minor = element_blank(),
        axis.line = element_line(color = "black",
                                 linetype = "solid"), 
        axis.ticks = element_line(color = "black")) +
  transition_reveal(date) 

animate(COVID19plot, nframes = 200, duration = 30)

anim_save("COVID19.gif")
```
  
  

```r
knitr::include_graphics("COVID19.gif")
```

![](COVID19.gif)<!-- -->

*The beginning of the plot is a bit erratic, as the numbers of cases is less consistent at the beginning of the pandemic, but overall the trend is fairly linear in the positive direction*

  
  
  7. In this exercise you will animate a map of the US, showing how cumulative COVID-19 cases per 10,000 residents has changed over time. This is similar to exercises 11 & 12 from the previous exercises, with the added animation! So, in the end, you should have something like the static map you made there, but animated over all the days. The code below gives the population estimates for each state and loads the `states_map` data. Here is a list of details you should include in the plot:
  
  * Put date in the subtitle.   
  * Because there are so many dates, you are going to only do the animation for all Fridays. So, use `wday()` to create a day of week variable and filter to all the Fridays.   
  * Use the `animate()` function to make the animation 200 frames instead of the default 100 and to pause for 10 frames on the end frame.   
  * Use `group = date` in `aes()`.   
  * Comment on what you see.  



```r
census_pop_est_2018 <- read_csv("https://www.dropbox.com/s/6txwv3b4ng7pepe/us_census_2018_state_pop_est.csv?dl=1") %>% 
  separate(state, into = c("dot","state"), extra = "merge") %>% 
  select(-dot) %>% 
  mutate(state = str_to_lower(state))
```

```
## 
## -- Column specification --------------------------------------------------------
## cols(
##   state = col_character(),
##   est_pop_2018 = col_double()
## )
```

```r
states_map <- map_data("state")
```



```r
states_map <- map_data("state")

statemapcovid19 <- covid19 %>% 
  mutate(state = str_to_lower(state)) %>%  
  left_join(census_pop_est_2018, 
            by = c("state")) %>% 
  mutate(per10k = (cases/est_pop_2018)*10000) %>%
  mutate(weekday = wday(date, label = TRUE)) %>% 
  filter(weekday == "Fri") %>% 
  ggplot() + 
  geom_map(map = states_map, 
           aes(map_id = state, 
               fill = per10k, 
               group = date)) +
  expand_limits(x = states_map$long, y = states_map$lat) +
  theme_map() +
  scale_fill_viridis_c(option = "magma") +
  labs(title = "Most Recent Total Cumulative Number of COVID-19 Cases (per 10,000 people) by State in the US",
       subtitle = "date: {frame_time}", 
       y = "", 
       x = "")+ 
  transition_time(date) +
  theme(plot.title.position= "plot") 

animate(statemapcovid19, nframes = 200, end_pause = 10)

anim_save("USCOVID.gif")
```



```r
knitr::include_graphics("USCOVID.gif")
```

![](USCOVID.gif)<!-- -->

*Comment: *



## Your first `shiny` app (for next week!)

NOT DUE THIS WEEK! If any of you want to work ahead, this will be on next week's exercises.

  8. This app will also use the COVID data. Make sure you load that data and all the libraries you need in the `app.R` file you create. Below, you will post a link to the app that you publish on shinyapps.io. You will create an app to compare states' cumulative number of COVID cases over time. The x-axis will be number of days since 20+ cases and the y-axis will be cumulative cases on the log scale (`scale_y_log10()`). We use number of days since 20+ cases on the x-axis so we can make better comparisons of the curve trajectories. You will have an input box where the user can choose which states to compare (`selectInput()`) and have a submit button to click once the user has chosen all states they're interested in comparing. The graph should display a different line for each state, with labels either on the graph or in a legend. Color can be used if needed. 
  
## GitHub link

  9. Below, provide a link to your GitHub page with this set of Weekly Exercises. Specifically, if the name of the file is 05_exercises.Rmd, provide a link to the 05_exercises.md file, which is the one that will be most readable on GitHub. If that file isn't very readable, then provide a link to your main GitHub page.


**DID YOU REMEMBER TO UNCOMMENT THE OPTIONS AT THE TOP?**
