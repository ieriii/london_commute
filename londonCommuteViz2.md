---
id: litvis

elm:
  dependencies:
    gicentre/elm-vegalite: latest
    gicentre/tidy: latest

follows: importDataAndSettings.md
---

@import "css/datavis.less"


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

### Visualisation 2

Visualisation 2 shows total passengers flow for each station as a multiple of the London average for each 30 mins time intervals. To illustrate, a passengers flow equal to ‘2x’ between 6.00-6.30 AM means that that station has a passengers flow which is 2 times larger than the London average at that specific time.

This visualisation shows that there is a large variation in the number of passengers at each individual station, even for station that are relatively close to each other (10/20 mins walking). As an example, Upton Park has a passengers flow equal to 2x the London average between 6.30-7.00 AM whereas Plaistow shows a flow that is very close to the average at that time.

Moreover, the visualisation shows complex patterns when comparing flows in different areas of London. While there are similar flows in North and South London, this does not appear to be the case when comparing West vs East London. This is particularly true in the early AM hours (e.g. 5.00-5.30AM) where East London stations show passengers flows well above the London average compared to the majority of the stations in the West.

It is also worth noting that train stations are usually quite busy throughout the day and can get exceptionally busy at specific time intervals (as seen in visualisation 1 and in line with the principle of representation invariance [1]).


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

I believe that both visualisation 1 and visualisation 2 are very effective not only to find answers to my research questions but also to identify some interesting patterns in the data that would have probably very difficult to discover in big excel or SQL tables.

Visualisation 1 provides users with a simple, clean and minimal interface. It is also very intuitive and little instructions are required to be able to read or understand patterns. In general, users can satisfy their information need with very limited cognitive effort, without being distracted or side-tracked by too much information.

Nonetheless, the visualisation is restricted to display only one station at a time. This makes comparison between stations quite difficult, especially for users with short term memory deficit (e.g. dyslexic users). Moreover, this visualisation only works if we show aggregated time intervals which means users can only draw simple high-level conclusions, especially when compared to a visualisation showing passengers counts at 15 minutes time intervals. Further work could include the use of two multiples concatenated side-by-side where users can select, compare and contrast the patterns of two different stations simultaneously.

Visualisation 2 provides users with a design that tries to combine both ‘logos’ and ‘pathos’. Users can keep clicking on random time intervals and every time be amused by an unexpected station-specific spike. Also, I believe the visaulisation conveys a sense of movement as if tube stations are floating up and down on the map or as if areas of London are distorted by the flow of passengers. At the same time, though, the visualisation enables quite an accurate comparison of passengers flows between stations.

However, given that fare zone 1 attracts a very large number of passengers throughout the day, sometimes it becomes a bit difficult to compare stations across the entire underground network without the use of the zoom. Also, users can only focus on one time interval at a time and therefore might find difficult to get an overview of passengers flows during the full day without the possibility to watch animated transitions. Further work would involve the creation of short animations. I have investigated the possibility to add a javascript recording button but unfortunately, I could not manage to make it work. Also, I would like to improve the sketchiness appearance of the stations (both locationSquare and paxSquare). For locationSquare, a potential solution could be to draw each square using interpolation and different value for tension. However, there are 268 stations in the London network which means this is quite a burdensome exercise. I cold not find an ad-hoc alternative for paxSquare.

The map could be also enriched by adding tube lines (i.e. Circle, Jubilee, Central etc etc) or other London famous landmarks such as the Royal Parks whose outlines are quite iconic. This could help less experienced Londoners to navigate the map.

A final technical refinement could be the possibility to use the median in the data transformation step (instead of the mean) to see how the results might change. Additional work could also include analysis for weekends passengers flow.