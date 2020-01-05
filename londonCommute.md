---
id: litvis

elm:
  dependencies:
    gicentre/elm-vegalite: latest
    gicentre/tidy: latest

follows: importDataAndSettings.md
---

@import "../css/datavis.less"

# Passengers flow in the London Underground Network

In the last 6 years, I have put more and more effort in trying to minimise the amount of carbon emissions produced by my daily commute. I became a long-distance cyclist and an intense user of the London underground, particularly in winter when the weather can be quite adverse (at least for Italians who are prone to be [‘hit by air’](https://www.bbc.com/news/magazine-15987082) ).

Being agoraphobic, I find very challenging to travel on crowded trains / wait at tube stations at rush hours. I am used to plan the best route for my journey well in advance using TfL data. However, this usually requires a lot of time and cognitive effort. The reason for this is that there are more than 250 tube stations in London and passengers count data is provided at very small time intervals (i.e. 15 mins) and in absolute numbers. Thus, it can be burdensome to understand how busy each station is and to make comparison between stations or times. For instance, what does it mean to have 2,000 passengers at Baker street station at 6PM? Is it a lot? How does this compare with Great Portland Street?

{(questions|}

- What are the busiest times for each London underground station during weekdays? In particular:
- do individual stations show any pattern?
- how do stations compare to one another?

{|questions)}

{(visualization|}

### Visualisation 1:

How busy each station is? Do invidividual stations show any pattern?
(_Note: Please select a station from the drop down menu and start exploring. Enjoy!_)

```elm {v l=hidden interactive}
isotypeSingleStation : Spec
isotypeSingleStation =
    let
        manPath =
            "M1.7 -1.7h-0.8c0.3 -0.2 0.6 -0.5 0.6 -0.9c0 -0.6 -0.4 -1 -1 -1c-0.6 0 -1 0.4 -1 1c0 0.4 0.2 0.7 0.6 0.9h-0.8c-0.4 0 -0.7 0.3 -0.7 0.6v1.9c0 0.3 0.3 0.6 0.6 0.6h0.2c0 0 0 0.1 0 0.1v1.9c0 0.3 0.2 0.6 0.3 0.6h1.3c0.2 0 0.3 -0.3 0.3 -0.6v-1.8c0 0 0 -0.1 0 -0.1h0.2c0.3 0 0.6 -0.3 0.6 -0.6v-2c0.2 -0.3 -0.1 -0.6 -0.4 -0.6z"

        cfg =
            configure
                << configuration (coView [ vicoStroke Nothing ])

        data =
            dataFromColumns []
                << dataColumn "col" (londonTubeFlowNorm |> Tidy.numColumn "id" |> nums)
                << dataColumn "station" (londonTubeFlowNorm |> Tidy.strColumn "object" |> strs)
                << dataColumn "type" (londonTubeFlowNorm |> Tidy.strColumn "type" |> strs)
                << dataColumn "time" (londonTubeFlowNorm |> Tidy.strColumn "time" |> strs)
                << dataColumn "count" (londonTubeFlowNorm |> Tidy.numColumn "count" |> nums)
                << dataColumn "tooltip" (londonTubeFlowNorm |> Tidy.strColumn "tooltip" |> strs)

        encFrame =
            encoding
                << position X [ pName "col", pMType Ordinal, pAxis [] ]
                << position Y
                    [ pName "time"
                    , pMType Ordinal
                    , pAxis
                        [ axTitle "", axTicks False, axLabelPadding 3, axDomain False, axLabelPadding 5 ]
                    , pScale [ scDomain (doStrs [ "Early", "AM Peak", "Inter Peak", "PM Peak", "Evening", "Late" ]) ]
                    ]
                << shape
                    [ mName "type"
                    , mMType Nominal
                    , mScale
                        (categoricalDomainMap
                            [ ( "Background", manPath ) ]
                        )
                    , mLegend []
                    ]

        encStation =
            encoding
                << position X [ pName "col", pMType Ordinal, pAxis [] ]
                << position Y
                    [ pName "time"
                    , pMType Ordinal
                    , pAxis [ axTitle "", axTicks False, axLabelPadding 3 ]
                    , pScale [ scDomain (doStrs [ "Early", "AM Peak", "Inter Peak", "PM Peak", "Evening", "Late" ]) ]
                    ]
                -- << row [ fName "time", fMType Nominal, fHeader [ hdTitle "" ] ]
                << shape
                    [ mName "type"
                    , mMType Nominal
                    , mScale
                        (categoricalDomainMap
                            [ ( "Station", manPath ) ]
                        )
                    , mLegend []
                    ]
                << tooltip [ tName "tooltip" ]

        selStation =
            selection
                << select "stationSelection"
                    seSingle
                    [ seFields [ "station" ]
                    , seBind
                        [ iSelect "station"
                            [ inName "Going somewhere?"
                            , inOptions listOfStations
                            ]
                        ]
                    , seEmpty
                    ]

        transFrame =
            transform
                -- Filter according to frame selection
                << filter (fiExpr "datum.type == 'Background'")

        transStation =
            -- Filter according to station selection
            transform
                << filter (fiSelection "stationSelection")

        specFrame =
            asSpec
                [ encFrame []
                , transFrame []
                , point
                    [ maSize 90
                    , maFilled False
                    , maStroke "black"
                    , maStrokeWidth 0.5
                    , maTooltip ttNone
                    ]
                ]

        specStation =
            asSpec
                [ encStation []
                , transStation []
                , selStation []
                , point
                    [ maSize 90
                    , maFill "grey"
                    ]
                ]
    in
    toVegaLite
        [ cfg []
        , width 300
        , height 300
        , data []
        , layer [ specFrame, specStation ]
        ]
```

### Visualisation 2

How busy each station is? How do stations compare to one another?
(_Note: Please enlarge preview tab to enjoy the full visualisation. Also feel free to play with interaction such as filter time intervals and zoom_)

```elm{l=hidden}
londonStation : Table
londonStation =
    -- Join grid and count of passangers
    leftJoin ( londonTubeFlow, "object" ) ( londonMapSchema, "object" )


londonRiver : Table
londonRiver =
    -- Store all other elements of the grid in a separate table
    rightDiff ( londonTubeFlow, "object" ) ( londonMapSchema, "object" )


londonGridMap : Table
londonGridMap =
    -- Join all information together (station, river and zone)
    outerJoin "key"
        ( insertIndexColumn "key" "s" londonStation, "key" )
        ( insertIndexColumn "key" "r" londonRiver, "key" )
        |> removeColumn "key"
```

```elm {v l=hidden interactive}
isotypeAllStations : Spec
isotypeAllStations =
    let
        stationPath =
            --"M0 0 l-3 0 L-5 -2 0z"
            "M0 0 h-10 v-10 h10 0z"

        -- cfg =
        --     configure
        -- << configuration (coView [ vicoStroke Nothing ])
        data =
            dataFromColumns []
                << dataColumn "gridRow" (londonGridMap |> Tidy.numColumn "RowReverse" |> nums)
                << dataColumn "gridCol" (londonGridMap |> Tidy.numColumn "Col" |> nums)
                << dataColumn "gridRowPerturbated" (londonGridMap |> Tidy.numColumn "rowSketch" |> nums)
                << dataColumn "gridColPerturbated" (londonGridMap |> Tidy.numColumn "colSketch" |> nums)
                << dataColumn "orientation" (londonGridMap |> Tidy.strColumn "gridOrientation" |> strs)
                << dataColumn "type" (londonGridMap |> Tidy.strColumn "Type" |> strs)
                << dataColumn "time" (londonGridMap |> Tidy.strColumn "time" |> strs)
                << dataColumn "flow" (londonGridMap |> Tidy.numColumn "count" |> nums)
                << dataColumn "object" (londonGridMap |> Tidy.strColumn "object" |> strs)
                << dataColumn "showZone" (londonGridMap |> Tidy.strColumn "showTubeZone" |> strs)
                << dataColumn "open" (londonGridMap |> Tidy.numColumn "open" |> nums)

        transData =
            -- This is to calculate the flow of passangers compared the average in each time slot (ie 30 mins)
            transform
                << window
                    [ ( [ wiAggregateOp opSum
                        , wiField "flow"
                        ]
                      , "totalFlowTime"
                      )
                    , ( [ wiAggregateOp opSum
                        , wiField "open"
                        ]
                      , "totalCountTime"
                      )
                    ]
                    [ wiGroupBy [ "time" ], wiFrame Nothing Nothing ]
                << calculateAs "datum.totalFlowTime/datum.totalCountTime" "averageFlow"
                << calculateAs "datum.flow/datum.averageFlow" "flowFromAverage"

        encZone1 =
            encoding
                << position X [ pName "gridCol", pMType Quantitative, pAxis [] ]
                << position Y [ pName "gridRow", pMType Quantitative, pAxis [] ]
                << tooltip [ tName "type", tMType Nominal ]

        encRiver =
            encoding
                << position X [ pName "gridCol", pMType Quantitative, pAxis [] ]
                << position Y [ pName "gridRow", pMType Quantitative, pAxis [] ]
                << tooltip [ tName "type", tMType Nominal ]

        encStationFrame =
            encoding
                << position X [ pName "gridCol", pMType Quantitative, pAxis [] ]
                << position Y [ pName "gridRow", pMType Quantitative, pAxis [] ]

        -- encStationFramePerturbated =
        --     encoding
        --         << position X [ pName "gridRowPerturbated", pMType Quantitative, pAxis [], pScale [ scDomain (doNums [ 10, 38.3 ]) ] ]
        --         << position Y [ pName "gridColPerturbated", pMType Quantitative, pAxis [], pScale [ scDomain (doNums [ 6, 38 ]) ] ]
        --<< tooltip [ tName "object", tMType Nominal ]
        encStation =
            encoding
                << position X [ pName "gridCol", pMType Quantitative, pAxis [] ]
                << position Y [ pName "gridRow", pMType Quantitative, pAxis [] ]
                << size
                    [ mSelectionCondition (selectionName "timeSelection")
                        -- Size when selected:
                        [ mName "flowFromAverage"
                        , mMType Quantitative
                        , mScale
                            [ scDomain (doNums [ 0, 2 ])
                            , scNice niFalse

                            -- Flannery Correction
                            , scType scPow
                            , scExponent 1.4
                            ]
                        , mLegend
                            [ leSymbolType symSquare
                            , leValues (leNums [ 0.5, 1, 2, 4, 8 ])
                            , leTitle "Compared to avg."
                            ]
                        ]
                        -- Size when _not_ selected:
                        []
                    ]
                << tooltips
                    [ [ tName "object", tMType Nominal ]
                    , [ tName "time", tMType Nominal ]
                    , [ tName "flowFromAverage", tMType Quantitative ]
                    ]

        selZoom =
            selection
                << select "zoomSelection" seInterval [ seBindScales ]

        selTime =
            selection
                << select "timeSelection"
                    seSingle
                    [ seFields [ "time" ]
                    , seBind
                        [ iSelect "time"
                            [ inName "Time?"
                            , inOptions listOfTimes
                            , inDebounce 25
                            ]
                        ]
                    , seEmpty
                    ]

        selZone =
            selection
                << select "zoneSelection"
                    seSingle
                    [ seFields [ "showZone" ]
                    , seBind
                        [ iRadio "showZone"
                            [ inName "Show Fare Zone 1?"
                            , inOptions
                                [ "Yes", "No" ]
                            ]
                        ]
                    , seInit [ ( "showZone", str "Yes" ) ]
                    ]

        transZone1 =
            -- Filter the table to keep only rows related to Zone1
            transform
                << filter (fiExpr "datum.type == 'Zone1'")
                << filter (fiSelection "zoneSelection")

        transRiver =
            -- Filter the table to keep only rows related to the Thames river
            transform
                << filter (fiExpr "datum.type == 'River'")

        transStationFrame =
            -- Filter the table to keep only rows related to Stations
            transform
                << filter (fiExpr "datum.type == 'Station'")

        transStation =
            -- Filter according to time selection
            transform
                << filter (fiSelection "timeSelection")

        specZone1 =
            asSpec
                [ encZone1 []
                , selZone []
                , transZone1 []
                , line
                    [ maInterpolate miCardinalClosed
                    , maTension 0.91

                    -- , maFill "lightgrey"
                    , maStrokeWidth 3
                    , maColor "rgb(220, 36, 31)"
                    , maOpacity 0.4
                    ]
                ]

        specRiver =
            asSpec
                [ encRiver []
                , transRiver []
                , line
                    [ maInterpolate miMonotone
                    , maStrokeWidth 5
                    , maColor "rgb(0, 160, 226)"
                    , maOpacity 1
                    ]
                ]

        specStationFrame =
            asSpec
                [ encStationFrame []
                , selZoom []
                , transStationFrame []
                , square
                    [ maSize 70
                    , maFilled False
                    , maStroke "black"
                    , maStrokeWidth 0.1
                    , maStrokeOpacity 0.5
                    , maStrokeJoin joRound
                    , maTooltip ttNone
                    ]
                ]

        -- specStationFramePerturbated =
        --     -- This is to add sketchiness to station frame
        --     asSpec
        --         [ encStationFramePerturbated []
        --         , transStationFrame []
        --         , square
        --             [ maSize 100
        --             , maFilled False
        --             , maStroke "black"
        --             , maStrokeWidth 0.2
        --             , maStrokeOpacity 1
        --             , maStrokeJoin joRound
        --             ]
        --         ]
        specStation =
            asSpec
                [ encStation []
                , selTime []
                , transStation []
                , square
                    [ maFill "rgb(0,25,168)"
                    , maOpacity 0.6
                    , maStroke "rgb(0,25,168)"
                    , maStrokeOpacity 1
                    , maStrokeWidth 0.1
                    , maStrokeJoin joRound
                    , maStrokeCap caRound
                    ]
                ]

        res =
            resolve
                << resolution
                    (reScale
                        [ ( chShape, reIndependent )
                        , ( chColor, reIndependent )
                        ]
                    )
    in
    toVegaLite
        [ height 600, width 800, data [], transData [], res [], layer [ specRiver, specZone1, specStationFrame, specStation ] ]
```

{|visualization)}

{(insights|}

The visualisations show interesting patterns both within individual stations and between stations, including the impact of passengers flows on different geographical areas of London.

### Visualisation 1

Visualisation 1 shows total number of passengers entering or exiting (hereinafter passengers flow) each tube station as fractions of the tube station capacity at 6 different time intervals. The interpretation is the following: 10/10 passengers means that the station reached capacity and therefore is exceptionally busy, 5/10 means that the station is half full (or some would say half empty) and so on and so forth. Note: The total capacity of the station has been estimated considering TfL loading data for each station.

Visualisation 1 shows that the London tube network is characterised by interesting patterns. For instance, Bank & Monument or Canary Wharf station are very busy during AM Peak and PM Peak suggesting these stations are predominately used by commuters. Conversely, Bayswater station or Leicester square have spikes at Inter Peaks times or late at night suggesting that these stations are also used by tourists or party-goers.

Interestingly, some stations show peaks only at specific times of the day. For example, Rickmansworth or Stockwell stations are very busy at AM Peak but they are not as busy for the rest of the day. A similar flow but at PM Peak hours can be found for Old street or North Greenwich. This result is very interesting since it contradicts the expectation that stations have a sort of cycle whereby people get in the tube in the morning and come back later in the evening.

In addition to this, the visualisation shows that the total number of passengers reaches (almost) full capacity for many stations during at least one specific time during the day. This is especially true for train stations (e.g. King’s Cross).

### Visualisation 2

Visualisation 2 shows total passengers flow for each station as a multiple of the London average for each 30 mins time intervals. To illustrate, a passengers flow equal to ‘2x’ between 6.00-6.30 AM means that that station has a passengers flow which is 2 times larger than the London average at that specific time.

This visualisation shows that there is a large variation in the number of passengers at each individual station, even for station that are relatively close to each other (10/20 mins walking). As an example, Upton Park has a passengers flow equal to 2x the London average between 6.30-7.00 AM whereas Plaistow shows a flow that is very close to the average at that time.

Moreover, the visualisation shows complex patterns when comparing flows in different areas of London. While there are similar flows in North and South London, this does not appear to be the case when comparing West vs East London. This is particularly true in the early AM hours (e.g. 5.00-5.30AM) where East London stations show passengers flows well above the London average compared to the majority of the stations in the West.

It is also worth noting that train stations are usually quite busy throughout the day and can get exceptionally busy at specific time intervals (as seen in visualisation 1 and in line with the principle of representation invariance [1]).

Overall, one day of passengers flows on the London underground network looks like the following
(_Note: Please click play on the video below - it is only 1 min and 33 seconds long. Also remember to enlarge the preview tab_):

<video width="800" height="600" controls>
  <source src="oneDayinLondonFinal.mov" type="video/mp4">
</video>

{|insights)}

{(designJustification|}

### Visualisation 1

#### Design approach

For visualisation 1, the source of inspiration is my recent visit to Heathrow terminal 5. In the terminal, there are two big screens indicating how busy each security gate is (see pic below). I think this visualisation is very effective since within seconds passengers can get an intuition of the waiting time at the security gates, compare them and take an informed decision without even knowing the actual number of people actually queueing at each gate.

![source1](../EA_Alemani_coursework/T5security.jpeg)
source: https://www.bella-beraet.de/images/2014-07-15_London_Heathrow_Security.JPG

Following [Tufte’s design principles](https://medium.com/adventures-in-data-design-development/the-tufte-totem-in-information-designland-1c887bffc1f4), I generate a minimalist visualisation which lets the data speak for itself and maximise the data-ink ratio by limiting the use of non-data ink to the y axis labels and interaction buttons. The non-data ink is necessary to interpret and explore patterns in the data.

#### Layout

The layout is a grid where icons are lined up to generate a series of vertically aligned bars. The reason for this is to show the progression of the number of passengers through time while facilitating comparison. In fact, users need to vertically scan the chart only once to quickly spot the busiest hours of the day and to compare time intervals against one another.

#### Symbolisation and visual variables

###### Symbolisation

I use Scalable Vector Graphics (SVG) path in order to draw repeating graphics symbolising male/female passengers [2]. By combining visual language (i.e. icons) with the representation of quantitative data, the visualisation is easier to read and understand because, as noted by R. Kosara in [3], the visualisation themselves contains hints to their subject matter.

This system known as isotype is very effective in this context where the aim is for users to draw conclusions / extract a story from the data with limited cognitive effort.

###### Colour, stroke and size

The visualisation consists of two juxtaposed layers: (i) a low-level layer showing the outline of each icon (i.e. no fill) and representing the capacity of each station, and (ii) an upper-level layer displaying the colour fill and depicting passengers flow. The use of two layers is to produce an effect similar to passengers filling up the floor area of the station and comparable to sea waves crashing on the seaside.

The fill colour is grey. I choose this colour because it is gender and race neutral. Also, it can be easily detected without alteration by colour blind users (tested using Color Oracle colour blindness simulator).

The size of each icon is fixed to 90 square units. The reason for this is to avoid overlapping icons while guaranteeing a visualisation that is aesthetically pleasing.

#### Interaction

The interaction consists of a drop-down menu where users can select the stations they are interested in. This interaction allows users to focus their attention on one station at a time.

Given the very large number of underground stations, alternative interactions which filter data by time interval while showing all stations would not be viable options. Despite these alternatives would enable users to make comparison between stations, it would also mean presenting too much information, leading users scrolling up and down the visualisation multiple times in the attempt to read, remember and compare patterns. Similarly, the use of multiples (one for each station) could probably cause information overload too.

The interaction also includes a tooltip showing the fraction of capacity taken by passengers. This is mainly to ease the comparison between time intervals (i.e. no need to count icons).

### Visualisation 2

#### Design approach

For visualisation 2, the source of inspiration is my educational background in economics. As an economist, my work is to translate the complexity of consumers’ choices or firms’ strategies into mathematical models which are usually a simplified version of reality.
I believe that the London tube map [4] is a good example of a simple model: it simplifies the complexity of the underground network by relaxing the geography of London. The result is a map that is easy to read, understand and remember.

Following [data humanism design principles](https://medium.com/@giorgialupi/data-humanism-the-revolution-will-be-visualized-31486a30dbfb), I hand-construct a simple map of London which shows the location of tube stations along with the river Thames and fare zone 1 which have the role to provide some geographical context for the users.

To reflect the fact that everything has been drawn manually, the design contains element of ‘sketchiness’ to communicate a sense of uncertainty and reduce the ‘formality’ of the visualisation so that users can feel comfortable playing with it. This sketchy drawing style is inspired by [5] and [6].

#### Layout

The layout consists of a grid where each tube station is positioned at specific row and column coordinates. The map resembles the TfL underground map issued in May 2010. The reason for this choice is that the TfL map is widely recognised as an iconic design and is an integral part of life for everyone living London.

#### Symbolisation and visual variables

###### Symbolisation

The symbols used are the following:
• a polygon to show fare zone 1;
• a line showing the river Thames;
• a square of fixed size (locationSquare) showing the location of each tube station; and
• a square of variable size (paxSquare) showing passengers flows.

While the symbols for fare zones and the river Thames are self-explanatory, for tube stations I use a square symbol because, I think, it is relatively easy to find the center of a square compared to other symbols such as triangles, circles or rectangles. This is key for this visualisation where users must be able to identify the center of each paxSquare (i.e. the locationSquare) for meaningful interpretation of the results.

###### Colour, stroke and size

For all symbols used in the visualisation, the colours correspond to the TfL colour standard [7]. The reason for this choice is because I want to use something the users might be already familiar with and also give a realistic touch to this visualisation as if it were a ‘real tool’ published on TfL website.

To add a sense of 'sketchiness' typical of hand-drawn maps, I use interpolation with tension lower than 1 to depict the river Thames and fare zone 1. This technique is used to make lines and shapes look ‘sketchy’ and give an idea of uncertainty and imperfection. Similarly, I have added a round stroke join to both locationSquare and paxSquare. However, this does not achieve the same degree of 'sketchy drawing style'. I have explored alternative approaches such as perturbing coordinates of each square and juxtaposing original and perturbed symbols on one another. However, the result looked like a series of out-of-focus square and I have eventually abandoned the idea (see code block commented out).

The size of the river Thames, fare zone1 and locationSquare is fixed whereas paxSquare varies according to passengers flows as a multiple of the London average, including a Flannery correction of exponent 1.4 so that size is perceived as proportional to magnitude.

#### Interaction

There are three interactions in this visualisation which follows Shneiderman’s mantra “Overview first, zoom and filter then details-on-demand”.

The first is a drop-down menu where users can choose the time interval they are interest in. This is to allow the comparison between tube station across the entire London underground network. The second is a radio button that can be used to hide fare zone 1. The reason for this is that for some users the fare zone 1 polygon might not have any added value but rather clutter the visualisation. The third is the possibility to zoom so that users can concentrate on specific areas of the tube network, boroughs etc etc.

The interaction also has a personalised tooltips showing the name of the station, time of the day selected by the user and passengers flow as a multiple of the London average for that specific time. This is to facilitate visual exploration.

{|designJustification)}

{(validation|}

I believe that both visualisation 1 and visualisation 2 are very effective not only to find answers to my research questions but also to identify some interesting patterns in the data that would have probably very difficult to discover in big excel or SQL tables.

Visualisation 1 provides users with a simple, clean and minimal interface. It is also very intuitive and little instructions are required to be able to read or understand patterns. In general, users can satisfy their information need with very limited cognitive effort, without being distracted or side-tracked by too much information.

Nonetheless, the visualisation is restricted to display only one station at a time. This makes comparison between stations quite difficult, especially for users with short term memory deficit (e.g. dyslexic users). Moreover, this visualisation only works if we show aggregated time intervals which means users can only draw simple high-level conclusions, especially when compared to a visualisation showing passengers counts at 15 minutes time intervals. Further work could include the use of two multiples concatenated side-by-side where users can select, compare and contrast the patterns of two different stations simultaneously.

Visualisation 2 provides users with a design that tries to combine both ‘logos’ and ‘pathos’. Users can keep clicking on random time intervals and every time be amused by an unexpected station-specific spike. Also, I believe the visaulisation conveys a sense of movement as if tube stations are floating up and down on the map or as if areas of London are distorted by the flow of passengers. At the same time, though, the visualisation enables quite an accurate comparison of passengers flows between stations.

However, given that fare zone 1 attracts a very large number of passengers throughout the day, sometimes it becomes a bit difficult to compare stations across the entire underground network without the use of the zoom. Also, users can only focus on one time interval at a time and therefore might find difficult to get an overview of passengers flows during the full day without the possibility to watch animated transitions. Further work would involve the creation of short animations. I have investigated the possibility to add a javascript recording button but unfortunately, I could not manage to make it work. Also, I would like to improve the sketchiness appearance of the stations (both locationSquare and paxSquare). For locationSquare, a potential solution could be to draw each square using interpolation and different value for tension. However, there are 268 stations in the London network which means this is quite a burdensome exercise. I cold not find an ad-hoc alternative for paxSquare.

The map could be also enriched by adding tube lines (i.e. Circle, Jubilee, Central etc etc) or other London famous landmarks such as the Royal Parks whose outlines are quite iconic. This could help less experienced Londoners to navigate the map.

A final technical refinement could be the possibility to use the median in the data transformation step (instead of the mean) to see how the results might change. Additional work could also include analysis for weekends passengers flow.

{|validation)}

{(references|}

[1] **Kindlmann, G. and Scheidegger, C.** (2014) An algebraic process for visualization design IEEE transactions on Visualization and Computer Braphics 20(12), pp.2181-2190

[2] **Smith, A.** (2019) Pictogram grid in d3js [Online]. [Available at http://bl.ocks.org/alansmithy/d832fc03f6e6a91e99f4] (Accessed 3 April 2019)

[3] **Kosara, R.** (2013) The isotype [Online]. [Available at https://eagereyes.org/techniques/isotype] (Accessed 3 April 2019)

[4] **BBC** (2010) London Underground Map [Online]. [Available at http://www.bbc.co.uk/london/travel/downloads/tube_map.html] (Accessed 6 March 2019)

[5] **Wood, J., Isenberg, P., Isenberg, T., Dykes, J., Boukhelifa, N. & Slingsby, A.** (2012). Sketchy rendering for information visualization. IEEE Transactions on Visualization and Computer Graphics, 18(12), pp. 2749-2758. doi: 10.1109/TVCG.2012.262

[6] **giCentre** (2017) Handy gallery [Online]. [Available at https://www.gicentre.net/handy/gallery/] (Accessed 3 April 2019)

[7] **Transport for London** (2016) Colour standard [Online]. [Available at http://content.tfl.gov.uk/tfl-colour-standards-issue04.pdf] (Accessed 10 April 2019)

### Data sources

**TfL** London Underground passenger counts data (En17week.csv, Ex17week.csv).
[Available at https://api-portal.tfl.gov.uk/docs]

**TfL** Busiest times on trains and in stations (LUTrainLoadingData.csv). [Available at http://crowding.data.tfl.gov.uk/]

{|references)}
