---
id: litvis

elm:
  dependencies:
    gicentre/elm-vegalite: latest
    gicentre/tidy: latest

follows: importDataAndSettings.md
---

@import "css/datavis.less"


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


The visualisations show interesting patterns both within individual stations and between stations, including the impact of passengers flows on different geographical areas of London.

### Visualisation 1
Visualisation 1 shows total number of passengers entering or exiting (hereinafter passengers flow) each tube station as fractions of the tube station capacity at 6 different time intervals. The interpretation is the following: 10/10 passengers means that the station reached capacity and therefore is exceptionally busy, 5/10 means that the station is half full (or some would say half empty) and so on and so forth. Note: The total capacity of the station has been estimated considering TfL loading data for each station.

Visualisation 1 shows that the London tube network is characterised by interesting patterns. For instance, Bank & Monument or Canary Wharf station are very busy during AM Peak and PM Peak suggesting these stations are predominately used by commuters. Conversely, Bayswater station or Leicester square have spikes at Inter Peaks times or late at night suggesting that these stations are also used by tourists or party-goers.

Interestingly, some stations show peaks only at specific times of the day. For example, Rickmansworth or Stockwell stations are very busy at AM Peak but they are not as busy for the rest of the day. A similar flow but at PM Peak hours can be found for Old street or North Greenwich. This result is very interesting since it contradicts the expectation that stations have a sort of cycle whereby people get in the tube in the morning and come back later in the evening.

In addition to this, the visualisation shows that the total number of passengers reaches (almost) full capacity for many stations during at least one specific time during the day. This is especially true for train stations (e.g. King’s Cross).


#### Design approach
For visualisation 1, the source of inspiration is my recent visit to Heathrow terminal 5. In the terminal, there are two big screens indicating how busy each security gate is (see pic below). I think this visualisation is very effective since within seconds passengers can get an intuition of the waiting time at the security gates, compare them and take an informed decision without even knowing the actual number of people actually queueing at each gate.

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
