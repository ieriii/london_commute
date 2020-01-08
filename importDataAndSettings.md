---
id: litvis

narrative-schemas:
  - narrative-schemas/vizSchema.yml

elm:
  dependencies:
    gicentre/elm-vegalite: latest
    gicentre/tidy: latest
---

@import "../css/datavis.less"

```elm {l=hidden}
import Tidy exposing (..)
import VegaLite exposing (..)
```

```elm{l=hidden}
listOfStations : List String



-- This is a list of stations


listOfStations =
    [ "Please select a station"
    , "Acton Town"
    , "Aldgate"
    , "Aldgate East"
    , "Alperton"
    , "Amersham"
    , "Angel"
    , "Archway"
    , "Arnos Grove"
    , "Arsenal"
    , "Baker Street"
    , "Balham"
    , "Bank & Monument"
    , "Barbican"
    , "Barking"
    , "Barkingside"
    , "Barons Court"
    , "Bayswater"
    , "Becontree"
    , "Belsize Park"
    , "Bermondsey"
    , "Bethnal Green"
    , "Blackfriars"
    , "Blackhorse Road"
    , "Bond Street"
    , "Borough"
    , "Boston Manor"
    , "Bounds Green"
    , "Bow Road"
    , "Brent Cross"
    , "Brixton"
    , "Bromley-by-Bow"
    , "Buckhurst Hill"
    , "Burnt Oak"
    , "Caledonian Road"
    , "Camden Town"
    , "Canada Water"
    , "Canary Wharf"
    , "Canning Town"
    , "Cannon Street"
    , "Canons Park"
    , "Chalfont & Latimer"
    , "Chalk Farm"
    , "Chancery Lane"
    , "Charing Cross"
    , "Chesham"
    , "Chigwell"
    , "Chiswick Park"
    , "Chorleywood"
    , "Clapham Common"
    , "Clapham North"
    , "Clapham South"
    , "Cockfosters"
    , "Colindale"
    , "Colliers Wood"
    , "Covent Garden"
    , "Croxley"
    , "Dagenham East"
    , "Dagenham Heathway"
    , "Debden"
    , "Dollis Hill"
    , "Ealing Broadway"
    , "Ealing Common"
    , "Earl's Court"
    , "East Acton"
    , "East Finchley"
    , "East Ham"
    , "East Putney"
    , "Eastcote"
    , "Edgware"
    , "Edgware Road (Bak)"
    , "Edgware Road (Cir)"
    , "Elephant & Castle"
    , "Elm Park"
    , "Embankment"
    , "Epping"
    , "Euston"
    , "Euston Square"
    , "Fairlop"
    , "Farringdon"
    , "Finchley Central"
    , "Finchley Road"
    , "Finsbury Park"
    , "Fulham Broadway"
    , "Gants Hill"
    , "Gloucester Road"
    , "Golders Green"
    , "Goldhawk Road"
    , "Goodge Street"
    , "Grange Hill"
    , "Great Portland Street"
    , "Green Park"
    , "Greenford"
    , "Gunnersbury"
    , "Hainault"
    , "Hammersmith (Dis)"
    , "Hammersmith (H&C)"
    , "Hampstead"
    , "Hanger Lane"
    , "Harlesden"
    , "Harrow & Wealdstone"
    , "Harrow-on-the-Hill"
    , "Hatton Cross"
    , "Heathrow Terminals 123"
    , "Heathrow Terminal 4"
    , "Heathrow Terminal 5"
    , "Hendon Central"
    , "High Barnet"
    , "High Street Kensington"
    , "Highbury & Islington"
    , "Highgate"
    , "Hillingdon"
    , "Holborn"
    , "Holland Park"
    , "Holloway Road"
    , "Hornchurch"
    , "Hounslow Central"
    , "Hounslow East"
    , "Hounslow West"
    , "Hyde Park Corner"
    , "Ickenham"
    , "Kennington"
    , "Kensal Green"
    , "Kensington (Olympia)"
    , "Kentish Town"
    , "Kenton"
    , "Kew Gardens"
    , "Kilburn"
    , "Kilburn Park"
    , "King's Cross St. Pancras"
    , "Kingsbury"
    , "Knightsbridge"
    , "Ladbroke Grove"
    , "Lambeth North"
    , "Lancaster Gate"
    , "Latimer Road"
    , "Leicester Square"
    , "Leyton"
    , "Leytonstone"
    , "Liverpool Street"
    , "London Bridge"
    , "Loughton"
    , "Maida Vale"
    , "Manor House"
    , "Mansion House"
    , "Marble Arch"
    , "Marylebone"
    , "Mile End"
    , "Mill Hill East"
    , "Moor Park"
    , "Moorgate"
    , "Morden"
    , "Mornington Crescent"
    , "Neasden"
    , "Newbury Park"
    , "North Acton"
    , "North Ealing"
    , "North Greenwich"
    , "North Harrow"
    , "North Wembley"
    , "Northfields"
    , "Northolt"
    , "Northwick Park"
    , "Northwood"
    , "Northwood Hills"
    , "Notting Hill Gate"
    , "Oakwood"
    , "Old Street"
    , "Osterley"
    , "Oval"
    , "Oxford Circus"
    , "Paddington"
    , "Park Royal"
    , "Parsons Green"
    , "Perivale"
    , "Piccadilly Circus"
    , "Pimlico"
    , "Pinner"
    , "Plaistow"
    , "Preston Road"
    , "Putney Bridge"
    , "Queen's Park"
    , "Queensbury"
    , "Queensway"
    , "Ravenscourt Park"
    , "Rayners Lane"
    , "Redbridge"
    , "Regent's Park"
    , "Richmond"
    , "Rickmansworth"
    , "Roding Valley"
    , "Royal Oak"
    , "Ruislip"
    , "Ruislip Gardens"
    , "Ruislip Manor"
    , "Russell Square"
    , "Seven Sisters"
    , "Shepherd's Bush (Cen)"
    , "Shepherd's Bush (H&C)"
    , "Sloane Square"
    , "Snaresbrook"
    , "South Ealing"
    , "South Harrow"
    , "South Kensington"
    , "South Kenton"
    , "South Ruislip"
    , "South Wimbledon"
    , "South Woodford"
    , "Southfields"
    , "Southgate"
    , "Southwark"
    , "St. James's Park"
    , "St. John's Wood"
    , "St. Paul's"
    , "Stamford Brook"
    , "Stanmore"
    , "Stepney Green"
    , "Stockwell"
    , "Stonebridge Park"
    , "Stratford"
    , "Sudbury Hill"
    , "Sudbury Town"
    , "Swiss Cottage"
    , "Temple"
    , "Theydon Bois"
    , "Tooting Bec"
    , "Tooting Broadway"
    , "Tottenham Court Road"
    , "Tottenham Hale"
    , "Totteridge & Whetstone"
    , "Tower Hill"
    , "Tufnell Park"
    , "Turnham Green"
    , "Turnpike Lane"
    , "Upminster"
    , "Upminster Bridge"
    , "Upney"
    , "Upton Park"
    , "Uxbridge"
    , "Vauxhall"
    , "Victoria"
    , "Walthamstow Central"
    , "Wanstead"
    , "Warren Street"
    , "Warwick Avenue"
    , "Waterloo"
    , "Watford"
    , "Wembley Central"
    , "Wembley Park"
    , "West Acton"
    , "West Brompton"
    , "West Finchley"
    , "West Ham"
    , "West Hampstead"
    , "West Harrow"
    , "West Kensington"
    , "West Ruislip"
    , "Westbourne Park"
    , "Westminster"
    , "White City"
    , "Whitechapel"
    , "Willesden Green"
    , "Willesden Junction"
    , "Wimbledon"
    , "Wimbledon Park"
    , "Wood Green"
    , "Wood Lane"
    , "Woodford"
    , "Woodside Park"
    ]

londonTubeFlowNorm : Table
londonTubeFlowNorm =
        """object	time	count	id	tooltip	type
    Acton Town	Early	1	0	1/10	Station
    Acton Town	AM Peak	6	0	6/10	Station
    Acton Town	AM Peak	6	1	6/10	Station
    Acton Town	AM Peak	6	2	6/10	Station
    Acton Town	AM Peak	6	3	6/10	Station
    Acton Town	AM Peak	6	4	6/10	Station
    Acton Town	AM Peak	6	5	6/10	Station
    Acton Town	Inter Peak	5	0	5/10	Station
    Acton Town	Inter Peak	5	1	5/10	Station
    Acton Town	Inter Peak	5	2	5/10	Station
    Acton Town	Inter Peak	5	3	5/10	Station
    Acton Town	Inter Peak	5	4	5/10	Station
    Acton Town	PM Peak	6	0	6/10	Station
    Acton Town	PM Peak	6	1	6/10	Station
    Acton Town	PM Peak	6	2	6/10	Station
    Acton Town	PM Peak	6	3	6/10	Station
    Acton Town	PM Peak	6	4	6/10	Station
    Acton Town	PM Peak	6	5	6/10	Station
    Acton Town	Evening	3	0	3/10	Station
    Acton Town	Evening	3	1	3/10	Station
    Acton Town	Evening	3	2	3/10	Station
    Acton Town	Late	2	0	2/10	Station
    Acton Town	Late	2	1	2/10	Station
    Aldgate	AM Peak	6	0	6/10	Station
    Aldgate	AM Peak	6	1	6/10	Station
    Aldgate	AM Peak	6	2	6/10	Station
    Aldgate	AM Peak	6	3	6/10	Station
    Aldgate	AM Peak	6	4	6/10	Station
    Aldgate	AM Peak	6	5	6/10	Station
    Aldgate	Inter Peak	4	0	4/10	Station
    Aldgate	Inter Peak	4	1	4/10	Station
    Aldgate	Inter Peak	4	2	4/10	Station
    Aldgate	Inter Peak	4	3	4/10	Station
    Aldgate	PM Peak	5	0	5/10	Station
    Aldgate	PM Peak	5	1	5/10	Station
    Aldgate	PM Peak	5	2	5/10	Station
    Aldgate	PM Peak	5	3	5/10	Station
    Aldgate	PM Peak	5	4	5/10	Station
    Aldgate	Evening	1	0	1/10	Station
    Aldgate East	AM Peak	6	0	6/10	Station
    Aldgate East	AM Peak	6	1	6/10	Station
    Aldgate East	AM Peak	6	2	6/10	Station
    Aldgate East	AM Peak	6	3	6/10	Station
    Aldgate East	AM Peak	6	4	6/10	Station
    Aldgate East	AM Peak	6	5	6/10	Station
    Aldgate East	Inter Peak	6	0	6/10	Station
    Aldgate East	Inter Peak	6	1	6/10	Station
    Aldgate East	Inter Peak	6	2	6/10	Station
    Aldgate East	Inter Peak	6	3	6/10	Station
    Aldgate East	Inter Peak	6	4	6/10	Station
    Aldgate East	Inter Peak	6	5	6/10	Station
    Aldgate East	PM Peak	6	0	6/10	Station
    Aldgate East	PM Peak	6	1	6/10	Station
    Aldgate East	PM Peak	6	2	6/10	Station
    Aldgate East	PM Peak	6	3	6/10	Station
    Aldgate East	PM Peak	6	4	6/10	Station
    Aldgate East	PM Peak	6	5	6/10	Station
    Aldgate East	Evening	3	0	3/10	Station
    Aldgate East	Evening	3	1	3/10	Station
    Aldgate East	Evening	3	2	3/10	Station
    Aldgate East	Late	1	0	1/10	Station
    Alperton	Early	1	0	1/10	Station
    Alperton	AM Peak	5	0	5/10	Station
    Alperton	AM Peak	5	1	5/10	Station
    Alperton	AM Peak	5	2	5/10	Station
    Alperton	AM Peak	5	3	5/10	Station
    Alperton	AM Peak	5	4	5/10	Station
    Alperton	Inter Peak	5	0	5/10	Station
    Alperton	Inter Peak	5	1	5/10	Station
    Alperton	Inter Peak	5	2	5/10	Station
    Alperton	Inter Peak	5	3	5/10	Station
    Alperton	Inter Peak	5	4	5/10	Station
    Alperton	PM Peak	6	0	6/10	Station
    Alperton	PM Peak	6	1	6/10	Station
    Alperton	PM Peak	6	2	6/10	Station
    Alperton	PM Peak	6	3	6/10	Station
    Alperton	PM Peak	6	4	6/10	Station
    Alperton	PM Peak	6	5	6/10	Station
    Alperton	Evening	2	0	2/10	Station
    Alperton	Evening	2	1	2/10	Station
    Alperton	Late	1	0	1/10	Station
    Amersham	Early	1	0	1/10	Station
    Amersham	AM Peak	5	0	5/10	Station
    Amersham	AM Peak	5	1	5/10	Station
    Amersham	AM Peak	5	2	5/10	Station
    Amersham	AM Peak	5	3	5/10	Station
    Amersham	AM Peak	5	4	5/10	Station
    Amersham	Inter Peak	3	0	3/10	Station
    Amersham	Inter Peak	3	1	3/10	Station
    Amersham	Inter Peak	3	2	3/10	Station
    Amersham	PM Peak	4	0	4/10	Station
    Amersham	PM Peak	4	1	4/10	Station
    Amersham	PM Peak	4	2	4/10	Station
    Amersham	PM Peak	4	3	4/10	Station
    Amersham	Evening	2	0	2/10	Station
    Amersham	Evening	2	1	2/10	Station
    Amersham	Late	1	0	1/10	Station
    Angel	AM Peak	8	0	8/10	Station
    Angel	AM Peak	8	1	8/10	Station
    Angel	AM Peak	8	2	8/10	Station
    Angel	AM Peak	8	3	8/10	Station
    Angel	AM Peak	8	4	8/10	Station
    Angel	AM Peak	8	5	8/10	Station
    Angel	AM Peak	8	6	8/10	Station
    Angel	AM Peak	8	7	8/10	Station
    Angel	Inter Peak	9	0	9/10	Station
    Angel	Inter Peak	9	1	9/10	Station
    Angel	Inter Peak	9	2	9/10	Station
    Angel	Inter Peak	9	3	9/10	Station
    Angel	Inter Peak	9	4	9/10	Station
    Angel	Inter Peak	9	5	9/10	Station
    Angel	Inter Peak	9	6	9/10	Station
    Angel	Inter Peak	9	7	9/10	Station
    Angel	Inter Peak	9	8	9/10	Station
    Angel	PM Peak	9	0	9/10	Station
    Angel	PM Peak	9	1	9/10	Station
    Angel	PM Peak	9	2	9/10	Station
    Angel	PM Peak	9	3	9/10	Station
    Angel	PM Peak	9	4	9/10	Station
    Angel	PM Peak	9	5	9/10	Station
    Angel	PM Peak	9	6	9/10	Station
    Angel	PM Peak	9	7	9/10	Station
    Angel	PM Peak	9	8	9/10	Station
    Angel	Evening	5	0	5/10	Station
    Angel	Evening	5	1	5/10	Station
    Angel	Evening	5	2	5/10	Station
    Angel	Evening	5	3	5/10	Station
    Angel	Evening	5	4	5/10	Station
    Angel	Late	2	0	2/10	Station
    Angel	Late	2	1	2/10	Station
    Archway	Early	1	0	1/10	Station
    Archway	AM Peak	8	0	8/10	Station
    Archway	AM Peak	8	1	8/10	Station
    Archway	AM Peak	8	2	8/10	Station
    Archway	AM Peak	8	3	8/10	Station
    Archway	AM Peak	8	4	8/10	Station
    Archway	AM Peak	8	5	8/10	Station
    Archway	AM Peak	8	6	8/10	Station
    Archway	AM Peak	8	7	8/10	Station
    Archway	Inter Peak	7	0	7/10	Station
    Archway	Inter Peak	7	1	7/10	Station
    Archway	Inter Peak	7	2	7/10	Station
    Archway	Inter Peak	7	3	7/10	Station
    Archway	Inter Peak	7	4	7/10	Station
    Archway	Inter Peak	7	5	7/10	Station
    Archway	Inter Peak	7	6	7/10	Station
    Archway	PM Peak	7	0	7/10	Station
    Archway	PM Peak	7	1	7/10	Station
    Archway	PM Peak	7	2	7/10	Station
    Archway	PM Peak	7	3	7/10	Station
    Archway	PM Peak	7	4	7/10	Station
    Archway	PM Peak	7	5	7/10	Station
    Archway	PM Peak	7	6	7/10	Station
    Archway	Evening	4	0	4/10	Station
    Archway	Evening	4	1	4/10	Station
    Archway	Evening	4	2	4/10	Station
    Archway	Evening	4	3	4/10	Station
    Archway	Late	2	0	2/10	Station
    Archway	Late	2	1	2/10	Station
    Arnos Grove	Early	1	0	1/10	Station
    Arnos Grove	AM Peak	5	0	5/10	Station
    Arnos Grove	AM Peak	5	1	5/10	Station
    Arnos Grove	AM Peak	5	2	5/10	Station
    Arnos Grove	AM Peak	5	3	5/10	Station
    Arnos Grove	AM Peak	5	4	5/10	Station
    Arnos Grove	Inter Peak	4	0	4/10	Station
    Arnos Grove	Inter Peak	4	1	4/10	Station
    Arnos Grove	Inter Peak	4	2	4/10	Station
    Arnos Grove	Inter Peak	4	3	4/10	Station
    Arnos Grove	PM Peak	5	0	5/10	Station
    Arnos Grove	PM Peak	5	1	5/10	Station
    Arnos Grove	PM Peak	5	2	5/10	Station
    Arnos Grove	PM Peak	5	3	5/10	Station
    Arnos Grove	PM Peak	5	4	5/10	Station
    Arnos Grove	Evening	2	0	2/10	Station
    Arnos Grove	Evening	2	1	2/10	Station
    Arnos Grove	Late	1	0	1/10	Station
    Arsenal	AM Peak	6	0	6/10	Station
    Arsenal	AM Peak	6	1	6/10	Station
    Arsenal	AM Peak	6	2	6/10	Station
    Arsenal	AM Peak	6	3	6/10	Station
    Arsenal	AM Peak	6	4	6/10	Station
    Arsenal	AM Peak	6	5	6/10	Station
    Arsenal	Inter Peak	4	0	4/10	Station
    Arsenal	Inter Peak	4	1	4/10	Station
    Arsenal	Inter Peak	4	2	4/10	Station
    Arsenal	Inter Peak	4	3	4/10	Station
    Arsenal	PM Peak	4	0	4/10	Station
    Arsenal	PM Peak	4	1	4/10	Station
    Arsenal	PM Peak	4	2	4/10	Station
    Arsenal	PM Peak	4	3	4/10	Station
    Arsenal	Evening	3	0	3/10	Station
    Arsenal	Evening	3	1	3/10	Station
    Arsenal	Evening	3	2	3/10	Station
    Arsenal	Late	1	0	1/10	Station
    Baker Street	Early	1	0	1/10	Station
    Baker Street	AM Peak	8	0	8/10	Station
    Baker Street	AM Peak	8	1	8/10	Station
    Baker Street	AM Peak	8	2	8/10	Station
    Baker Street	AM Peak	8	3	8/10	Station
    Baker Street	AM Peak	8	4	8/10	Station
    Baker Street	AM Peak	8	5	8/10	Station
    Baker Street	AM Peak	8	6	8/10	Station
    Baker Street	AM Peak	8	7	8/10	Station
    Baker Street	Inter Peak	9	0	9/10	Station
    Baker Street	Inter Peak	9	1	9/10	Station
    Baker Street	Inter Peak	9	2	9/10	Station
    Baker Street	Inter Peak	9	3	9/10	Station
    Baker Street	Inter Peak	9	4	9/10	Station
    Baker Street	Inter Peak	9	5	9/10	Station
    Baker Street	Inter Peak	9	6	9/10	Station
    Baker Street	Inter Peak	9	7	9/10	Station
    Baker Street	Inter Peak	9	8	9/10	Station
    Baker Street	PM Peak	8	0	8/10	Station
    Baker Street	PM Peak	8	1	8/10	Station
    Baker Street	PM Peak	8	2	8/10	Station
    Baker Street	PM Peak	8	3	8/10	Station
    Baker Street	PM Peak	8	4	8/10	Station
    Baker Street	PM Peak	8	5	8/10	Station
    Baker Street	PM Peak	8	6	8/10	Station
    Baker Street	PM Peak	8	7	8/10	Station
    Baker Street	Evening	3	0	3/10	Station
    Baker Street	Evening	3	1	3/10	Station
    Baker Street	Evening	3	2	3/10	Station
    Baker Street	Late	1	0	1/10	Station
    Balham	Early	1	0	1/10	Station
    Balham	AM Peak	8	0	8/10	Station
    Balham	AM Peak	8	1	8/10	Station
    Balham	AM Peak	8	2	8/10	Station
    Balham	AM Peak	8	3	8/10	Station
    Balham	AM Peak	8	4	8/10	Station
    Balham	AM Peak	8	5	8/10	Station
    Balham	AM Peak	8	6	8/10	Station
    Balham	AM Peak	8	7	8/10	Station
    Balham	Inter Peak	5	0	5/10	Station
    Balham	Inter Peak	5	1	5/10	Station
    Balham	Inter Peak	5	2	5/10	Station
    Balham	Inter Peak	5	3	5/10	Station
    Balham	Inter Peak	5	4	5/10	Station
    Balham	PM Peak	7	0	7/10	Station
    Balham	PM Peak	7	1	7/10	Station
    Balham	PM Peak	7	2	7/10	Station
    Balham	PM Peak	7	3	7/10	Station
    Balham	PM Peak	7	4	7/10	Station
    Balham	PM Peak	7	5	7/10	Station
    Balham	PM Peak	7	6	7/10	Station
    Balham	Evening	4	0	4/10	Station
    Balham	Evening	4	1	4/10	Station
    Balham	Evening	4	2	4/10	Station
    Balham	Evening	4	3	4/10	Station
    Balham	Late	2	0	2/10	Station
    Balham	Late	2	1	2/10	Station
    Bank & Monument	Early	1	0	1/10	Station
    Bank & Monument	AM Peak	9	0	9/10	Station
    Bank & Monument	AM Peak	9	1	9/10	Station
    Bank & Monument	AM Peak	9	2	9/10	Station
    Bank & Monument	AM Peak	9	3	9/10	Station
    Bank & Monument	AM Peak	9	4	9/10	Station
    Bank & Monument	AM Peak	9	5	9/10	Station
    Bank & Monument	AM Peak	9	6	9/10	Station
    Bank & Monument	AM Peak	9	7	9/10	Station
    Bank & Monument	AM Peak	9	8	9/10	Station
    Bank & Monument	Inter Peak	6	0	6/10	Station
    Bank & Monument	Inter Peak	6	1	6/10	Station
    Bank & Monument	Inter Peak	6	2	6/10	Station
    Bank & Monument	Inter Peak	6	3	6/10	Station
    Bank & Monument	Inter Peak	6	4	6/10	Station
    Bank & Monument	Inter Peak	6	5	6/10	Station
    Bank & Monument	PM Peak	9	0	9/10	Station
    Bank & Monument	PM Peak	9	1	9/10	Station
    Bank & Monument	PM Peak	9	2	9/10	Station
    Bank & Monument	PM Peak	9	3	9/10	Station
    Bank & Monument	PM Peak	9	4	9/10	Station
    Bank & Monument	PM Peak	9	5	9/10	Station
    Bank & Monument	PM Peak	9	6	9/10	Station
    Bank & Monument	PM Peak	9	7	9/10	Station
    Bank & Monument	PM Peak	9	8	9/10	Station
    Bank & Monument	Evening	3	0	3/10	Station
    Bank & Monument	Evening	3	1	3/10	Station
    Bank & Monument	Evening	3	2	3/10	Station
    Bank & Monument	Late	1	0	1/10	Station
    Barbican	Early	1	0	1/10	Station
    Barbican	AM Peak	9	0	9/10	Station
    Barbican	AM Peak	9	1	9/10	Station
    Barbican	AM Peak	9	2	9/10	Station
    Barbican	AM Peak	9	3	9/10	Station
    Barbican	AM Peak	9	4	9/10	Station
    Barbican	AM Peak	9	5	9/10	Station
    Barbican	AM Peak	9	6	9/10	Station
    Barbican	AM Peak	9	7	9/10	Station
    Barbican	AM Peak	9	8	9/10	Station
    Barbican	Inter Peak	8	0	8/10	Station
    Barbican	Inter Peak	8	1	8/10	Station
    Barbican	Inter Peak	8	2	8/10	Station
    Barbican	Inter Peak	8	3	8/10	Station
    Barbican	Inter Peak	8	4	8/10	Station
    Barbican	Inter Peak	8	5	8/10	Station
    Barbican	Inter Peak	8	6	8/10	Station
    Barbican	Inter Peak	8	7	8/10	Station
    Barbican	PM Peak	9	0	9/10	Station
    Barbican	PM Peak	9	1	9/10	Station
    Barbican	PM Peak	9	2	9/10	Station
    Barbican	PM Peak	9	3	9/10	Station
    Barbican	PM Peak	9	4	9/10	Station
    Barbican	PM Peak	9	5	9/10	Station
    Barbican	PM Peak	9	6	9/10	Station
    Barbican	PM Peak	9	7	9/10	Station
    Barbican	PM Peak	9	8	9/10	Station
    Barbican	Evening	3	0	3/10	Station
    Barbican	Evening	3	1	3/10	Station
    Barbican	Evening	3	2	3/10	Station
    Barbican	Late	1	0	1/10	Station
    Barking	Early	2	0	2/10	Station
    Barking	Early	2	1	2/10	Station
    Barking	AM Peak	5	0	5/10	Station
    Barking	AM Peak	5	1	5/10	Station
    Barking	AM Peak	5	2	5/10	Station
    Barking	AM Peak	5	3	5/10	Station
    Barking	AM Peak	5	4	5/10	Station
    Barking	Inter Peak	5	0	5/10	Station
    Barking	Inter Peak	5	1	5/10	Station
    Barking	Inter Peak	5	2	5/10	Station
    Barking	Inter Peak	5	3	5/10	Station
    Barking	Inter Peak	5	4	5/10	Station
    Barking	PM Peak	6	0	6/10	Station
    Barking	PM Peak	6	1	6/10	Station
    Barking	PM Peak	6	2	6/10	Station
    Barking	PM Peak	6	3	6/10	Station
    Barking	PM Peak	6	4	6/10	Station
    Barking	PM Peak	6	5	6/10	Station
    Barking	Evening	3	0	3/10	Station
    Barking	Evening	3	1	3/10	Station
    Barking	Evening	3	2	3/10	Station
    Barking	Late	1	0	1/10	Station
    Barkingside	Early	2	0	2/10	Station
    Barkingside	Early	2	1	2/10	Station
    Barkingside	AM Peak	5	0	5/10	Station
    Barkingside	AM Peak	5	1	5/10	Station
    Barkingside	AM Peak	5	2	5/10	Station
    Barkingside	AM Peak	5	3	5/10	Station
    Barkingside	AM Peak	5	4	5/10	Station
    Barkingside	Inter Peak	3	0	3/10	Station
    Barkingside	Inter Peak	3	1	3/10	Station
    Barkingside	Inter Peak	3	2	3/10	Station
    Barkingside	PM Peak	5	0	5/10	Station
    Barkingside	PM Peak	5	1	5/10	Station
    Barkingside	PM Peak	5	2	5/10	Station
    Barkingside	PM Peak	5	3	5/10	Station
    Barkingside	PM Peak	5	4	5/10	Station
    Barkingside	Evening	2	0	2/10	Station
    Barkingside	Evening	2	1	2/10	Station
    Barkingside	Late	1	0	1/10	Station
    Barons Court	AM Peak	6	0	6/10	Station
    Barons Court	AM Peak	6	1	6/10	Station
    Barons Court	AM Peak	6	2	6/10	Station
    Barons Court	AM Peak	6	3	6/10	Station
    Barons Court	AM Peak	6	4	6/10	Station
    Barons Court	AM Peak	6	5	6/10	Station
    Barons Court	Inter Peak	5	0	5/10	Station
    Barons Court	Inter Peak	5	1	5/10	Station
    Barons Court	Inter Peak	5	2	5/10	Station
    Barons Court	Inter Peak	5	3	5/10	Station
    Barons Court	Inter Peak	5	4	5/10	Station
    Barons Court	PM Peak	5	0	5/10	Station
    Barons Court	PM Peak	5	1	5/10	Station
    Barons Court	PM Peak	5	2	5/10	Station
    Barons Court	PM Peak	5	3	5/10	Station
    Barons Court	PM Peak	5	4	5/10	Station
    Barons Court	Evening	2	0	2/10	Station
    Barons Court	Evening	2	1	2/10	Station
    Barons Court	Late	1	0	1/10	Station
    Bayswater	AM Peak	3	0	3/10	Station
    Bayswater	AM Peak	3	1	3/10	Station
    Bayswater	AM Peak	3	2	3/10	Station
    Bayswater	Inter Peak	6	0	6/10	Station
    Bayswater	Inter Peak	6	1	6/10	Station
    Bayswater	Inter Peak	6	2	6/10	Station
    Bayswater	Inter Peak	6	3	6/10	Station
    Bayswater	Inter Peak	6	4	6/10	Station
    Bayswater	Inter Peak	6	5	6/10	Station
    Bayswater	PM Peak	4	0	4/10	Station
    Bayswater	PM Peak	4	1	4/10	Station
    Bayswater	PM Peak	4	2	4/10	Station
    Bayswater	PM Peak	4	3	4/10	Station
    Bayswater	Evening	3	0	3/10	Station
    Bayswater	Evening	3	1	3/10	Station
    Bayswater	Evening	3	2	3/10	Station
    Bayswater	Late	1	0	1/10	Station
    Becontree	Early	2	0	2/10	Station
    Becontree	Early	2	1	2/10	Station
    Becontree	AM Peak	5	0	5/10	Station
    Becontree	AM Peak	5	1	5/10	Station
    Becontree	AM Peak	5	2	5/10	Station
    Becontree	AM Peak	5	3	5/10	Station
    Becontree	AM Peak	5	4	5/10	Station
    Becontree	Inter Peak	5	0	5/10	Station
    Becontree	Inter Peak	5	1	5/10	Station
    Becontree	Inter Peak	5	2	5/10	Station
    Becontree	Inter Peak	5	3	5/10	Station
    Becontree	Inter Peak	5	4	5/10	Station
    Becontree	PM Peak	6	0	6/10	Station
    Becontree	PM Peak	6	1	6/10	Station
    Becontree	PM Peak	6	2	6/10	Station
    Becontree	PM Peak	6	3	6/10	Station
    Becontree	PM Peak	6	4	6/10	Station
    Becontree	PM Peak	6	5	6/10	Station
    Becontree	Evening	2	0	2/10	Station
    Becontree	Evening	2	1	2/10	Station
    Becontree	Late	1	0	1/10	Station
    Belsize Park	AM Peak	5	0	5/10	Station
    Belsize Park	AM Peak	5	1	5/10	Station
    Belsize Park	AM Peak	5	2	5/10	Station
    Belsize Park	AM Peak	5	3	5/10	Station
    Belsize Park	AM Peak	5	4	5/10	Station
    Belsize Park	Inter Peak	6	0	6/10	Station
    Belsize Park	Inter Peak	6	1	6/10	Station
    Belsize Park	Inter Peak	6	2	6/10	Station
    Belsize Park	Inter Peak	6	3	6/10	Station
    Belsize Park	Inter Peak	6	4	6/10	Station
    Belsize Park	Inter Peak	6	5	6/10	Station
    Belsize Park	PM Peak	5	0	5/10	Station
    Belsize Park	PM Peak	5	1	5/10	Station
    Belsize Park	PM Peak	5	2	5/10	Station
    Belsize Park	PM Peak	5	3	5/10	Station
    Belsize Park	PM Peak	5	4	5/10	Station
    Belsize Park	Evening	3	0	3/10	Station
    Belsize Park	Evening	3	1	3/10	Station
    Belsize Park	Evening	3	2	3/10	Station
    Belsize Park	Late	1	0	1/10	Station
    Bermondsey	Early	1	0	1/10	Station
    Bermondsey	AM Peak	9	0	9/10	Station
    Bermondsey	AM Peak	9	1	9/10	Station
    Bermondsey	AM Peak	9	2	9/10	Station
    Bermondsey	AM Peak	9	3	9/10	Station
    Bermondsey	AM Peak	9	4	9/10	Station
    Bermondsey	AM Peak	9	5	9/10	Station
    Bermondsey	AM Peak	9	6	9/10	Station
    Bermondsey	AM Peak	9	7	9/10	Station
    Bermondsey	AM Peak	9	8	9/10	Station
    Bermondsey	Inter Peak	7	0	7/10	Station
    Bermondsey	Inter Peak	7	1	7/10	Station
    Bermondsey	Inter Peak	7	2	7/10	Station
    Bermondsey	Inter Peak	7	3	7/10	Station
    Bermondsey	Inter Peak	7	4	7/10	Station
    Bermondsey	Inter Peak	7	5	7/10	Station
    Bermondsey	Inter Peak	7	6	7/10	Station
    Bermondsey	PM Peak	8	0	8/10	Station
    Bermondsey	PM Peak	8	1	8/10	Station
    Bermondsey	PM Peak	8	2	8/10	Station
    Bermondsey	PM Peak	8	3	8/10	Station
    Bermondsey	PM Peak	8	4	8/10	Station
    Bermondsey	PM Peak	8	5	8/10	Station
    Bermondsey	PM Peak	8	6	8/10	Station
    Bermondsey	PM Peak	8	7	8/10	Station
    Bermondsey	Evening	5	0	5/10	Station
    Bermondsey	Evening	5	1	5/10	Station
    Bermondsey	Evening	5	2	5/10	Station
    Bermondsey	Evening	5	3	5/10	Station
    Bermondsey	Evening	5	4	5/10	Station
    Bermondsey	Late	2	0	2/10	Station
    Bermondsey	Late	2	1	2/10	Station
    Bethnal Green	Early	1	0	1/10	Station
    Bethnal Green	AM Peak	8	0	8/10	Station
    Bethnal Green	AM Peak	8	1	8/10	Station
    Bethnal Green	AM Peak	8	2	8/10	Station
    Bethnal Green	AM Peak	8	3	8/10	Station
    Bethnal Green	AM Peak	8	4	8/10	Station
    Bethnal Green	AM Peak	8	5	8/10	Station
    Bethnal Green	AM Peak	8	6	8/10	Station
    Bethnal Green	AM Peak	8	7	8/10	Station
    Bethnal Green	Inter Peak	9	0	9/10	Station
    Bethnal Green	Inter Peak	9	1	9/10	Station
    Bethnal Green	Inter Peak	9	2	9/10	Station
    Bethnal Green	Inter Peak	9	3	9/10	Station
    Bethnal Green	Inter Peak	9	4	9/10	Station
    Bethnal Green	Inter Peak	9	5	9/10	Station
    Bethnal Green	Inter Peak	9	6	9/10	Station
    Bethnal Green	Inter Peak	9	7	9/10	Station
    Bethnal Green	Inter Peak	9	8	9/10	Station
    Bethnal Green	PM Peak	9	0	9/10	Station
    Bethnal Green	PM Peak	9	1	9/10	Station
    Bethnal Green	PM Peak	9	2	9/10	Station
    Bethnal Green	PM Peak	9	3	9/10	Station
    Bethnal Green	PM Peak	9	4	9/10	Station
    Bethnal Green	PM Peak	9	5	9/10	Station
    Bethnal Green	PM Peak	9	6	9/10	Station
    Bethnal Green	PM Peak	9	7	9/10	Station
    Bethnal Green	PM Peak	9	8	9/10	Station
    Bethnal Green	Evening	5	0	5/10	Station
    Bethnal Green	Evening	5	1	5/10	Station
    Bethnal Green	Evening	5	2	5/10	Station
    Bethnal Green	Evening	5	3	5/10	Station
    Bethnal Green	Evening	5	4	5/10	Station
    Bethnal Green	Late	3	0	3/10	Station
    Bethnal Green	Late	3	1	3/10	Station
    Bethnal Green	Late	3	2	3/10	Station
    Blackfriars	AM Peak	6	0	6/10	Station
    Blackfriars	AM Peak	6	1	6/10	Station
    Blackfriars	AM Peak	6	2	6/10	Station
    Blackfriars	AM Peak	6	3	6/10	Station
    Blackfriars	AM Peak	6	4	6/10	Station
    Blackfriars	AM Peak	6	5	6/10	Station
    Blackfriars	Inter Peak	4	0	4/10	Station
    Blackfriars	Inter Peak	4	1	4/10	Station
    Blackfriars	Inter Peak	4	2	4/10	Station
    Blackfriars	Inter Peak	4	3	4/10	Station
    Blackfriars	PM Peak	6	0	6/10	Station
    Blackfriars	PM Peak	6	1	6/10	Station
    Blackfriars	PM Peak	6	2	6/10	Station
    Blackfriars	PM Peak	6	3	6/10	Station
    Blackfriars	PM Peak	6	4	6/10	Station
    Blackfriars	PM Peak	6	5	6/10	Station
    Blackfriars	Evening	2	0	2/10	Station
    Blackfriars	Evening	2	1	2/10	Station
    Blackfriars	Late	1	0	1/10	Station
    Blackhorse Road	Early	2	0	2/10	Station
    Blackhorse Road	Early	2	1	2/10	Station
    Blackhorse Road	AM Peak	7	0	7/10	Station
    Blackhorse Road	AM Peak	7	1	7/10	Station
    Blackhorse Road	AM Peak	7	2	7/10	Station
    Blackhorse Road	AM Peak	7	3	7/10	Station
    Blackhorse Road	AM Peak	7	4	7/10	Station
    Blackhorse Road	AM Peak	7	5	7/10	Station
    Blackhorse Road	AM Peak	7	6	7/10	Station
    Blackhorse Road	Inter Peak	5	0	5/10	Station
    Blackhorse Road	Inter Peak	5	1	5/10	Station
    Blackhorse Road	Inter Peak	5	2	5/10	Station
    Blackhorse Road	Inter Peak	5	3	5/10	Station
    Blackhorse Road	Inter Peak	5	4	5/10	Station
    Blackhorse Road	PM Peak	7	0	7/10	Station
    Blackhorse Road	PM Peak	7	1	7/10	Station
    Blackhorse Road	PM Peak	7	2	7/10	Station
    Blackhorse Road	PM Peak	7	3	7/10	Station
    Blackhorse Road	PM Peak	7	4	7/10	Station
    Blackhorse Road	PM Peak	7	5	7/10	Station
    Blackhorse Road	PM Peak	7	6	7/10	Station
    Blackhorse Road	Evening	3	0	3/10	Station
    Blackhorse Road	Evening	3	1	3/10	Station
    Blackhorse Road	Evening	3	2	3/10	Station
    Blackhorse Road	Late	2	0	2/10	Station
    Blackhorse Road	Late	2	1	2/10	Station
    Bond Street	AM Peak	4	0	4/10	Station
    Bond Street	AM Peak	4	1	4/10	Station
    Bond Street	AM Peak	4	2	4/10	Station
    Bond Street	AM Peak	4	3	4/10	Station
    Bond Street	Inter Peak	7	0	7/10	Station
    Bond Street	Inter Peak	7	1	7/10	Station
    Bond Street	Inter Peak	7	2	7/10	Station
    Bond Street	Inter Peak	7	3	7/10	Station
    Bond Street	Inter Peak	7	4	7/10	Station
    Bond Street	Inter Peak	7	5	7/10	Station
    Bond Street	Inter Peak	7	6	7/10	Station
    Bond Street	PM Peak	7	0	7/10	Station
    Bond Street	PM Peak	7	1	7/10	Station
    Bond Street	PM Peak	7	2	7/10	Station
    Bond Street	PM Peak	7	3	7/10	Station
    Bond Street	PM Peak	7	4	7/10	Station
    Bond Street	PM Peak	7	5	7/10	Station
    Bond Street	PM Peak	7	6	7/10	Station
    Bond Street	Evening	3	0	3/10	Station
    Bond Street	Evening	3	1	3/10	Station
    Bond Street	Evening	3	2	3/10	Station
    Bond Street	Late	1	0	1/10	Station
    Borough	Early	1	0	1/10	Station
    Borough	AM Peak	9	0	9/10	Station
    Borough	AM Peak	9	1	9/10	Station
    Borough	AM Peak	9	2	9/10	Station
    Borough	AM Peak	9	3	9/10	Station
    Borough	AM Peak	9	4	9/10	Station
    Borough	AM Peak	9	5	9/10	Station
    Borough	AM Peak	9	6	9/10	Station
    Borough	AM Peak	9	7	9/10	Station
    Borough	AM Peak	9	8	9/10	Station
    Borough	Inter Peak	9	0	9/10	Station
    Borough	Inter Peak	9	1	9/10	Station
    Borough	Inter Peak	9	2	9/10	Station
    Borough	Inter Peak	9	3	9/10	Station
    Borough	Inter Peak	9	4	9/10	Station
    Borough	Inter Peak	9	5	9/10	Station
    Borough	Inter Peak	9	6	9/10	Station
    Borough	Inter Peak	9	7	9/10	Station
    Borough	Inter Peak	9	8	9/10	Station
    Borough	PM Peak	9	0	9/10	Station
    Borough	PM Peak	9	1	9/10	Station
    Borough	PM Peak	9	2	9/10	Station
    Borough	PM Peak	9	3	9/10	Station
    Borough	PM Peak	9	4	9/10	Station
    Borough	PM Peak	9	5	9/10	Station
    Borough	PM Peak	9	6	9/10	Station
    Borough	PM Peak	9	7	9/10	Station
    Borough	PM Peak	9	8	9/10	Station
    Borough	Evening	4	0	4/10	Station
    Borough	Evening	4	1	4/10	Station
    Borough	Evening	4	2	4/10	Station
    Borough	Evening	4	3	4/10	Station
    Borough	Late	2	0	2/10	Station
    Borough	Late	2	1	2/10	Station
    Boston Manor	Early	1	0	1/10	Station
    Boston Manor	AM Peak	6	0	6/10	Station
    Boston Manor	AM Peak	6	1	6/10	Station
    Boston Manor	AM Peak	6	2	6/10	Station
    Boston Manor	AM Peak	6	3	6/10	Station
    Boston Manor	AM Peak	6	4	6/10	Station
    Boston Manor	AM Peak	6	5	6/10	Station
    Boston Manor	Inter Peak	4	0	4/10	Station
    Boston Manor	Inter Peak	4	1	4/10	Station
    Boston Manor	Inter Peak	4	2	4/10	Station
    Boston Manor	Inter Peak	4	3	4/10	Station
    Boston Manor	PM Peak	5	0	5/10	Station
    Boston Manor	PM Peak	5	1	5/10	Station
    Boston Manor	PM Peak	5	2	5/10	Station
    Boston Manor	PM Peak	5	3	5/10	Station
    Boston Manor	PM Peak	5	4	5/10	Station
    Boston Manor	Evening	2	0	2/10	Station
    Boston Manor	Evening	2	1	2/10	Station
    Boston Manor	Late	1	0	1/10	Station
    Bounds Green	Early	1	0	1/10	Station
    Bounds Green	AM Peak	6	0	6/10	Station
    Bounds Green	AM Peak	6	1	6/10	Station
    Bounds Green	AM Peak	6	2	6/10	Station
    Bounds Green	AM Peak	6	3	6/10	Station
    Bounds Green	AM Peak	6	4	6/10	Station
    Bounds Green	AM Peak	6	5	6/10	Station
    Bounds Green	Inter Peak	4	0	4/10	Station
    Bounds Green	Inter Peak	4	1	4/10	Station
    Bounds Green	Inter Peak	4	2	4/10	Station
    Bounds Green	Inter Peak	4	3	4/10	Station
    Bounds Green	PM Peak	5	0	5/10	Station
    Bounds Green	PM Peak	5	1	5/10	Station
    Bounds Green	PM Peak	5	2	5/10	Station
    Bounds Green	PM Peak	5	3	5/10	Station
    Bounds Green	PM Peak	5	4	5/10	Station
    Bounds Green	Evening	3	0	3/10	Station
    Bounds Green	Evening	3	1	3/10	Station
    Bounds Green	Evening	3	2	3/10	Station
    Bounds Green	Late	1	0	1/10	Station
    Bow Road	Early	1	0	1/10	Station
    Bow Road	AM Peak	7	0	7/10	Station
    Bow Road	AM Peak	7	1	7/10	Station
    Bow Road	AM Peak	7	2	7/10	Station
    Bow Road	AM Peak	7	3	7/10	Station
    Bow Road	AM Peak	7	4	7/10	Station
    Bow Road	AM Peak	7	5	7/10	Station
    Bow Road	AM Peak	7	6	7/10	Station
    Bow Road	Inter Peak	5	0	5/10	Station
    Bow Road	Inter Peak	5	1	5/10	Station
    Bow Road	Inter Peak	5	2	5/10	Station
    Bow Road	Inter Peak	5	3	5/10	Station
    Bow Road	Inter Peak	5	4	5/10	Station
    Bow Road	PM Peak	6	0	6/10	Station
    Bow Road	PM Peak	6	1	6/10	Station
    Bow Road	PM Peak	6	2	6/10	Station
    Bow Road	PM Peak	6	3	6/10	Station
    Bow Road	PM Peak	6	4	6/10	Station
    Bow Road	PM Peak	6	5	6/10	Station
    Bow Road	Evening	3	0	3/10	Station
    Bow Road	Evening	3	1	3/10	Station
    Bow Road	Evening	3	2	3/10	Station
    Bow Road	Late	2	0	2/10	Station
    Bow Road	Late	2	1	2/10	Station
    Brent Cross	Early	1	0	1/10	Station
    Brent Cross	AM Peak	5	0	5/10	Station
    Brent Cross	AM Peak	5	1	5/10	Station
    Brent Cross	AM Peak	5	2	5/10	Station
    Brent Cross	AM Peak	5	3	5/10	Station
    Brent Cross	AM Peak	5	4	5/10	Station
    Brent Cross	Inter Peak	5	0	5/10	Station
    Brent Cross	Inter Peak	5	1	5/10	Station
    Brent Cross	Inter Peak	5	2	5/10	Station
    Brent Cross	Inter Peak	5	3	5/10	Station
    Brent Cross	Inter Peak	5	4	5/10	Station
    Brent Cross	PM Peak	6	0	6/10	Station
    Brent Cross	PM Peak	6	1	6/10	Station
    Brent Cross	PM Peak	6	2	6/10	Station
    Brent Cross	PM Peak	6	3	6/10	Station
    Brent Cross	PM Peak	6	4	6/10	Station
    Brent Cross	PM Peak	6	5	6/10	Station
    Brent Cross	Evening	3	0	3/10	Station
    Brent Cross	Evening	3	1	3/10	Station
    Brent Cross	Evening	3	2	3/10	Station
    Brent Cross	Late	1	0	1/10	Station
    Brixton	Early	1	0	1/10	Station
    Brixton	AM Peak	6	0	6/10	Station
    Brixton	AM Peak	6	1	6/10	Station
    Brixton	AM Peak	6	2	6/10	Station
    Brixton	AM Peak	6	3	6/10	Station
    Brixton	AM Peak	6	4	6/10	Station
    Brixton	AM Peak	6	5	6/10	Station
    Brixton	Inter Peak	4	0	4/10	Station
    Brixton	Inter Peak	4	1	4/10	Station
    Brixton	Inter Peak	4	2	4/10	Station
    Brixton	Inter Peak	4	3	4/10	Station
    Brixton	PM Peak	5	0	5/10	Station
    Brixton	PM Peak	5	1	5/10	Station
    Brixton	PM Peak	5	2	5/10	Station
    Brixton	PM Peak	5	3	5/10	Station
    Brixton	PM Peak	5	4	5/10	Station
    Brixton	Evening	3	0	3/10	Station
    Brixton	Evening	3	1	3/10	Station
    Brixton	Evening	3	2	3/10	Station
    Brixton	Late	2	0	2/10	Station
    Brixton	Late	2	1	2/10	Station
    Bromley-by-Bow	Early	1	0	1/10	Station
    Bromley-by-Bow	AM Peak	6	0	6/10	Station
    Bromley-by-Bow	AM Peak	6	1	6/10	Station
    Bromley-by-Bow	AM Peak	6	2	6/10	Station
    Bromley-by-Bow	AM Peak	6	3	6/10	Station
    Bromley-by-Bow	AM Peak	6	4	6/10	Station
    Bromley-by-Bow	AM Peak	6	5	6/10	Station
    Bromley-by-Bow	Inter Peak	5	0	5/10	Station
    Bromley-by-Bow	Inter Peak	5	1	5/10	Station
    Bromley-by-Bow	Inter Peak	5	2	5/10	Station
    Bromley-by-Bow	Inter Peak	5	3	5/10	Station
    Bromley-by-Bow	Inter Peak	5	4	5/10	Station
    Bromley-by-Bow	PM Peak	6	0	6/10	Station
    Bromley-by-Bow	PM Peak	6	1	6/10	Station
    Bromley-by-Bow	PM Peak	6	2	6/10	Station
    Bromley-by-Bow	PM Peak	6	3	6/10	Station
    Bromley-by-Bow	PM Peak	6	4	6/10	Station
    Bromley-by-Bow	PM Peak	6	5	6/10	Station
    Bromley-by-Bow	Evening	3	0	3/10	Station
    Bromley-by-Bow	Evening	3	1	3/10	Station
    Bromley-by-Bow	Evening	3	2	3/10	Station
    Bromley-by-Bow	Late	1	0	1/10	Station
    Buckhurst Hill	Early	1	0	1/10	Station
    Buckhurst Hill	AM Peak	6	0	6/10	Station
    Buckhurst Hill	AM Peak	6	1	6/10	Station
    Buckhurst Hill	AM Peak	6	2	6/10	Station
    Buckhurst Hill	AM Peak	6	3	6/10	Station
    Buckhurst Hill	AM Peak	6	4	6/10	Station
    Buckhurst Hill	AM Peak	6	5	6/10	Station
    Buckhurst Hill	Inter Peak	3	0	3/10	Station
    Buckhurst Hill	Inter Peak	3	1	3/10	Station
    Buckhurst Hill	Inter Peak	3	2	3/10	Station
    Buckhurst Hill	PM Peak	5	0	5/10	Station
    Buckhurst Hill	PM Peak	5	1	5/10	Station
    Buckhurst Hill	PM Peak	5	2	5/10	Station
    Buckhurst Hill	PM Peak	5	3	5/10	Station
    Buckhurst Hill	PM Peak	5	4	5/10	Station
    Buckhurst Hill	Evening	2	0	2/10	Station
    Buckhurst Hill	Evening	2	1	2/10	Station
    Buckhurst Hill	Late	1	0	1/10	Station
    Burnt Oak	Early	2	0	2/10	Station
    Burnt Oak	Early	2	1	2/10	Station
    Burnt Oak	AM Peak	5	0	5/10	Station
    Burnt Oak	AM Peak	5	1	5/10	Station
    Burnt Oak	AM Peak	5	2	5/10	Station
    Burnt Oak	AM Peak	5	3	5/10	Station
    Burnt Oak	AM Peak	5	4	5/10	Station
    Burnt Oak	Inter Peak	4	0	4/10	Station
    Burnt Oak	Inter Peak	4	1	4/10	Station
    Burnt Oak	Inter Peak	4	2	4/10	Station
    Burnt Oak	Inter Peak	4	3	4/10	Station
    Burnt Oak	PM Peak	5	0	5/10	Station
    Burnt Oak	PM Peak	5	1	5/10	Station
    Burnt Oak	PM Peak	5	2	5/10	Station
    Burnt Oak	PM Peak	5	3	5/10	Station
    Burnt Oak	PM Peak	5	4	5/10	Station
    Burnt Oak	Evening	2	0	2/10	Station
    Burnt Oak	Evening	2	1	2/10	Station
    Burnt Oak	Late	1	0	1/10	Station
    Caledonian Road	Early	1	0	1/10	Station
    Caledonian Road	AM Peak	7	0	7/10	Station
    Caledonian Road	AM Peak	7	1	7/10	Station
    Caledonian Road	AM Peak	7	2	7/10	Station
    Caledonian Road	AM Peak	7	3	7/10	Station
    Caledonian Road	AM Peak	7	4	7/10	Station
    Caledonian Road	AM Peak	7	5	7/10	Station
    Caledonian Road	AM Peak	7	6	7/10	Station
    Caledonian Road	Inter Peak	7	0	7/10	Station
    Caledonian Road	Inter Peak	7	1	7/10	Station
    Caledonian Road	Inter Peak	7	2	7/10	Station
    Caledonian Road	Inter Peak	7	3	7/10	Station
    Caledonian Road	Inter Peak	7	4	7/10	Station
    Caledonian Road	Inter Peak	7	5	7/10	Station
    Caledonian Road	Inter Peak	7	6	7/10	Station
    Caledonian Road	PM Peak	7	0	7/10	Station
    Caledonian Road	PM Peak	7	1	7/10	Station
    Caledonian Road	PM Peak	7	2	7/10	Station
    Caledonian Road	PM Peak	7	3	7/10	Station
    Caledonian Road	PM Peak	7	4	7/10	Station
    Caledonian Road	PM Peak	7	5	7/10	Station
    Caledonian Road	PM Peak	7	6	7/10	Station
    Caledonian Road	Evening	4	0	4/10	Station
    Caledonian Road	Evening	4	1	4/10	Station
    Caledonian Road	Evening	4	2	4/10	Station
    Caledonian Road	Evening	4	3	4/10	Station
    Caledonian Road	Late	2	0	2/10	Station
    Caledonian Road	Late	2	1	2/10	Station
    Camden Town	AM Peak	4	0	4/10	Station
    Camden Town	AM Peak	4	1	4/10	Station
    Camden Town	AM Peak	4	2	4/10	Station
    Camden Town	AM Peak	4	3	4/10	Station
    Camden Town	Inter Peak	8	0	8/10	Station
    Camden Town	Inter Peak	8	1	8/10	Station
    Camden Town	Inter Peak	8	2	8/10	Station
    Camden Town	Inter Peak	8	3	8/10	Station
    Camden Town	Inter Peak	8	4	8/10	Station
    Camden Town	Inter Peak	8	5	8/10	Station
    Camden Town	Inter Peak	8	6	8/10	Station
    Camden Town	Inter Peak	8	7	8/10	Station
    Camden Town	PM Peak	7	0	7/10	Station
    Camden Town	PM Peak	7	1	7/10	Station
    Camden Town	PM Peak	7	2	7/10	Station
    Camden Town	PM Peak	7	3	7/10	Station
    Camden Town	PM Peak	7	4	7/10	Station
    Camden Town	PM Peak	7	5	7/10	Station
    Camden Town	PM Peak	7	6	7/10	Station
    Camden Town	Evening	3	0	3/10	Station
    Camden Town	Evening	3	1	3/10	Station
    Camden Town	Evening	3	2	3/10	Station
    Camden Town	Late	2	0	2/10	Station
    Camden Town	Late	2	1	2/10	Station
    Canada Water	Early	1	0	1/10	Station
    Canada Water	AM Peak	9	0	9/10	Station
    Canada Water	AM Peak	9	1	9/10	Station
    Canada Water	AM Peak	9	2	9/10	Station
    Canada Water	AM Peak	9	3	9/10	Station
    Canada Water	AM Peak	9	4	9/10	Station
    Canada Water	AM Peak	9	5	9/10	Station
    Canada Water	AM Peak	9	6	9/10	Station
    Canada Water	AM Peak	9	7	9/10	Station
    Canada Water	AM Peak	9	8	9/10	Station
    Canada Water	Inter Peak	7	0	7/10	Station
    Canada Water	Inter Peak	7	1	7/10	Station
    Canada Water	Inter Peak	7	2	7/10	Station
    Canada Water	Inter Peak	7	3	7/10	Station
    Canada Water	Inter Peak	7	4	7/10	Station
    Canada Water	Inter Peak	7	5	7/10	Station
    Canada Water	Inter Peak	7	6	7/10	Station
    Canada Water	PM Peak	9	0	9/10	Station
    Canada Water	PM Peak	9	1	9/10	Station
    Canada Water	PM Peak	9	2	9/10	Station
    Canada Water	PM Peak	9	3	9/10	Station
    Canada Water	PM Peak	9	4	9/10	Station
    Canada Water	PM Peak	9	5	9/10	Station
    Canada Water	PM Peak	9	6	9/10	Station
    Canada Water	PM Peak	9	7	9/10	Station
    Canada Water	PM Peak	9	8	9/10	Station
    Canada Water	Evening	5	0	5/10	Station
    Canada Water	Evening	5	1	5/10	Station
    Canada Water	Evening	5	2	5/10	Station
    Canada Water	Evening	5	3	5/10	Station
    Canada Water	Evening	5	4	5/10	Station
    Canada Water	Late	3	0	3/10	Station
    Canada Water	Late	3	1	3/10	Station
    Canada Water	Late	3	2	3/10	Station
    Canary Wharf	Early	1	0	1/10	Station
    Canary Wharf	AM Peak	7	0	7/10	Station
    Canary Wharf	AM Peak	7	1	7/10	Station
    Canary Wharf	AM Peak	7	2	7/10	Station
    Canary Wharf	AM Peak	7	3	7/10	Station
    Canary Wharf	AM Peak	7	4	7/10	Station
    Canary Wharf	AM Peak	7	5	7/10	Station
    Canary Wharf	AM Peak	7	6	7/10	Station
    Canary Wharf	Inter Peak	4	0	4/10	Station
    Canary Wharf	Inter Peak	4	1	4/10	Station
    Canary Wharf	Inter Peak	4	2	4/10	Station
    Canary Wharf	Inter Peak	4	3	4/10	Station
    Canary Wharf	PM Peak	7	0	7/10	Station
    Canary Wharf	PM Peak	7	1	7/10	Station
    Canary Wharf	PM Peak	7	2	7/10	Station
    Canary Wharf	PM Peak	7	3	7/10	Station
    Canary Wharf	PM Peak	7	4	7/10	Station
    Canary Wharf	PM Peak	7	5	7/10	Station
    Canary Wharf	PM Peak	7	6	7/10	Station
    Canary Wharf	Evening	3	0	3/10	Station
    Canary Wharf	Evening	3	1	3/10	Station
    Canary Wharf	Evening	3	2	3/10	Station
    Canary Wharf	Late	1	0	1/10	Station
    Canning Town	Early	3	0	3/10	Station
    Canning Town	Early	3	1	3/10	Station
    Canning Town	Early	3	2	3/10	Station
    Canning Town	AM Peak	8	0	8/10	Station
    Canning Town	AM Peak	8	1	8/10	Station
    Canning Town	AM Peak	8	2	8/10	Station
    Canning Town	AM Peak	8	3	8/10	Station
    Canning Town	AM Peak	8	4	8/10	Station
    Canning Town	AM Peak	8	5	8/10	Station
    Canning Town	AM Peak	8	6	8/10	Station
    Canning Town	AM Peak	8	7	8/10	Station
    Canning Town	Inter Peak	7	0	7/10	Station
    Canning Town	Inter Peak	7	1	7/10	Station
    Canning Town	Inter Peak	7	2	7/10	Station
    Canning Town	Inter Peak	7	3	7/10	Station
    Canning Town	Inter Peak	7	4	7/10	Station
    Canning Town	Inter Peak	7	5	7/10	Station
    Canning Town	Inter Peak	7	6	7/10	Station
    Canning Town	PM Peak	8	0	8/10	Station
    Canning Town	PM Peak	8	1	8/10	Station
    Canning Town	PM Peak	8	2	8/10	Station
    Canning Town	PM Peak	8	3	8/10	Station
    Canning Town	PM Peak	8	4	8/10	Station
    Canning Town	PM Peak	8	5	8/10	Station
    Canning Town	PM Peak	8	6	8/10	Station
    Canning Town	PM Peak	8	7	8/10	Station
    Canning Town	Evening	4	0	4/10	Station
    Canning Town	Evening	4	1	4/10	Station
    Canning Town	Evening	4	2	4/10	Station
    Canning Town	Evening	4	3	4/10	Station
    Canning Town	Late	2	0	2/10	Station
    Canning Town	Late	2	1	2/10	Station
    Cannon Street	Early	1	0	1/10	Station
    Cannon Street	AM Peak	6	0	6/10	Station
    Cannon Street	AM Peak	6	1	6/10	Station
    Cannon Street	AM Peak	6	2	6/10	Station
    Cannon Street	AM Peak	6	3	6/10	Station
    Cannon Street	AM Peak	6	4	6/10	Station
    Cannon Street	AM Peak	6	5	6/10	Station
    Cannon Street	Inter Peak	4	0	4/10	Station
    Cannon Street	Inter Peak	4	1	4/10	Station
    Cannon Street	Inter Peak	4	2	4/10	Station
    Cannon Street	Inter Peak	4	3	4/10	Station
    Cannon Street	PM Peak	5	0	5/10	Station
    Cannon Street	PM Peak	5	1	5/10	Station
    Cannon Street	PM Peak	5	2	5/10	Station
    Cannon Street	PM Peak	5	3	5/10	Station
    Cannon Street	PM Peak	5	4	5/10	Station
    Cannon Street	Evening	2	0	2/10	Station
    Cannon Street	Evening	2	1	2/10	Station
    Cannon Street	Late	1	0	1/10	Station
    Canons Park	Early	1	0	1/10	Station
    Canons Park	AM Peak	5	0	5/10	Station
    Canons Park	AM Peak	5	1	5/10	Station
    Canons Park	AM Peak	5	2	5/10	Station
    Canons Park	AM Peak	5	3	5/10	Station
    Canons Park	AM Peak	5	4	5/10	Station
    Canons Park	Inter Peak	3	0	3/10	Station
    Canons Park	Inter Peak	3	1	3/10	Station
    Canons Park	Inter Peak	3	2	3/10	Station
    Canons Park	PM Peak	5	0	5/10	Station
    Canons Park	PM Peak	5	1	5/10	Station
    Canons Park	PM Peak	5	2	5/10	Station
    Canons Park	PM Peak	5	3	5/10	Station
    Canons Park	PM Peak	5	4	5/10	Station
    Canons Park	Evening	2	0	2/10	Station
    Canons Park	Evening	2	1	2/10	Station
    Canons Park	Late	1	0	1/10	Station
    Chalfont & Latimer	Early	1	0	1/10	Station
    Chalfont & Latimer	AM Peak	6	0	6/10	Station
    Chalfont & Latimer	AM Peak	6	1	6/10	Station
    Chalfont & Latimer	AM Peak	6	2	6/10	Station
    Chalfont & Latimer	AM Peak	6	3	6/10	Station
    Chalfont & Latimer	AM Peak	6	4	6/10	Station
    Chalfont & Latimer	AM Peak	6	5	6/10	Station
    Chalfont & Latimer	Inter Peak	3	0	3/10	Station
    Chalfont & Latimer	Inter Peak	3	1	3/10	Station
    Chalfont & Latimer	Inter Peak	3	2	3/10	Station
    Chalfont & Latimer	PM Peak	4	0	4/10	Station
    Chalfont & Latimer	PM Peak	4	1	4/10	Station
    Chalfont & Latimer	PM Peak	4	2	4/10	Station
    Chalfont & Latimer	PM Peak	4	3	4/10	Station
    Chalfont & Latimer	Evening	2	0	2/10	Station
    Chalfont & Latimer	Evening	2	1	2/10	Station
    Chalfont & Latimer	Late	1	0	1/10	Station
    Chalk Farm	AM Peak	6	0	6/10	Station
    Chalk Farm	AM Peak	6	1	6/10	Station
    Chalk Farm	AM Peak	6	2	6/10	Station
    Chalk Farm	AM Peak	6	3	6/10	Station
    Chalk Farm	AM Peak	6	4	6/10	Station
    Chalk Farm	AM Peak	6	5	6/10	Station
    Chalk Farm	Inter Peak	6	0	6/10	Station
    Chalk Farm	Inter Peak	6	1	6/10	Station
    Chalk Farm	Inter Peak	6	2	6/10	Station
    Chalk Farm	Inter Peak	6	3	6/10	Station
    Chalk Farm	Inter Peak	6	4	6/10	Station
    Chalk Farm	Inter Peak	6	5	6/10	Station
    Chalk Farm	PM Peak	6	0	6/10	Station
    Chalk Farm	PM Peak	6	1	6/10	Station
    Chalk Farm	PM Peak	6	2	6/10	Station
    Chalk Farm	PM Peak	6	3	6/10	Station
    Chalk Farm	PM Peak	6	4	6/10	Station
    Chalk Farm	PM Peak	6	5	6/10	Station
    Chalk Farm	Evening	4	0	4/10	Station
    Chalk Farm	Evening	4	1	4/10	Station
    Chalk Farm	Evening	4	2	4/10	Station
    Chalk Farm	Evening	4	3	4/10	Station
    Chalk Farm	Late	2	0	2/10	Station
    Chalk Farm	Late	2	1	2/10	Station
    Chancery Lane	AM Peak	8	0	8/10	Station
    Chancery Lane	AM Peak	8	1	8/10	Station
    Chancery Lane	AM Peak	8	2	8/10	Station
    Chancery Lane	AM Peak	8	3	8/10	Station
    Chancery Lane	AM Peak	8	4	8/10	Station
    Chancery Lane	AM Peak	8	5	8/10	Station
    Chancery Lane	AM Peak	8	6	8/10	Station
    Chancery Lane	AM Peak	8	7	8/10	Station
    Chancery Lane	Inter Peak	8	0	8/10	Station
    Chancery Lane	Inter Peak	8	1	8/10	Station
    Chancery Lane	Inter Peak	8	2	8/10	Station
    Chancery Lane	Inter Peak	8	3	8/10	Station
    Chancery Lane	Inter Peak	8	4	8/10	Station
    Chancery Lane	Inter Peak	8	5	8/10	Station
    Chancery Lane	Inter Peak	8	6	8/10	Station
    Chancery Lane	Inter Peak	8	7	8/10	Station
    Chancery Lane	PM Peak	8	0	8/10	Station
    Chancery Lane	PM Peak	8	1	8/10	Station
    Chancery Lane	PM Peak	8	2	8/10	Station
    Chancery Lane	PM Peak	8	3	8/10	Station
    Chancery Lane	PM Peak	8	4	8/10	Station
    Chancery Lane	PM Peak	8	5	8/10	Station
    Chancery Lane	PM Peak	8	6	8/10	Station
    Chancery Lane	PM Peak	8	7	8/10	Station
    Chancery Lane	Evening	3	0	3/10	Station
    Chancery Lane	Evening	3	1	3/10	Station
    Chancery Lane	Evening	3	2	3/10	Station
    Chancery Lane	Late	1	0	1/10	Station
    Charing Cross	AM Peak	4	0	4/10	Station
    Charing Cross	AM Peak	4	1	4/10	Station
    Charing Cross	AM Peak	4	2	4/10	Station
    Charing Cross	AM Peak	4	3	4/10	Station
    Charing Cross	Inter Peak	6	0	6/10	Station
    Charing Cross	Inter Peak	6	1	6/10	Station
    Charing Cross	Inter Peak	6	2	6/10	Station
    Charing Cross	Inter Peak	6	3	6/10	Station
    Charing Cross	Inter Peak	6	4	6/10	Station
    Charing Cross	Inter Peak	6	5	6/10	Station
    Charing Cross	PM Peak	6	0	6/10	Station
    Charing Cross	PM Peak	6	1	6/10	Station
    Charing Cross	PM Peak	6	2	6/10	Station
    Charing Cross	PM Peak	6	3	6/10	Station
    Charing Cross	PM Peak	6	4	6/10	Station
    Charing Cross	PM Peak	6	5	6/10	Station
    Charing Cross	Evening	3	0	3/10	Station
    Charing Cross	Evening	3	1	3/10	Station
    Charing Cross	Evening	3	2	3/10	Station
    Charing Cross	Late	1	0	1/10	Station
    Chesham	Early	2	0	2/10	Station
    Chesham	Early	2	1	2/10	Station
    Chesham	AM Peak	6	0	6/10	Station
    Chesham	AM Peak	6	1	6/10	Station
    Chesham	AM Peak	6	2	6/10	Station
    Chesham	AM Peak	6	3	6/10	Station
    Chesham	AM Peak	6	4	6/10	Station
    Chesham	AM Peak	6	5	6/10	Station
    Chesham	Inter Peak	3	0	3/10	Station
    Chesham	Inter Peak	3	1	3/10	Station
    Chesham	Inter Peak	3	2	3/10	Station
    Chesham	PM Peak	4	0	4/10	Station
    Chesham	PM Peak	4	1	4/10	Station
    Chesham	PM Peak	4	2	4/10	Station
    Chesham	PM Peak	4	3	4/10	Station
    Chesham	Evening	2	0	2/10	Station
    Chesham	Evening	2	1	2/10	Station
    Chesham	Late	1	0	1/10	Station
    Chigwell	Early	1	0	1/10	Station
    Chigwell	AM Peak	5	0	5/10	Station
    Chigwell	AM Peak	5	1	5/10	Station
    Chigwell	AM Peak	5	2	5/10	Station
    Chigwell	AM Peak	5	3	5/10	Station
    Chigwell	AM Peak	5	4	5/10	Station
    Chigwell	Inter Peak	2	0	2/10	Station
    Chigwell	Inter Peak	2	1	2/10	Station
    Chigwell	PM Peak	3	0	3/10	Station
    Chigwell	PM Peak	3	1	3/10	Station
    Chigwell	PM Peak	3	2	3/10	Station
    Chigwell	Evening	1	0	1/10	Station
    Chiswick Park	AM Peak	6	0	6/10	Station
    Chiswick Park	AM Peak	6	1	6/10	Station
    Chiswick Park	AM Peak	6	2	6/10	Station
    Chiswick Park	AM Peak	6	3	6/10	Station
    Chiswick Park	AM Peak	6	4	6/10	Station
    Chiswick Park	AM Peak	6	5	6/10	Station
    Chiswick Park	Inter Peak	4	0	4/10	Station
    Chiswick Park	Inter Peak	4	1	4/10	Station
    Chiswick Park	Inter Peak	4	2	4/10	Station
    Chiswick Park	Inter Peak	4	3	4/10	Station
    Chiswick Park	PM Peak	5	0	5/10	Station
    Chiswick Park	PM Peak	5	1	5/10	Station
    Chiswick Park	PM Peak	5	2	5/10	Station
    Chiswick Park	PM Peak	5	3	5/10	Station
    Chiswick Park	PM Peak	5	4	5/10	Station
    Chiswick Park	Evening	2	0	2/10	Station
    Chiswick Park	Evening	2	1	2/10	Station
    Chiswick Park	Late	1	0	1/10	Station
    Chorleywood	Early	1	0	1/10	Station
    Chorleywood	AM Peak	6	0	6/10	Station
    Chorleywood	AM Peak	6	1	6/10	Station
    Chorleywood	AM Peak	6	2	6/10	Station
    Chorleywood	AM Peak	6	3	6/10	Station
    Chorleywood	AM Peak	6	4	6/10	Station
    Chorleywood	AM Peak	6	5	6/10	Station
    Chorleywood	Inter Peak	4	0	4/10	Station
    Chorleywood	Inter Peak	4	1	4/10	Station
    Chorleywood	Inter Peak	4	2	4/10	Station
    Chorleywood	Inter Peak	4	3	4/10	Station
    Chorleywood	PM Peak	5	0	5/10	Station
    Chorleywood	PM Peak	5	1	5/10	Station
    Chorleywood	PM Peak	5	2	5/10	Station
    Chorleywood	PM Peak	5	3	5/10	Station
    Chorleywood	PM Peak	5	4	5/10	Station
    Chorleywood	Evening	3	0	3/10	Station
    Chorleywood	Evening	3	1	3/10	Station
    Chorleywood	Evening	3	2	3/10	Station
    Chorleywood	Late	1	0	1/10	Station
    Clapham Common	Early	1	0	1/10	Station
    Clapham Common	AM Peak	9	0	9/10	Station
    Clapham Common	AM Peak	9	1	9/10	Station
    Clapham Common	AM Peak	9	2	9/10	Station
    Clapham Common	AM Peak	9	3	9/10	Station
    Clapham Common	AM Peak	9	4	9/10	Station
    Clapham Common	AM Peak	9	5	9/10	Station
    Clapham Common	AM Peak	9	6	9/10	Station
    Clapham Common	AM Peak	9	7	9/10	Station
    Clapham Common	AM Peak	9	8	9/10	Station
    Clapham Common	Inter Peak	7	0	7/10	Station
    Clapham Common	Inter Peak	7	1	7/10	Station
    Clapham Common	Inter Peak	7	2	7/10	Station
    Clapham Common	Inter Peak	7	3	7/10	Station
    Clapham Common	Inter Peak	7	4	7/10	Station
    Clapham Common	Inter Peak	7	5	7/10	Station
    Clapham Common	Inter Peak	7	6	7/10	Station
    Clapham Common	PM Peak	9	0	9/10	Station
    Clapham Common	PM Peak	9	1	9/10	Station
    Clapham Common	PM Peak	9	2	9/10	Station
    Clapham Common	PM Peak	9	3	9/10	Station
    Clapham Common	PM Peak	9	4	9/10	Station
    Clapham Common	PM Peak	9	5	9/10	Station
    Clapham Common	PM Peak	9	6	9/10	Station
    Clapham Common	PM Peak	9	7	9/10	Station
    Clapham Common	PM Peak	9	8	9/10	Station
    Clapham Common	Evening	6	0	6/10	Station
    Clapham Common	Evening	6	1	6/10	Station
    Clapham Common	Evening	6	2	6/10	Station
    Clapham Common	Evening	6	3	6/10	Station
    Clapham Common	Evening	6	4	6/10	Station
    Clapham Common	Evening	6	5	6/10	Station
    Clapham Common	Late	3	0	3/10	Station
    Clapham Common	Late	3	1	3/10	Station
    Clapham Common	Late	3	2	3/10	Station
    Clapham North	Early	1	0	1/10	Station
    Clapham North	AM Peak	9	0	9/10	Station
    Clapham North	AM Peak	9	1	9/10	Station
    Clapham North	AM Peak	9	2	9/10	Station
    Clapham North	AM Peak	9	3	9/10	Station
    Clapham North	AM Peak	9	4	9/10	Station
    Clapham North	AM Peak	9	5	9/10	Station
    Clapham North	AM Peak	9	6	9/10	Station
    Clapham North	AM Peak	9	7	9/10	Station
    Clapham North	AM Peak	9	8	9/10	Station
    Clapham North	Inter Peak	6	0	6/10	Station
    Clapham North	Inter Peak	6	1	6/10	Station
    Clapham North	Inter Peak	6	2	6/10	Station
    Clapham North	Inter Peak	6	3	6/10	Station
    Clapham North	Inter Peak	6	4	6/10	Station
    Clapham North	Inter Peak	6	5	6/10	Station
    Clapham North	PM Peak	9	0	9/10	Station
    Clapham North	PM Peak	9	1	9/10	Station
    Clapham North	PM Peak	9	2	9/10	Station
    Clapham North	PM Peak	9	3	9/10	Station
    Clapham North	PM Peak	9	4	9/10	Station
    Clapham North	PM Peak	9	5	9/10	Station
    Clapham North	PM Peak	9	6	9/10	Station
    Clapham North	PM Peak	9	7	9/10	Station
    Clapham North	PM Peak	9	8	9/10	Station
    Clapham North	Evening	6	0	6/10	Station
    Clapham North	Evening	6	1	6/10	Station
    Clapham North	Evening	6	2	6/10	Station
    Clapham North	Evening	6	3	6/10	Station
    Clapham North	Evening	6	4	6/10	Station
    Clapham North	Evening	6	5	6/10	Station
    Clapham North	Late	3	0	3/10	Station
    Clapham North	Late	3	1	3/10	Station
    Clapham North	Late	3	2	3/10	Station
    Clapham South	Early	1	0	1/10	Station
    Clapham South	AM Peak	8	0	8/10	Station
    Clapham South	AM Peak	8	1	8/10	Station
    Clapham South	AM Peak	8	2	8/10	Station
    Clapham South	AM Peak	8	3	8/10	Station
    Clapham South	AM Peak	8	4	8/10	Station
    Clapham South	AM Peak	8	5	8/10	Station
    Clapham South	AM Peak	8	6	8/10	Station
    Clapham South	AM Peak	8	7	8/10	Station
    Clapham South	Inter Peak	4	0	4/10	Station
    Clapham South	Inter Peak	4	1	4/10	Station
    Clapham South	Inter Peak	4	2	4/10	Station
    Clapham South	Inter Peak	4	3	4/10	Station
    Clapham South	PM Peak	6	0	6/10	Station
    Clapham South	PM Peak	6	1	6/10	Station
    Clapham South	PM Peak	6	2	6/10	Station
    Clapham South	PM Peak	6	3	6/10	Station
    Clapham South	PM Peak	6	4	6/10	Station
    Clapham South	PM Peak	6	5	6/10	Station
    Clapham South	Evening	4	0	4/10	Station
    Clapham South	Evening	4	1	4/10	Station
    Clapham South	Evening	4	2	4/10	Station
    Clapham South	Evening	4	3	4/10	Station
    Clapham South	Late	2	0	2/10	Station
    Clapham South	Late	2	1	2/10	Station
    Cockfosters	Early	1	0	1/10	Station
    Cockfosters	AM Peak	5	0	5/10	Station
    Cockfosters	AM Peak	5	1	5/10	Station
    Cockfosters	AM Peak	5	2	5/10	Station
    Cockfosters	AM Peak	5	3	5/10	Station
    Cockfosters	AM Peak	5	4	5/10	Station
    Cockfosters	Inter Peak	5	0	5/10	Station
    Cockfosters	Inter Peak	5	1	5/10	Station
    Cockfosters	Inter Peak	5	2	5/10	Station
    Cockfosters	Inter Peak	5	3	5/10	Station
    Cockfosters	Inter Peak	5	4	5/10	Station
    Cockfosters	PM Peak	5	0	5/10	Station
    Cockfosters	PM Peak	5	1	5/10	Station
    Cockfosters	PM Peak	5	2	5/10	Station
    Cockfosters	PM Peak	5	3	5/10	Station
    Cockfosters	PM Peak	5	4	5/10	Station
    Cockfosters	Evening	2	0	2/10	Station
    Cockfosters	Evening	2	1	2/10	Station
    Cockfosters	Late	1	0	1/10	Station
    Colindale	Early	1	0	1/10	Station
    Colindale	AM Peak	5	0	5/10	Station
    Colindale	AM Peak	5	1	5/10	Station
    Colindale	AM Peak	5	2	5/10	Station
    Colindale	AM Peak	5	3	5/10	Station
    Colindale	AM Peak	5	4	5/10	Station
    Colindale	Inter Peak	4	0	4/10	Station
    Colindale	Inter Peak	4	1	4/10	Station
    Colindale	Inter Peak	4	2	4/10	Station
    Colindale	Inter Peak	4	3	4/10	Station
    Colindale	PM Peak	4	0	4/10	Station
    Colindale	PM Peak	4	1	4/10	Station
    Colindale	PM Peak	4	2	4/10	Station
    Colindale	PM Peak	4	3	4/10	Station
    Colindale	Evening	2	0	2/10	Station
    Colindale	Evening	2	1	2/10	Station
    Colindale	Late	1	0	1/10	Station
    Colliers Wood	Early	1	0	1/10	Station
    Colliers Wood	AM Peak	6	0	6/10	Station
    Colliers Wood	AM Peak	6	1	6/10	Station
    Colliers Wood	AM Peak	6	2	6/10	Station
    Colliers Wood	AM Peak	6	3	6/10	Station
    Colliers Wood	AM Peak	6	4	6/10	Station
    Colliers Wood	AM Peak	6	5	6/10	Station
    Colliers Wood	Inter Peak	4	0	4/10	Station
    Colliers Wood	Inter Peak	4	1	4/10	Station
    Colliers Wood	Inter Peak	4	2	4/10	Station
    Colliers Wood	Inter Peak	4	3	4/10	Station
    Colliers Wood	PM Peak	5	0	5/10	Station
    Colliers Wood	PM Peak	5	1	5/10	Station
    Colliers Wood	PM Peak	5	2	5/10	Station
    Colliers Wood	PM Peak	5	3	5/10	Station
    Colliers Wood	PM Peak	5	4	5/10	Station
    Colliers Wood	Evening	3	0	3/10	Station
    Colliers Wood	Evening	3	1	3/10	Station
    Colliers Wood	Evening	3	2	3/10	Station
    Colliers Wood	Late	1	0	1/10	Station
    Covent Garden	AM Peak	2	0	2/10	Station
    Covent Garden	AM Peak	2	1	2/10	Station
    Covent Garden	Inter Peak	6	0	6/10	Station
    Covent Garden	Inter Peak	6	1	6/10	Station
    Covent Garden	Inter Peak	6	2	6/10	Station
    Covent Garden	Inter Peak	6	3	6/10	Station
    Covent Garden	Inter Peak	6	4	6/10	Station
    Covent Garden	Inter Peak	6	5	6/10	Station
    Covent Garden	PM Peak	6	0	6/10	Station
    Covent Garden	PM Peak	6	1	6/10	Station
    Covent Garden	PM Peak	6	2	6/10	Station
    Covent Garden	PM Peak	6	3	6/10	Station
    Covent Garden	PM Peak	6	4	6/10	Station
    Covent Garden	PM Peak	6	5	6/10	Station
    Covent Garden	Evening	3	0	3/10	Station
    Covent Garden	Evening	3	1	3/10	Station
    Covent Garden	Evening	3	2	3/10	Station
    Covent Garden	Late	2	0	2/10	Station
    Covent Garden	Late	2	1	2/10	Station
    Croxley	Early	1	0	1/10	Station
    Croxley	AM Peak	5	0	5/10	Station
    Croxley	AM Peak	5	1	5/10	Station
    Croxley	AM Peak	5	2	5/10	Station
    Croxley	AM Peak	5	3	5/10	Station
    Croxley	AM Peak	5	4	5/10	Station
    Croxley	Inter Peak	2	0	2/10	Station
    Croxley	Inter Peak	2	1	2/10	Station
    Croxley	PM Peak	4	0	4/10	Station
    Croxley	PM Peak	4	1	4/10	Station
    Croxley	PM Peak	4	2	4/10	Station
    Croxley	PM Peak	4	3	4/10	Station
    Croxley	Evening	2	0	2/10	Station
    Croxley	Evening	2	1	2/10	Station
    Croxley	Late	1	0	1/10	Station
    Dagenham East	Early	2	0	2/10	Station
    Dagenham East	Early	2	1	2/10	Station
    Dagenham East	AM Peak	6	0	6/10	Station
    Dagenham East	AM Peak	6	1	6/10	Station
    Dagenham East	AM Peak	6	2	6/10	Station
    Dagenham East	AM Peak	6	3	6/10	Station
    Dagenham East	AM Peak	6	4	6/10	Station
    Dagenham East	AM Peak	6	5	6/10	Station
    Dagenham East	Inter Peak	5	0	5/10	Station
    Dagenham East	Inter Peak	5	1	5/10	Station
    Dagenham East	Inter Peak	5	2	5/10	Station
    Dagenham East	Inter Peak	5	3	5/10	Station
    Dagenham East	Inter Peak	5	4	5/10	Station
    Dagenham East	PM Peak	5	0	5/10	Station
    Dagenham East	PM Peak	5	1	5/10	Station
    Dagenham East	PM Peak	5	2	5/10	Station
    Dagenham East	PM Peak	5	3	5/10	Station
    Dagenham East	PM Peak	5	4	5/10	Station
    Dagenham East	Evening	2	0	2/10	Station
    Dagenham East	Evening	2	1	2/10	Station
    Dagenham East	Late	1	0	1/10	Station
    Dagenham Heathway	Early	2	0	2/10	Station
    Dagenham Heathway	Early	2	1	2/10	Station
    Dagenham Heathway	AM Peak	5	0	5/10	Station
    Dagenham Heathway	AM Peak	5	1	5/10	Station
    Dagenham Heathway	AM Peak	5	2	5/10	Station
    Dagenham Heathway	AM Peak	5	3	5/10	Station
    Dagenham Heathway	AM Peak	5	4	5/10	Station
    Dagenham Heathway	Inter Peak	5	0	5/10	Station
    Dagenham Heathway	Inter Peak	5	1	5/10	Station
    Dagenham Heathway	Inter Peak	5	2	5/10	Station
    Dagenham Heathway	Inter Peak	5	3	5/10	Station
    Dagenham Heathway	Inter Peak	5	4	5/10	Station
    Dagenham Heathway	PM Peak	6	0	6/10	Station
    Dagenham Heathway	PM Peak	6	1	6/10	Station
    Dagenham Heathway	PM Peak	6	2	6/10	Station
    Dagenham Heathway	PM Peak	6	3	6/10	Station
    Dagenham Heathway	PM Peak	6	4	6/10	Station
    Dagenham Heathway	PM Peak	6	5	6/10	Station
    Dagenham Heathway	Evening	2	0	2/10	Station
    Dagenham Heathway	Evening	2	1	2/10	Station
    Dagenham Heathway	Late	1	0	1/10	Station
    Debden	Early	1	0	1/10	Station
    Debden	AM Peak	5	0	5/10	Station
    Debden	AM Peak	5	1	5/10	Station
    Debden	AM Peak	5	2	5/10	Station
    Debden	AM Peak	5	3	5/10	Station
    Debden	AM Peak	5	4	5/10	Station
    Debden	Inter Peak	4	0	4/10	Station
    Debden	Inter Peak	4	1	4/10	Station
    Debden	Inter Peak	4	2	4/10	Station
    Debden	Inter Peak	4	3	4/10	Station
    Debden	PM Peak	4	0	4/10	Station
    Debden	PM Peak	4	1	4/10	Station
    Debden	PM Peak	4	2	4/10	Station
    Debden	PM Peak	4	3	4/10	Station
    Debden	Evening	1	0	1/10	Station
    Debden	Late	1	0	1/10	Station
    Dollis Hill	Early	1	0	1/10	Station
    Dollis Hill	AM Peak	6	0	6/10	Station
    Dollis Hill	AM Peak	6	1	6/10	Station
    Dollis Hill	AM Peak	6	2	6/10	Station
    Dollis Hill	AM Peak	6	3	6/10	Station
    Dollis Hill	AM Peak	6	4	6/10	Station
    Dollis Hill	AM Peak	6	5	6/10	Station
    Dollis Hill	Inter Peak	5	0	5/10	Station
    Dollis Hill	Inter Peak	5	1	5/10	Station
    Dollis Hill	Inter Peak	5	2	5/10	Station
    Dollis Hill	Inter Peak	5	3	5/10	Station
    Dollis Hill	Inter Peak	5	4	5/10	Station
    Dollis Hill	PM Peak	5	0	5/10	Station
    Dollis Hill	PM Peak	5	1	5/10	Station
    Dollis Hill	PM Peak	5	2	5/10	Station
    Dollis Hill	PM Peak	5	3	5/10	Station
    Dollis Hill	PM Peak	5	4	5/10	Station
    Dollis Hill	Evening	3	0	3/10	Station
    Dollis Hill	Evening	3	1	3/10	Station
    Dollis Hill	Evening	3	2	3/10	Station
    Dollis Hill	Late	1	0	1/10	Station
    Ealing Broadway	Early	1	0	1/10	Station
    Ealing Broadway	AM Peak	6	0	6/10	Station
    Ealing Broadway	AM Peak	6	1	6/10	Station
    Ealing Broadway	AM Peak	6	2	6/10	Station
    Ealing Broadway	AM Peak	6	3	6/10	Station
    Ealing Broadway	AM Peak	6	4	6/10	Station
    Ealing Broadway	AM Peak	6	5	6/10	Station
    Ealing Broadway	Inter Peak	4	0	4/10	Station
    Ealing Broadway	Inter Peak	4	1	4/10	Station
    Ealing Broadway	Inter Peak	4	2	4/10	Station
    Ealing Broadway	Inter Peak	4	3	4/10	Station
    Ealing Broadway	PM Peak	5	0	5/10	Station
    Ealing Broadway	PM Peak	5	1	5/10	Station
    Ealing Broadway	PM Peak	5	2	5/10	Station
    Ealing Broadway	PM Peak	5	3	5/10	Station
    Ealing Broadway	PM Peak	5	4	5/10	Station
    Ealing Broadway	Evening	2	0	2/10	Station
    Ealing Broadway	Evening	2	1	2/10	Station
    Ealing Broadway	Late	1	0	1/10	Station
    Ealing Common	Early	1	0	1/10	Station
    Ealing Common	AM Peak	6	0	6/10	Station
    Ealing Common	AM Peak	6	1	6/10	Station
    Ealing Common	AM Peak	6	2	6/10	Station
    Ealing Common	AM Peak	6	3	6/10	Station
    Ealing Common	AM Peak	6	4	6/10	Station
    Ealing Common	AM Peak	6	5	6/10	Station
    Ealing Common	Inter Peak	4	0	4/10	Station
    Ealing Common	Inter Peak	4	1	4/10	Station
    Ealing Common	Inter Peak	4	2	4/10	Station
    Ealing Common	Inter Peak	4	3	4/10	Station
    Ealing Common	PM Peak	5	0	5/10	Station
    Ealing Common	PM Peak	5	1	5/10	Station
    Ealing Common	PM Peak	5	2	5/10	Station
    Ealing Common	PM Peak	5	3	5/10	Station
    Ealing Common	PM Peak	5	4	5/10	Station
    Ealing Common	Evening	2	0	2/10	Station
    Ealing Common	Evening	2	1	2/10	Station
    Ealing Common	Late	1	0	1/10	Station
    Earl's Court	Early	1	0	1/10	Station
    Earl's Court	AM Peak	6	0	6/10	Station
    Earl's Court	AM Peak	6	1	6/10	Station
    Earl's Court	AM Peak	6	2	6/10	Station
    Earl's Court	AM Peak	6	3	6/10	Station
    Earl's Court	AM Peak	6	4	6/10	Station
    Earl's Court	AM Peak	6	5	6/10	Station
    Earl's Court	Inter Peak	7	0	7/10	Station
    Earl's Court	Inter Peak	7	1	7/10	Station
    Earl's Court	Inter Peak	7	2	7/10	Station
    Earl's Court	Inter Peak	7	3	7/10	Station
    Earl's Court	Inter Peak	7	4	7/10	Station
    Earl's Court	Inter Peak	7	5	7/10	Station
    Earl's Court	Inter Peak	7	6	7/10	Station
    Earl's Court	PM Peak	6	0	6/10	Station
    Earl's Court	PM Peak	6	1	6/10	Station
    Earl's Court	PM Peak	6	2	6/10	Station
    Earl's Court	PM Peak	6	3	6/10	Station
    Earl's Court	PM Peak	6	4	6/10	Station
    Earl's Court	PM Peak	6	5	6/10	Station
    Earl's Court	Evening	4	0	4/10	Station
    Earl's Court	Evening	4	1	4/10	Station
    Earl's Court	Evening	4	2	4/10	Station
    Earl's Court	Evening	4	3	4/10	Station
    Earl's Court	Late	2	0	2/10	Station
    Earl's Court	Late	2	1	2/10	Station
    East Acton	Early	1	0	1/10	Station
    East Acton	AM Peak	6	0	6/10	Station
    East Acton	AM Peak	6	1	6/10	Station
    East Acton	AM Peak	6	2	6/10	Station
    East Acton	AM Peak	6	3	6/10	Station
    East Acton	AM Peak	6	4	6/10	Station
    East Acton	AM Peak	6	5	6/10	Station
    East Acton	Inter Peak	5	0	5/10	Station
    East Acton	Inter Peak	5	1	5/10	Station
    East Acton	Inter Peak	5	2	5/10	Station
    East Acton	Inter Peak	5	3	5/10	Station
    East Acton	Inter Peak	5	4	5/10	Station
    East Acton	PM Peak	5	0	5/10	Station
    East Acton	PM Peak	5	1	5/10	Station
    East Acton	PM Peak	5	2	5/10	Station
    East Acton	PM Peak	5	3	5/10	Station
    East Acton	PM Peak	5	4	5/10	Station
    East Acton	Evening	2	0	2/10	Station
    East Acton	Evening	2	1	2/10	Station
    East Acton	Late	1	0	1/10	Station
    East Finchley	Early	1	0	1/10	Station
    East Finchley	AM Peak	6	0	6/10	Station
    East Finchley	AM Peak	6	1	6/10	Station
    East Finchley	AM Peak	6	2	6/10	Station
    East Finchley	AM Peak	6	3	6/10	Station
    East Finchley	AM Peak	6	4	6/10	Station
    East Finchley	AM Peak	6	5	6/10	Station
    East Finchley	Inter Peak	4	0	4/10	Station
    East Finchley	Inter Peak	4	1	4/10	Station
    East Finchley	Inter Peak	4	2	4/10	Station
    East Finchley	Inter Peak	4	3	4/10	Station
    East Finchley	PM Peak	5	0	5/10	Station
    East Finchley	PM Peak	5	1	5/10	Station
    East Finchley	PM Peak	5	2	5/10	Station
    East Finchley	PM Peak	5	3	5/10	Station
    East Finchley	PM Peak	5	4	5/10	Station
    East Finchley	Evening	3	0	3/10	Station
    East Finchley	Evening	3	1	3/10	Station
    East Finchley	Evening	3	2	3/10	Station
    East Finchley	Late	1	0	1/10	Station
    East Ham	Early	2	0	2/10	Station
    East Ham	Early	2	1	2/10	Station
    East Ham	AM Peak	5	0	5/10	Station
    East Ham	AM Peak	5	1	5/10	Station
    East Ham	AM Peak	5	2	5/10	Station
    East Ham	AM Peak	5	3	5/10	Station
    East Ham	AM Peak	5	4	5/10	Station
    East Ham	Inter Peak	5	0	5/10	Station
    East Ham	Inter Peak	5	1	5/10	Station
    East Ham	Inter Peak	5	2	5/10	Station
    East Ham	Inter Peak	5	3	5/10	Station
    East Ham	Inter Peak	5	4	5/10	Station
    East Ham	PM Peak	6	0	6/10	Station
    East Ham	PM Peak	6	1	6/10	Station
    East Ham	PM Peak	6	2	6/10	Station
    East Ham	PM Peak	6	3	6/10	Station
    East Ham	PM Peak	6	4	6/10	Station
    East Ham	PM Peak	6	5	6/10	Station
    East Ham	Evening	3	0	3/10	Station
    East Ham	Evening	3	1	3/10	Station
    East Ham	Evening	3	2	3/10	Station
    East Ham	Late	1	0	1/10	Station
    East Putney	Early	1	0	1/10	Station
    East Putney	AM Peak	6	0	6/10	Station
    East Putney	AM Peak	6	1	6/10	Station
    East Putney	AM Peak	6	2	6/10	Station
    East Putney	AM Peak	6	3	6/10	Station
    East Putney	AM Peak	6	4	6/10	Station
    East Putney	AM Peak	6	5	6/10	Station
    East Putney	Inter Peak	3	0	3/10	Station
    East Putney	Inter Peak	3	1	3/10	Station
    East Putney	Inter Peak	3	2	3/10	Station
    East Putney	PM Peak	4	0	4/10	Station
    East Putney	PM Peak	4	1	4/10	Station
    East Putney	PM Peak	4	2	4/10	Station
    East Putney	PM Peak	4	3	4/10	Station
    East Putney	Evening	2	0	2/10	Station
    East Putney	Evening	2	1	2/10	Station
    East Putney	Late	1	0	1/10	Station
    Eastcote	Early	1	0	1/10	Station
    Eastcote	AM Peak	6	0	6/10	Station
    Eastcote	AM Peak	6	1	6/10	Station
    Eastcote	AM Peak	6	2	6/10	Station
    Eastcote	AM Peak	6	3	6/10	Station
    Eastcote	AM Peak	6	4	6/10	Station
    Eastcote	AM Peak	6	5	6/10	Station
    Eastcote	Inter Peak	4	0	4/10	Station
    Eastcote	Inter Peak	4	1	4/10	Station
    Eastcote	Inter Peak	4	2	4/10	Station
    Eastcote	Inter Peak	4	3	4/10	Station
    Eastcote	PM Peak	5	0	5/10	Station
    Eastcote	PM Peak	5	1	5/10	Station
    Eastcote	PM Peak	5	2	5/10	Station
    Eastcote	PM Peak	5	3	5/10	Station
    Eastcote	PM Peak	5	4	5/10	Station
    Eastcote	Evening	2	0	2/10	Station
    Eastcote	Evening	2	1	2/10	Station
    Eastcote	Late	1	0	1/10	Station
    Edgware	Early	1	0	1/10	Station
    Edgware	AM Peak	5	0	5/10	Station
    Edgware	AM Peak	5	1	5/10	Station
    Edgware	AM Peak	5	2	5/10	Station
    Edgware	AM Peak	5	3	5/10	Station
    Edgware	AM Peak	5	4	5/10	Station
    Edgware	Inter Peak	5	0	5/10	Station
    Edgware	Inter Peak	5	1	5/10	Station
    Edgware	Inter Peak	5	2	5/10	Station
    Edgware	Inter Peak	5	3	5/10	Station
    Edgware	Inter Peak	5	4	5/10	Station
    Edgware	PM Peak	4	0	4/10	Station
    Edgware	PM Peak	4	1	4/10	Station
    Edgware	PM Peak	4	2	4/10	Station
    Edgware	PM Peak	4	3	4/10	Station
    Edgware	Evening	2	0	2/10	Station
    Edgware	Evening	2	1	2/10	Station
    Edgware	Late	1	0	1/10	Station
    Edgware Road (Bak)	Early	1	0	1/10	Station
    Edgware Road (Bak)	AM Peak	8	0	8/10	Station
    Edgware Road (Bak)	AM Peak	8	1	8/10	Station
    Edgware Road (Bak)	AM Peak	8	2	8/10	Station
    Edgware Road (Bak)	AM Peak	8	3	8/10	Station
    Edgware Road (Bak)	AM Peak	8	4	8/10	Station
    Edgware Road (Bak)	AM Peak	8	5	8/10	Station
    Edgware Road (Bak)	AM Peak	8	6	8/10	Station
    Edgware Road (Bak)	AM Peak	8	7	8/10	Station
    Edgware Road (Bak)	Inter Peak	9	0	9/10	Station
    Edgware Road (Bak)	Inter Peak	9	1	9/10	Station
    Edgware Road (Bak)	Inter Peak	9	2	9/10	Station
    Edgware Road (Bak)	Inter Peak	9	3	9/10	Station
    Edgware Road (Bak)	Inter Peak	9	4	9/10	Station
    Edgware Road (Bak)	Inter Peak	9	5	9/10	Station
    Edgware Road (Bak)	Inter Peak	9	6	9/10	Station
    Edgware Road (Bak)	Inter Peak	9	7	9/10	Station
    Edgware Road (Bak)	Inter Peak	9	8	9/10	Station
    Edgware Road (Bak)	PM Peak	9	0	9/10	Station
    Edgware Road (Bak)	PM Peak	9	1	9/10	Station
    Edgware Road (Bak)	PM Peak	9	2	9/10	Station
    Edgware Road (Bak)	PM Peak	9	3	9/10	Station
    Edgware Road (Bak)	PM Peak	9	4	9/10	Station
    Edgware Road (Bak)	PM Peak	9	5	9/10	Station
    Edgware Road (Bak)	PM Peak	9	6	9/10	Station
    Edgware Road (Bak)	PM Peak	9	7	9/10	Station
    Edgware Road (Bak)	PM Peak	9	8	9/10	Station
    Edgware Road (Bak)	Evening	4	0	4/10	Station
    Edgware Road (Bak)	Evening	4	1	4/10	Station
    Edgware Road (Bak)	Evening	4	2	4/10	Station
    Edgware Road (Bak)	Evening	4	3	4/10	Station
    Edgware Road (Bak)	Late	2	0	2/10	Station
    Edgware Road (Bak)	Late	2	1	2/10	Station
    Edgware Road (Cir)	Early	1	0	1/10	Station
    Edgware Road (Cir)	AM Peak	8	0	8/10	Station
    Edgware Road (Cir)	AM Peak	8	1	8/10	Station
    Edgware Road (Cir)	AM Peak	8	2	8/10	Station
    Edgware Road (Cir)	AM Peak	8	3	8/10	Station
    Edgware Road (Cir)	AM Peak	8	4	8/10	Station
    Edgware Road (Cir)	AM Peak	8	5	8/10	Station
    Edgware Road (Cir)	AM Peak	8	6	8/10	Station
    Edgware Road (Cir)	AM Peak	8	7	8/10	Station
    Edgware Road (Cir)	Inter Peak	9	0	9/10	Station
    Edgware Road (Cir)	Inter Peak	9	1	9/10	Station
    Edgware Road (Cir)	Inter Peak	9	2	9/10	Station
    Edgware Road (Cir)	Inter Peak	9	3	9/10	Station
    Edgware Road (Cir)	Inter Peak	9	4	9/10	Station
    Edgware Road (Cir)	Inter Peak	9	5	9/10	Station
    Edgware Road (Cir)	Inter Peak	9	6	9/10	Station
    Edgware Road (Cir)	Inter Peak	9	7	9/10	Station
    Edgware Road (Cir)	Inter Peak	9	8	9/10	Station
    Edgware Road (Cir)	PM Peak	9	0	9/10	Station
    Edgware Road (Cir)	PM Peak	9	1	9/10	Station
    Edgware Road (Cir)	PM Peak	9	2	9/10	Station
    Edgware Road (Cir)	PM Peak	9	3	9/10	Station
    Edgware Road (Cir)	PM Peak	9	4	9/10	Station
    Edgware Road (Cir)	PM Peak	9	5	9/10	Station
    Edgware Road (Cir)	PM Peak	9	6	9/10	Station
    Edgware Road (Cir)	PM Peak	9	7	9/10	Station
    Edgware Road (Cir)	PM Peak	9	8	9/10	Station
    Edgware Road (Cir)	Evening	4	0	4/10	Station
    Edgware Road (Cir)	Evening	4	1	4/10	Station
    Edgware Road (Cir)	Evening	4	2	4/10	Station
    Edgware Road (Cir)	Evening	4	3	4/10	Station
    Edgware Road (Cir)	Late	1	0	1/10	Station
    Elephant & Castle	Early	1	0	1/10	Station
    Elephant & Castle	AM Peak	9	0	9/10	Station
    Elephant & Castle	AM Peak	9	1	9/10	Station
    Elephant & Castle	AM Peak	9	2	9/10	Station
    Elephant & Castle	AM Peak	9	3	9/10	Station
    Elephant & Castle	AM Peak	9	4	9/10	Station
    Elephant & Castle	AM Peak	9	5	9/10	Station
    Elephant & Castle	AM Peak	9	6	9/10	Station
    Elephant & Castle	AM Peak	9	7	9/10	Station
    Elephant & Castle	AM Peak	9	8	9/10	Station
    Elephant & Castle	Inter Peak	9	0	9/10	Station
    Elephant & Castle	Inter Peak	9	1	9/10	Station
    Elephant & Castle	Inter Peak	9	2	9/10	Station
    Elephant & Castle	Inter Peak	9	3	9/10	Station
    Elephant & Castle	Inter Peak	9	4	9/10	Station
    Elephant & Castle	Inter Peak	9	5	9/10	Station
    Elephant & Castle	Inter Peak	9	6	9/10	Station
    Elephant & Castle	Inter Peak	9	7	9/10	Station
    Elephant & Castle	Inter Peak	9	8	9/10	Station
    Elephant & Castle	PM Peak	8	0	8/10	Station
    Elephant & Castle	PM Peak	8	1	8/10	Station
    Elephant & Castle	PM Peak	8	2	8/10	Station
    Elephant & Castle	PM Peak	8	3	8/10	Station
    Elephant & Castle	PM Peak	8	4	8/10	Station
    Elephant & Castle	PM Peak	8	5	8/10	Station
    Elephant & Castle	PM Peak	8	6	8/10	Station
    Elephant & Castle	PM Peak	8	7	8/10	Station
    Elephant & Castle	Evening	4	0	4/10	Station
    Elephant & Castle	Evening	4	1	4/10	Station
    Elephant & Castle	Evening	4	2	4/10	Station
    Elephant & Castle	Evening	4	3	4/10	Station
    Elephant & Castle	Late	2	0	2/10	Station
    Elephant & Castle	Late	2	1	2/10	Station
    Elm Park	Early	2	0	2/10	Station
    Elm Park	Early	2	1	2/10	Station
    Elm Park	AM Peak	6	0	6/10	Station
    Elm Park	AM Peak	6	1	6/10	Station
    Elm Park	AM Peak	6	2	6/10	Station
    Elm Park	AM Peak	6	3	6/10	Station
    Elm Park	AM Peak	6	4	6/10	Station
    Elm Park	AM Peak	6	5	6/10	Station
    Elm Park	Inter Peak	3	0	3/10	Station
    Elm Park	Inter Peak	3	1	3/10	Station
    Elm Park	Inter Peak	3	2	3/10	Station
    Elm Park	PM Peak	5	0	5/10	Station
    Elm Park	PM Peak	5	1	5/10	Station
    Elm Park	PM Peak	5	2	5/10	Station
    Elm Park	PM Peak	5	3	5/10	Station
    Elm Park	PM Peak	5	4	5/10	Station
    Elm Park	Evening	2	0	2/10	Station
    Elm Park	Evening	2	1	2/10	Station
    Elm Park	Late	1	0	1/10	Station
    Embankment	AM Peak	5	0	5/10	Station
    Embankment	AM Peak	5	1	5/10	Station
    Embankment	AM Peak	5	2	5/10	Station
    Embankment	AM Peak	5	3	5/10	Station
    Embankment	AM Peak	5	4	5/10	Station
    Embankment	Inter Peak	6	0	6/10	Station
    Embankment	Inter Peak	6	1	6/10	Station
    Embankment	Inter Peak	6	2	6/10	Station
    Embankment	Inter Peak	6	3	6/10	Station
    Embankment	Inter Peak	6	4	6/10	Station
    Embankment	Inter Peak	6	5	6/10	Station
    Embankment	PM Peak	7	0	7/10	Station
    Embankment	PM Peak	7	1	7/10	Station
    Embankment	PM Peak	7	2	7/10	Station
    Embankment	PM Peak	7	3	7/10	Station
    Embankment	PM Peak	7	4	7/10	Station
    Embankment	PM Peak	7	5	7/10	Station
    Embankment	PM Peak	7	6	7/10	Station
    Embankment	Evening	3	0	3/10	Station
    Embankment	Evening	3	1	3/10	Station
    Embankment	Evening	3	2	3/10	Station
    Embankment	Late	2	0	2/10	Station
    Embankment	Late	2	1	2/10	Station
    Epping	Early	2	0	2/10	Station
    Epping	Early	2	1	2/10	Station
    Epping	AM Peak	5	0	5/10	Station
    Epping	AM Peak	5	1	5/10	Station
    Epping	AM Peak	5	2	5/10	Station
    Epping	AM Peak	5	3	5/10	Station
    Epping	AM Peak	5	4	5/10	Station
    Epping	Inter Peak	3	0	3/10	Station
    Epping	Inter Peak	3	1	3/10	Station
    Epping	Inter Peak	3	2	3/10	Station
    Epping	PM Peak	5	0	5/10	Station
    Epping	PM Peak	5	1	5/10	Station
    Epping	PM Peak	5	2	5/10	Station
    Epping	PM Peak	5	3	5/10	Station
    Epping	PM Peak	5	4	5/10	Station
    Epping	Evening	2	0	2/10	Station
    Epping	Evening	2	1	2/10	Station
    Epping	Late	1	0	1/10	Station
    Euston	Early	1	0	1/10	Station
    Euston	AM Peak	7	0	7/10	Station
    Euston	AM Peak	7	1	7/10	Station
    Euston	AM Peak	7	2	7/10	Station
    Euston	AM Peak	7	3	7/10	Station
    Euston	AM Peak	7	4	7/10	Station
    Euston	AM Peak	7	5	7/10	Station
    Euston	AM Peak	7	6	7/10	Station
    Euston	Inter Peak	9	0	9/10	Station
    Euston	Inter Peak	9	1	9/10	Station
    Euston	Inter Peak	9	2	9/10	Station
    Euston	Inter Peak	9	3	9/10	Station
    Euston	Inter Peak	9	4	9/10	Station
    Euston	Inter Peak	9	5	9/10	Station
    Euston	Inter Peak	9	6	9/10	Station
    Euston	Inter Peak	9	7	9/10	Station
    Euston	Inter Peak	9	8	9/10	Station
    Euston	PM Peak	8	0	8/10	Station
    Euston	PM Peak	8	1	8/10	Station
    Euston	PM Peak	8	2	8/10	Station
    Euston	PM Peak	8	3	8/10	Station
    Euston	PM Peak	8	4	8/10	Station
    Euston	PM Peak	8	5	8/10	Station
    Euston	PM Peak	8	6	8/10	Station
    Euston	PM Peak	8	7	8/10	Station
    Euston	Evening	4	0	4/10	Station
    Euston	Evening	4	1	4/10	Station
    Euston	Evening	4	2	4/10	Station
    Euston	Evening	4	3	4/10	Station
    Euston	Late	1	0	1/10	Station
    Euston Square	Early	1	0	1/10	Station
    Euston Square	AM Peak	8	0	8/10	Station
    Euston Square	AM Peak	8	1	8/10	Station
    Euston Square	AM Peak	8	2	8/10	Station
    Euston Square	AM Peak	8	3	8/10	Station
    Euston Square	AM Peak	8	4	8/10	Station
    Euston Square	AM Peak	8	5	8/10	Station
    Euston Square	AM Peak	8	6	8/10	Station
    Euston Square	AM Peak	8	7	8/10	Station
    Euston Square	Inter Peak	8	0	8/10	Station
    Euston Square	Inter Peak	8	1	8/10	Station
    Euston Square	Inter Peak	8	2	8/10	Station
    Euston Square	Inter Peak	8	3	8/10	Station
    Euston Square	Inter Peak	8	4	8/10	Station
    Euston Square	Inter Peak	8	5	8/10	Station
    Euston Square	Inter Peak	8	6	8/10	Station
    Euston Square	Inter Peak	8	7	8/10	Station
    Euston Square	PM Peak	9	0	9/10	Station
    Euston Square	PM Peak	9	1	9/10	Station
    Euston Square	PM Peak	9	2	9/10	Station
    Euston Square	PM Peak	9	3	9/10	Station
    Euston Square	PM Peak	9	4	9/10	Station
    Euston Square	PM Peak	9	5	9/10	Station
    Euston Square	PM Peak	9	6	9/10	Station
    Euston Square	PM Peak	9	7	9/10	Station
    Euston Square	PM Peak	9	8	9/10	Station
    Euston Square	Evening	3	0	3/10	Station
    Euston Square	Evening	3	1	3/10	Station
    Euston Square	Evening	3	2	3/10	Station
    Euston Square	Late	1	0	1/10	Station
    Fairlop	Early	2	0	2/10	Station
    Fairlop	Early	2	1	2/10	Station
    Fairlop	AM Peak	5	0	5/10	Station
    Fairlop	AM Peak	5	1	5/10	Station
    Fairlop	AM Peak	5	2	5/10	Station
    Fairlop	AM Peak	5	3	5/10	Station
    Fairlop	AM Peak	5	4	5/10	Station
    Fairlop	Inter Peak	3	0	3/10	Station
    Fairlop	Inter Peak	3	1	3/10	Station
    Fairlop	Inter Peak	3	2	3/10	Station
    Fairlop	PM Peak	4	0	4/10	Station
    Fairlop	PM Peak	4	1	4/10	Station
    Fairlop	PM Peak	4	2	4/10	Station
    Fairlop	PM Peak	4	3	4/10	Station
    Fairlop	Evening	2	0	2/10	Station
    Fairlop	Evening	2	1	2/10	Station
    Fairlop	Late	1	0	1/10	Station
    Farringdon	AM Peak	9	0	9/10	Station
    Farringdon	AM Peak	9	1	9/10	Station
    Farringdon	AM Peak	9	2	9/10	Station
    Farringdon	AM Peak	9	3	9/10	Station
    Farringdon	AM Peak	9	4	9/10	Station
    Farringdon	AM Peak	9	5	9/10	Station
    Farringdon	AM Peak	9	6	9/10	Station
    Farringdon	AM Peak	9	7	9/10	Station
    Farringdon	AM Peak	9	8	9/10	Station
    Farringdon	Inter Peak	6	0	6/10	Station
    Farringdon	Inter Peak	6	1	6/10	Station
    Farringdon	Inter Peak	6	2	6/10	Station
    Farringdon	Inter Peak	6	3	6/10	Station
    Farringdon	Inter Peak	6	4	6/10	Station
    Farringdon	Inter Peak	6	5	6/10	Station
    Farringdon	PM Peak	9	0	9/10	Station
    Farringdon	PM Peak	9	1	9/10	Station
    Farringdon	PM Peak	9	2	9/10	Station
    Farringdon	PM Peak	9	3	9/10	Station
    Farringdon	PM Peak	9	4	9/10	Station
    Farringdon	PM Peak	9	5	9/10	Station
    Farringdon	PM Peak	9	6	9/10	Station
    Farringdon	PM Peak	9	7	9/10	Station
    Farringdon	PM Peak	9	8	9/10	Station
    Farringdon	Evening	3	0	3/10	Station
    Farringdon	Evening	3	1	3/10	Station
    Farringdon	Evening	3	2	3/10	Station
    Farringdon	Late	1	0	1/10	Station
    Finchley Central	Early	1	0	1/10	Station
    Finchley Central	AM Peak	6	0	6/10	Station
    Finchley Central	AM Peak	6	1	6/10	Station
    Finchley Central	AM Peak	6	2	6/10	Station
    Finchley Central	AM Peak	6	3	6/10	Station
    Finchley Central	AM Peak	6	4	6/10	Station
    Finchley Central	AM Peak	6	5	6/10	Station
    Finchley Central	Inter Peak	4	0	4/10	Station
    Finchley Central	Inter Peak	4	1	4/10	Station
    Finchley Central	Inter Peak	4	2	4/10	Station
    Finchley Central	Inter Peak	4	3	4/10	Station
    Finchley Central	PM Peak	5	0	5/10	Station
    Finchley Central	PM Peak	5	1	5/10	Station
    Finchley Central	PM Peak	5	2	5/10	Station
    Finchley Central	PM Peak	5	3	5/10	Station
    Finchley Central	PM Peak	5	4	5/10	Station
    Finchley Central	Evening	2	0	2/10	Station
    Finchley Central	Evening	2	1	2/10	Station
    Finchley Central	Late	1	0	1/10	Station
    Finchley Road	Early	1	0	1/10	Station
    Finchley Road	AM Peak	6	0	6/10	Station
    Finchley Road	AM Peak	6	1	6/10	Station
    Finchley Road	AM Peak	6	2	6/10	Station
    Finchley Road	AM Peak	6	3	6/10	Station
    Finchley Road	AM Peak	6	4	6/10	Station
    Finchley Road	AM Peak	6	5	6/10	Station
    Finchley Road	Inter Peak	5	0	5/10	Station
    Finchley Road	Inter Peak	5	1	5/10	Station
    Finchley Road	Inter Peak	5	2	5/10	Station
    Finchley Road	Inter Peak	5	3	5/10	Station
    Finchley Road	Inter Peak	5	4	5/10	Station
    Finchley Road	PM Peak	6	0	6/10	Station
    Finchley Road	PM Peak	6	1	6/10	Station
    Finchley Road	PM Peak	6	2	6/10	Station
    Finchley Road	PM Peak	6	3	6/10	Station
    Finchley Road	PM Peak	6	4	6/10	Station
    Finchley Road	PM Peak	6	5	6/10	Station
    Finchley Road	Evening	3	0	3/10	Station
    Finchley Road	Evening	3	1	3/10	Station
    Finchley Road	Evening	3	2	3/10	Station
    Finchley Road	Late	1	0	1/10	Station
    Finsbury Park	Early	1	0	1/10	Station
    Finsbury Park	AM Peak	7	0	7/10	Station
    Finsbury Park	AM Peak	7	1	7/10	Station
    Finsbury Park	AM Peak	7	2	7/10	Station
    Finsbury Park	AM Peak	7	3	7/10	Station
    Finsbury Park	AM Peak	7	4	7/10	Station
    Finsbury Park	AM Peak	7	5	7/10	Station
    Finsbury Park	AM Peak	7	6	7/10	Station
    Finsbury Park	Inter Peak	6	0	6/10	Station
    Finsbury Park	Inter Peak	6	1	6/10	Station
    Finsbury Park	Inter Peak	6	2	6/10	Station
    Finsbury Park	Inter Peak	6	3	6/10	Station
    Finsbury Park	Inter Peak	6	4	6/10	Station
    Finsbury Park	Inter Peak	6	5	6/10	Station
    Finsbury Park	PM Peak	7	0	7/10	Station
    Finsbury Park	PM Peak	7	1	7/10	Station
    Finsbury Park	PM Peak	7	2	7/10	Station
    Finsbury Park	PM Peak	7	3	7/10	Station
    Finsbury Park	PM Peak	7	4	7/10	Station
    Finsbury Park	PM Peak	7	5	7/10	Station
    Finsbury Park	PM Peak	7	6	7/10	Station
    Finsbury Park	Evening	4	0	4/10	Station
    Finsbury Park	Evening	4	1	4/10	Station
    Finsbury Park	Evening	4	2	4/10	Station
    Finsbury Park	Evening	4	3	4/10	Station
    Finsbury Park	Late	2	0	2/10	Station
    Finsbury Park	Late	2	1	2/10	Station
    Fulham Broadway	AM Peak	6	0	6/10	Station
    Fulham Broadway	AM Peak	6	1	6/10	Station
    Fulham Broadway	AM Peak	6	2	6/10	Station
    Fulham Broadway	AM Peak	6	3	6/10	Station
    Fulham Broadway	AM Peak	6	4	6/10	Station
    Fulham Broadway	AM Peak	6	5	6/10	Station
    Fulham Broadway	Inter Peak	7	0	7/10	Station
    Fulham Broadway	Inter Peak	7	1	7/10	Station
    Fulham Broadway	Inter Peak	7	2	7/10	Station
    Fulham Broadway	Inter Peak	7	3	7/10	Station
    Fulham Broadway	Inter Peak	7	4	7/10	Station
    Fulham Broadway	Inter Peak	7	5	7/10	Station
    Fulham Broadway	Inter Peak	7	6	7/10	Station
    Fulham Broadway	PM Peak	7	0	7/10	Station
    Fulham Broadway	PM Peak	7	1	7/10	Station
    Fulham Broadway	PM Peak	7	2	7/10	Station
    Fulham Broadway	PM Peak	7	3	7/10	Station
    Fulham Broadway	PM Peak	7	4	7/10	Station
    Fulham Broadway	PM Peak	7	5	7/10	Station
    Fulham Broadway	PM Peak	7	6	7/10	Station
    Fulham Broadway	Evening	3	0	3/10	Station
    Fulham Broadway	Evening	3	1	3/10	Station
    Fulham Broadway	Evening	3	2	3/10	Station
    Fulham Broadway	Late	2	0	2/10	Station
    Fulham Broadway	Late	2	1	2/10	Station
    Gants Hill	Early	2	0	2/10	Station
    Gants Hill	Early	2	1	2/10	Station
    Gants Hill	AM Peak	6	0	6/10	Station
    Gants Hill	AM Peak	6	1	6/10	Station
    Gants Hill	AM Peak	6	2	6/10	Station
    Gants Hill	AM Peak	6	3	6/10	Station
    Gants Hill	AM Peak	6	4	6/10	Station
    Gants Hill	AM Peak	6	5	6/10	Station
    Gants Hill	Inter Peak	4	0	4/10	Station
    Gants Hill	Inter Peak	4	1	4/10	Station
    Gants Hill	Inter Peak	4	2	4/10	Station
    Gants Hill	Inter Peak	4	3	4/10	Station
    Gants Hill	PM Peak	5	0	5/10	Station
    Gants Hill	PM Peak	5	1	5/10	Station
    Gants Hill	PM Peak	5	2	5/10	Station
    Gants Hill	PM Peak	5	3	5/10	Station
    Gants Hill	PM Peak	5	4	5/10	Station
    Gants Hill	Evening	3	0	3/10	Station
    Gants Hill	Evening	3	1	3/10	Station
    Gants Hill	Evening	3	2	3/10	Station
    Gants Hill	Late	1	0	1/10	Station
    Gloucester Road	AM Peak	6	0	6/10	Station
    Gloucester Road	AM Peak	6	1	6/10	Station
    Gloucester Road	AM Peak	6	2	6/10	Station
    Gloucester Road	AM Peak	6	3	6/10	Station
    Gloucester Road	AM Peak	6	4	6/10	Station
    Gloucester Road	AM Peak	6	5	6/10	Station
    Gloucester Road	Inter Peak	7	0	7/10	Station
    Gloucester Road	Inter Peak	7	1	7/10	Station
    Gloucester Road	Inter Peak	7	2	7/10	Station
    Gloucester Road	Inter Peak	7	3	7/10	Station
    Gloucester Road	Inter Peak	7	4	7/10	Station
    Gloucester Road	Inter Peak	7	5	7/10	Station
    Gloucester Road	Inter Peak	7	6	7/10	Station
    Gloucester Road	PM Peak	6	0	6/10	Station
    Gloucester Road	PM Peak	6	1	6/10	Station
    Gloucester Road	PM Peak	6	2	6/10	Station
    Gloucester Road	PM Peak	6	3	6/10	Station
    Gloucester Road	PM Peak	6	4	6/10	Station
    Gloucester Road	PM Peak	6	5	6/10	Station
    Gloucester Road	Evening	3	0	3/10	Station
    Gloucester Road	Evening	3	1	3/10	Station
    Gloucester Road	Evening	3	2	3/10	Station
    Gloucester Road	Late	2	0	2/10	Station
    Gloucester Road	Late	2	1	2/10	Station
    Golders Green	Early	1	0	1/10	Station
    Golders Green	AM Peak	6	0	6/10	Station
    Golders Green	AM Peak	6	1	6/10	Station
    Golders Green	AM Peak	6	2	6/10	Station
    Golders Green	AM Peak	6	3	6/10	Station
    Golders Green	AM Peak	6	4	6/10	Station
    Golders Green	AM Peak	6	5	6/10	Station
    Golders Green	Inter Peak	6	0	6/10	Station
    Golders Green	Inter Peak	6	1	6/10	Station
    Golders Green	Inter Peak	6	2	6/10	Station
    Golders Green	Inter Peak	6	3	6/10	Station
    Golders Green	Inter Peak	6	4	6/10	Station
    Golders Green	Inter Peak	6	5	6/10	Station
    Golders Green	PM Peak	5	0	5/10	Station
    Golders Green	PM Peak	5	1	5/10	Station
    Golders Green	PM Peak	5	2	5/10	Station
    Golders Green	PM Peak	5	3	5/10	Station
    Golders Green	PM Peak	5	4	5/10	Station
    Golders Green	Evening	3	0	3/10	Station
    Golders Green	Evening	3	1	3/10	Station
    Golders Green	Evening	3	2	3/10	Station
    Golders Green	Late	1	0	1/10	Station
    Goldhawk Road	Early	1	0	1/10	Station
    Goldhawk Road	AM Peak	6	0	6/10	Station
    Goldhawk Road	AM Peak	6	1	6/10	Station
    Goldhawk Road	AM Peak	6	2	6/10	Station
    Goldhawk Road	AM Peak	6	3	6/10	Station
    Goldhawk Road	AM Peak	6	4	6/10	Station
    Goldhawk Road	AM Peak	6	5	6/10	Station
    Goldhawk Road	Inter Peak	6	0	6/10	Station
    Goldhawk Road	Inter Peak	6	1	6/10	Station
    Goldhawk Road	Inter Peak	6	2	6/10	Station
    Goldhawk Road	Inter Peak	6	3	6/10	Station
    Goldhawk Road	Inter Peak	6	4	6/10	Station
    Goldhawk Road	Inter Peak	6	5	6/10	Station
    Goldhawk Road	PM Peak	5	0	5/10	Station
    Goldhawk Road	PM Peak	5	1	5/10	Station
    Goldhawk Road	PM Peak	5	2	5/10	Station
    Goldhawk Road	PM Peak	5	3	5/10	Station
    Goldhawk Road	PM Peak	5	4	5/10	Station
    Goldhawk Road	Evening	3	0	3/10	Station
    Goldhawk Road	Evening	3	1	3/10	Station
    Goldhawk Road	Evening	3	2	3/10	Station
    Goldhawk Road	Late	1	0	1/10	Station
    Goodge Street	AM Peak	5	0	5/10	Station
    Goodge Street	AM Peak	5	1	5/10	Station
    Goodge Street	AM Peak	5	2	5/10	Station
    Goodge Street	AM Peak	5	3	5/10	Station
    Goodge Street	AM Peak	5	4	5/10	Station
    Goodge Street	Inter Peak	6	0	6/10	Station
    Goodge Street	Inter Peak	6	1	6/10	Station
    Goodge Street	Inter Peak	6	2	6/10	Station
    Goodge Street	Inter Peak	6	3	6/10	Station
    Goodge Street	Inter Peak	6	4	6/10	Station
    Goodge Street	Inter Peak	6	5	6/10	Station
    Goodge Street	PM Peak	6	0	6/10	Station
    Goodge Street	PM Peak	6	1	6/10	Station
    Goodge Street	PM Peak	6	2	6/10	Station
    Goodge Street	PM Peak	6	3	6/10	Station
    Goodge Street	PM Peak	6	4	6/10	Station
    Goodge Street	PM Peak	6	5	6/10	Station
    Goodge Street	Evening	3	0	3/10	Station
    Goodge Street	Evening	3	1	3/10	Station
    Goodge Street	Evening	3	2	3/10	Station
    Goodge Street	Late	1	0	1/10	Station
    Grange Hill	Early	1	0	1/10	Station
    Grange Hill	AM Peak	6	0	6/10	Station
    Grange Hill	AM Peak	6	1	6/10	Station
    Grange Hill	AM Peak	6	2	6/10	Station
    Grange Hill	AM Peak	6	3	6/10	Station
    Grange Hill	AM Peak	6	4	6/10	Station
    Grange Hill	AM Peak	6	5	6/10	Station
    Grange Hill	Inter Peak	3	0	3/10	Station
    Grange Hill	Inter Peak	3	1	3/10	Station
    Grange Hill	Inter Peak	3	2	3/10	Station
    Grange Hill	PM Peak	4	0	4/10	Station
    Grange Hill	PM Peak	4	1	4/10	Station
    Grange Hill	PM Peak	4	2	4/10	Station
    Grange Hill	PM Peak	4	3	4/10	Station
    Grange Hill	Evening	2	0	2/10	Station
    Grange Hill	Evening	2	1	2/10	Station
    Grange Hill	Late	1	0	1/10	Station
    Great Portland Street	AM Peak	9	0	9/10	Station
    Great Portland Street	AM Peak	9	1	9/10	Station
    Great Portland Street	AM Peak	9	2	9/10	Station
    Great Portland Street	AM Peak	9	3	9/10	Station
    Great Portland Street	AM Peak	9	4	9/10	Station
    Great Portland Street	AM Peak	9	5	9/10	Station
    Great Portland Street	AM Peak	9	6	9/10	Station
    Great Portland Street	AM Peak	9	7	9/10	Station
    Great Portland Street	AM Peak	9	8	9/10	Station
    Great Portland Street	Inter Peak	8	0	8/10	Station
    Great Portland Street	Inter Peak	8	1	8/10	Station
    Great Portland Street	Inter Peak	8	2	8/10	Station
    Great Portland Street	Inter Peak	8	3	8/10	Station
    Great Portland Street	Inter Peak	8	4	8/10	Station
    Great Portland Street	Inter Peak	8	5	8/10	Station
    Great Portland Street	Inter Peak	8	6	8/10	Station
    Great Portland Street	Inter Peak	8	7	8/10	Station
    Great Portland Street	PM Peak	9	0	9/10	Station
    Great Portland Street	PM Peak	9	1	9/10	Station
    Great Portland Street	PM Peak	9	2	9/10	Station
    Great Portland Street	PM Peak	9	3	9/10	Station
    Great Portland Street	PM Peak	9	4	9/10	Station
    Great Portland Street	PM Peak	9	5	9/10	Station
    Great Portland Street	PM Peak	9	6	9/10	Station
    Great Portland Street	PM Peak	9	7	9/10	Station
    Great Portland Street	PM Peak	9	8	9/10	Station
    Great Portland Street	Evening	3	0	3/10	Station
    Great Portland Street	Evening	3	1	3/10	Station
    Great Portland Street	Evening	3	2	3/10	Station
    Great Portland Street	Late	1	0	1/10	Station
    Green Park	Early	1	0	1/10	Station
    Green Park	AM Peak	6	0	6/10	Station
    Green Park	AM Peak	6	1	6/10	Station
    Green Park	AM Peak	6	2	6/10	Station
    Green Park	AM Peak	6	3	6/10	Station
    Green Park	AM Peak	6	4	6/10	Station
    Green Park	AM Peak	6	5	6/10	Station
    Green Park	Inter Peak	7	0	7/10	Station
    Green Park	Inter Peak	7	1	7/10	Station
    Green Park	Inter Peak	7	2	7/10	Station
    Green Park	Inter Peak	7	3	7/10	Station
    Green Park	Inter Peak	7	4	7/10	Station
    Green Park	Inter Peak	7	5	7/10	Station
    Green Park	Inter Peak	7	6	7/10	Station
    Green Park	PM Peak	7	0	7/10	Station
    Green Park	PM Peak	7	1	7/10	Station
    Green Park	PM Peak	7	2	7/10	Station
    Green Park	PM Peak	7	3	7/10	Station
    Green Park	PM Peak	7	4	7/10	Station
    Green Park	PM Peak	7	5	7/10	Station
    Green Park	PM Peak	7	6	7/10	Station
    Green Park	Evening	3	0	3/10	Station
    Green Park	Evening	3	1	3/10	Station
    Green Park	Evening	3	2	3/10	Station
    Green Park	Late	1	0	1/10	Station
    Greenford	Early	2	0	2/10	Station
    Greenford	Early	2	1	2/10	Station
    Greenford	AM Peak	5	0	5/10	Station
    Greenford	AM Peak	5	1	5/10	Station
    Greenford	AM Peak	5	2	5/10	Station
    Greenford	AM Peak	5	3	5/10	Station
    Greenford	AM Peak	5	4	5/10	Station
    Greenford	Inter Peak	4	0	4/10	Station
    Greenford	Inter Peak	4	1	4/10	Station
    Greenford	Inter Peak	4	2	4/10	Station
    Greenford	Inter Peak	4	3	4/10	Station
    Greenford	PM Peak	6	0	6/10	Station
    Greenford	PM Peak	6	1	6/10	Station
    Greenford	PM Peak	6	2	6/10	Station
    Greenford	PM Peak	6	3	6/10	Station
    Greenford	PM Peak	6	4	6/10	Station
    Greenford	PM Peak	6	5	6/10	Station
    Greenford	Evening	2	0	2/10	Station
    Greenford	Evening	2	1	2/10	Station
    Greenford	Late	1	0	1/10	Station
    Gunnersbury	AM Peak	6	0	6/10	Station
    Gunnersbury	AM Peak	6	1	6/10	Station
    Gunnersbury	AM Peak	6	2	6/10	Station
    Gunnersbury	AM Peak	6	3	6/10	Station
    Gunnersbury	AM Peak	6	4	6/10	Station
    Gunnersbury	AM Peak	6	5	6/10	Station
    Gunnersbury	Inter Peak	3	0	3/10	Station
    Gunnersbury	Inter Peak	3	1	3/10	Station
    Gunnersbury	Inter Peak	3	2	3/10	Station
    Gunnersbury	PM Peak	5	0	5/10	Station
    Gunnersbury	PM Peak	5	1	5/10	Station
    Gunnersbury	PM Peak	5	2	5/10	Station
    Gunnersbury	PM Peak	5	3	5/10	Station
    Gunnersbury	PM Peak	5	4	5/10	Station
    Gunnersbury	Evening	2	0	2/10	Station
    Gunnersbury	Evening	2	1	2/10	Station
    Gunnersbury	Late	1	0	1/10	Station
    Hainault	Early	2	0	2/10	Station
    Hainault	Early	2	1	2/10	Station
    Hainault	AM Peak	5	0	5/10	Station
    Hainault	AM Peak	5	1	5/10	Station
    Hainault	AM Peak	5	2	5/10	Station
    Hainault	AM Peak	5	3	5/10	Station
    Hainault	AM Peak	5	4	5/10	Station
    Hainault	Inter Peak	3	0	3/10	Station
    Hainault	Inter Peak	3	1	3/10	Station
    Hainault	Inter Peak	3	2	3/10	Station
    Hainault	PM Peak	5	0	5/10	Station
    Hainault	PM Peak	5	1	5/10	Station
    Hainault	PM Peak	5	2	5/10	Station
    Hainault	PM Peak	5	3	5/10	Station
    Hainault	PM Peak	5	4	5/10	Station
    Hainault	Evening	2	0	2/10	Station
    Hainault	Evening	2	1	2/10	Station
    Hainault	Late	1	0	1/10	Station
    Hammersmith (Dis)	AM Peak	6	0	6/10	Station
    Hammersmith (Dis)	AM Peak	6	1	6/10	Station
    Hammersmith (Dis)	AM Peak	6	2	6/10	Station
    Hammersmith (Dis)	AM Peak	6	3	6/10	Station
    Hammersmith (Dis)	AM Peak	6	4	6/10	Station
    Hammersmith (Dis)	AM Peak	6	5	6/10	Station
    Hammersmith (Dis)	Inter Peak	5	0	5/10	Station
    Hammersmith (Dis)	Inter Peak	5	1	5/10	Station
    Hammersmith (Dis)	Inter Peak	5	2	5/10	Station
    Hammersmith (Dis)	Inter Peak	5	3	5/10	Station
    Hammersmith (Dis)	Inter Peak	5	4	5/10	Station
    Hammersmith (Dis)	PM Peak	6	0	6/10	Station
    Hammersmith (Dis)	PM Peak	6	1	6/10	Station
    Hammersmith (Dis)	PM Peak	6	2	6/10	Station
    Hammersmith (Dis)	PM Peak	6	3	6/10	Station
    Hammersmith (Dis)	PM Peak	6	4	6/10	Station
    Hammersmith (Dis)	PM Peak	6	5	6/10	Station
    Hammersmith (Dis)	Evening	3	0	3/10	Station
    Hammersmith (Dis)	Evening	3	1	3/10	Station
    Hammersmith (Dis)	Evening	3	2	3/10	Station
    Hammersmith (Dis)	Late	2	0	2/10	Station
    Hammersmith (Dis)	Late	2	1	2/10	Station
    Hammersmith (H&C)	AM Peak	6	0	6/10	Station
    Hammersmith (H&C)	AM Peak	6	1	6/10	Station
    Hammersmith (H&C)	AM Peak	6	2	6/10	Station
    Hammersmith (H&C)	AM Peak	6	3	6/10	Station
    Hammersmith (H&C)	AM Peak	6	4	6/10	Station
    Hammersmith (H&C)	AM Peak	6	5	6/10	Station
    Hammersmith (H&C)	Inter Peak	6	0	6/10	Station
    Hammersmith (H&C)	Inter Peak	6	1	6/10	Station
    Hammersmith (H&C)	Inter Peak	6	2	6/10	Station
    Hammersmith (H&C)	Inter Peak	6	3	6/10	Station
    Hammersmith (H&C)	Inter Peak	6	4	6/10	Station
    Hammersmith (H&C)	Inter Peak	6	5	6/10	Station
    Hammersmith (H&C)	PM Peak	6	0	6/10	Station
    Hammersmith (H&C)	PM Peak	6	1	6/10	Station
    Hammersmith (H&C)	PM Peak	6	2	6/10	Station
    Hammersmith (H&C)	PM Peak	6	3	6/10	Station
    Hammersmith (H&C)	PM Peak	6	4	6/10	Station
    Hammersmith (H&C)	PM Peak	6	5	6/10	Station
    Hammersmith (H&C)	Evening	3	0	3/10	Station
    Hammersmith (H&C)	Evening	3	1	3/10	Station
    Hammersmith (H&C)	Evening	3	2	3/10	Station
    Hammersmith (H&C)	Late	1	0	1/10	Station
    Hampstead	AM Peak	5	0	5/10	Station
    Hampstead	AM Peak	5	1	5/10	Station
    Hampstead	AM Peak	5	2	5/10	Station
    Hampstead	AM Peak	5	3	5/10	Station
    Hampstead	AM Peak	5	4	5/10	Station
    Hampstead	Inter Peak	6	0	6/10	Station
    Hampstead	Inter Peak	6	1	6/10	Station
    Hampstead	Inter Peak	6	2	6/10	Station
    Hampstead	Inter Peak	6	3	6/10	Station
    Hampstead	Inter Peak	6	4	6/10	Station
    Hampstead	Inter Peak	6	5	6/10	Station
    Hampstead	PM Peak	5	0	5/10	Station
    Hampstead	PM Peak	5	1	5/10	Station
    Hampstead	PM Peak	5	2	5/10	Station
    Hampstead	PM Peak	5	3	5/10	Station
    Hampstead	PM Peak	5	4	5/10	Station
    Hampstead	Evening	2	0	2/10	Station
    Hampstead	Evening	2	1	2/10	Station
    Hampstead	Late	1	0	1/10	Station
    Hanger Lane	Early	1	0	1/10	Station
    Hanger Lane	AM Peak	6	0	6/10	Station
    Hanger Lane	AM Peak	6	1	6/10	Station
    Hanger Lane	AM Peak	6	2	6/10	Station
    Hanger Lane	AM Peak	6	3	6/10	Station
    Hanger Lane	AM Peak	6	4	6/10	Station
    Hanger Lane	AM Peak	6	5	6/10	Station
    Hanger Lane	Inter Peak	4	0	4/10	Station
    Hanger Lane	Inter Peak	4	1	4/10	Station
    Hanger Lane	Inter Peak	4	2	4/10	Station
    Hanger Lane	Inter Peak	4	3	4/10	Station
    Hanger Lane	PM Peak	6	0	6/10	Station
    Hanger Lane	PM Peak	6	1	6/10	Station
    Hanger Lane	PM Peak	6	2	6/10	Station
    Hanger Lane	PM Peak	6	3	6/10	Station
    Hanger Lane	PM Peak	6	4	6/10	Station
    Hanger Lane	PM Peak	6	5	6/10	Station
    Hanger Lane	Evening	2	0	2/10	Station
    Hanger Lane	Evening	2	1	2/10	Station
    Hanger Lane	Late	1	0	1/10	Station
    Harlesden	Early	1	0	1/10	Station
    Harlesden	AM Peak	6	0	6/10	Station
    Harlesden	AM Peak	6	1	6/10	Station
    Harlesden	AM Peak	6	2	6/10	Station
    Harlesden	AM Peak	6	3	6/10	Station
    Harlesden	AM Peak	6	4	6/10	Station
    Harlesden	AM Peak	6	5	6/10	Station
    Harlesden	Inter Peak	5	0	5/10	Station
    Harlesden	Inter Peak	5	1	5/10	Station
    Harlesden	Inter Peak	5	2	5/10	Station
    Harlesden	Inter Peak	5	3	5/10	Station
    Harlesden	Inter Peak	5	4	5/10	Station
    Harlesden	PM Peak	5	0	5/10	Station
    Harlesden	PM Peak	5	1	5/10	Station
    Harlesden	PM Peak	5	2	5/10	Station
    Harlesden	PM Peak	5	3	5/10	Station
    Harlesden	PM Peak	5	4	5/10	Station
    Harlesden	Evening	2	0	2/10	Station
    Harlesden	Evening	2	1	2/10	Station
    Harlesden	Late	1	0	1/10	Station
    Harrow & Wealdstone	Early	1	0	1/10	Station
    Harrow & Wealdstone	AM Peak	6	0	6/10	Station
    Harrow & Wealdstone	AM Peak	6	1	6/10	Station
    Harrow & Wealdstone	AM Peak	6	2	6/10	Station
    Harrow & Wealdstone	AM Peak	6	3	6/10	Station
    Harrow & Wealdstone	AM Peak	6	4	6/10	Station
    Harrow & Wealdstone	AM Peak	6	5	6/10	Station
    Harrow & Wealdstone	Inter Peak	4	0	4/10	Station
    Harrow & Wealdstone	Inter Peak	4	1	4/10	Station
    Harrow & Wealdstone	Inter Peak	4	2	4/10	Station
    Harrow & Wealdstone	Inter Peak	4	3	4/10	Station
    Harrow & Wealdstone	PM Peak	5	0	5/10	Station
    Harrow & Wealdstone	PM Peak	5	1	5/10	Station
    Harrow & Wealdstone	PM Peak	5	2	5/10	Station
    Harrow & Wealdstone	PM Peak	5	3	5/10	Station
    Harrow & Wealdstone	PM Peak	5	4	5/10	Station
    Harrow & Wealdstone	Evening	2	0	2/10	Station
    Harrow & Wealdstone	Evening	2	1	2/10	Station
    Harrow & Wealdstone	Late	1	0	1/10	Station
    Harrow-on-the-Hill	Early	2	0	2/10	Station
    Harrow-on-the-Hill	Early	2	1	2/10	Station
    Harrow-on-the-Hill	AM Peak	8	0	8/10	Station
    Harrow-on-the-Hill	AM Peak	8	1	8/10	Station
    Harrow-on-the-Hill	AM Peak	8	2	8/10	Station
    Harrow-on-the-Hill	AM Peak	8	3	8/10	Station
    Harrow-on-the-Hill	AM Peak	8	4	8/10	Station
    Harrow-on-the-Hill	AM Peak	8	5	8/10	Station
    Harrow-on-the-Hill	AM Peak	8	6	8/10	Station
    Harrow-on-the-Hill	AM Peak	8	7	8/10	Station
    Harrow-on-the-Hill	Inter Peak	8	0	8/10	Station
    Harrow-on-the-Hill	Inter Peak	8	1	8/10	Station
    Harrow-on-the-Hill	Inter Peak	8	2	8/10	Station
    Harrow-on-the-Hill	Inter Peak	8	3	8/10	Station
    Harrow-on-the-Hill	Inter Peak	8	4	8/10	Station
    Harrow-on-the-Hill	Inter Peak	8	5	8/10	Station
    Harrow-on-the-Hill	Inter Peak	8	6	8/10	Station
    Harrow-on-the-Hill	Inter Peak	8	7	8/10	Station
    Harrow-on-the-Hill	PM Peak	9	0	9/10	Station
    Harrow-on-the-Hill	PM Peak	9	1	9/10	Station
    Harrow-on-the-Hill	PM Peak	9	2	9/10	Station
    Harrow-on-the-Hill	PM Peak	9	3	9/10	Station
    Harrow-on-the-Hill	PM Peak	9	4	9/10	Station
    Harrow-on-the-Hill	PM Peak	9	5	9/10	Station
    Harrow-on-the-Hill	PM Peak	9	6	9/10	Station
    Harrow-on-the-Hill	PM Peak	9	7	9/10	Station
    Harrow-on-the-Hill	PM Peak	9	8	9/10	Station
    Harrow-on-the-Hill	Evening	4	0	4/10	Station
    Harrow-on-the-Hill	Evening	4	1	4/10	Station
    Harrow-on-the-Hill	Evening	4	2	4/10	Station
    Harrow-on-the-Hill	Evening	4	3	4/10	Station
    Harrow-on-the-Hill	Late	2	0	2/10	Station
    Harrow-on-the-Hill	Late	2	1	2/10	Station
    Hatton Cross	Early	2	0	2/10	Station
    Hatton Cross	Early	2	1	2/10	Station
    Hatton Cross	AM Peak	5	0	5/10	Station
    Hatton Cross	AM Peak	5	1	5/10	Station
    Hatton Cross	AM Peak	5	2	5/10	Station
    Hatton Cross	AM Peak	5	3	5/10	Station
    Hatton Cross	AM Peak	5	4	5/10	Station
    Hatton Cross	Inter Peak	5	0	5/10	Station
    Hatton Cross	Inter Peak	5	1	5/10	Station
    Hatton Cross	Inter Peak	5	2	5/10	Station
    Hatton Cross	Inter Peak	5	3	5/10	Station
    Hatton Cross	Inter Peak	5	4	5/10	Station
    Hatton Cross	PM Peak	5	0	5/10	Station
    Hatton Cross	PM Peak	5	1	5/10	Station
    Hatton Cross	PM Peak	5	2	5/10	Station
    Hatton Cross	PM Peak	5	3	5/10	Station
    Hatton Cross	PM Peak	5	4	5/10	Station
    Hatton Cross	Evening	2	0	2/10	Station
    Hatton Cross	Evening	2	1	2/10	Station
    Hatton Cross	Late	1	0	1/10	Station
    Heathrow Terminals 123	Early	1	0	1/10	Station
    Heathrow Terminals 123	AM Peak	2	0	2/10	Station
    Heathrow Terminals 123	AM Peak	2	1	2/10	Station
    Heathrow Terminals 123	Inter Peak	5	0	5/10	Station
    Heathrow Terminals 123	Inter Peak	5	1	5/10	Station
    Heathrow Terminals 123	Inter Peak	5	2	5/10	Station
    Heathrow Terminals 123	Inter Peak	5	3	5/10	Station
    Heathrow Terminals 123	Inter Peak	5	4	5/10	Station
    Heathrow Terminals 123	PM Peak	3	0	3/10	Station
    Heathrow Terminals 123	PM Peak	3	1	3/10	Station
    Heathrow Terminals 123	PM Peak	3	2	3/10	Station
    Heathrow Terminals 123	Evening	2	0	2/10	Station
    Heathrow Terminals 123	Evening	2	1	2/10	Station
    Heathrow Terminals 123	Late	1	0	1/10	Station
    Heathrow Terminal 4	Early	1	0	1/10	Station
    Heathrow Terminal 4	AM Peak	2	0	2/10	Station
    Heathrow Terminal 4	AM Peak	2	1	2/10	Station
    Heathrow Terminal 4	Inter Peak	5	0	5/10	Station
    Heathrow Terminal 4	Inter Peak	5	1	5/10	Station
    Heathrow Terminal 4	Inter Peak	5	2	5/10	Station
    Heathrow Terminal 4	Inter Peak	5	3	5/10	Station
    Heathrow Terminal 4	Inter Peak	5	4	5/10	Station
    Heathrow Terminal 4	PM Peak	4	0	4/10	Station
    Heathrow Terminal 4	PM Peak	4	1	4/10	Station
    Heathrow Terminal 4	PM Peak	4	2	4/10	Station
    Heathrow Terminal 4	PM Peak	4	3	4/10	Station
    Heathrow Terminal 4	Evening	2	0	2/10	Station
    Heathrow Terminal 4	Evening	2	1	2/10	Station
    Heathrow Terminal 4	Late	1	0	1/10	Station
    Heathrow Terminal 5	Early	1	0	1/10	Station
    Heathrow Terminal 5	AM Peak	2	0	2/10	Station
    Heathrow Terminal 5	AM Peak	2	1	2/10	Station
    Heathrow Terminal 5	Inter Peak	5	0	5/10	Station
    Heathrow Terminal 5	Inter Peak	5	1	5/10	Station
    Heathrow Terminal 5	Inter Peak	5	2	5/10	Station
    Heathrow Terminal 5	Inter Peak	5	3	5/10	Station
    Heathrow Terminal 5	Inter Peak	5	4	5/10	Station
    Heathrow Terminal 5	PM Peak	3	0	3/10	Station
    Heathrow Terminal 5	PM Peak	3	1	3/10	Station
    Heathrow Terminal 5	PM Peak	3	2	3/10	Station
    Heathrow Terminal 5	Evening	2	0	2/10	Station
    Heathrow Terminal 5	Evening	2	1	2/10	Station
    Heathrow Terminal 5	Late	1	0	1/10	Station
    Hendon Central	Early	1	0	1/10	Station
    Hendon Central	AM Peak	5	0	5/10	Station
    Hendon Central	AM Peak	5	1	5/10	Station
    Hendon Central	AM Peak	5	2	5/10	Station
    Hendon Central	AM Peak	5	3	5/10	Station
    Hendon Central	AM Peak	5	4	5/10	Station
    Hendon Central	Inter Peak	6	0	6/10	Station
    Hendon Central	Inter Peak	6	1	6/10	Station
    Hendon Central	Inter Peak	6	2	6/10	Station
    Hendon Central	Inter Peak	6	3	6/10	Station
    Hendon Central	Inter Peak	6	4	6/10	Station
    Hendon Central	Inter Peak	6	5	6/10	Station
    Hendon Central	PM Peak	5	0	5/10	Station
    Hendon Central	PM Peak	5	1	5/10	Station
    Hendon Central	PM Peak	5	2	5/10	Station
    Hendon Central	PM Peak	5	3	5/10	Station
    Hendon Central	PM Peak	5	4	5/10	Station
    Hendon Central	Evening	2	0	2/10	Station
    Hendon Central	Evening	2	1	2/10	Station
    Hendon Central	Late	1	0	1/10	Station
    High Barnet	Early	1	0	1/10	Station
    High Barnet	AM Peak	5	0	5/10	Station
    High Barnet	AM Peak	5	1	5/10	Station
    High Barnet	AM Peak	5	2	5/10	Station
    High Barnet	AM Peak	5	3	5/10	Station
    High Barnet	AM Peak	5	4	5/10	Station
    High Barnet	Inter Peak	3	0	3/10	Station
    High Barnet	Inter Peak	3	1	3/10	Station
    High Barnet	Inter Peak	3	2	3/10	Station
    High Barnet	PM Peak	4	0	4/10	Station
    High Barnet	PM Peak	4	1	4/10	Station
    High Barnet	PM Peak	4	2	4/10	Station
    High Barnet	PM Peak	4	3	4/10	Station
    High Barnet	Evening	2	0	2/10	Station
    High Barnet	Evening	2	1	2/10	Station
    High Barnet	Late	1	0	1/10	Station
    High Street Kensington	AM Peak	4	0	4/10	Station
    High Street Kensington	AM Peak	4	1	4/10	Station
    High Street Kensington	AM Peak	4	2	4/10	Station
    High Street Kensington	AM Peak	4	3	4/10	Station
    High Street Kensington	Inter Peak	6	0	6/10	Station
    High Street Kensington	Inter Peak	6	1	6/10	Station
    High Street Kensington	Inter Peak	6	2	6/10	Station
    High Street Kensington	Inter Peak	6	3	6/10	Station
    High Street Kensington	Inter Peak	6	4	6/10	Station
    High Street Kensington	Inter Peak	6	5	6/10	Station
    High Street Kensington	PM Peak	5	0	5/10	Station
    High Street Kensington	PM Peak	5	1	5/10	Station
    High Street Kensington	PM Peak	5	2	5/10	Station
    High Street Kensington	PM Peak	5	3	5/10	Station
    High Street Kensington	PM Peak	5	4	5/10	Station
    High Street Kensington	Evening	2	0	2/10	Station
    High Street Kensington	Evening	2	1	2/10	Station
    High Street Kensington	Late	1	0	1/10	Station
    Highbury & Islington	Early	1	0	1/10	Station
    Highbury & Islington	AM Peak	8	0	8/10	Station
    Highbury & Islington	AM Peak	8	1	8/10	Station
    Highbury & Islington	AM Peak	8	2	8/10	Station
    Highbury & Islington	AM Peak	8	3	8/10	Station
    Highbury & Islington	AM Peak	8	4	8/10	Station
    Highbury & Islington	AM Peak	8	5	8/10	Station
    Highbury & Islington	AM Peak	8	6	8/10	Station
    Highbury & Islington	AM Peak	8	7	8/10	Station
    Highbury & Islington	Inter Peak	7	0	7/10	Station
    Highbury & Islington	Inter Peak	7	1	7/10	Station
    Highbury & Islington	Inter Peak	7	2	7/10	Station
    Highbury & Islington	Inter Peak	7	3	7/10	Station
    Highbury & Islington	Inter Peak	7	4	7/10	Station
    Highbury & Islington	Inter Peak	7	5	7/10	Station
    Highbury & Islington	Inter Peak	7	6	7/10	Station
    Highbury & Islington	PM Peak	8	0	8/10	Station
    Highbury & Islington	PM Peak	8	1	8/10	Station
    Highbury & Islington	PM Peak	8	2	8/10	Station
    Highbury & Islington	PM Peak	8	3	8/10	Station
    Highbury & Islington	PM Peak	8	4	8/10	Station
    Highbury & Islington	PM Peak	8	5	8/10	Station
    Highbury & Islington	PM Peak	8	6	8/10	Station
    Highbury & Islington	PM Peak	8	7	8/10	Station
    Highbury & Islington	Evening	4	0	4/10	Station
    Highbury & Islington	Evening	4	1	4/10	Station
    Highbury & Islington	Evening	4	2	4/10	Station
    Highbury & Islington	Evening	4	3	4/10	Station
    Highbury & Islington	Late	2	0	2/10	Station
    Highbury & Islington	Late	2	1	2/10	Station
    Highgate	Early	1	0	1/10	Station
    Highgate	AM Peak	7	0	7/10	Station
    Highgate	AM Peak	7	1	7/10	Station
    Highgate	AM Peak	7	2	7/10	Station
    Highgate	AM Peak	7	3	7/10	Station
    Highgate	AM Peak	7	4	7/10	Station
    Highgate	AM Peak	7	5	7/10	Station
    Highgate	AM Peak	7	6	7/10	Station
    Highgate	Inter Peak	4	0	4/10	Station
    Highgate	Inter Peak	4	1	4/10	Station
    Highgate	Inter Peak	4	2	4/10	Station
    Highgate	Inter Peak	4	3	4/10	Station
    Highgate	PM Peak	6	0	6/10	Station
    Highgate	PM Peak	6	1	6/10	Station
    Highgate	PM Peak	6	2	6/10	Station
    Highgate	PM Peak	6	3	6/10	Station
    Highgate	PM Peak	6	4	6/10	Station
    Highgate	PM Peak	6	5	6/10	Station
    Highgate	Evening	3	0	3/10	Station
    Highgate	Evening	3	1	3/10	Station
    Highgate	Evening	3	2	3/10	Station
    Highgate	Late	1	0	1/10	Station
    Hillingdon	Early	1	0	1/10	Station
    Hillingdon	AM Peak	5	0	5/10	Station
    Hillingdon	AM Peak	5	1	5/10	Station
    Hillingdon	AM Peak	5	2	5/10	Station
    Hillingdon	AM Peak	5	3	5/10	Station
    Hillingdon	AM Peak	5	4	5/10	Station
    Hillingdon	Inter Peak	3	0	3/10	Station
    Hillingdon	Inter Peak	3	1	3/10	Station
    Hillingdon	Inter Peak	3	2	3/10	Station
    Hillingdon	PM Peak	4	0	4/10	Station
    Hillingdon	PM Peak	4	1	4/10	Station
    Hillingdon	PM Peak	4	2	4/10	Station
    Hillingdon	PM Peak	4	3	4/10	Station
    Hillingdon	Evening	2	0	2/10	Station
    Hillingdon	Evening	2	1	2/10	Station
    Hillingdon	Late	1	0	1/10	Station
    Holborn	AM Peak	6	0	6/10	Station
    Holborn	AM Peak	6	1	6/10	Station
    Holborn	AM Peak	6	2	6/10	Station
    Holborn	AM Peak	6	3	6/10	Station
    Holborn	AM Peak	6	4	6/10	Station
    Holborn	AM Peak	6	5	6/10	Station
    Holborn	Inter Peak	7	0	7/10	Station
    Holborn	Inter Peak	7	1	7/10	Station
    Holborn	Inter Peak	7	2	7/10	Station
    Holborn	Inter Peak	7	3	7/10	Station
    Holborn	Inter Peak	7	4	7/10	Station
    Holborn	Inter Peak	7	5	7/10	Station
    Holborn	Inter Peak	7	6	7/10	Station
    Holborn	PM Peak	6	0	6/10	Station
    Holborn	PM Peak	6	1	6/10	Station
    Holborn	PM Peak	6	2	6/10	Station
    Holborn	PM Peak	6	3	6/10	Station
    Holborn	PM Peak	6	4	6/10	Station
    Holborn	PM Peak	6	5	6/10	Station
    Holborn	Evening	3	0	3/10	Station
    Holborn	Evening	3	1	3/10	Station
    Holborn	Evening	3	2	3/10	Station
    Holborn	Late	1	0	1/10	Station
    Holland Park	AM Peak	6	0	6/10	Station
    Holland Park	AM Peak	6	1	6/10	Station
    Holland Park	AM Peak	6	2	6/10	Station
    Holland Park	AM Peak	6	3	6/10	Station
    Holland Park	AM Peak	6	4	6/10	Station
    Holland Park	AM Peak	6	5	6/10	Station
    Holland Park	Inter Peak	5	0	5/10	Station
    Holland Park	Inter Peak	5	1	5/10	Station
    Holland Park	Inter Peak	5	2	5/10	Station
    Holland Park	Inter Peak	5	3	5/10	Station
    Holland Park	Inter Peak	5	4	5/10	Station
    Holland Park	PM Peak	5	0	5/10	Station
    Holland Park	PM Peak	5	1	5/10	Station
    Holland Park	PM Peak	5	2	5/10	Station
    Holland Park	PM Peak	5	3	5/10	Station
    Holland Park	PM Peak	5	4	5/10	Station
    Holland Park	Evening	2	0	2/10	Station
    Holland Park	Evening	2	1	2/10	Station
    Holland Park	Late	1	0	1/10	Station
    Holloway Road	AM Peak	6	0	6/10	Station
    Holloway Road	AM Peak	6	1	6/10	Station
    Holloway Road	AM Peak	6	2	6/10	Station
    Holloway Road	AM Peak	6	3	6/10	Station
    Holloway Road	AM Peak	6	4	6/10	Station
    Holloway Road	AM Peak	6	5	6/10	Station
    Holloway Road	Inter Peak	7	0	7/10	Station
    Holloway Road	Inter Peak	7	1	7/10	Station
    Holloway Road	Inter Peak	7	2	7/10	Station
    Holloway Road	Inter Peak	7	3	7/10	Station
    Holloway Road	Inter Peak	7	4	7/10	Station
    Holloway Road	Inter Peak	7	5	7/10	Station
    Holloway Road	Inter Peak	7	6	7/10	Station
    Holloway Road	PM Peak	6	0	6/10	Station
    Holloway Road	PM Peak	6	1	6/10	Station
    Holloway Road	PM Peak	6	2	6/10	Station
    Holloway Road	PM Peak	6	3	6/10	Station
    Holloway Road	PM Peak	6	4	6/10	Station
    Holloway Road	PM Peak	6	5	6/10	Station
    Holloway Road	Evening	3	0	3/10	Station
    Holloway Road	Evening	3	1	3/10	Station
    Holloway Road	Evening	3	2	3/10	Station
    Holloway Road	Late	2	0	2/10	Station
    Holloway Road	Late	2	1	2/10	Station
    Hornchurch	Early	1	0	1/10	Station
    Hornchurch	AM Peak	5	0	5/10	Station
    Hornchurch	AM Peak	5	1	5/10	Station
    Hornchurch	AM Peak	5	2	5/10	Station
    Hornchurch	AM Peak	5	3	5/10	Station
    Hornchurch	AM Peak	5	4	5/10	Station
    Hornchurch	Inter Peak	3	0	3/10	Station
    Hornchurch	Inter Peak	3	1	3/10	Station
    Hornchurch	Inter Peak	3	2	3/10	Station
    Hornchurch	PM Peak	5	0	5/10	Station
    Hornchurch	PM Peak	5	1	5/10	Station
    Hornchurch	PM Peak	5	2	5/10	Station
    Hornchurch	PM Peak	5	3	5/10	Station
    Hornchurch	PM Peak	5	4	5/10	Station
    Hornchurch	Evening	2	0	2/10	Station
    Hornchurch	Evening	2	1	2/10	Station
    Hornchurch	Late	1	0	1/10	Station
    Hounslow Central	Early	2	0	2/10	Station
    Hounslow Central	Early	2	1	2/10	Station
    Hounslow Central	AM Peak	6	0	6/10	Station
    Hounslow Central	AM Peak	6	1	6/10	Station
    Hounslow Central	AM Peak	6	2	6/10	Station
    Hounslow Central	AM Peak	6	3	6/10	Station
    Hounslow Central	AM Peak	6	4	6/10	Station
    Hounslow Central	AM Peak	6	5	6/10	Station
    Hounslow Central	Inter Peak	5	0	5/10	Station
    Hounslow Central	Inter Peak	5	1	5/10	Station
    Hounslow Central	Inter Peak	5	2	5/10	Station
    Hounslow Central	Inter Peak	5	3	5/10	Station
    Hounslow Central	Inter Peak	5	4	5/10	Station
    Hounslow Central	PM Peak	5	0	5/10	Station
    Hounslow Central	PM Peak	5	1	5/10	Station
    Hounslow Central	PM Peak	5	2	5/10	Station
    Hounslow Central	PM Peak	5	3	5/10	Station
    Hounslow Central	PM Peak	5	4	5/10	Station
    Hounslow Central	Evening	2	0	2/10	Station
    Hounslow Central	Evening	2	1	2/10	Station
    Hounslow Central	Late	1	0	1/10	Station
    Hounslow East	Early	2	0	2/10	Station
    Hounslow East	Early	2	1	2/10	Station
    Hounslow East	AM Peak	5	0	5/10	Station
    Hounslow East	AM Peak	5	1	5/10	Station
    Hounslow East	AM Peak	5	2	5/10	Station
    Hounslow East	AM Peak	5	3	5/10	Station
    Hounslow East	AM Peak	5	4	5/10	Station
    Hounslow East	Inter Peak	5	0	5/10	Station
    Hounslow East	Inter Peak	5	1	5/10	Station
    Hounslow East	Inter Peak	5	2	5/10	Station
    Hounslow East	Inter Peak	5	3	5/10	Station
    Hounslow East	Inter Peak	5	4	5/10	Station
    Hounslow East	PM Peak	6	0	6/10	Station
    Hounslow East	PM Peak	6	1	6/10	Station
    Hounslow East	PM Peak	6	2	6/10	Station
    Hounslow East	PM Peak	6	3	6/10	Station
    Hounslow East	PM Peak	6	4	6/10	Station
    Hounslow East	PM Peak	6	5	6/10	Station
    Hounslow East	Evening	3	0	3/10	Station
    Hounslow East	Evening	3	1	3/10	Station
    Hounslow East	Evening	3	2	3/10	Station
    Hounslow East	Late	1	0	1/10	Station
    Hounslow West	Early	2	0	2/10	Station
    Hounslow West	Early	2	1	2/10	Station
    Hounslow West	AM Peak	5	0	5/10	Station
    Hounslow West	AM Peak	5	1	5/10	Station
    Hounslow West	AM Peak	5	2	5/10	Station
    Hounslow West	AM Peak	5	3	5/10	Station
    Hounslow West	AM Peak	5	4	5/10	Station
    Hounslow West	Inter Peak	6	0	6/10	Station
    Hounslow West	Inter Peak	6	1	6/10	Station
    Hounslow West	Inter Peak	6	2	6/10	Station
    Hounslow West	Inter Peak	6	3	6/10	Station
    Hounslow West	Inter Peak	6	4	6/10	Station
    Hounslow West	Inter Peak	6	5	6/10	Station
    Hounslow West	PM Peak	5	0	5/10	Station
    Hounslow West	PM Peak	5	1	5/10	Station
    Hounslow West	PM Peak	5	2	5/10	Station
    Hounslow West	PM Peak	5	3	5/10	Station
    Hounslow West	PM Peak	5	4	5/10	Station
    Hounslow West	Evening	3	0	3/10	Station
    Hounslow West	Evening	3	1	3/10	Station
    Hounslow West	Evening	3	2	3/10	Station
    Hounslow West	Late	2	0	2/10	Station
    Hounslow West	Late	2	1	2/10	Station
    Hyde Park Corner	AM Peak	4	0	4/10	Station
    Hyde Park Corner	AM Peak	4	1	4/10	Station
    Hyde Park Corner	AM Peak	4	2	4/10	Station
    Hyde Park Corner	AM Peak	4	3	4/10	Station
    Hyde Park Corner	Inter Peak	7	0	7/10	Station
    Hyde Park Corner	Inter Peak	7	1	7/10	Station
    Hyde Park Corner	Inter Peak	7	2	7/10	Station
    Hyde Park Corner	Inter Peak	7	3	7/10	Station
    Hyde Park Corner	Inter Peak	7	4	7/10	Station
    Hyde Park Corner	Inter Peak	7	5	7/10	Station
    Hyde Park Corner	Inter Peak	7	6	7/10	Station
    Hyde Park Corner	PM Peak	6	0	6/10	Station
    Hyde Park Corner	PM Peak	6	1	6/10	Station
    Hyde Park Corner	PM Peak	6	2	6/10	Station
    Hyde Park Corner	PM Peak	6	3	6/10	Station
    Hyde Park Corner	PM Peak	6	4	6/10	Station
    Hyde Park Corner	PM Peak	6	5	6/10	Station
    Hyde Park Corner	Evening	3	0	3/10	Station
    Hyde Park Corner	Evening	3	1	3/10	Station
    Hyde Park Corner	Evening	3	2	3/10	Station
    Hyde Park Corner	Late	1	0	1/10	Station
    Ickenham	Early	1	0	1/10	Station
    Ickenham	AM Peak	5	0	5/10	Station
    Ickenham	AM Peak	5	1	5/10	Station
    Ickenham	AM Peak	5	2	5/10	Station
    Ickenham	AM Peak	5	3	5/10	Station
    Ickenham	AM Peak	5	4	5/10	Station
    Ickenham	Inter Peak	4	0	4/10	Station
    Ickenham	Inter Peak	4	1	4/10	Station
    Ickenham	Inter Peak	4	2	4/10	Station
    Ickenham	Inter Peak	4	3	4/10	Station
    Ickenham	PM Peak	5	0	5/10	Station
    Ickenham	PM Peak	5	1	5/10	Station
    Ickenham	PM Peak	5	2	5/10	Station
    Ickenham	PM Peak	5	3	5/10	Station
    Ickenham	PM Peak	5	4	5/10	Station
    Ickenham	Evening	2	0	2/10	Station
    Ickenham	Evening	2	1	2/10	Station
    Ickenham	Late	1	0	1/10	Station
    Kennington	Early	1	0	1/10	Station
    Kennington	AM Peak	8	0	8/10	Station
    Kennington	AM Peak	8	1	8/10	Station
    Kennington	AM Peak	8	2	8/10	Station
    Kennington	AM Peak	8	3	8/10	Station
    Kennington	AM Peak	8	4	8/10	Station
    Kennington	AM Peak	8	5	8/10	Station
    Kennington	AM Peak	8	6	8/10	Station
    Kennington	AM Peak	8	7	8/10	Station
    Kennington	Inter Peak	6	0	6/10	Station
    Kennington	Inter Peak	6	1	6/10	Station
    Kennington	Inter Peak	6	2	6/10	Station
    Kennington	Inter Peak	6	3	6/10	Station
    Kennington	Inter Peak	6	4	6/10	Station
    Kennington	Inter Peak	6	5	6/10	Station
    Kennington	PM Peak	7	0	7/10	Station
    Kennington	PM Peak	7	1	7/10	Station
    Kennington	PM Peak	7	2	7/10	Station
    Kennington	PM Peak	7	3	7/10	Station
    Kennington	PM Peak	7	4	7/10	Station
    Kennington	PM Peak	7	5	7/10	Station
    Kennington	PM Peak	7	6	7/10	Station
    Kennington	Evening	4	0	4/10	Station
    Kennington	Evening	4	1	4/10	Station
    Kennington	Evening	4	2	4/10	Station
    Kennington	Evening	4	3	4/10	Station
    Kennington	Late	3	0	3/10	Station
    Kennington	Late	3	1	3/10	Station
    Kennington	Late	3	2	3/10	Station
    Kensal Green	Early	1	0	1/10	Station
    Kensal Green	AM Peak	6	0	6/10	Station
    Kensal Green	AM Peak	6	1	6/10	Station
    Kensal Green	AM Peak	6	2	6/10	Station
    Kensal Green	AM Peak	6	3	6/10	Station
    Kensal Green	AM Peak	6	4	6/10	Station
    Kensal Green	AM Peak	6	5	6/10	Station
    Kensal Green	Inter Peak	4	0	4/10	Station
    Kensal Green	Inter Peak	4	1	4/10	Station
    Kensal Green	Inter Peak	4	2	4/10	Station
    Kensal Green	Inter Peak	4	3	4/10	Station
    Kensal Green	PM Peak	4	0	4/10	Station
    Kensal Green	PM Peak	4	1	4/10	Station
    Kensal Green	PM Peak	4	2	4/10	Station
    Kensal Green	PM Peak	4	3	4/10	Station
    Kensal Green	Evening	2	0	2/10	Station
    Kensal Green	Evening	2	1	2/10	Station
    Kensal Green	Late	1	0	1/10	Station
    Kensington (Olympia)	AM Peak	2	0	2/10	Station
    Kensington (Olympia)	AM Peak	2	1	2/10	Station
    Kensington (Olympia)	Inter Peak	5	0	5/10	Station
    Kensington (Olympia)	Inter Peak	5	1	5/10	Station
    Kensington (Olympia)	Inter Peak	5	2	5/10	Station
    Kensington (Olympia)	Inter Peak	5	3	5/10	Station
    Kensington (Olympia)	Inter Peak	5	4	5/10	Station
    Kensington (Olympia)	PM Peak	2	0	2/10	Station
    Kensington (Olympia)	PM Peak	2	1	2/10	Station
    Kensington (Olympia)	Evening	1	0	1/10	Station
    Kentish Town	Early	1	0	1/10	Station
    Kentish Town	AM Peak	8	0	8/10	Station
    Kentish Town	AM Peak	8	1	8/10	Station
    Kentish Town	AM Peak	8	2	8/10	Station
    Kentish Town	AM Peak	8	3	8/10	Station
    Kentish Town	AM Peak	8	4	8/10	Station
    Kentish Town	AM Peak	8	5	8/10	Station
    Kentish Town	AM Peak	8	6	8/10	Station
    Kentish Town	AM Peak	8	7	8/10	Station
    Kentish Town	Inter Peak	7	0	7/10	Station
    Kentish Town	Inter Peak	7	1	7/10	Station
    Kentish Town	Inter Peak	7	2	7/10	Station
    Kentish Town	Inter Peak	7	3	7/10	Station
    Kentish Town	Inter Peak	7	4	7/10	Station
    Kentish Town	Inter Peak	7	5	7/10	Station
    Kentish Town	Inter Peak	7	6	7/10	Station
    Kentish Town	PM Peak	8	0	8/10	Station
    Kentish Town	PM Peak	8	1	8/10	Station
    Kentish Town	PM Peak	8	2	8/10	Station
    Kentish Town	PM Peak	8	3	8/10	Station
    Kentish Town	PM Peak	8	4	8/10	Station
    Kentish Town	PM Peak	8	5	8/10	Station
    Kentish Town	PM Peak	8	6	8/10	Station
    Kentish Town	PM Peak	8	7	8/10	Station
    Kentish Town	Evening	4	0	4/10	Station
    Kentish Town	Evening	4	1	4/10	Station
    Kentish Town	Evening	4	2	4/10	Station
    Kentish Town	Evening	4	3	4/10	Station
    Kentish Town	Late	3	0	3/10	Station
    Kentish Town	Late	3	1	3/10	Station
    Kentish Town	Late	3	2	3/10	Station
    Kenton	Early	2	0	2/10	Station
    Kenton	Early	2	1	2/10	Station
    Kenton	AM Peak	7	0	7/10	Station
    Kenton	AM Peak	7	1	7/10	Station
    Kenton	AM Peak	7	2	7/10	Station
    Kenton	AM Peak	7	3	7/10	Station
    Kenton	AM Peak	7	4	7/10	Station
    Kenton	AM Peak	7	5	7/10	Station
    Kenton	AM Peak	7	6	7/10	Station
    Kenton	Inter Peak	6	0	6/10	Station
    Kenton	Inter Peak	6	1	6/10	Station
    Kenton	Inter Peak	6	2	6/10	Station
    Kenton	Inter Peak	6	3	6/10	Station
    Kenton	Inter Peak	6	4	6/10	Station
    Kenton	Inter Peak	6	5	6/10	Station
    Kenton	PM Peak	7	0	7/10	Station
    Kenton	PM Peak	7	1	7/10	Station
    Kenton	PM Peak	7	2	7/10	Station
    Kenton	PM Peak	7	3	7/10	Station
    Kenton	PM Peak	7	4	7/10	Station
    Kenton	PM Peak	7	5	7/10	Station
    Kenton	PM Peak	7	6	7/10	Station
    Kenton	Evening	3	0	3/10	Station
    Kenton	Evening	3	1	3/10	Station
    Kenton	Evening	3	2	3/10	Station
    Kenton	Late	1	0	1/10	Station
    Kew Gardens	Early	1	0	1/10	Station
    Kew Gardens	AM Peak	5	0	5/10	Station
    Kew Gardens	AM Peak	5	1	5/10	Station
    Kew Gardens	AM Peak	5	2	5/10	Station
    Kew Gardens	AM Peak	5	3	5/10	Station
    Kew Gardens	AM Peak	5	4	5/10	Station
    Kew Gardens	Inter Peak	5	0	5/10	Station
    Kew Gardens	Inter Peak	5	1	5/10	Station
    Kew Gardens	Inter Peak	5	2	5/10	Station
    Kew Gardens	Inter Peak	5	3	5/10	Station
    Kew Gardens	Inter Peak	5	4	5/10	Station
    Kew Gardens	PM Peak	6	0	6/10	Station
    Kew Gardens	PM Peak	6	1	6/10	Station
    Kew Gardens	PM Peak	6	2	6/10	Station
    Kew Gardens	PM Peak	6	3	6/10	Station
    Kew Gardens	PM Peak	6	4	6/10	Station
    Kew Gardens	PM Peak	6	5	6/10	Station
    Kew Gardens	Evening	3	0	3/10	Station
    Kew Gardens	Evening	3	1	3/10	Station
    Kew Gardens	Evening	3	2	3/10	Station
    Kew Gardens	Late	1	0	1/10	Station
    Kilburn	Early	1	0	1/10	Station
    Kilburn	AM Peak	6	0	6/10	Station
    Kilburn	AM Peak	6	1	6/10	Station
    Kilburn	AM Peak	6	2	6/10	Station
    Kilburn	AM Peak	6	3	6/10	Station
    Kilburn	AM Peak	6	4	6/10	Station
    Kilburn	AM Peak	6	5	6/10	Station
    Kilburn	Inter Peak	5	0	5/10	Station
    Kilburn	Inter Peak	5	1	5/10	Station
    Kilburn	Inter Peak	5	2	5/10	Station
    Kilburn	Inter Peak	5	3	5/10	Station
    Kilburn	Inter Peak	5	4	5/10	Station
    Kilburn	PM Peak	5	0	5/10	Station
    Kilburn	PM Peak	5	1	5/10	Station
    Kilburn	PM Peak	5	2	5/10	Station
    Kilburn	PM Peak	5	3	5/10	Station
    Kilburn	PM Peak	5	4	5/10	Station
    Kilburn	Evening	3	0	3/10	Station
    Kilburn	Evening	3	1	3/10	Station
    Kilburn	Evening	3	2	3/10	Station
    Kilburn	Late	2	0	2/10	Station
    Kilburn	Late	2	1	2/10	Station
    Kilburn Park	Early	1	0	1/10	Station
    Kilburn Park	AM Peak	5	0	5/10	Station
    Kilburn Park	AM Peak	5	1	5/10	Station
    Kilburn Park	AM Peak	5	2	5/10	Station
    Kilburn Park	AM Peak	5	3	5/10	Station
    Kilburn Park	AM Peak	5	4	5/10	Station
    Kilburn Park	Inter Peak	6	0	6/10	Station
    Kilburn Park	Inter Peak	6	1	6/10	Station
    Kilburn Park	Inter Peak	6	2	6/10	Station
    Kilburn Park	Inter Peak	6	3	6/10	Station
    Kilburn Park	Inter Peak	6	4	6/10	Station
    Kilburn Park	Inter Peak	6	5	6/10	Station
    Kilburn Park	PM Peak	5	0	5/10	Station
    Kilburn Park	PM Peak	5	1	5/10	Station
    Kilburn Park	PM Peak	5	2	5/10	Station
    Kilburn Park	PM Peak	5	3	5/10	Station
    Kilburn Park	PM Peak	5	4	5/10	Station
    Kilburn Park	Evening	3	0	3/10	Station
    Kilburn Park	Evening	3	1	3/10	Station
    Kilburn Park	Evening	3	2	3/10	Station
    Kilburn Park	Late	1	0	1/10	Station
    King's Cross St. Pancras	Early	1	0	1/10	Station
    King's Cross St. Pancras	AM Peak	7	0	7/10	Station
    King's Cross St. Pancras	AM Peak	7	1	7/10	Station
    King's Cross St. Pancras	AM Peak	7	2	7/10	Station
    King's Cross St. Pancras	AM Peak	7	3	7/10	Station
    King's Cross St. Pancras	AM Peak	7	4	7/10	Station
    King's Cross St. Pancras	AM Peak	7	5	7/10	Station
    King's Cross St. Pancras	AM Peak	7	6	7/10	Station
    King's Cross St. Pancras	Inter Peak	9	0	9/10	Station
    King's Cross St. Pancras	Inter Peak	9	1	9/10	Station
    King's Cross St. Pancras	Inter Peak	9	2	9/10	Station
    King's Cross St. Pancras	Inter Peak	9	3	9/10	Station
    King's Cross St. Pancras	Inter Peak	9	4	9/10	Station
    King's Cross St. Pancras	Inter Peak	9	5	9/10	Station
    King's Cross St. Pancras	Inter Peak	9	6	9/10	Station
    King's Cross St. Pancras	Inter Peak	9	7	9/10	Station
    King's Cross St. Pancras	Inter Peak	9	8	9/10	Station
    King's Cross St. Pancras	PM Peak	8	0	8/10	Station
    King's Cross St. Pancras	PM Peak	8	1	8/10	Station
    King's Cross St. Pancras	PM Peak	8	2	8/10	Station
    King's Cross St. Pancras	PM Peak	8	3	8/10	Station
    King's Cross St. Pancras	PM Peak	8	4	8/10	Station
    King's Cross St. Pancras	PM Peak	8	5	8/10	Station
    King's Cross St. Pancras	PM Peak	8	6	8/10	Station
    King's Cross St. Pancras	PM Peak	8	7	8/10	Station
    King's Cross St. Pancras	Evening	4	0	4/10	Station
    King's Cross St. Pancras	Evening	4	1	4/10	Station
    King's Cross St. Pancras	Evening	4	2	4/10	Station
    King's Cross St. Pancras	Evening	4	3	4/10	Station
    King's Cross St. Pancras	Late	2	0	2/10	Station
    King's Cross St. Pancras	Late	2	1	2/10	Station
    Kingsbury	Early	2	0	2/10	Station
    Kingsbury	Early	2	1	2/10	Station
    Kingsbury	AM Peak	5	0	5/10	Station
    Kingsbury	AM Peak	5	1	5/10	Station
    Kingsbury	AM Peak	5	2	5/10	Station
    Kingsbury	AM Peak	5	3	5/10	Station
    Kingsbury	AM Peak	5	4	5/10	Station
    Kingsbury	Inter Peak	4	0	4/10	Station
    Kingsbury	Inter Peak	4	1	4/10	Station
    Kingsbury	Inter Peak	4	2	4/10	Station
    Kingsbury	Inter Peak	4	3	4/10	Station
    Kingsbury	PM Peak	6	0	6/10	Station
    Kingsbury	PM Peak	6	1	6/10	Station
    Kingsbury	PM Peak	6	2	6/10	Station
    Kingsbury	PM Peak	6	3	6/10	Station
    Kingsbury	PM Peak	6	4	6/10	Station
    Kingsbury	PM Peak	6	5	6/10	Station
    Kingsbury	Evening	2	0	2/10	Station
    Kingsbury	Evening	2	1	2/10	Station
    Kingsbury	Late	1	0	1/10	Station
    Knightsbridge	AM Peak	3	0	3/10	Station
    Knightsbridge	AM Peak	3	1	3/10	Station
    Knightsbridge	AM Peak	3	2	3/10	Station
    Knightsbridge	Inter Peak	7	0	7/10	Station
    Knightsbridge	Inter Peak	7	1	7/10	Station
    Knightsbridge	Inter Peak	7	2	7/10	Station
    Knightsbridge	Inter Peak	7	3	7/10	Station
    Knightsbridge	Inter Peak	7	4	7/10	Station
    Knightsbridge	Inter Peak	7	5	7/10	Station
    Knightsbridge	Inter Peak	7	6	7/10	Station
    Knightsbridge	PM Peak	6	0	6/10	Station
    Knightsbridge	PM Peak	6	1	6/10	Station
    Knightsbridge	PM Peak	6	2	6/10	Station
    Knightsbridge	PM Peak	6	3	6/10	Station
    Knightsbridge	PM Peak	6	4	6/10	Station
    Knightsbridge	PM Peak	6	5	6/10	Station
    Knightsbridge	Evening	2	0	2/10	Station
    Knightsbridge	Evening	2	1	2/10	Station
    Knightsbridge	Late	1	0	1/10	Station
    Ladbroke Grove	AM Peak	6	0	6/10	Station
    Ladbroke Grove	AM Peak	6	1	6/10	Station
    Ladbroke Grove	AM Peak	6	2	6/10	Station
    Ladbroke Grove	AM Peak	6	3	6/10	Station
    Ladbroke Grove	AM Peak	6	4	6/10	Station
    Ladbroke Grove	AM Peak	6	5	6/10	Station
    Ladbroke Grove	Inter Peak	6	0	6/10	Station
    Ladbroke Grove	Inter Peak	6	1	6/10	Station
    Ladbroke Grove	Inter Peak	6	2	6/10	Station
    Ladbroke Grove	Inter Peak	6	3	6/10	Station
    Ladbroke Grove	Inter Peak	6	4	6/10	Station
    Ladbroke Grove	Inter Peak	6	5	6/10	Station
    Ladbroke Grove	PM Peak	6	0	6/10	Station
    Ladbroke Grove	PM Peak	6	1	6/10	Station
    Ladbroke Grove	PM Peak	6	2	6/10	Station
    Ladbroke Grove	PM Peak	6	3	6/10	Station
    Ladbroke Grove	PM Peak	6	4	6/10	Station
    Ladbroke Grove	PM Peak	6	5	6/10	Station
    Ladbroke Grove	Evening	2	0	2/10	Station
    Ladbroke Grove	Evening	2	1	2/10	Station
    Ladbroke Grove	Late	1	0	1/10	Station
    Lambeth North	AM Peak	3	0	3/10	Station
    Lambeth North	AM Peak	3	1	3/10	Station
    Lambeth North	AM Peak	3	2	3/10	Station
    Lambeth North	Inter Peak	5	0	5/10	Station
    Lambeth North	Inter Peak	5	1	5/10	Station
    Lambeth North	Inter Peak	5	2	5/10	Station
    Lambeth North	Inter Peak	5	3	5/10	Station
    Lambeth North	Inter Peak	5	4	5/10	Station
    Lambeth North	PM Peak	4	0	4/10	Station
    Lambeth North	PM Peak	4	1	4/10	Station
    Lambeth North	PM Peak	4	2	4/10	Station
    Lambeth North	PM Peak	4	3	4/10	Station
    Lambeth North	Evening	2	0	2/10	Station
    Lambeth North	Evening	2	1	2/10	Station
    Lambeth North	Late	1	0	1/10	Station
    Lancaster Gate	Early	1	0	1/10	Station
    Lancaster Gate	AM Peak	7	0	7/10	Station
    Lancaster Gate	AM Peak	7	1	7/10	Station
    Lancaster Gate	AM Peak	7	2	7/10	Station
    Lancaster Gate	AM Peak	7	3	7/10	Station
    Lancaster Gate	AM Peak	7	4	7/10	Station
    Lancaster Gate	AM Peak	7	5	7/10	Station
    Lancaster Gate	AM Peak	7	6	7/10	Station
    Lancaster Gate	Inter Peak	7	0	7/10	Station
    Lancaster Gate	Inter Peak	7	1	7/10	Station
    Lancaster Gate	Inter Peak	7	2	7/10	Station
    Lancaster Gate	Inter Peak	7	3	7/10	Station
    Lancaster Gate	Inter Peak	7	4	7/10	Station
    Lancaster Gate	Inter Peak	7	5	7/10	Station
    Lancaster Gate	Inter Peak	7	6	7/10	Station
    Lancaster Gate	PM Peak	7	0	7/10	Station
    Lancaster Gate	PM Peak	7	1	7/10	Station
    Lancaster Gate	PM Peak	7	2	7/10	Station
    Lancaster Gate	PM Peak	7	3	7/10	Station
    Lancaster Gate	PM Peak	7	4	7/10	Station
    Lancaster Gate	PM Peak	7	5	7/10	Station
    Lancaster Gate	PM Peak	7	6	7/10	Station
    Lancaster Gate	Evening	3	0	3/10	Station
    Lancaster Gate	Evening	3	1	3/10	Station
    Lancaster Gate	Evening	3	2	3/10	Station
    Lancaster Gate	Late	2	0	2/10	Station
    Lancaster Gate	Late	2	1	2/10	Station
    Latimer Road	AM Peak	6	0	6/10	Station
    Latimer Road	AM Peak	6	1	6/10	Station
    Latimer Road	AM Peak	6	2	6/10	Station
    Latimer Road	AM Peak	6	3	6/10	Station
    Latimer Road	AM Peak	6	4	6/10	Station
    Latimer Road	AM Peak	6	5	6/10	Station
    Latimer Road	Inter Peak	5	0	5/10	Station
    Latimer Road	Inter Peak	5	1	5/10	Station
    Latimer Road	Inter Peak	5	2	5/10	Station
    Latimer Road	Inter Peak	5	3	5/10	Station
    Latimer Road	Inter Peak	5	4	5/10	Station
    Latimer Road	PM Peak	6	0	6/10	Station
    Latimer Road	PM Peak	6	1	6/10	Station
    Latimer Road	PM Peak	6	2	6/10	Station
    Latimer Road	PM Peak	6	3	6/10	Station
    Latimer Road	PM Peak	6	4	6/10	Station
    Latimer Road	PM Peak	6	5	6/10	Station
    Latimer Road	Evening	3	0	3/10	Station
    Latimer Road	Evening	3	1	3/10	Station
    Latimer Road	Evening	3	2	3/10	Station
    Latimer Road	Late	1	0	1/10	Station
    Leicester Square	AM Peak	2	0	2/10	Station
    Leicester Square	AM Peak	2	1	2/10	Station
    Leicester Square	Inter Peak	6	0	6/10	Station
    Leicester Square	Inter Peak	6	1	6/10	Station
    Leicester Square	Inter Peak	6	2	6/10	Station
    Leicester Square	Inter Peak	6	3	6/10	Station
    Leicester Square	Inter Peak	6	4	6/10	Station
    Leicester Square	Inter Peak	6	5	6/10	Station
    Leicester Square	PM Peak	6	0	6/10	Station
    Leicester Square	PM Peak	6	1	6/10	Station
    Leicester Square	PM Peak	6	2	6/10	Station
    Leicester Square	PM Peak	6	3	6/10	Station
    Leicester Square	PM Peak	6	4	6/10	Station
    Leicester Square	PM Peak	6	5	6/10	Station
    Leicester Square	Evening	4	0	4/10	Station
    Leicester Square	Evening	4	1	4/10	Station
    Leicester Square	Evening	4	2	4/10	Station
    Leicester Square	Evening	4	3	4/10	Station
    Leicester Square	Late	4	0	4/10	Station
    Leicester Square	Late	4	1	4/10	Station
    Leicester Square	Late	4	2	4/10	Station
    Leicester Square	Late	4	3	4/10	Station
    Leyton	Early	2	0	2/10	Station
    Leyton	Early	2	1	2/10	Station
    Leyton	AM Peak	6	0	6/10	Station
    Leyton	AM Peak	6	1	6/10	Station
    Leyton	AM Peak	6	2	6/10	Station
    Leyton	AM Peak	6	3	6/10	Station
    Leyton	AM Peak	6	4	6/10	Station
    Leyton	AM Peak	6	5	6/10	Station
    Leyton	Inter Peak	6	0	6/10	Station
    Leyton	Inter Peak	6	1	6/10	Station
    Leyton	Inter Peak	6	2	6/10	Station
    Leyton	Inter Peak	6	3	6/10	Station
    Leyton	Inter Peak	6	4	6/10	Station
    Leyton	Inter Peak	6	5	6/10	Station
    Leyton	PM Peak	7	0	7/10	Station
    Leyton	PM Peak	7	1	7/10	Station
    Leyton	PM Peak	7	2	7/10	Station
    Leyton	PM Peak	7	3	7/10	Station
    Leyton	PM Peak	7	4	7/10	Station
    Leyton	PM Peak	7	5	7/10	Station
    Leyton	PM Peak	7	6	7/10	Station
    Leyton	Evening	4	0	4/10	Station
    Leyton	Evening	4	1	4/10	Station
    Leyton	Evening	4	2	4/10	Station
    Leyton	Evening	4	3	4/10	Station
    Leyton	Late	2	0	2/10	Station
    Leyton	Late	2	1	2/10	Station
    Leytonstone	Early	2	0	2/10	Station
    Leytonstone	Early	2	1	2/10	Station
    Leytonstone	AM Peak	7	0	7/10	Station
    Leytonstone	AM Peak	7	1	7/10	Station
    Leytonstone	AM Peak	7	2	7/10	Station
    Leytonstone	AM Peak	7	3	7/10	Station
    Leytonstone	AM Peak	7	4	7/10	Station
    Leytonstone	AM Peak	7	5	7/10	Station
    Leytonstone	AM Peak	7	6	7/10	Station
    Leytonstone	Inter Peak	6	0	6/10	Station
    Leytonstone	Inter Peak	6	1	6/10	Station
    Leytonstone	Inter Peak	6	2	6/10	Station
    Leytonstone	Inter Peak	6	3	6/10	Station
    Leytonstone	Inter Peak	6	4	6/10	Station
    Leytonstone	Inter Peak	6	5	6/10	Station
    Leytonstone	PM Peak	7	0	7/10	Station
    Leytonstone	PM Peak	7	1	7/10	Station
    Leytonstone	PM Peak	7	2	7/10	Station
    Leytonstone	PM Peak	7	3	7/10	Station
    Leytonstone	PM Peak	7	4	7/10	Station
    Leytonstone	PM Peak	7	5	7/10	Station
    Leytonstone	PM Peak	7	6	7/10	Station
    Leytonstone	Evening	4	0	4/10	Station
    Leytonstone	Evening	4	1	4/10	Station
    Leytonstone	Evening	4	2	4/10	Station
    Leytonstone	Evening	4	3	4/10	Station
    Leytonstone	Late	2	0	2/10	Station
    Leytonstone	Late	2	1	2/10	Station
    Liverpool Street	AM Peak	8	0	8/10	Station
    Liverpool Street	AM Peak	8	1	8/10	Station
    Liverpool Street	AM Peak	8	2	8/10	Station
    Liverpool Street	AM Peak	8	3	8/10	Station
    Liverpool Street	AM Peak	8	4	8/10	Station
    Liverpool Street	AM Peak	8	5	8/10	Station
    Liverpool Street	AM Peak	8	6	8/10	Station
    Liverpool Street	AM Peak	8	7	8/10	Station
    Liverpool Street	Inter Peak	7	0	7/10	Station
    Liverpool Street	Inter Peak	7	1	7/10	Station
    Liverpool Street	Inter Peak	7	2	7/10	Station
    Liverpool Street	Inter Peak	7	3	7/10	Station
    Liverpool Street	Inter Peak	7	4	7/10	Station
    Liverpool Street	Inter Peak	7	5	7/10	Station
    Liverpool Street	Inter Peak	7	6	7/10	Station
    Liverpool Street	PM Peak	9	0	9/10	Station
    Liverpool Street	PM Peak	9	1	9/10	Station
    Liverpool Street	PM Peak	9	2	9/10	Station
    Liverpool Street	PM Peak	9	3	9/10	Station
    Liverpool Street	PM Peak	9	4	9/10	Station
    Liverpool Street	PM Peak	9	5	9/10	Station
    Liverpool Street	PM Peak	9	6	9/10	Station
    Liverpool Street	PM Peak	9	7	9/10	Station
    Liverpool Street	PM Peak	9	8	9/10	Station
    Liverpool Street	Evening	3	0	3/10	Station
    Liverpool Street	Evening	3	1	3/10	Station
    Liverpool Street	Evening	3	2	3/10	Station
    Liverpool Street	Late	1	0	1/10	Station
    London Bridge	Early	1	0	1/10	Station
    London Bridge	AM Peak	9	0	9/10	Station
    London Bridge	AM Peak	9	1	9/10	Station
    London Bridge	AM Peak	9	2	9/10	Station
    London Bridge	AM Peak	9	3	9/10	Station
    London Bridge	AM Peak	9	4	9/10	Station
    London Bridge	AM Peak	9	5	9/10	Station
    London Bridge	AM Peak	9	6	9/10	Station
    London Bridge	AM Peak	9	7	9/10	Station
    London Bridge	AM Peak	9	8	9/10	Station
    London Bridge	Inter Peak	8	0	8/10	Station
    London Bridge	Inter Peak	8	1	8/10	Station
    London Bridge	Inter Peak	8	2	8/10	Station
    London Bridge	Inter Peak	8	3	8/10	Station
    London Bridge	Inter Peak	8	4	8/10	Station
    London Bridge	Inter Peak	8	5	8/10	Station
    London Bridge	Inter Peak	8	6	8/10	Station
    London Bridge	Inter Peak	8	7	8/10	Station
    London Bridge	PM Peak	9	0	9/10	Station
    London Bridge	PM Peak	9	1	9/10	Station
    London Bridge	PM Peak	9	2	9/10	Station
    London Bridge	PM Peak	9	3	9/10	Station
    London Bridge	PM Peak	9	4	9/10	Station
    London Bridge	PM Peak	9	5	9/10	Station
    London Bridge	PM Peak	9	6	9/10	Station
    London Bridge	PM Peak	9	7	9/10	Station
    London Bridge	PM Peak	9	8	9/10	Station
    London Bridge	Evening	4	0	4/10	Station
    London Bridge	Evening	4	1	4/10	Station
    London Bridge	Evening	4	2	4/10	Station
    London Bridge	Evening	4	3	4/10	Station
    London Bridge	Late	2	0	2/10	Station
    London Bridge	Late	2	1	2/10	Station
    Loughton	Early	1	0	1/10	Station
    Loughton	AM Peak	6	0	6/10	Station
    Loughton	AM Peak	6	1	6/10	Station
    Loughton	AM Peak	6	2	6/10	Station
    Loughton	AM Peak	6	3	6/10	Station
    Loughton	AM Peak	6	4	6/10	Station
    Loughton	AM Peak	6	5	6/10	Station
    Loughton	Inter Peak	4	0	4/10	Station
    Loughton	Inter Peak	4	1	4/10	Station
    Loughton	Inter Peak	4	2	4/10	Station
    Loughton	Inter Peak	4	3	4/10	Station
    Loughton	PM Peak	5	0	5/10	Station
    Loughton	PM Peak	5	1	5/10	Station
    Loughton	PM Peak	5	2	5/10	Station
    Loughton	PM Peak	5	3	5/10	Station
    Loughton	PM Peak	5	4	5/10	Station
    Loughton	Evening	2	0	2/10	Station
    Loughton	Evening	2	1	2/10	Station
    Loughton	Late	1	0	1/10	Station
    Maida Vale	AM Peak	6	0	6/10	Station
    Maida Vale	AM Peak	6	1	6/10	Station
    Maida Vale	AM Peak	6	2	6/10	Station
    Maida Vale	AM Peak	6	3	6/10	Station
    Maida Vale	AM Peak	6	4	6/10	Station
    Maida Vale	AM Peak	6	5	6/10	Station
    Maida Vale	Inter Peak	5	0	5/10	Station
    Maida Vale	Inter Peak	5	1	5/10	Station
    Maida Vale	Inter Peak	5	2	5/10	Station
    Maida Vale	Inter Peak	5	3	5/10	Station
    Maida Vale	Inter Peak	5	4	5/10	Station
    Maida Vale	PM Peak	5	0	5/10	Station
    Maida Vale	PM Peak	5	1	5/10	Station
    Maida Vale	PM Peak	5	2	5/10	Station
    Maida Vale	PM Peak	5	3	5/10	Station
    Maida Vale	PM Peak	5	4	5/10	Station
    Maida Vale	Evening	3	0	3/10	Station
    Maida Vale	Evening	3	1	3/10	Station
    Maida Vale	Evening	3	2	3/10	Station
    Maida Vale	Late	1	0	1/10	Station
    Manor House	Early	1	0	1/10	Station
    Manor House	AM Peak	7	0	7/10	Station
    Manor House	AM Peak	7	1	7/10	Station
    Manor House	AM Peak	7	2	7/10	Station
    Manor House	AM Peak	7	3	7/10	Station
    Manor House	AM Peak	7	4	7/10	Station
    Manor House	AM Peak	7	5	7/10	Station
    Manor House	AM Peak	7	6	7/10	Station
    Manor House	Inter Peak	6	0	6/10	Station
    Manor House	Inter Peak	6	1	6/10	Station
    Manor House	Inter Peak	6	2	6/10	Station
    Manor House	Inter Peak	6	3	6/10	Station
    Manor House	Inter Peak	6	4	6/10	Station
    Manor House	Inter Peak	6	5	6/10	Station
    Manor House	PM Peak	7	0	7/10	Station
    Manor House	PM Peak	7	1	7/10	Station
    Manor House	PM Peak	7	2	7/10	Station
    Manor House	PM Peak	7	3	7/10	Station
    Manor House	PM Peak	7	4	7/10	Station
    Manor House	PM Peak	7	5	7/10	Station
    Manor House	PM Peak	7	6	7/10	Station
    Manor House	Evening	4	0	4/10	Station
    Manor House	Evening	4	1	4/10	Station
    Manor House	Evening	4	2	4/10	Station
    Manor House	Evening	4	3	4/10	Station
    Manor House	Late	3	0	3/10	Station
    Manor House	Late	3	1	3/10	Station
    Manor House	Late	3	2	3/10	Station
    Mansion House	AM Peak	6	0	6/10	Station
    Mansion House	AM Peak	6	1	6/10	Station
    Mansion House	AM Peak	6	2	6/10	Station
    Mansion House	AM Peak	6	3	6/10	Station
    Mansion House	AM Peak	6	4	6/10	Station
    Mansion House	AM Peak	6	5	6/10	Station
    Mansion House	Inter Peak	4	0	4/10	Station
    Mansion House	Inter Peak	4	1	4/10	Station
    Mansion House	Inter Peak	4	2	4/10	Station
    Mansion House	Inter Peak	4	3	4/10	Station
    Mansion House	PM Peak	6	0	6/10	Station
    Mansion House	PM Peak	6	1	6/10	Station
    Mansion House	PM Peak	6	2	6/10	Station
    Mansion House	PM Peak	6	3	6/10	Station
    Mansion House	PM Peak	6	4	6/10	Station
    Mansion House	PM Peak	6	5	6/10	Station
    Mansion House	Evening	2	0	2/10	Station
    Mansion House	Evening	2	1	2/10	Station
    Marble Arch	AM Peak	5	0	5/10	Station
    Marble Arch	AM Peak	5	1	5/10	Station
    Marble Arch	AM Peak	5	2	5/10	Station
    Marble Arch	AM Peak	5	3	5/10	Station
    Marble Arch	AM Peak	5	4	5/10	Station
    Marble Arch	Inter Peak	7	0	7/10	Station
    Marble Arch	Inter Peak	7	1	7/10	Station
    Marble Arch	Inter Peak	7	2	7/10	Station
    Marble Arch	Inter Peak	7	3	7/10	Station
    Marble Arch	Inter Peak	7	4	7/10	Station
    Marble Arch	Inter Peak	7	5	7/10	Station
    Marble Arch	Inter Peak	7	6	7/10	Station
    Marble Arch	PM Peak	7	0	7/10	Station
    Marble Arch	PM Peak	7	1	7/10	Station
    Marble Arch	PM Peak	7	2	7/10	Station
    Marble Arch	PM Peak	7	3	7/10	Station
    Marble Arch	PM Peak	7	4	7/10	Station
    Marble Arch	PM Peak	7	5	7/10	Station
    Marble Arch	PM Peak	7	6	7/10	Station
    Marble Arch	Evening	4	0	4/10	Station
    Marble Arch	Evening	4	1	4/10	Station
    Marble Arch	Evening	4	2	4/10	Station
    Marble Arch	Evening	4	3	4/10	Station
    Marble Arch	Late	2	0	2/10	Station
    Marble Arch	Late	2	1	2/10	Station
    Marylebone	Early	1	0	1/10	Station
    Marylebone	AM Peak	8	0	8/10	Station
    Marylebone	AM Peak	8	1	8/10	Station
    Marylebone	AM Peak	8	2	8/10	Station
    Marylebone	AM Peak	8	3	8/10	Station
    Marylebone	AM Peak	8	4	8/10	Station
    Marylebone	AM Peak	8	5	8/10	Station
    Marylebone	AM Peak	8	6	8/10	Station
    Marylebone	AM Peak	8	7	8/10	Station
    Marylebone	Inter Peak	7	0	7/10	Station
    Marylebone	Inter Peak	7	1	7/10	Station
    Marylebone	Inter Peak	7	2	7/10	Station
    Marylebone	Inter Peak	7	3	7/10	Station
    Marylebone	Inter Peak	7	4	7/10	Station
    Marylebone	Inter Peak	7	5	7/10	Station
    Marylebone	Inter Peak	7	6	7/10	Station
    Marylebone	PM Peak	8	0	8/10	Station
    Marylebone	PM Peak	8	1	8/10	Station
    Marylebone	PM Peak	8	2	8/10	Station
    Marylebone	PM Peak	8	3	8/10	Station
    Marylebone	PM Peak	8	4	8/10	Station
    Marylebone	PM Peak	8	5	8/10	Station
    Marylebone	PM Peak	8	6	8/10	Station
    Marylebone	PM Peak	8	7	8/10	Station
    Marylebone	Evening	3	0	3/10	Station
    Marylebone	Evening	3	1	3/10	Station
    Marylebone	Evening	3	2	3/10	Station
    Marylebone	Late	1	0	1/10	Station
    Mile End	Early	1	0	1/10	Station
    Mile End	AM Peak	7	0	7/10	Station
    Mile End	AM Peak	7	1	7/10	Station
    Mile End	AM Peak	7	2	7/10	Station
    Mile End	AM Peak	7	3	7/10	Station
    Mile End	AM Peak	7	4	7/10	Station
    Mile End	AM Peak	7	5	7/10	Station
    Mile End	AM Peak	7	6	7/10	Station
    Mile End	Inter Peak	8	0	8/10	Station
    Mile End	Inter Peak	8	1	8/10	Station
    Mile End	Inter Peak	8	2	8/10	Station
    Mile End	Inter Peak	8	3	8/10	Station
    Mile End	Inter Peak	8	4	8/10	Station
    Mile End	Inter Peak	8	5	8/10	Station
    Mile End	Inter Peak	8	6	8/10	Station
    Mile End	Inter Peak	8	7	8/10	Station
    Mile End	PM Peak	7	0	7/10	Station
    Mile End	PM Peak	7	1	7/10	Station
    Mile End	PM Peak	7	2	7/10	Station
    Mile End	PM Peak	7	3	7/10	Station
    Mile End	PM Peak	7	4	7/10	Station
    Mile End	PM Peak	7	5	7/10	Station
    Mile End	PM Peak	7	6	7/10	Station
    Mile End	Evening	4	0	4/10	Station
    Mile End	Evening	4	1	4/10	Station
    Mile End	Evening	4	2	4/10	Station
    Mile End	Evening	4	3	4/10	Station
    Mile End	Late	2	0	2/10	Station
    Mile End	Late	2	1	2/10	Station
    Mill Hill East	Early	1	0	1/10	Station
    Mill Hill East	AM Peak	5	0	5/10	Station
    Mill Hill East	AM Peak	5	1	5/10	Station
    Mill Hill East	AM Peak	5	2	5/10	Station
    Mill Hill East	AM Peak	5	3	5/10	Station
    Mill Hill East	AM Peak	5	4	5/10	Station
    Mill Hill East	Inter Peak	3	0	3/10	Station
    Mill Hill East	Inter Peak	3	1	3/10	Station
    Mill Hill East	Inter Peak	3	2	3/10	Station
    Mill Hill East	PM Peak	4	0	4/10	Station
    Mill Hill East	PM Peak	4	1	4/10	Station
    Mill Hill East	PM Peak	4	2	4/10	Station
    Mill Hill East	PM Peak	4	3	4/10	Station
    Mill Hill East	Evening	1	0	1/10	Station
    Mill Hill East	Late	1	0	1/10	Station
    Moor Park	Early	1	0	1/10	Station
    Moor Park	AM Peak	6	0	6/10	Station
    Moor Park	AM Peak	6	1	6/10	Station
    Moor Park	AM Peak	6	2	6/10	Station
    Moor Park	AM Peak	6	3	6/10	Station
    Moor Park	AM Peak	6	4	6/10	Station
    Moor Park	AM Peak	6	5	6/10	Station
    Moor Park	Inter Peak	3	0	3/10	Station
    Moor Park	Inter Peak	3	1	3/10	Station
    Moor Park	Inter Peak	3	2	3/10	Station
    Moor Park	PM Peak	4	0	4/10	Station
    Moor Park	PM Peak	4	1	4/10	Station
    Moor Park	PM Peak	4	2	4/10	Station
    Moor Park	PM Peak	4	3	4/10	Station
    Moor Park	Evening	1	0	1/10	Station
    Moor Park	Late	1	0	1/10	Station
    Moorgate	Early	1	0	1/10	Station
    Moorgate	AM Peak	9	0	9/10	Station
    Moorgate	AM Peak	9	1	9/10	Station
    Moorgate	AM Peak	9	2	9/10	Station
    Moorgate	AM Peak	9	3	9/10	Station
    Moorgate	AM Peak	9	4	9/10	Station
    Moorgate	AM Peak	9	5	9/10	Station
    Moorgate	AM Peak	9	6	9/10	Station
    Moorgate	AM Peak	9	7	9/10	Station
    Moorgate	AM Peak	9	8	9/10	Station
    Moorgate	Inter Peak	5	0	5/10	Station
    Moorgate	Inter Peak	5	1	5/10	Station
    Moorgate	Inter Peak	5	2	5/10	Station
    Moorgate	Inter Peak	5	3	5/10	Station
    Moorgate	Inter Peak	5	4	5/10	Station
    Moorgate	PM Peak	8	0	8/10	Station
    Moorgate	PM Peak	8	1	8/10	Station
    Moorgate	PM Peak	8	2	8/10	Station
    Moorgate	PM Peak	8	3	8/10	Station
    Moorgate	PM Peak	8	4	8/10	Station
    Moorgate	PM Peak	8	5	8/10	Station
    Moorgate	PM Peak	8	6	8/10	Station
    Moorgate	PM Peak	8	7	8/10	Station
    Moorgate	Evening	2	0	2/10	Station
    Moorgate	Evening	2	1	2/10	Station
    Moorgate	Late	1	0	1/10	Station
    Morden	Early	1	0	1/10	Station
    Morden	AM Peak	5	0	5/10	Station
    Morden	AM Peak	5	1	5/10	Station
    Morden	AM Peak	5	2	5/10	Station
    Morden	AM Peak	5	3	5/10	Station
    Morden	AM Peak	5	4	5/10	Station
    Morden	Inter Peak	3	0	3/10	Station
    Morden	Inter Peak	3	1	3/10	Station
    Morden	Inter Peak	3	2	3/10	Station
    Morden	PM Peak	4	0	4/10	Station
    Morden	PM Peak	4	1	4/10	Station
    Morden	PM Peak	4	2	4/10	Station
    Morden	PM Peak	4	3	4/10	Station
    Morden	Evening	2	0	2/10	Station
    Morden	Evening	2	1	2/10	Station
    Morden	Late	1	0	1/10	Station
    Mornington Crescent	AM Peak	6	0	6/10	Station
    Mornington Crescent	AM Peak	6	1	6/10	Station
    Mornington Crescent	AM Peak	6	2	6/10	Station
    Mornington Crescent	AM Peak	6	3	6/10	Station
    Mornington Crescent	AM Peak	6	4	6/10	Station
    Mornington Crescent	AM Peak	6	5	6/10	Station
    Mornington Crescent	Inter Peak	4	0	4/10	Station
    Mornington Crescent	Inter Peak	4	1	4/10	Station
    Mornington Crescent	Inter Peak	4	2	4/10	Station
    Mornington Crescent	Inter Peak	4	3	4/10	Station
    Mornington Crescent	PM Peak	6	0	6/10	Station
    Mornington Crescent	PM Peak	6	1	6/10	Station
    Mornington Crescent	PM Peak	6	2	6/10	Station
    Mornington Crescent	PM Peak	6	3	6/10	Station
    Mornington Crescent	PM Peak	6	4	6/10	Station
    Mornington Crescent	PM Peak	6	5	6/10	Station
    Mornington Crescent	Evening	2	0	2/10	Station
    Mornington Crescent	Evening	2	1	2/10	Station
    Mornington Crescent	Late	2	0	2/10	Station
    Mornington Crescent	Late	2	1	2/10	Station
    Neasden	Early	2	0	2/10	Station
    Neasden	Early	2	1	2/10	Station
    Neasden	AM Peak	6	0	6/10	Station
    Neasden	AM Peak	6	1	6/10	Station
    Neasden	AM Peak	6	2	6/10	Station
    Neasden	AM Peak	6	3	6/10	Station
    Neasden	AM Peak	6	4	6/10	Station
    Neasden	AM Peak	6	5	6/10	Station
    Neasden	Inter Peak	4	0	4/10	Station
    Neasden	Inter Peak	4	1	4/10	Station
    Neasden	Inter Peak	4	2	4/10	Station
    Neasden	Inter Peak	4	3	4/10	Station
    Neasden	PM Peak	6	0	6/10	Station
    Neasden	PM Peak	6	1	6/10	Station
    Neasden	PM Peak	6	2	6/10	Station
    Neasden	PM Peak	6	3	6/10	Station
    Neasden	PM Peak	6	4	6/10	Station
    Neasden	PM Peak	6	5	6/10	Station
    Neasden	Evening	2	0	2/10	Station
    Neasden	Evening	2	1	2/10	Station
    Neasden	Late	1	0	1/10	Station
    Newbury Park	Early	2	0	2/10	Station
    Newbury Park	Early	2	1	2/10	Station
    Newbury Park	AM Peak	6	0	6/10	Station
    Newbury Park	AM Peak	6	1	6/10	Station
    Newbury Park	AM Peak	6	2	6/10	Station
    Newbury Park	AM Peak	6	3	6/10	Station
    Newbury Park	AM Peak	6	4	6/10	Station
    Newbury Park	AM Peak	6	5	6/10	Station
    Newbury Park	Inter Peak	4	0	4/10	Station
    Newbury Park	Inter Peak	4	1	4/10	Station
    Newbury Park	Inter Peak	4	2	4/10	Station
    Newbury Park	Inter Peak	4	3	4/10	Station
    Newbury Park	PM Peak	5	0	5/10	Station
    Newbury Park	PM Peak	5	1	5/10	Station
    Newbury Park	PM Peak	5	2	5/10	Station
    Newbury Park	PM Peak	5	3	5/10	Station
    Newbury Park	PM Peak	5	4	5/10	Station
    Newbury Park	Evening	2	0	2/10	Station
    Newbury Park	Evening	2	1	2/10	Station
    Newbury Park	Late	1	0	1/10	Station
    North Acton	Early	1	0	1/10	Station
    North Acton	AM Peak	6	0	6/10	Station
    North Acton	AM Peak	6	1	6/10	Station
    North Acton	AM Peak	6	2	6/10	Station
    North Acton	AM Peak	6	3	6/10	Station
    North Acton	AM Peak	6	4	6/10	Station
    North Acton	AM Peak	6	5	6/10	Station
    North Acton	Inter Peak	4	0	4/10	Station
    North Acton	Inter Peak	4	1	4/10	Station
    North Acton	Inter Peak	4	2	4/10	Station
    North Acton	Inter Peak	4	3	4/10	Station
    North Acton	PM Peak	6	0	6/10	Station
    North Acton	PM Peak	6	1	6/10	Station
    North Acton	PM Peak	6	2	6/10	Station
    North Acton	PM Peak	6	3	6/10	Station
    North Acton	PM Peak	6	4	6/10	Station
    North Acton	PM Peak	6	5	6/10	Station
    North Acton	Evening	2	0	2/10	Station
    North Acton	Evening	2	1	2/10	Station
    North Acton	Late	1	0	1/10	Station
    North Ealing	Early	1	0	1/10	Station
    North Ealing	AM Peak	6	0	6/10	Station
    North Ealing	AM Peak	6	1	6/10	Station
    North Ealing	AM Peak	6	2	6/10	Station
    North Ealing	AM Peak	6	3	6/10	Station
    North Ealing	AM Peak	6	4	6/10	Station
    North Ealing	AM Peak	6	5	6/10	Station
    North Ealing	Inter Peak	5	0	5/10	Station
    North Ealing	Inter Peak	5	1	5/10	Station
    North Ealing	Inter Peak	5	2	5/10	Station
    North Ealing	Inter Peak	5	3	5/10	Station
    North Ealing	Inter Peak	5	4	5/10	Station
    North Ealing	PM Peak	4	0	4/10	Station
    North Ealing	PM Peak	4	1	4/10	Station
    North Ealing	PM Peak	4	2	4/10	Station
    North Ealing	PM Peak	4	3	4/10	Station
    North Ealing	Evening	2	0	2/10	Station
    North Ealing	Evening	2	1	2/10	Station
    North Ealing	Late	1	0	1/10	Station
    North Greenwich	Early	1	0	1/10	Station
    North Greenwich	AM Peak	7	0	7/10	Station
    North Greenwich	AM Peak	7	1	7/10	Station
    North Greenwich	AM Peak	7	2	7/10	Station
    North Greenwich	AM Peak	7	3	7/10	Station
    North Greenwich	AM Peak	7	4	7/10	Station
    North Greenwich	AM Peak	7	5	7/10	Station
    North Greenwich	AM Peak	7	6	7/10	Station
    North Greenwich	Inter Peak	6	0	6/10	Station
    North Greenwich	Inter Peak	6	1	6/10	Station
    North Greenwich	Inter Peak	6	2	6/10	Station
    North Greenwich	Inter Peak	6	3	6/10	Station
    North Greenwich	Inter Peak	6	4	6/10	Station
    North Greenwich	Inter Peak	6	5	6/10	Station
    North Greenwich	PM Peak	8	0	8/10	Station
    North Greenwich	PM Peak	8	1	8/10	Station
    North Greenwich	PM Peak	8	2	8/10	Station
    North Greenwich	PM Peak	8	3	8/10	Station
    North Greenwich	PM Peak	8	4	8/10	Station
    North Greenwich	PM Peak	8	5	8/10	Station
    North Greenwich	PM Peak	8	6	8/10	Station
    North Greenwich	PM Peak	8	7	8/10	Station
    North Greenwich	Evening	4	0	4/10	Station
    North Greenwich	Evening	4	1	4/10	Station
    North Greenwich	Evening	4	2	4/10	Station
    North Greenwich	Evening	4	3	4/10	Station
    North Greenwich	Late	3	0	3/10	Station
    North Greenwich	Late	3	1	3/10	Station
    North Greenwich	Late	3	2	3/10	Station
    North Harrow	Early	2	0	2/10	Station
    North Harrow	Early	2	1	2/10	Station
    North Harrow	AM Peak	8	0	8/10	Station
    North Harrow	AM Peak	8	1	8/10	Station
    North Harrow	AM Peak	8	2	8/10	Station
    North Harrow	AM Peak	8	3	8/10	Station
    North Harrow	AM Peak	8	4	8/10	Station
    North Harrow	AM Peak	8	5	8/10	Station
    North Harrow	AM Peak	8	6	8/10	Station
    North Harrow	AM Peak	8	7	8/10	Station
    North Harrow	Inter Peak	5	0	5/10	Station
    North Harrow	Inter Peak	5	1	5/10	Station
    North Harrow	Inter Peak	5	2	5/10	Station
    North Harrow	Inter Peak	5	3	5/10	Station
    North Harrow	Inter Peak	5	4	5/10	Station
    North Harrow	PM Peak	7	0	7/10	Station
    North Harrow	PM Peak	7	1	7/10	Station
    North Harrow	PM Peak	7	2	7/10	Station
    North Harrow	PM Peak	7	3	7/10	Station
    North Harrow	PM Peak	7	4	7/10	Station
    North Harrow	PM Peak	7	5	7/10	Station
    North Harrow	PM Peak	7	6	7/10	Station
    North Harrow	Evening	3	0	3/10	Station
    North Harrow	Evening	3	1	3/10	Station
    North Harrow	Evening	3	2	3/10	Station
    North Harrow	Late	1	0	1/10	Station
    North Wembley	Early	3	0	3/10	Station
    North Wembley	Early	3	1	3/10	Station
    North Wembley	Early	3	2	3/10	Station
    North Wembley	AM Peak	9	0	9/10	Station
    North Wembley	AM Peak	9	1	9/10	Station
    North Wembley	AM Peak	9	2	9/10	Station
    North Wembley	AM Peak	9	3	9/10	Station
    North Wembley	AM Peak	9	4	9/10	Station
    North Wembley	AM Peak	9	5	9/10	Station
    North Wembley	AM Peak	9	6	9/10	Station
    North Wembley	AM Peak	9	7	9/10	Station
    North Wembley	AM Peak	9	8	9/10	Station
    North Wembley	Inter Peak	7	0	7/10	Station
    North Wembley	Inter Peak	7	1	7/10	Station
    North Wembley	Inter Peak	7	2	7/10	Station
    North Wembley	Inter Peak	7	3	7/10	Station
    North Wembley	Inter Peak	7	4	7/10	Station
    North Wembley	Inter Peak	7	5	7/10	Station
    North Wembley	Inter Peak	7	6	7/10	Station
    North Wembley	PM Peak	9	0	9/10	Station
    North Wembley	PM Peak	9	1	9/10	Station
    North Wembley	PM Peak	9	2	9/10	Station
    North Wembley	PM Peak	9	3	9/10	Station
    North Wembley	PM Peak	9	4	9/10	Station
    North Wembley	PM Peak	9	5	9/10	Station
    North Wembley	PM Peak	9	6	9/10	Station
    North Wembley	PM Peak	9	7	9/10	Station
    North Wembley	PM Peak	9	8	9/10	Station
    North Wembley	Evening	4	0	4/10	Station
    North Wembley	Evening	4	1	4/10	Station
    North Wembley	Evening	4	2	4/10	Station
    North Wembley	Evening	4	3	4/10	Station
    North Wembley	Late	1	0	1/10	Station
    Northfields	Early	1	0	1/10	Station
    Northfields	AM Peak	7	0	7/10	Station
    Northfields	AM Peak	7	1	7/10	Station
    Northfields	AM Peak	7	2	7/10	Station
    Northfields	AM Peak	7	3	7/10	Station
    Northfields	AM Peak	7	4	7/10	Station
    Northfields	AM Peak	7	5	7/10	Station
    Northfields	AM Peak	7	6	7/10	Station
    Northfields	Inter Peak	5	0	5/10	Station
    Northfields	Inter Peak	5	1	5/10	Station
    Northfields	Inter Peak	5	2	5/10	Station
    Northfields	Inter Peak	5	3	5/10	Station
    Northfields	Inter Peak	5	4	5/10	Station
    Northfields	PM Peak	6	0	6/10	Station
    Northfields	PM Peak	6	1	6/10	Station
    Northfields	PM Peak	6	2	6/10	Station
    Northfields	PM Peak	6	3	6/10	Station
    Northfields	PM Peak	6	4	6/10	Station
    Northfields	PM Peak	6	5	6/10	Station
    Northfields	Evening	3	0	3/10	Station
    Northfields	Evening	3	1	3/10	Station
    Northfields	Evening	3	2	3/10	Station
    Northfields	Late	2	0	2/10	Station
    Northfields	Late	2	1	2/10	Station
    Northolt	Early	2	0	2/10	Station
    Northolt	Early	2	1	2/10	Station
    Northolt	AM Peak	5	0	5/10	Station
    Northolt	AM Peak	5	1	5/10	Station
    Northolt	AM Peak	5	2	5/10	Station
    Northolt	AM Peak	5	3	5/10	Station
    Northolt	AM Peak	5	4	5/10	Station
    Northolt	Inter Peak	4	0	4/10	Station
    Northolt	Inter Peak	4	1	4/10	Station
    Northolt	Inter Peak	4	2	4/10	Station
    Northolt	Inter Peak	4	3	4/10	Station
    Northolt	PM Peak	6	0	6/10	Station
    Northolt	PM Peak	6	1	6/10	Station
    Northolt	PM Peak	6	2	6/10	Station
    Northolt	PM Peak	6	3	6/10	Station
    Northolt	PM Peak	6	4	6/10	Station
    Northolt	PM Peak	6	5	6/10	Station
    Northolt	Evening	3	0	3/10	Station
    Northolt	Evening	3	1	3/10	Station
    Northolt	Evening	3	2	3/10	Station
    Northolt	Late	1	0	1/10	Station
    Northwick Park	Early	2	0	2/10	Station
    Northwick Park	Early	2	1	2/10	Station
    Northwick Park	AM Peak	9	0	9/10	Station
    Northwick Park	AM Peak	9	1	9/10	Station
    Northwick Park	AM Peak	9	2	9/10	Station
    Northwick Park	AM Peak	9	3	9/10	Station
    Northwick Park	AM Peak	9	4	9/10	Station
    Northwick Park	AM Peak	9	5	9/10	Station
    Northwick Park	AM Peak	9	6	9/10	Station
    Northwick Park	AM Peak	9	7	9/10	Station
    Northwick Park	AM Peak	9	8	9/10	Station
    Northwick Park	Inter Peak	8	0	8/10	Station
    Northwick Park	Inter Peak	8	1	8/10	Station
    Northwick Park	Inter Peak	8	2	8/10	Station
    Northwick Park	Inter Peak	8	3	8/10	Station
    Northwick Park	Inter Peak	8	4	8/10	Station
    Northwick Park	Inter Peak	8	5	8/10	Station
    Northwick Park	Inter Peak	8	6	8/10	Station
    Northwick Park	Inter Peak	8	7	8/10	Station
    Northwick Park	PM Peak	9	0	9/10	Station
    Northwick Park	PM Peak	9	1	9/10	Station
    Northwick Park	PM Peak	9	2	9/10	Station
    Northwick Park	PM Peak	9	3	9/10	Station
    Northwick Park	PM Peak	9	4	9/10	Station
    Northwick Park	PM Peak	9	5	9/10	Station
    Northwick Park	PM Peak	9	6	9/10	Station
    Northwick Park	PM Peak	9	7	9/10	Station
    Northwick Park	PM Peak	9	8	9/10	Station
    Northwick Park	Evening	4	0	4/10	Station
    Northwick Park	Evening	4	1	4/10	Station
    Northwick Park	Evening	4	2	4/10	Station
    Northwick Park	Evening	4	3	4/10	Station
    Northwick Park	Late	1	0	1/10	Station
    Northwood	Early	1	0	1/10	Station
    Northwood	AM Peak	6	0	6/10	Station
    Northwood	AM Peak	6	1	6/10	Station
    Northwood	AM Peak	6	2	6/10	Station
    Northwood	AM Peak	6	3	6/10	Station
    Northwood	AM Peak	6	4	6/10	Station
    Northwood	AM Peak	6	5	6/10	Station
    Northwood	Inter Peak	3	0	3/10	Station
    Northwood	Inter Peak	3	1	3/10	Station
    Northwood	Inter Peak	3	2	3/10	Station
    Northwood	PM Peak	4	0	4/10	Station
    Northwood	PM Peak	4	1	4/10	Station
    Northwood	PM Peak	4	2	4/10	Station
    Northwood	PM Peak	4	3	4/10	Station
    Northwood	Evening	2	0	2/10	Station
    Northwood	Evening	2	1	2/10	Station
    Northwood	Late	1	0	1/10	Station
    Northwood Hills	Early	1	0	1/10	Station
    Northwood Hills	AM Peak	7	0	7/10	Station
    Northwood Hills	AM Peak	7	1	7/10	Station
    Northwood Hills	AM Peak	7	2	7/10	Station
    Northwood Hills	AM Peak	7	3	7/10	Station
    Northwood Hills	AM Peak	7	4	7/10	Station
    Northwood Hills	AM Peak	7	5	7/10	Station
    Northwood Hills	AM Peak	7	6	7/10	Station
    Northwood Hills	Inter Peak	5	0	5/10	Station
    Northwood Hills	Inter Peak	5	1	5/10	Station
    Northwood Hills	Inter Peak	5	2	5/10	Station
    Northwood Hills	Inter Peak	5	3	5/10	Station
    Northwood Hills	Inter Peak	5	4	5/10	Station
    Northwood Hills	PM Peak	6	0	6/10	Station
    Northwood Hills	PM Peak	6	1	6/10	Station
    Northwood Hills	PM Peak	6	2	6/10	Station
    Northwood Hills	PM Peak	6	3	6/10	Station
    Northwood Hills	PM Peak	6	4	6/10	Station
    Northwood Hills	PM Peak	6	5	6/10	Station
    Northwood Hills	Evening	3	0	3/10	Station
    Northwood Hills	Evening	3	1	3/10	Station
    Northwood Hills	Evening	3	2	3/10	Station
    Northwood Hills	Late	1	0	1/10	Station
    Notting Hill Gate	AM Peak	5	0	5/10	Station
    Notting Hill Gate	AM Peak	5	1	5/10	Station
    Notting Hill Gate	AM Peak	5	2	5/10	Station
    Notting Hill Gate	AM Peak	5	3	5/10	Station
    Notting Hill Gate	AM Peak	5	4	5/10	Station
    Notting Hill Gate	Inter Peak	6	0	6/10	Station
    Notting Hill Gate	Inter Peak	6	1	6/10	Station
    Notting Hill Gate	Inter Peak	6	2	6/10	Station
    Notting Hill Gate	Inter Peak	6	3	6/10	Station
    Notting Hill Gate	Inter Peak	6	4	6/10	Station
    Notting Hill Gate	Inter Peak	6	5	6/10	Station
    Notting Hill Gate	PM Peak	6	0	6/10	Station
    Notting Hill Gate	PM Peak	6	1	6/10	Station
    Notting Hill Gate	PM Peak	6	2	6/10	Station
    Notting Hill Gate	PM Peak	6	3	6/10	Station
    Notting Hill Gate	PM Peak	6	4	6/10	Station
    Notting Hill Gate	PM Peak	6	5	6/10	Station
    Notting Hill Gate	Evening	3	0	3/10	Station
    Notting Hill Gate	Evening	3	1	3/10	Station
    Notting Hill Gate	Evening	3	2	3/10	Station
    Notting Hill Gate	Late	1	0	1/10	Station
    Oakwood	Early	1	0	1/10	Station
    Oakwood	AM Peak	5	0	5/10	Station
    Oakwood	AM Peak	5	1	5/10	Station
    Oakwood	AM Peak	5	2	5/10	Station
    Oakwood	AM Peak	5	3	5/10	Station
    Oakwood	AM Peak	5	4	5/10	Station
    Oakwood	Inter Peak	5	0	5/10	Station
    Oakwood	Inter Peak	5	1	5/10	Station
    Oakwood	Inter Peak	5	2	5/10	Station
    Oakwood	Inter Peak	5	3	5/10	Station
    Oakwood	Inter Peak	5	4	5/10	Station
    Oakwood	PM Peak	4	0	4/10	Station
    Oakwood	PM Peak	4	1	4/10	Station
    Oakwood	PM Peak	4	2	4/10	Station
    Oakwood	PM Peak	4	3	4/10	Station
    Oakwood	Evening	2	0	2/10	Station
    Oakwood	Evening	2	1	2/10	Station
    Oakwood	Late	1	0	1/10	Station
    Old Street	AM Peak	8	0	8/10	Station
    Old Street	AM Peak	8	1	8/10	Station
    Old Street	AM Peak	8	2	8/10	Station
    Old Street	AM Peak	8	3	8/10	Station
    Old Street	AM Peak	8	4	8/10	Station
    Old Street	AM Peak	8	5	8/10	Station
    Old Street	AM Peak	8	6	8/10	Station
    Old Street	AM Peak	8	7	8/10	Station
    Old Street	Inter Peak	8	0	8/10	Station
    Old Street	Inter Peak	8	1	8/10	Station
    Old Street	Inter Peak	8	2	8/10	Station
    Old Street	Inter Peak	8	3	8/10	Station
    Old Street	Inter Peak	8	4	8/10	Station
    Old Street	Inter Peak	8	5	8/10	Station
    Old Street	Inter Peak	8	6	8/10	Station
    Old Street	Inter Peak	8	7	8/10	Station
    Old Street	PM Peak	9	0	9/10	Station
    Old Street	PM Peak	9	1	9/10	Station
    Old Street	PM Peak	9	2	9/10	Station
    Old Street	PM Peak	9	3	9/10	Station
    Old Street	PM Peak	9	4	9/10	Station
    Old Street	PM Peak	9	5	9/10	Station
    Old Street	PM Peak	9	6	9/10	Station
    Old Street	PM Peak	9	7	9/10	Station
    Old Street	PM Peak	9	8	9/10	Station
    Old Street	Evening	4	0	4/10	Station
    Old Street	Evening	4	1	4/10	Station
    Old Street	Evening	4	2	4/10	Station
    Old Street	Evening	4	3	4/10	Station
    Old Street	Late	2	0	2/10	Station
    Old Street	Late	2	1	2/10	Station
    Osterley	Early	1	0	1/10	Station
    Osterley	AM Peak	6	0	6/10	Station
    Osterley	AM Peak	6	1	6/10	Station
    Osterley	AM Peak	6	2	6/10	Station
    Osterley	AM Peak	6	3	6/10	Station
    Osterley	AM Peak	6	4	6/10	Station
    Osterley	AM Peak	6	5	6/10	Station
    Osterley	Inter Peak	4	0	4/10	Station
    Osterley	Inter Peak	4	1	4/10	Station
    Osterley	Inter Peak	4	2	4/10	Station
    Osterley	Inter Peak	4	3	4/10	Station
    Osterley	PM Peak	6	0	6/10	Station
    Osterley	PM Peak	6	1	6/10	Station
    Osterley	PM Peak	6	2	6/10	Station
    Osterley	PM Peak	6	3	6/10	Station
    Osterley	PM Peak	6	4	6/10	Station
    Osterley	PM Peak	6	5	6/10	Station
    Osterley	Evening	3	0	3/10	Station
    Osterley	Evening	3	1	3/10	Station
    Osterley	Evening	3	2	3/10	Station
    Osterley	Late	1	0	1/10	Station
    Oval	Early	1	0	1/10	Station
    Oval	AM Peak	9	0	9/10	Station
    Oval	AM Peak	9	1	9/10	Station
    Oval	AM Peak	9	2	9/10	Station
    Oval	AM Peak	9	3	9/10	Station
    Oval	AM Peak	9	4	9/10	Station
    Oval	AM Peak	9	5	9/10	Station
    Oval	AM Peak	9	6	9/10	Station
    Oval	AM Peak	9	7	9/10	Station
    Oval	AM Peak	9	8	9/10	Station
    Oval	Inter Peak	8	0	8/10	Station
    Oval	Inter Peak	8	1	8/10	Station
    Oval	Inter Peak	8	2	8/10	Station
    Oval	Inter Peak	8	3	8/10	Station
    Oval	Inter Peak	8	4	8/10	Station
    Oval	Inter Peak	8	5	8/10	Station
    Oval	Inter Peak	8	6	8/10	Station
    Oval	Inter Peak	8	7	8/10	Station
    Oval	PM Peak	9	0	9/10	Station
    Oval	PM Peak	9	1	9/10	Station
    Oval	PM Peak	9	2	9/10	Station
    Oval	PM Peak	9	3	9/10	Station
    Oval	PM Peak	9	4	9/10	Station
    Oval	PM Peak	9	5	9/10	Station
    Oval	PM Peak	9	6	9/10	Station
    Oval	PM Peak	9	7	9/10	Station
    Oval	PM Peak	9	8	9/10	Station
    Oval	Evening	5	0	5/10	Station
    Oval	Evening	5	1	5/10	Station
    Oval	Evening	5	2	5/10	Station
    Oval	Evening	5	3	5/10	Station
    Oval	Evening	5	4	5/10	Station
    Oval	Late	3	0	3/10	Station
    Oval	Late	3	1	3/10	Station
    Oval	Late	3	2	3/10	Station
    Oxford Circus	AM Peak	4	0	4/10	Station
    Oxford Circus	AM Peak	4	1	4/10	Station
    Oxford Circus	AM Peak	4	2	4/10	Station
    Oxford Circus	AM Peak	4	3	4/10	Station
    Oxford Circus	Inter Peak	7	0	7/10	Station
    Oxford Circus	Inter Peak	7	1	7/10	Station
    Oxford Circus	Inter Peak	7	2	7/10	Station
    Oxford Circus	Inter Peak	7	3	7/10	Station
    Oxford Circus	Inter Peak	7	4	7/10	Station
    Oxford Circus	Inter Peak	7	5	7/10	Station
    Oxford Circus	Inter Peak	7	6	7/10	Station
    Oxford Circus	PM Peak	6	0	6/10	Station
    Oxford Circus	PM Peak	6	1	6/10	Station
    Oxford Circus	PM Peak	6	2	6/10	Station
    Oxford Circus	PM Peak	6	3	6/10	Station
    Oxford Circus	PM Peak	6	4	6/10	Station
    Oxford Circus	PM Peak	6	5	6/10	Station
    Oxford Circus	Evening	3	0	3/10	Station
    Oxford Circus	Evening	3	1	3/10	Station
    Oxford Circus	Evening	3	2	3/10	Station
    Oxford Circus	Late	1	0	1/10	Station
    Paddington	Early	1	0	1/10	Station
    Paddington	AM Peak	8	0	8/10	Station
    Paddington	AM Peak	8	1	8/10	Station
    Paddington	AM Peak	8	2	8/10	Station
    Paddington	AM Peak	8	3	8/10	Station
    Paddington	AM Peak	8	4	8/10	Station
    Paddington	AM Peak	8	5	8/10	Station
    Paddington	AM Peak	8	6	8/10	Station
    Paddington	AM Peak	8	7	8/10	Station
    Paddington	Inter Peak	9	0	9/10	Station
    Paddington	Inter Peak	9	1	9/10	Station
    Paddington	Inter Peak	9	2	9/10	Station
    Paddington	Inter Peak	9	3	9/10	Station
    Paddington	Inter Peak	9	4	9/10	Station
    Paddington	Inter Peak	9	5	9/10	Station
    Paddington	Inter Peak	9	6	9/10	Station
    Paddington	Inter Peak	9	7	9/10	Station
    Paddington	Inter Peak	9	8	9/10	Station
    Paddington	PM Peak	9	0	9/10	Station
    Paddington	PM Peak	9	1	9/10	Station
    Paddington	PM Peak	9	2	9/10	Station
    Paddington	PM Peak	9	3	9/10	Station
    Paddington	PM Peak	9	4	9/10	Station
    Paddington	PM Peak	9	5	9/10	Station
    Paddington	PM Peak	9	6	9/10	Station
    Paddington	PM Peak	9	7	9/10	Station
    Paddington	PM Peak	9	8	9/10	Station
    Paddington	Evening	4	0	4/10	Station
    Paddington	Evening	4	1	4/10	Station
    Paddington	Evening	4	2	4/10	Station
    Paddington	Evening	4	3	4/10	Station
    Paddington	Late	1	0	1/10	Station
    Park Royal	Early	1	0	1/10	Station
    Park Royal	AM Peak	5	0	5/10	Station
    Park Royal	AM Peak	5	1	5/10	Station
    Park Royal	AM Peak	5	2	5/10	Station
    Park Royal	AM Peak	5	3	5/10	Station
    Park Royal	AM Peak	5	4	5/10	Station
    Park Royal	Inter Peak	4	0	4/10	Station
    Park Royal	Inter Peak	4	1	4/10	Station
    Park Royal	Inter Peak	4	2	4/10	Station
    Park Royal	Inter Peak	4	3	4/10	Station
    Park Royal	PM Peak	6	0	6/10	Station
    Park Royal	PM Peak	6	1	6/10	Station
    Park Royal	PM Peak	6	2	6/10	Station
    Park Royal	PM Peak	6	3	6/10	Station
    Park Royal	PM Peak	6	4	6/10	Station
    Park Royal	PM Peak	6	5	6/10	Station
    Park Royal	Evening	2	0	2/10	Station
    Park Royal	Evening	2	1	2/10	Station
    Park Royal	Late	1	0	1/10	Station
    Parsons Green	AM Peak	7	0	7/10	Station
    Parsons Green	AM Peak	7	1	7/10	Station
    Parsons Green	AM Peak	7	2	7/10	Station
    Parsons Green	AM Peak	7	3	7/10	Station
    Parsons Green	AM Peak	7	4	7/10	Station
    Parsons Green	AM Peak	7	5	7/10	Station
    Parsons Green	AM Peak	7	6	7/10	Station
    Parsons Green	Inter Peak	5	0	5/10	Station
    Parsons Green	Inter Peak	5	1	5/10	Station
    Parsons Green	Inter Peak	5	2	5/10	Station
    Parsons Green	Inter Peak	5	3	5/10	Station
    Parsons Green	Inter Peak	5	4	5/10	Station
    Parsons Green	PM Peak	6	0	6/10	Station
    Parsons Green	PM Peak	6	1	6/10	Station
    Parsons Green	PM Peak	6	2	6/10	Station
    Parsons Green	PM Peak	6	3	6/10	Station
    Parsons Green	PM Peak	6	4	6/10	Station
    Parsons Green	PM Peak	6	5	6/10	Station
    Parsons Green	Evening	3	0	3/10	Station
    Parsons Green	Evening	3	1	3/10	Station
    Parsons Green	Evening	3	2	3/10	Station
    Parsons Green	Late	1	0	1/10	Station
    Perivale	Early	1	0	1/10	Station
    Perivale	AM Peak	6	0	6/10	Station
    Perivale	AM Peak	6	1	6/10	Station
    Perivale	AM Peak	6	2	6/10	Station
    Perivale	AM Peak	6	3	6/10	Station
    Perivale	AM Peak	6	4	6/10	Station
    Perivale	AM Peak	6	5	6/10	Station
    Perivale	Inter Peak	4	0	4/10	Station
    Perivale	Inter Peak	4	1	4/10	Station
    Perivale	Inter Peak	4	2	4/10	Station
    Perivale	Inter Peak	4	3	4/10	Station
    Perivale	PM Peak	5	0	5/10	Station
    Perivale	PM Peak	5	1	5/10	Station
    Perivale	PM Peak	5	2	5/10	Station
    Perivale	PM Peak	5	3	5/10	Station
    Perivale	PM Peak	5	4	5/10	Station
    Perivale	Evening	2	0	2/10	Station
    Perivale	Evening	2	1	2/10	Station
    Perivale	Late	1	0	1/10	Station
    Piccadilly Circus	AM Peak	3	0	3/10	Station
    Piccadilly Circus	AM Peak	3	1	3/10	Station
    Piccadilly Circus	AM Peak	3	2	3/10	Station
    Piccadilly Circus	Inter Peak	6	0	6/10	Station
    Piccadilly Circus	Inter Peak	6	1	6/10	Station
    Piccadilly Circus	Inter Peak	6	2	6/10	Station
    Piccadilly Circus	Inter Peak	6	3	6/10	Station
    Piccadilly Circus	Inter Peak	6	4	6/10	Station
    Piccadilly Circus	Inter Peak	6	5	6/10	Station
    Piccadilly Circus	PM Peak	6	0	6/10	Station
    Piccadilly Circus	PM Peak	6	1	6/10	Station
    Piccadilly Circus	PM Peak	6	2	6/10	Station
    Piccadilly Circus	PM Peak	6	3	6/10	Station
    Piccadilly Circus	PM Peak	6	4	6/10	Station
    Piccadilly Circus	PM Peak	6	5	6/10	Station
    Piccadilly Circus	Evening	4	0	4/10	Station
    Piccadilly Circus	Evening	4	1	4/10	Station
    Piccadilly Circus	Evening	4	2	4/10	Station
    Piccadilly Circus	Evening	4	3	4/10	Station
    Piccadilly Circus	Late	2	0	2/10	Station
    Piccadilly Circus	Late	2	1	2/10	Station
    Pimlico	AM Peak	7	0	7/10	Station
    Pimlico	AM Peak	7	1	7/10	Station
    Pimlico	AM Peak	7	2	7/10	Station
    Pimlico	AM Peak	7	3	7/10	Station
    Pimlico	AM Peak	7	4	7/10	Station
    Pimlico	AM Peak	7	5	7/10	Station
    Pimlico	AM Peak	7	6	7/10	Station
    Pimlico	Inter Peak	7	0	7/10	Station
    Pimlico	Inter Peak	7	1	7/10	Station
    Pimlico	Inter Peak	7	2	7/10	Station
    Pimlico	Inter Peak	7	3	7/10	Station
    Pimlico	Inter Peak	7	4	7/10	Station
    Pimlico	Inter Peak	7	5	7/10	Station
    Pimlico	Inter Peak	7	6	7/10	Station
    Pimlico	PM Peak	7	0	7/10	Station
    Pimlico	PM Peak	7	1	7/10	Station
    Pimlico	PM Peak	7	2	7/10	Station
    Pimlico	PM Peak	7	3	7/10	Station
    Pimlico	PM Peak	7	4	7/10	Station
    Pimlico	PM Peak	7	5	7/10	Station
    Pimlico	PM Peak	7	6	7/10	Station
    Pimlico	Evening	3	0	3/10	Station
    Pimlico	Evening	3	1	3/10	Station
    Pimlico	Evening	3	2	3/10	Station
    Pimlico	Late	1	0	1/10	Station
    Pinner	Early	1	0	1/10	Station
    Pinner	AM Peak	7	0	7/10	Station
    Pinner	AM Peak	7	1	7/10	Station
    Pinner	AM Peak	7	2	7/10	Station
    Pinner	AM Peak	7	3	7/10	Station
    Pinner	AM Peak	7	4	7/10	Station
    Pinner	AM Peak	7	5	7/10	Station
    Pinner	AM Peak	7	6	7/10	Station
    Pinner	Inter Peak	4	0	4/10	Station
    Pinner	Inter Peak	4	1	4/10	Station
    Pinner	Inter Peak	4	2	4/10	Station
    Pinner	Inter Peak	4	3	4/10	Station
    Pinner	PM Peak	6	0	6/10	Station
    Pinner	PM Peak	6	1	6/10	Station
    Pinner	PM Peak	6	2	6/10	Station
    Pinner	PM Peak	6	3	6/10	Station
    Pinner	PM Peak	6	4	6/10	Station
    Pinner	PM Peak	6	5	6/10	Station
    Pinner	Evening	3	0	3/10	Station
    Pinner	Evening	3	1	3/10	Station
    Pinner	Evening	3	2	3/10	Station
    Pinner	Late	1	0	1/10	Station
    Plaistow	Early	3	0	3/10	Station
    Plaistow	Early	3	1	3/10	Station
    Plaistow	Early	3	2	3/10	Station
    Plaistow	AM Peak	8	0	8/10	Station
    Plaistow	AM Peak	8	1	8/10	Station
    Plaistow	AM Peak	8	2	8/10	Station
    Plaistow	AM Peak	8	3	8/10	Station
    Plaistow	AM Peak	8	4	8/10	Station
    Plaistow	AM Peak	8	5	8/10	Station
    Plaistow	AM Peak	8	6	8/10	Station
    Plaistow	AM Peak	8	7	8/10	Station
    Plaistow	Inter Peak	7	0	7/10	Station
    Plaistow	Inter Peak	7	1	7/10	Station
    Plaistow	Inter Peak	7	2	7/10	Station
    Plaistow	Inter Peak	7	3	7/10	Station
    Plaistow	Inter Peak	7	4	7/10	Station
    Plaistow	Inter Peak	7	5	7/10	Station
    Plaistow	Inter Peak	7	6	7/10	Station
    Plaistow	PM Peak	8	0	8/10	Station
    Plaistow	PM Peak	8	1	8/10	Station
    Plaistow	PM Peak	8	2	8/10	Station
    Plaistow	PM Peak	8	3	8/10	Station
    Plaistow	PM Peak	8	4	8/10	Station
    Plaistow	PM Peak	8	5	8/10	Station
    Plaistow	PM Peak	8	6	8/10	Station
    Plaistow	PM Peak	8	7	8/10	Station
    Plaistow	Evening	4	0	4/10	Station
    Plaistow	Evening	4	1	4/10	Station
    Plaistow	Evening	4	2	4/10	Station
    Plaistow	Evening	4	3	4/10	Station
    Plaistow	Late	2	0	2/10	Station
    Plaistow	Late	2	1	2/10	Station
    Preston Road	Early	2	0	2/10	Station
    Preston Road	Early	2	1	2/10	Station
    Preston Road	AM Peak	9	0	9/10	Station
    Preston Road	AM Peak	9	1	9/10	Station
    Preston Road	AM Peak	9	2	9/10	Station
    Preston Road	AM Peak	9	3	9/10	Station
    Preston Road	AM Peak	9	4	9/10	Station
    Preston Road	AM Peak	9	5	9/10	Station
    Preston Road	AM Peak	9	6	9/10	Station
    Preston Road	AM Peak	9	7	9/10	Station
    Preston Road	AM Peak	9	8	9/10	Station
    Preston Road	Inter Peak	7	0	7/10	Station
    Preston Road	Inter Peak	7	1	7/10	Station
    Preston Road	Inter Peak	7	2	7/10	Station
    Preston Road	Inter Peak	7	3	7/10	Station
    Preston Road	Inter Peak	7	4	7/10	Station
    Preston Road	Inter Peak	7	5	7/10	Station
    Preston Road	Inter Peak	7	6	7/10	Station
    Preston Road	PM Peak	8	0	8/10	Station
    Preston Road	PM Peak	8	1	8/10	Station
    Preston Road	PM Peak	8	2	8/10	Station
    Preston Road	PM Peak	8	3	8/10	Station
    Preston Road	PM Peak	8	4	8/10	Station
    Preston Road	PM Peak	8	5	8/10	Station
    Preston Road	PM Peak	8	6	8/10	Station
    Preston Road	PM Peak	8	7	8/10	Station
    Preston Road	Evening	3	0	3/10	Station
    Preston Road	Evening	3	1	3/10	Station
    Preston Road	Evening	3	2	3/10	Station
    Preston Road	Late	1	0	1/10	Station
    Putney Bridge	Early	1	0	1/10	Station
    Putney Bridge	AM Peak	6	0	6/10	Station
    Putney Bridge	AM Peak	6	1	6/10	Station
    Putney Bridge	AM Peak	6	2	6/10	Station
    Putney Bridge	AM Peak	6	3	6/10	Station
    Putney Bridge	AM Peak	6	4	6/10	Station
    Putney Bridge	AM Peak	6	5	6/10	Station
    Putney Bridge	Inter Peak	5	0	5/10	Station
    Putney Bridge	Inter Peak	5	1	5/10	Station
    Putney Bridge	Inter Peak	5	2	5/10	Station
    Putney Bridge	Inter Peak	5	3	5/10	Station
    Putney Bridge	Inter Peak	5	4	5/10	Station
    Putney Bridge	PM Peak	6	0	6/10	Station
    Putney Bridge	PM Peak	6	1	6/10	Station
    Putney Bridge	PM Peak	6	2	6/10	Station
    Putney Bridge	PM Peak	6	3	6/10	Station
    Putney Bridge	PM Peak	6	4	6/10	Station
    Putney Bridge	PM Peak	6	5	6/10	Station
    Putney Bridge	Evening	3	0	3/10	Station
    Putney Bridge	Evening	3	1	3/10	Station
    Putney Bridge	Evening	3	2	3/10	Station
    Putney Bridge	Late	1	0	1/10	Station
    Queen's Park	Early	1	0	1/10	Station
    Queen's Park	AM Peak	6	0	6/10	Station
    Queen's Park	AM Peak	6	1	6/10	Station
    Queen's Park	AM Peak	6	2	6/10	Station
    Queen's Park	AM Peak	6	3	6/10	Station
    Queen's Park	AM Peak	6	4	6/10	Station
    Queen's Park	AM Peak	6	5	6/10	Station
    Queen's Park	Inter Peak	4	0	4/10	Station
    Queen's Park	Inter Peak	4	1	4/10	Station
    Queen's Park	Inter Peak	4	2	4/10	Station
    Queen's Park	Inter Peak	4	3	4/10	Station
    Queen's Park	PM Peak	5	0	5/10	Station
    Queen's Park	PM Peak	5	1	5/10	Station
    Queen's Park	PM Peak	5	2	5/10	Station
    Queen's Park	PM Peak	5	3	5/10	Station
    Queen's Park	PM Peak	5	4	5/10	Station
    Queen's Park	Evening	3	0	3/10	Station
    Queen's Park	Evening	3	1	3/10	Station
    Queen's Park	Evening	3	2	3/10	Station
    Queen's Park	Late	1	0	1/10	Station
    Queensbury	Early	2	0	2/10	Station
    Queensbury	Early	2	1	2/10	Station
    Queensbury	AM Peak	4	0	4/10	Station
    Queensbury	AM Peak	4	1	4/10	Station
    Queensbury	AM Peak	4	2	4/10	Station
    Queensbury	AM Peak	4	3	4/10	Station
    Queensbury	Inter Peak	3	0	3/10	Station
    Queensbury	Inter Peak	3	1	3/10	Station
    Queensbury	Inter Peak	3	2	3/10	Station
    Queensbury	PM Peak	5	0	5/10	Station
    Queensbury	PM Peak	5	1	5/10	Station
    Queensbury	PM Peak	5	2	5/10	Station
    Queensbury	PM Peak	5	3	5/10	Station
    Queensbury	PM Peak	5	4	5/10	Station
    Queensbury	Evening	2	0	2/10	Station
    Queensbury	Evening	2	1	2/10	Station
    Queensbury	Late	1	0	1/10	Station
    Queensway	AM Peak	4	0	4/10	Station
    Queensway	AM Peak	4	1	4/10	Station
    Queensway	AM Peak	4	2	4/10	Station
    Queensway	AM Peak	4	3	4/10	Station
    Queensway	Inter Peak	6	0	6/10	Station
    Queensway	Inter Peak	6	1	6/10	Station
    Queensway	Inter Peak	6	2	6/10	Station
    Queensway	Inter Peak	6	3	6/10	Station
    Queensway	Inter Peak	6	4	6/10	Station
    Queensway	Inter Peak	6	5	6/10	Station
    Queensway	PM Peak	5	0	5/10	Station
    Queensway	PM Peak	5	1	5/10	Station
    Queensway	PM Peak	5	2	5/10	Station
    Queensway	PM Peak	5	3	5/10	Station
    Queensway	PM Peak	5	4	5/10	Station
    Queensway	Evening	3	0	3/10	Station
    Queensway	Evening	3	1	3/10	Station
    Queensway	Evening	3	2	3/10	Station
    Queensway	Late	2	0	2/10	Station
    Queensway	Late	2	1	2/10	Station
    Ravenscourt Park	AM Peak	6	0	6/10	Station
    Ravenscourt Park	AM Peak	6	1	6/10	Station
    Ravenscourt Park	AM Peak	6	2	6/10	Station
    Ravenscourt Park	AM Peak	6	3	6/10	Station
    Ravenscourt Park	AM Peak	6	4	6/10	Station
    Ravenscourt Park	AM Peak	6	5	6/10	Station
    Ravenscourt Park	Inter Peak	4	0	4/10	Station
    Ravenscourt Park	Inter Peak	4	1	4/10	Station
    Ravenscourt Park	Inter Peak	4	2	4/10	Station
    Ravenscourt Park	Inter Peak	4	3	4/10	Station
    Ravenscourt Park	PM Peak	5	0	5/10	Station
    Ravenscourt Park	PM Peak	5	1	5/10	Station
    Ravenscourt Park	PM Peak	5	2	5/10	Station
    Ravenscourt Park	PM Peak	5	3	5/10	Station
    Ravenscourt Park	PM Peak	5	4	5/10	Station
    Ravenscourt Park	Evening	2	0	2/10	Station
    Ravenscourt Park	Evening	2	1	2/10	Station
    Ravenscourt Park	Late	1	0	1/10	Station
    Rayners Lane	Early	1	0	1/10	Station
    Rayners Lane	AM Peak	6	0	6/10	Station
    Rayners Lane	AM Peak	6	1	6/10	Station
    Rayners Lane	AM Peak	6	2	6/10	Station
    Rayners Lane	AM Peak	6	3	6/10	Station
    Rayners Lane	AM Peak	6	4	6/10	Station
    Rayners Lane	AM Peak	6	5	6/10	Station
    Rayners Lane	Inter Peak	4	0	4/10	Station
    Rayners Lane	Inter Peak	4	1	4/10	Station
    Rayners Lane	Inter Peak	4	2	4/10	Station
    Rayners Lane	Inter Peak	4	3	4/10	Station
    Rayners Lane	PM Peak	5	0	5/10	Station
    Rayners Lane	PM Peak	5	1	5/10	Station
    Rayners Lane	PM Peak	5	2	5/10	Station
    Rayners Lane	PM Peak	5	3	5/10	Station
    Rayners Lane	PM Peak	5	4	5/10	Station
    Rayners Lane	Evening	2	0	2/10	Station
    Rayners Lane	Evening	2	1	2/10	Station
    Rayners Lane	Late	1	0	1/10	Station
    Redbridge	Early	2	0	2/10	Station
    Redbridge	Early	2	1	2/10	Station
    Redbridge	AM Peak	6	0	6/10	Station
    Redbridge	AM Peak	6	1	6/10	Station
    Redbridge	AM Peak	6	2	6/10	Station
    Redbridge	AM Peak	6	3	6/10	Station
    Redbridge	AM Peak	6	4	6/10	Station
    Redbridge	AM Peak	6	5	6/10	Station
    Redbridge	Inter Peak	5	0	5/10	Station
    Redbridge	Inter Peak	5	1	5/10	Station
    Redbridge	Inter Peak	5	2	5/10	Station
    Redbridge	Inter Peak	5	3	5/10	Station
    Redbridge	Inter Peak	5	4	5/10	Station
    Redbridge	PM Peak	6	0	6/10	Station
    Redbridge	PM Peak	6	1	6/10	Station
    Redbridge	PM Peak	6	2	6/10	Station
    Redbridge	PM Peak	6	3	6/10	Station
    Redbridge	PM Peak	6	4	6/10	Station
    Redbridge	PM Peak	6	5	6/10	Station
    Redbridge	Evening	3	0	3/10	Station
    Redbridge	Evening	3	1	3/10	Station
    Redbridge	Evening	3	2	3/10	Station
    Redbridge	Late	1	0	1/10	Station
    Regent's Park	AM Peak	6	0	6/10	Station
    Regent's Park	AM Peak	6	1	6/10	Station
    Regent's Park	AM Peak	6	2	6/10	Station
    Regent's Park	AM Peak	6	3	6/10	Station
    Regent's Park	AM Peak	6	4	6/10	Station
    Regent's Park	AM Peak	6	5	6/10	Station
    Regent's Park	Inter Peak	7	0	7/10	Station
    Regent's Park	Inter Peak	7	1	7/10	Station
    Regent's Park	Inter Peak	7	2	7/10	Station
    Regent's Park	Inter Peak	7	3	7/10	Station
    Regent's Park	Inter Peak	7	4	7/10	Station
    Regent's Park	Inter Peak	7	5	7/10	Station
    Regent's Park	Inter Peak	7	6	7/10	Station
    Regent's Park	PM Peak	6	0	6/10	Station
    Regent's Park	PM Peak	6	1	6/10	Station
    Regent's Park	PM Peak	6	2	6/10	Station
    Regent's Park	PM Peak	6	3	6/10	Station
    Regent's Park	PM Peak	6	4	6/10	Station
    Regent's Park	PM Peak	6	5	6/10	Station
    Regent's Park	Evening	2	0	2/10	Station
    Regent's Park	Evening	2	1	2/10	Station
    Regent's Park	Late	1	0	1/10	Station
    Richmond	AM Peak	5	0	5/10	Station
    Richmond	AM Peak	5	1	5/10	Station
    Richmond	AM Peak	5	2	5/10	Station
    Richmond	AM Peak	5	3	5/10	Station
    Richmond	AM Peak	5	4	5/10	Station
    Richmond	Inter Peak	4	0	4/10	Station
    Richmond	Inter Peak	4	1	4/10	Station
    Richmond	Inter Peak	4	2	4/10	Station
    Richmond	Inter Peak	4	3	4/10	Station
    Richmond	PM Peak	5	0	5/10	Station
    Richmond	PM Peak	5	1	5/10	Station
    Richmond	PM Peak	5	2	5/10	Station
    Richmond	PM Peak	5	3	5/10	Station
    Richmond	PM Peak	5	4	5/10	Station
    Richmond	Evening	2	0	2/10	Station
    Richmond	Evening	2	1	2/10	Station
    Richmond	Late	1	0	1/10	Station
    Rickmansworth	Early	1	0	1/10	Station
    Rickmansworth	AM Peak	6	0	6/10	Station
    Rickmansworth	AM Peak	6	1	6/10	Station
    Rickmansworth	AM Peak	6	2	6/10	Station
    Rickmansworth	AM Peak	6	3	6/10	Station
    Rickmansworth	AM Peak	6	4	6/10	Station
    Rickmansworth	AM Peak	6	5	6/10	Station
    Rickmansworth	Inter Peak	4	0	4/10	Station
    Rickmansworth	Inter Peak	4	1	4/10	Station
    Rickmansworth	Inter Peak	4	2	4/10	Station
    Rickmansworth	Inter Peak	4	3	4/10	Station
    Rickmansworth	PM Peak	4	0	4/10	Station
    Rickmansworth	PM Peak	4	1	4/10	Station
    Rickmansworth	PM Peak	4	2	4/10	Station
    Rickmansworth	PM Peak	4	3	4/10	Station
    Rickmansworth	Evening	2	0	2/10	Station
    Rickmansworth	Evening	2	1	2/10	Station
    Rickmansworth	Late	1	0	1/10	Station
    Roding Valley	Early	1	0	1/10	Station
    Roding Valley	AM Peak	5	0	5/10	Station
    Roding Valley	AM Peak	5	1	5/10	Station
    Roding Valley	AM Peak	5	2	5/10	Station
    Roding Valley	AM Peak	5	3	5/10	Station
    Roding Valley	AM Peak	5	4	5/10	Station
    Roding Valley	Inter Peak	4	0	4/10	Station
    Roding Valley	Inter Peak	4	1	4/10	Station
    Roding Valley	Inter Peak	4	2	4/10	Station
    Roding Valley	Inter Peak	4	3	4/10	Station
    Roding Valley	PM Peak	4	0	4/10	Station
    Roding Valley	PM Peak	4	1	4/10	Station
    Roding Valley	PM Peak	4	2	4/10	Station
    Roding Valley	PM Peak	4	3	4/10	Station
    Roding Valley	Evening	1	0	1/10	Station
    Roding Valley	Late	1	0	1/10	Station
    Royal Oak	Early	1	0	1/10	Station
    Royal Oak	AM Peak	7	0	7/10	Station
    Royal Oak	AM Peak	7	1	7/10	Station
    Royal Oak	AM Peak	7	2	7/10	Station
    Royal Oak	AM Peak	7	3	7/10	Station
    Royal Oak	AM Peak	7	4	7/10	Station
    Royal Oak	AM Peak	7	5	7/10	Station
    Royal Oak	AM Peak	7	6	7/10	Station
    Royal Oak	Inter Peak	6	0	6/10	Station
    Royal Oak	Inter Peak	6	1	6/10	Station
    Royal Oak	Inter Peak	6	2	6/10	Station
    Royal Oak	Inter Peak	6	3	6/10	Station
    Royal Oak	Inter Peak	6	4	6/10	Station
    Royal Oak	Inter Peak	6	5	6/10	Station
    Royal Oak	PM Peak	7	0	7/10	Station
    Royal Oak	PM Peak	7	1	7/10	Station
    Royal Oak	PM Peak	7	2	7/10	Station
    Royal Oak	PM Peak	7	3	7/10	Station
    Royal Oak	PM Peak	7	4	7/10	Station
    Royal Oak	PM Peak	7	5	7/10	Station
    Royal Oak	PM Peak	7	6	7/10	Station
    Royal Oak	Evening	4	0	4/10	Station
    Royal Oak	Evening	4	1	4/10	Station
    Royal Oak	Evening	4	2	4/10	Station
    Royal Oak	Evening	4	3	4/10	Station
    Royal Oak	Late	1	0	1/10	Station
    Ruislip	Early	1	0	1/10	Station
    Ruislip	AM Peak	5	0	5/10	Station
    Ruislip	AM Peak	5	1	5/10	Station
    Ruislip	AM Peak	5	2	5/10	Station
    Ruislip	AM Peak	5	3	5/10	Station
    Ruislip	AM Peak	5	4	5/10	Station
    Ruislip	Inter Peak	6	0	6/10	Station
    Ruislip	Inter Peak	6	1	6/10	Station
    Ruislip	Inter Peak	6	2	6/10	Station
    Ruislip	Inter Peak	6	3	6/10	Station
    Ruislip	Inter Peak	6	4	6/10	Station
    Ruislip	Inter Peak	6	5	6/10	Station
    Ruislip	PM Peak	5	0	5/10	Station
    Ruislip	PM Peak	5	1	5/10	Station
    Ruislip	PM Peak	5	2	5/10	Station
    Ruislip	PM Peak	5	3	5/10	Station
    Ruislip	PM Peak	5	4	5/10	Station
    Ruislip	Evening	2	0	2/10	Station
    Ruislip	Evening	2	1	2/10	Station
    Ruislip	Late	1	0	1/10	Station
    Ruislip Gardens	Early	1	0	1/10	Station
    Ruislip Gardens	AM Peak	5	0	5/10	Station
    Ruislip Gardens	AM Peak	5	1	5/10	Station
    Ruislip Gardens	AM Peak	5	2	5/10	Station
    Ruislip Gardens	AM Peak	5	3	5/10	Station
    Ruislip Gardens	AM Peak	5	4	5/10	Station
    Ruislip Gardens	Inter Peak	3	0	3/10	Station
    Ruislip Gardens	Inter Peak	3	1	3/10	Station
    Ruislip Gardens	Inter Peak	3	2	3/10	Station
    Ruislip Gardens	PM Peak	4	0	4/10	Station
    Ruislip Gardens	PM Peak	4	1	4/10	Station
    Ruislip Gardens	PM Peak	4	2	4/10	Station
    Ruislip Gardens	PM Peak	4	3	4/10	Station
    Ruislip Gardens	Evening	2	0	2/10	Station
    Ruislip Gardens	Evening	2	1	2/10	Station
    Ruislip Gardens	Late	1	0	1/10	Station
    Ruislip Manor	Early	1	0	1/10	Station
    Ruislip Manor	AM Peak	6	0	6/10	Station
    Ruislip Manor	AM Peak	6	1	6/10	Station
    Ruislip Manor	AM Peak	6	2	6/10	Station
    Ruislip Manor	AM Peak	6	3	6/10	Station
    Ruislip Manor	AM Peak	6	4	6/10	Station
    Ruislip Manor	AM Peak	6	5	6/10	Station
    Ruislip Manor	Inter Peak	5	0	5/10	Station
    Ruislip Manor	Inter Peak	5	1	5/10	Station
    Ruislip Manor	Inter Peak	5	2	5/10	Station
    Ruislip Manor	Inter Peak	5	3	5/10	Station
    Ruislip Manor	Inter Peak	5	4	5/10	Station
    Ruislip Manor	PM Peak	5	0	5/10	Station
    Ruislip Manor	PM Peak	5	1	5/10	Station
    Ruislip Manor	PM Peak	5	2	5/10	Station
    Ruislip Manor	PM Peak	5	3	5/10	Station
    Ruislip Manor	PM Peak	5	4	5/10	Station
    Ruislip Manor	Evening	2	0	2/10	Station
    Ruislip Manor	Evening	2	1	2/10	Station
    Ruislip Manor	Late	1	0	1/10	Station
    Russell Square	AM Peak	5	0	5/10	Station
    Russell Square	AM Peak	5	1	5/10	Station
    Russell Square	AM Peak	5	2	5/10	Station
    Russell Square	AM Peak	5	3	5/10	Station
    Russell Square	AM Peak	5	4	5/10	Station
    Russell Square	Inter Peak	8	0	8/10	Station
    Russell Square	Inter Peak	8	1	8/10	Station
    Russell Square	Inter Peak	8	2	8/10	Station
    Russell Square	Inter Peak	8	3	8/10	Station
    Russell Square	Inter Peak	8	4	8/10	Station
    Russell Square	Inter Peak	8	5	8/10	Station
    Russell Square	Inter Peak	8	6	8/10	Station
    Russell Square	Inter Peak	8	7	8/10	Station
    Russell Square	PM Peak	7	0	7/10	Station
    Russell Square	PM Peak	7	1	7/10	Station
    Russell Square	PM Peak	7	2	7/10	Station
    Russell Square	PM Peak	7	3	7/10	Station
    Russell Square	PM Peak	7	4	7/10	Station
    Russell Square	PM Peak	7	5	7/10	Station
    Russell Square	PM Peak	7	6	7/10	Station
    Russell Square	Evening	4	0	4/10	Station
    Russell Square	Evening	4	1	4/10	Station
    Russell Square	Evening	4	2	4/10	Station
    Russell Square	Evening	4	3	4/10	Station
    Russell Square	Late	2	0	2/10	Station
    Russell Square	Late	2	1	2/10	Station
    Seven Sisters	Early	2	0	2/10	Station
    Seven Sisters	Early	2	1	2/10	Station
    Seven Sisters	AM Peak	6	0	6/10	Station
    Seven Sisters	AM Peak	6	1	6/10	Station
    Seven Sisters	AM Peak	6	2	6/10	Station
    Seven Sisters	AM Peak	6	3	6/10	Station
    Seven Sisters	AM Peak	6	4	6/10	Station
    Seven Sisters	AM Peak	6	5	6/10	Station
    Seven Sisters	Inter Peak	5	0	5/10	Station
    Seven Sisters	Inter Peak	5	1	5/10	Station
    Seven Sisters	Inter Peak	5	2	5/10	Station
    Seven Sisters	Inter Peak	5	3	5/10	Station
    Seven Sisters	Inter Peak	5	4	5/10	Station
    Seven Sisters	PM Peak	6	0	6/10	Station
    Seven Sisters	PM Peak	6	1	6/10	Station
    Seven Sisters	PM Peak	6	2	6/10	Station
    Seven Sisters	PM Peak	6	3	6/10	Station
    Seven Sisters	PM Peak	6	4	6/10	Station
    Seven Sisters	PM Peak	6	5	6/10	Station
    Seven Sisters	Evening	3	0	3/10	Station
    Seven Sisters	Evening	3	1	3/10	Station
    Seven Sisters	Evening	3	2	3/10	Station
    Seven Sisters	Late	2	0	2/10	Station
    Seven Sisters	Late	2	1	2/10	Station
    Shepherd's Bush (Cen)	Early	1	0	1/10	Station
    Shepherd's Bush (Cen)	AM Peak	6	0	6/10	Station
    Shepherd's Bush (Cen)	AM Peak	6	1	6/10	Station
    Shepherd's Bush (Cen)	AM Peak	6	2	6/10	Station
    Shepherd's Bush (Cen)	AM Peak	6	3	6/10	Station
    Shepherd's Bush (Cen)	AM Peak	6	4	6/10	Station
    Shepherd's Bush (Cen)	AM Peak	6	5	6/10	Station
    Shepherd's Bush (Cen)	Inter Peak	6	0	6/10	Station
    Shepherd's Bush (Cen)	Inter Peak	6	1	6/10	Station
    Shepherd's Bush (Cen)	Inter Peak	6	2	6/10	Station
    Shepherd's Bush (Cen)	Inter Peak	6	3	6/10	Station
    Shepherd's Bush (Cen)	Inter Peak	6	4	6/10	Station
    Shepherd's Bush (Cen)	Inter Peak	6	5	6/10	Station
    Shepherd's Bush (Cen)	PM Peak	6	0	6/10	Station
    Shepherd's Bush (Cen)	PM Peak	6	1	6/10	Station
    Shepherd's Bush (Cen)	PM Peak	6	2	6/10	Station
    Shepherd's Bush (Cen)	PM Peak	6	3	6/10	Station
    Shepherd's Bush (Cen)	PM Peak	6	4	6/10	Station
    Shepherd's Bush (Cen)	PM Peak	6	5	6/10	Station
    Shepherd's Bush (Cen)	Evening	3	0	3/10	Station
    Shepherd's Bush (Cen)	Evening	3	1	3/10	Station
    Shepherd's Bush (Cen)	Evening	3	2	3/10	Station
    Shepherd's Bush (Cen)	Late	2	0	2/10	Station
    Shepherd's Bush (Cen)	Late	2	1	2/10	Station
    Shepherd's Bush (H&C)	Early	1	0	1/10	Station
    Shepherd's Bush (H&C)	AM Peak	8	0	8/10	Station
    Shepherd's Bush (H&C)	AM Peak	8	1	8/10	Station
    Shepherd's Bush (H&C)	AM Peak	8	2	8/10	Station
    Shepherd's Bush (H&C)	AM Peak	8	3	8/10	Station
    Shepherd's Bush (H&C)	AM Peak	8	4	8/10	Station
    Shepherd's Bush (H&C)	AM Peak	8	5	8/10	Station
    Shepherd's Bush (H&C)	AM Peak	8	6	8/10	Station
    Shepherd's Bush (H&C)	AM Peak	8	7	8/10	Station
    Shepherd's Bush (H&C)	Inter Peak	9	0	9/10	Station
    Shepherd's Bush (H&C)	Inter Peak	9	1	9/10	Station
    Shepherd's Bush (H&C)	Inter Peak	9	2	9/10	Station
    Shepherd's Bush (H&C)	Inter Peak	9	3	9/10	Station
    Shepherd's Bush (H&C)	Inter Peak	9	4	9/10	Station
    Shepherd's Bush (H&C)	Inter Peak	9	5	9/10	Station
    Shepherd's Bush (H&C)	Inter Peak	9	6	9/10	Station
    Shepherd's Bush (H&C)	Inter Peak	9	7	9/10	Station
    Shepherd's Bush (H&C)	Inter Peak	9	8	9/10	Station
    Shepherd's Bush (H&C)	PM Peak	9	0	9/10	Station
    Shepherd's Bush (H&C)	PM Peak	9	1	9/10	Station
    Shepherd's Bush (H&C)	PM Peak	9	2	9/10	Station
    Shepherd's Bush (H&C)	PM Peak	9	3	9/10	Station
    Shepherd's Bush (H&C)	PM Peak	9	4	9/10	Station
    Shepherd's Bush (H&C)	PM Peak	9	5	9/10	Station
    Shepherd's Bush (H&C)	PM Peak	9	6	9/10	Station
    Shepherd's Bush (H&C)	PM Peak	9	7	9/10	Station
    Shepherd's Bush (H&C)	PM Peak	9	8	9/10	Station
    Shepherd's Bush (H&C)	Evening	5	0	5/10	Station
    Shepherd's Bush (H&C)	Evening	5	1	5/10	Station
    Shepherd's Bush (H&C)	Evening	5	2	5/10	Station
    Shepherd's Bush (H&C)	Evening	5	3	5/10	Station
    Shepherd's Bush (H&C)	Evening	5	4	5/10	Station
    Shepherd's Bush (H&C)	Late	2	0	2/10	Station
    Shepherd's Bush (H&C)	Late	2	1	2/10	Station
    Sloane Square	Early	1	0	1/10	Station
    Sloane Square	AM Peak	6	0	6/10	Station
    Sloane Square	AM Peak	6	1	6/10	Station
    Sloane Square	AM Peak	6	2	6/10	Station
    Sloane Square	AM Peak	6	3	6/10	Station
    Sloane Square	AM Peak	6	4	6/10	Station
    Sloane Square	AM Peak	6	5	6/10	Station
    Sloane Square	Inter Peak	7	0	7/10	Station
    Sloane Square	Inter Peak	7	1	7/10	Station
    Sloane Square	Inter Peak	7	2	7/10	Station
    Sloane Square	Inter Peak	7	3	7/10	Station
    Sloane Square	Inter Peak	7	4	7/10	Station
    Sloane Square	Inter Peak	7	5	7/10	Station
    Sloane Square	Inter Peak	7	6	7/10	Station
    Sloane Square	PM Peak	6	0	6/10	Station
    Sloane Square	PM Peak	6	1	6/10	Station
    Sloane Square	PM Peak	6	2	6/10	Station
    Sloane Square	PM Peak	6	3	6/10	Station
    Sloane Square	PM Peak	6	4	6/10	Station
    Sloane Square	PM Peak	6	5	6/10	Station
    Sloane Square	Evening	3	0	3/10	Station
    Sloane Square	Evening	3	1	3/10	Station
    Sloane Square	Evening	3	2	3/10	Station
    Sloane Square	Late	1	0	1/10	Station
    Snaresbrook	Early	1	0	1/10	Station
    Snaresbrook	AM Peak	6	0	6/10	Station
    Snaresbrook	AM Peak	6	1	6/10	Station
    Snaresbrook	AM Peak	6	2	6/10	Station
    Snaresbrook	AM Peak	6	3	6/10	Station
    Snaresbrook	AM Peak	6	4	6/10	Station
    Snaresbrook	AM Peak	6	5	6/10	Station
    Snaresbrook	Inter Peak	3	0	3/10	Station
    Snaresbrook	Inter Peak	3	1	3/10	Station
    Snaresbrook	Inter Peak	3	2	3/10	Station
    Snaresbrook	PM Peak	3	0	3/10	Station
    Snaresbrook	PM Peak	3	1	3/10	Station
    Snaresbrook	PM Peak	3	2	3/10	Station
    Snaresbrook	Evening	2	0	2/10	Station
    Snaresbrook	Evening	2	1	2/10	Station
    Snaresbrook	Late	1	0	1/10	Station
    South Ealing	Early	1	0	1/10	Station
    South Ealing	AM Peak	7	0	7/10	Station
    South Ealing	AM Peak	7	1	7/10	Station
    South Ealing	AM Peak	7	2	7/10	Station
    South Ealing	AM Peak	7	3	7/10	Station
    South Ealing	AM Peak	7	4	7/10	Station
    South Ealing	AM Peak	7	5	7/10	Station
    South Ealing	AM Peak	7	6	7/10	Station
    South Ealing	Inter Peak	6	0	6/10	Station
    South Ealing	Inter Peak	6	1	6/10	Station
    South Ealing	Inter Peak	6	2	6/10	Station
    South Ealing	Inter Peak	6	3	6/10	Station
    South Ealing	Inter Peak	6	4	6/10	Station
    South Ealing	Inter Peak	6	5	6/10	Station
    South Ealing	PM Peak	7	0	7/10	Station
    South Ealing	PM Peak	7	1	7/10	Station
    South Ealing	PM Peak	7	2	7/10	Station
    South Ealing	PM Peak	7	3	7/10	Station
    South Ealing	PM Peak	7	4	7/10	Station
    South Ealing	PM Peak	7	5	7/10	Station
    South Ealing	PM Peak	7	6	7/10	Station
    South Ealing	Evening	3	0	3/10	Station
    South Ealing	Evening	3	1	3/10	Station
    South Ealing	Evening	3	2	3/10	Station
    South Ealing	Late	2	0	2/10	Station
    South Ealing	Late	2	1	2/10	Station
    South Harrow	Early	1	0	1/10	Station
    South Harrow	AM Peak	5	0	5/10	Station
    South Harrow	AM Peak	5	1	5/10	Station
    South Harrow	AM Peak	5	2	5/10	Station
    South Harrow	AM Peak	5	3	5/10	Station
    South Harrow	AM Peak	5	4	5/10	Station
    South Harrow	Inter Peak	4	0	4/10	Station
    South Harrow	Inter Peak	4	1	4/10	Station
    South Harrow	Inter Peak	4	2	4/10	Station
    South Harrow	Inter Peak	4	3	4/10	Station
    South Harrow	PM Peak	5	0	5/10	Station
    South Harrow	PM Peak	5	1	5/10	Station
    South Harrow	PM Peak	5	2	5/10	Station
    South Harrow	PM Peak	5	3	5/10	Station
    South Harrow	PM Peak	5	4	5/10	Station
    South Harrow	Evening	2	0	2/10	Station
    South Harrow	Evening	2	1	2/10	Station
    South Harrow	Late	1	0	1/10	Station
    South Kensington	AM Peak	4	0	4/10	Station
    South Kensington	AM Peak	4	1	4/10	Station
    South Kensington	AM Peak	4	2	4/10	Station
    South Kensington	AM Peak	4	3	4/10	Station
    South Kensington	Inter Peak	7	0	7/10	Station
    South Kensington	Inter Peak	7	1	7/10	Station
    South Kensington	Inter Peak	7	2	7/10	Station
    South Kensington	Inter Peak	7	3	7/10	Station
    South Kensington	Inter Peak	7	4	7/10	Station
    South Kensington	Inter Peak	7	5	7/10	Station
    South Kensington	Inter Peak	7	6	7/10	Station
    South Kensington	PM Peak	6	0	6/10	Station
    South Kensington	PM Peak	6	1	6/10	Station
    South Kensington	PM Peak	6	2	6/10	Station
    South Kensington	PM Peak	6	3	6/10	Station
    South Kensington	PM Peak	6	4	6/10	Station
    South Kensington	PM Peak	6	5	6/10	Station
    South Kensington	Evening	2	0	2/10	Station
    South Kensington	Evening	2	1	2/10	Station
    South Kensington	Late	1	0	1/10	Station
    South Kenton	Early	1	0	1/10	Station
    South Kenton	AM Peak	8	0	8/10	Station
    South Kenton	AM Peak	8	1	8/10	Station
    South Kenton	AM Peak	8	2	8/10	Station
    South Kenton	AM Peak	8	3	8/10	Station
    South Kenton	AM Peak	8	4	8/10	Station
    South Kenton	AM Peak	8	5	8/10	Station
    South Kenton	AM Peak	8	6	8/10	Station
    South Kenton	AM Peak	8	7	8/10	Station
    South Kenton	Inter Peak	7	0	7/10	Station
    South Kenton	Inter Peak	7	1	7/10	Station
    South Kenton	Inter Peak	7	2	7/10	Station
    South Kenton	Inter Peak	7	3	7/10	Station
    South Kenton	Inter Peak	7	4	7/10	Station
    South Kenton	Inter Peak	7	5	7/10	Station
    South Kenton	Inter Peak	7	6	7/10	Station
    South Kenton	PM Peak	7	0	7/10	Station
    South Kenton	PM Peak	7	1	7/10	Station
    South Kenton	PM Peak	7	2	7/10	Station
    South Kenton	PM Peak	7	3	7/10	Station
    South Kenton	PM Peak	7	4	7/10	Station
    South Kenton	PM Peak	7	5	7/10	Station
    South Kenton	PM Peak	7	6	7/10	Station
    South Kenton	Evening	2	0	2/10	Station
    South Kenton	Evening	2	1	2/10	Station
    South Kenton	Late	2	0	2/10	Station
    South Kenton	Late	2	1	2/10	Station
    South Ruislip	Early	1	0	1/10	Station
    South Ruislip	AM Peak	6	0	6/10	Station
    South Ruislip	AM Peak	6	1	6/10	Station
    South Ruislip	AM Peak	6	2	6/10	Station
    South Ruislip	AM Peak	6	3	6/10	Station
    South Ruislip	AM Peak	6	4	6/10	Station
    South Ruislip	AM Peak	6	5	6/10	Station
    South Ruislip	Inter Peak	3	0	3/10	Station
    South Ruislip	Inter Peak	3	1	3/10	Station
    South Ruislip	Inter Peak	3	2	3/10	Station
    South Ruislip	PM Peak	5	0	5/10	Station
    South Ruislip	PM Peak	5	1	5/10	Station
    South Ruislip	PM Peak	5	2	5/10	Station
    South Ruislip	PM Peak	5	3	5/10	Station
    South Ruislip	PM Peak	5	4	5/10	Station
    South Ruislip	Evening	2	0	2/10	Station
    South Ruislip	Evening	2	1	2/10	Station
    South Ruislip	Late	1	0	1/10	Station
    South Wimbledon	Early	1	0	1/10	Station
    South Wimbledon	AM Peak	5	0	5/10	Station
    South Wimbledon	AM Peak	5	1	5/10	Station
    South Wimbledon	AM Peak	5	2	5/10	Station
    South Wimbledon	AM Peak	5	3	5/10	Station
    South Wimbledon	AM Peak	5	4	5/10	Station
    South Wimbledon	Inter Peak	3	0	3/10	Station
    South Wimbledon	Inter Peak	3	1	3/10	Station
    South Wimbledon	Inter Peak	3	2	3/10	Station
    South Wimbledon	PM Peak	4	0	4/10	Station
    South Wimbledon	PM Peak	4	1	4/10	Station
    South Wimbledon	PM Peak	4	2	4/10	Station
    South Wimbledon	PM Peak	4	3	4/10	Station
    South Wimbledon	Evening	2	0	2/10	Station
    South Wimbledon	Evening	2	1	2/10	Station
    South Wimbledon	Late	1	0	1/10	Station
    South Woodford	Early	1	0	1/10	Station
    South Woodford	AM Peak	6	0	6/10	Station
    South Woodford	AM Peak	6	1	6/10	Station
    South Woodford	AM Peak	6	2	6/10	Station
    South Woodford	AM Peak	6	3	6/10	Station
    South Woodford	AM Peak	6	4	6/10	Station
    South Woodford	AM Peak	6	5	6/10	Station
    South Woodford	Inter Peak	4	0	4/10	Station
    South Woodford	Inter Peak	4	1	4/10	Station
    South Woodford	Inter Peak	4	2	4/10	Station
    South Woodford	Inter Peak	4	3	4/10	Station
    South Woodford	PM Peak	6	0	6/10	Station
    South Woodford	PM Peak	6	1	6/10	Station
    South Woodford	PM Peak	6	2	6/10	Station
    South Woodford	PM Peak	6	3	6/10	Station
    South Woodford	PM Peak	6	4	6/10	Station
    South Woodford	PM Peak	6	5	6/10	Station
    South Woodford	Evening	3	0	3/10	Station
    South Woodford	Evening	3	1	3/10	Station
    South Woodford	Evening	3	2	3/10	Station
    South Woodford	Late	1	0	1/10	Station
    Southfields	Early	1	0	1/10	Station
    Southfields	AM Peak	6	0	6/10	Station
    Southfields	AM Peak	6	1	6/10	Station
    Southfields	AM Peak	6	2	6/10	Station
    Southfields	AM Peak	6	3	6/10	Station
    Southfields	AM Peak	6	4	6/10	Station
    Southfields	AM Peak	6	5	6/10	Station
    Southfields	Inter Peak	4	0	4/10	Station
    Southfields	Inter Peak	4	1	4/10	Station
    Southfields	Inter Peak	4	2	4/10	Station
    Southfields	Inter Peak	4	3	4/10	Station
    Southfields	PM Peak	5	0	5/10	Station
    Southfields	PM Peak	5	1	5/10	Station
    Southfields	PM Peak	5	2	5/10	Station
    Southfields	PM Peak	5	3	5/10	Station
    Southfields	PM Peak	5	4	5/10	Station
    Southfields	Evening	2	0	2/10	Station
    Southfields	Evening	2	1	2/10	Station
    Southfields	Late	1	0	1/10	Station
    Southgate	Early	1	0	1/10	Station
    Southgate	AM Peak	5	0	5/10	Station
    Southgate	AM Peak	5	1	5/10	Station
    Southgate	AM Peak	5	2	5/10	Station
    Southgate	AM Peak	5	3	5/10	Station
    Southgate	AM Peak	5	4	5/10	Station
    Southgate	Inter Peak	4	0	4/10	Station
    Southgate	Inter Peak	4	1	4/10	Station
    Southgate	Inter Peak	4	2	4/10	Station
    Southgate	Inter Peak	4	3	4/10	Station
    Southgate	PM Peak	5	0	5/10	Station
    Southgate	PM Peak	5	1	5/10	Station
    Southgate	PM Peak	5	2	5/10	Station
    Southgate	PM Peak	5	3	5/10	Station
    Southgate	PM Peak	5	4	5/10	Station
    Southgate	Evening	2	0	2/10	Station
    Southgate	Evening	2	1	2/10	Station
    Southgate	Late	1	0	1/10	Station
    Southwark	Early	1	0	1/10	Station
    Southwark	AM Peak	9	0	9/10	Station
    Southwark	AM Peak	9	1	9/10	Station
    Southwark	AM Peak	9	2	9/10	Station
    Southwark	AM Peak	9	3	9/10	Station
    Southwark	AM Peak	9	4	9/10	Station
    Southwark	AM Peak	9	5	9/10	Station
    Southwark	AM Peak	9	6	9/10	Station
    Southwark	AM Peak	9	7	9/10	Station
    Southwark	AM Peak	9	8	9/10	Station
    Southwark	Inter Peak	7	0	7/10	Station
    Southwark	Inter Peak	7	1	7/10	Station
    Southwark	Inter Peak	7	2	7/10	Station
    Southwark	Inter Peak	7	3	7/10	Station
    Southwark	Inter Peak	7	4	7/10	Station
    Southwark	Inter Peak	7	5	7/10	Station
    Southwark	Inter Peak	7	6	7/10	Station
    Southwark	PM Peak	9	0	9/10	Station
    Southwark	PM Peak	9	1	9/10	Station
    Southwark	PM Peak	9	2	9/10	Station
    Southwark	PM Peak	9	3	9/10	Station
    Southwark	PM Peak	9	4	9/10	Station
    Southwark	PM Peak	9	5	9/10	Station
    Southwark	PM Peak	9	6	9/10	Station
    Southwark	PM Peak	9	7	9/10	Station
    Southwark	PM Peak	9	8	9/10	Station
    Southwark	Evening	3	0	3/10	Station
    Southwark	Evening	3	1	3/10	Station
    Southwark	Evening	3	2	3/10	Station
    Southwark	Late	1	0	1/10	Station
    St. James's Park	AM Peak	7	0	7/10	Station
    St. James's Park	AM Peak	7	1	7/10	Station
    St. James's Park	AM Peak	7	2	7/10	Station
    St. James's Park	AM Peak	7	3	7/10	Station
    St. James's Park	AM Peak	7	4	7/10	Station
    St. James's Park	AM Peak	7	5	7/10	Station
    St. James's Park	AM Peak	7	6	7/10	Station
    St. James's Park	Inter Peak	7	0	7/10	Station
    St. James's Park	Inter Peak	7	1	7/10	Station
    St. James's Park	Inter Peak	7	2	7/10	Station
    St. James's Park	Inter Peak	7	3	7/10	Station
    St. James's Park	Inter Peak	7	4	7/10	Station
    St. James's Park	Inter Peak	7	5	7/10	Station
    St. James's Park	Inter Peak	7	6	7/10	Station
    St. James's Park	PM Peak	7	0	7/10	Station
    St. James's Park	PM Peak	7	1	7/10	Station
    St. James's Park	PM Peak	7	2	7/10	Station
    St. James's Park	PM Peak	7	3	7/10	Station
    St. James's Park	PM Peak	7	4	7/10	Station
    St. James's Park	PM Peak	7	5	7/10	Station
    St. James's Park	PM Peak	7	6	7/10	Station
    St. James's Park	Evening	2	0	2/10	Station
    St. James's Park	Evening	2	1	2/10	Station
    St. John's Wood	Early	1	0	1/10	Station
    St. John's Wood	AM Peak	7	0	7/10	Station
    St. John's Wood	AM Peak	7	1	7/10	Station
    St. John's Wood	AM Peak	7	2	7/10	Station
    St. John's Wood	AM Peak	7	3	7/10	Station
    St. John's Wood	AM Peak	7	4	7/10	Station
    St. John's Wood	AM Peak	7	5	7/10	Station
    St. John's Wood	AM Peak	7	6	7/10	Station
    St. John's Wood	Inter Peak	7	0	7/10	Station
    St. John's Wood	Inter Peak	7	1	7/10	Station
    St. John's Wood	Inter Peak	7	2	7/10	Station
    St. John's Wood	Inter Peak	7	3	7/10	Station
    St. John's Wood	Inter Peak	7	4	7/10	Station
    St. John's Wood	Inter Peak	7	5	7/10	Station
    St. John's Wood	Inter Peak	7	6	7/10	Station
    St. John's Wood	PM Peak	6	0	6/10	Station
    St. John's Wood	PM Peak	6	1	6/10	Station
    St. John's Wood	PM Peak	6	2	6/10	Station
    St. John's Wood	PM Peak	6	3	6/10	Station
    St. John's Wood	PM Peak	6	4	6/10	Station
    St. John's Wood	PM Peak	6	5	6/10	Station
    St. John's Wood	Evening	3	0	3/10	Station
    St. John's Wood	Evening	3	1	3/10	Station
    St. John's Wood	Evening	3	2	3/10	Station
    St. John's Wood	Late	1	0	1/10	Station
    St. Paul's	Early	1	0	1/10	Station
    St. Paul's	AM Peak	8	0	8/10	Station
    St. Paul's	AM Peak	8	1	8/10	Station
    St. Paul's	AM Peak	8	2	8/10	Station
    St. Paul's	AM Peak	8	3	8/10	Station
    St. Paul's	AM Peak	8	4	8/10	Station
    St. Paul's	AM Peak	8	5	8/10	Station
    St. Paul's	AM Peak	8	6	8/10	Station
    St. Paul's	AM Peak	8	7	8/10	Station
    St. Paul's	Inter Peak	8	0	8/10	Station
    St. Paul's	Inter Peak	8	1	8/10	Station
    St. Paul's	Inter Peak	8	2	8/10	Station
    St. Paul's	Inter Peak	8	3	8/10	Station
    St. Paul's	Inter Peak	8	4	8/10	Station
    St. Paul's	Inter Peak	8	5	8/10	Station
    St. Paul's	Inter Peak	8	6	8/10	Station
    St. Paul's	Inter Peak	8	7	8/10	Station
    St. Paul's	PM Peak	8	0	8/10	Station
    St. Paul's	PM Peak	8	1	8/10	Station
    St. Paul's	PM Peak	8	2	8/10	Station
    St. Paul's	PM Peak	8	3	8/10	Station
    St. Paul's	PM Peak	8	4	8/10	Station
    St. Paul's	PM Peak	8	5	8/10	Station
    St. Paul's	PM Peak	8	6	8/10	Station
    St. Paul's	PM Peak	8	7	8/10	Station
    St. Paul's	Evening	3	0	3/10	Station
    St. Paul's	Evening	3	1	3/10	Station
    St. Paul's	Evening	3	2	3/10	Station
    St. Paul's	Late	1	0	1/10	Station
    Stamford Brook	AM Peak	6	0	6/10	Station
    Stamford Brook	AM Peak	6	1	6/10	Station
    Stamford Brook	AM Peak	6	2	6/10	Station
    Stamford Brook	AM Peak	6	3	6/10	Station
    Stamford Brook	AM Peak	6	4	6/10	Station
    Stamford Brook	AM Peak	6	5	6/10	Station
    Stamford Brook	Inter Peak	4	0	4/10	Station
    Stamford Brook	Inter Peak	4	1	4/10	Station
    Stamford Brook	Inter Peak	4	2	4/10	Station
    Stamford Brook	Inter Peak	4	3	4/10	Station
    Stamford Brook	PM Peak	5	0	5/10	Station
    Stamford Brook	PM Peak	5	1	5/10	Station
    Stamford Brook	PM Peak	5	2	5/10	Station
    Stamford Brook	PM Peak	5	3	5/10	Station
    Stamford Brook	PM Peak	5	4	5/10	Station
    Stamford Brook	Evening	3	0	3/10	Station
    Stamford Brook	Evening	3	1	3/10	Station
    Stamford Brook	Evening	3	2	3/10	Station
    Stamford Brook	Late	1	0	1/10	Station
    Stanmore	Early	1	0	1/10	Station
    Stanmore	AM Peak	5	0	5/10	Station
    Stanmore	AM Peak	5	1	5/10	Station
    Stanmore	AM Peak	5	2	5/10	Station
    Stanmore	AM Peak	5	3	5/10	Station
    Stanmore	AM Peak	5	4	5/10	Station
    Stanmore	Inter Peak	4	0	4/10	Station
    Stanmore	Inter Peak	4	1	4/10	Station
    Stanmore	Inter Peak	4	2	4/10	Station
    Stanmore	Inter Peak	4	3	4/10	Station
    Stanmore	PM Peak	5	0	5/10	Station
    Stanmore	PM Peak	5	1	5/10	Station
    Stanmore	PM Peak	5	2	5/10	Station
    Stanmore	PM Peak	5	3	5/10	Station
    Stanmore	PM Peak	5	4	5/10	Station
    Stanmore	Evening	2	0	2/10	Station
    Stanmore	Evening	2	1	2/10	Station
    Stanmore	Late	1	0	1/10	Station
    Stepney Green	Early	1	0	1/10	Station
    Stepney Green	AM Peak	7	0	7/10	Station
    Stepney Green	AM Peak	7	1	7/10	Station
    Stepney Green	AM Peak	7	2	7/10	Station
    Stepney Green	AM Peak	7	3	7/10	Station
    Stepney Green	AM Peak	7	4	7/10	Station
    Stepney Green	AM Peak	7	5	7/10	Station
    Stepney Green	AM Peak	7	6	7/10	Station
    Stepney Green	Inter Peak	8	0	8/10	Station
    Stepney Green	Inter Peak	8	1	8/10	Station
    Stepney Green	Inter Peak	8	2	8/10	Station
    Stepney Green	Inter Peak	8	3	8/10	Station
    Stepney Green	Inter Peak	8	4	8/10	Station
    Stepney Green	Inter Peak	8	5	8/10	Station
    Stepney Green	Inter Peak	8	6	8/10	Station
    Stepney Green	Inter Peak	8	7	8/10	Station
    Stepney Green	PM Peak	7	0	7/10	Station
    Stepney Green	PM Peak	7	1	7/10	Station
    Stepney Green	PM Peak	7	2	7/10	Station
    Stepney Green	PM Peak	7	3	7/10	Station
    Stepney Green	PM Peak	7	4	7/10	Station
    Stepney Green	PM Peak	7	5	7/10	Station
    Stepney Green	PM Peak	7	6	7/10	Station
    Stepney Green	Evening	4	0	4/10	Station
    Stepney Green	Evening	4	1	4/10	Station
    Stepney Green	Evening	4	2	4/10	Station
    Stepney Green	Evening	4	3	4/10	Station
    Stepney Green	Late	2	0	2/10	Station
    Stepney Green	Late	2	1	2/10	Station
    Stockwell	Early	1	0	1/10	Station
    Stockwell	AM Peak	9	0	9/10	Station
    Stockwell	AM Peak	9	1	9/10	Station
    Stockwell	AM Peak	9	2	9/10	Station
    Stockwell	AM Peak	9	3	9/10	Station
    Stockwell	AM Peak	9	4	9/10	Station
    Stockwell	AM Peak	9	5	9/10	Station
    Stockwell	AM Peak	9	6	9/10	Station
    Stockwell	AM Peak	9	7	9/10	Station
    Stockwell	AM Peak	9	8	9/10	Station
    Stockwell	Inter Peak	5	0	5/10	Station
    Stockwell	Inter Peak	5	1	5/10	Station
    Stockwell	Inter Peak	5	2	5/10	Station
    Stockwell	Inter Peak	5	3	5/10	Station
    Stockwell	Inter Peak	5	4	5/10	Station
    Stockwell	PM Peak	6	0	6/10	Station
    Stockwell	PM Peak	6	1	6/10	Station
    Stockwell	PM Peak	6	2	6/10	Station
    Stockwell	PM Peak	6	3	6/10	Station
    Stockwell	PM Peak	6	4	6/10	Station
    Stockwell	PM Peak	6	5	6/10	Station
    Stockwell	Evening	4	0	4/10	Station
    Stockwell	Evening	4	1	4/10	Station
    Stockwell	Evening	4	2	4/10	Station
    Stockwell	Evening	4	3	4/10	Station
    Stockwell	Late	2	0	2/10	Station
    Stockwell	Late	2	1	2/10	Station
    Stonebridge Park	Early	2	0	2/10	Station
    Stonebridge Park	Early	2	1	2/10	Station
    Stonebridge Park	AM Peak	5	0	5/10	Station
    Stonebridge Park	AM Peak	5	1	5/10	Station
    Stonebridge Park	AM Peak	5	2	5/10	Station
    Stonebridge Park	AM Peak	5	3	5/10	Station
    Stonebridge Park	AM Peak	5	4	5/10	Station
    Stonebridge Park	Inter Peak	4	0	4/10	Station
    Stonebridge Park	Inter Peak	4	1	4/10	Station
    Stonebridge Park	Inter Peak	4	2	4/10	Station
    Stonebridge Park	Inter Peak	4	3	4/10	Station
    Stonebridge Park	PM Peak	6	0	6/10	Station
    Stonebridge Park	PM Peak	6	1	6/10	Station
    Stonebridge Park	PM Peak	6	2	6/10	Station
    Stonebridge Park	PM Peak	6	3	6/10	Station
    Stonebridge Park	PM Peak	6	4	6/10	Station
    Stonebridge Park	PM Peak	6	5	6/10	Station
    Stonebridge Park	Evening	2	0	2/10	Station
    Stonebridge Park	Evening	2	1	2/10	Station
    Stonebridge Park	Late	1	0	1/10	Station
    Stratford	Early	1	0	1/10	Station
    Stratford	AM Peak	6	0	6/10	Station
    Stratford	AM Peak	6	1	6/10	Station
    Stratford	AM Peak	6	2	6/10	Station
    Stratford	AM Peak	6	3	6/10	Station
    Stratford	AM Peak	6	4	6/10	Station
    Stratford	AM Peak	6	5	6/10	Station
    Stratford	Inter Peak	8	0	8/10	Station
    Stratford	Inter Peak	8	1	8/10	Station
    Stratford	Inter Peak	8	2	8/10	Station
    Stratford	Inter Peak	8	3	8/10	Station
    Stratford	Inter Peak	8	4	8/10	Station
    Stratford	Inter Peak	8	5	8/10	Station
    Stratford	Inter Peak	8	6	8/10	Station
    Stratford	Inter Peak	8	7	8/10	Station
    Stratford	PM Peak	8	0	8/10	Station
    Stratford	PM Peak	8	1	8/10	Station
    Stratford	PM Peak	8	2	8/10	Station
    Stratford	PM Peak	8	3	8/10	Station
    Stratford	PM Peak	8	4	8/10	Station
    Stratford	PM Peak	8	5	8/10	Station
    Stratford	PM Peak	8	6	8/10	Station
    Stratford	PM Peak	8	7	8/10	Station
    Stratford	Evening	4	0	4/10	Station
    Stratford	Evening	4	1	4/10	Station
    Stratford	Evening	4	2	4/10	Station
    Stratford	Evening	4	3	4/10	Station
    Stratford	Late	1	0	1/10	Station
    Sudbury Hill	Early	2	0	2/10	Station
    Sudbury Hill	Early	2	1	2/10	Station
    Sudbury Hill	AM Peak	5	0	5/10	Station
    Sudbury Hill	AM Peak	5	1	5/10	Station
    Sudbury Hill	AM Peak	5	2	5/10	Station
    Sudbury Hill	AM Peak	5	3	5/10	Station
    Sudbury Hill	AM Peak	5	4	5/10	Station
    Sudbury Hill	Inter Peak	4	0	4/10	Station
    Sudbury Hill	Inter Peak	4	1	4/10	Station
    Sudbury Hill	Inter Peak	4	2	4/10	Station
    Sudbury Hill	Inter Peak	4	3	4/10	Station
    Sudbury Hill	PM Peak	6	0	6/10	Station
    Sudbury Hill	PM Peak	6	1	6/10	Station
    Sudbury Hill	PM Peak	6	2	6/10	Station
    Sudbury Hill	PM Peak	6	3	6/10	Station
    Sudbury Hill	PM Peak	6	4	6/10	Station
    Sudbury Hill	PM Peak	6	5	6/10	Station
    Sudbury Hill	Evening	2	0	2/10	Station
    Sudbury Hill	Evening	2	1	2/10	Station
    Sudbury Hill	Late	1	0	1/10	Station
    Sudbury Town	Early	2	0	2/10	Station
    Sudbury Town	Early	2	1	2/10	Station
    Sudbury Town	AM Peak	6	0	6/10	Station
    Sudbury Town	AM Peak	6	1	6/10	Station
    Sudbury Town	AM Peak	6	2	6/10	Station
    Sudbury Town	AM Peak	6	3	6/10	Station
    Sudbury Town	AM Peak	6	4	6/10	Station
    Sudbury Town	AM Peak	6	5	6/10	Station
    Sudbury Town	Inter Peak	4	0	4/10	Station
    Sudbury Town	Inter Peak	4	1	4/10	Station
    Sudbury Town	Inter Peak	4	2	4/10	Station
    Sudbury Town	Inter Peak	4	3	4/10	Station
    Sudbury Town	PM Peak	5	0	5/10	Station
    Sudbury Town	PM Peak	5	1	5/10	Station
    Sudbury Town	PM Peak	5	2	5/10	Station
    Sudbury Town	PM Peak	5	3	5/10	Station
    Sudbury Town	PM Peak	5	4	5/10	Station
    Sudbury Town	Evening	2	0	2/10	Station
    Sudbury Town	Evening	2	1	2/10	Station
    Sudbury Town	Late	1	0	1/10	Station
    Swiss Cottage	Early	1	0	1/10	Station
    Swiss Cottage	AM Peak	7	0	7/10	Station
    Swiss Cottage	AM Peak	7	1	7/10	Station
    Swiss Cottage	AM Peak	7	2	7/10	Station
    Swiss Cottage	AM Peak	7	3	7/10	Station
    Swiss Cottage	AM Peak	7	4	7/10	Station
    Swiss Cottage	AM Peak	7	5	7/10	Station
    Swiss Cottage	AM Peak	7	6	7/10	Station
    Swiss Cottage	Inter Peak	6	0	6/10	Station
    Swiss Cottage	Inter Peak	6	1	6/10	Station
    Swiss Cottage	Inter Peak	6	2	6/10	Station
    Swiss Cottage	Inter Peak	6	3	6/10	Station
    Swiss Cottage	Inter Peak	6	4	6/10	Station
    Swiss Cottage	Inter Peak	6	5	6/10	Station
    Swiss Cottage	PM Peak	7	0	7/10	Station
    Swiss Cottage	PM Peak	7	1	7/10	Station
    Swiss Cottage	PM Peak	7	2	7/10	Station
    Swiss Cottage	PM Peak	7	3	7/10	Station
    Swiss Cottage	PM Peak	7	4	7/10	Station
    Swiss Cottage	PM Peak	7	5	7/10	Station
    Swiss Cottage	PM Peak	7	6	7/10	Station
    Swiss Cottage	Evening	4	0	4/10	Station
    Swiss Cottage	Evening	4	1	4/10	Station
    Swiss Cottage	Evening	4	2	4/10	Station
    Swiss Cottage	Evening	4	3	4/10	Station
    Swiss Cottage	Late	2	0	2/10	Station
    Swiss Cottage	Late	2	1	2/10	Station
    Temple	AM Peak	5	0	5/10	Station
    Temple	AM Peak	5	1	5/10	Station
    Temple	AM Peak	5	2	5/10	Station
    Temple	AM Peak	5	3	5/10	Station
    Temple	AM Peak	5	4	5/10	Station
    Temple	Inter Peak	6	0	6/10	Station
    Temple	Inter Peak	6	1	6/10	Station
    Temple	Inter Peak	6	2	6/10	Station
    Temple	Inter Peak	6	3	6/10	Station
    Temple	Inter Peak	6	4	6/10	Station
    Temple	Inter Peak	6	5	6/10	Station
    Temple	PM Peak	6	0	6/10	Station
    Temple	PM Peak	6	1	6/10	Station
    Temple	PM Peak	6	2	6/10	Station
    Temple	PM Peak	6	3	6/10	Station
    Temple	PM Peak	6	4	6/10	Station
    Temple	PM Peak	6	5	6/10	Station
    Temple	Evening	2	0	2/10	Station
    Temple	Evening	2	1	2/10	Station
    Temple	Late	1	0	1/10	Station
    Theydon Bois	Early	2	0	2/10	Station
    Theydon Bois	Early	2	1	2/10	Station
    Theydon Bois	AM Peak	5	0	5/10	Station
    Theydon Bois	AM Peak	5	1	5/10	Station
    Theydon Bois	AM Peak	5	2	5/10	Station
    Theydon Bois	AM Peak	5	3	5/10	Station
    Theydon Bois	AM Peak	5	4	5/10	Station
    Theydon Bois	Inter Peak	3	0	3/10	Station
    Theydon Bois	Inter Peak	3	1	3/10	Station
    Theydon Bois	Inter Peak	3	2	3/10	Station
    Theydon Bois	PM Peak	5	0	5/10	Station
    Theydon Bois	PM Peak	5	1	5/10	Station
    Theydon Bois	PM Peak	5	2	5/10	Station
    Theydon Bois	PM Peak	5	3	5/10	Station
    Theydon Bois	PM Peak	5	4	5/10	Station
    Theydon Bois	Evening	2	0	2/10	Station
    Theydon Bois	Evening	2	1	2/10	Station
    Theydon Bois	Late	1	0	1/10	Station
    Tooting Bec	Early	1	0	1/10	Station
    Tooting Bec	AM Peak	6	0	6/10	Station
    Tooting Bec	AM Peak	6	1	6/10	Station
    Tooting Bec	AM Peak	6	2	6/10	Station
    Tooting Bec	AM Peak	6	3	6/10	Station
    Tooting Bec	AM Peak	6	4	6/10	Station
    Tooting Bec	AM Peak	6	5	6/10	Station
    Tooting Bec	Inter Peak	3	0	3/10	Station
    Tooting Bec	Inter Peak	3	1	3/10	Station
    Tooting Bec	Inter Peak	3	2	3/10	Station
    Tooting Bec	PM Peak	5	0	5/10	Station
    Tooting Bec	PM Peak	5	1	5/10	Station
    Tooting Bec	PM Peak	5	2	5/10	Station
    Tooting Bec	PM Peak	5	3	5/10	Station
    Tooting Bec	PM Peak	5	4	5/10	Station
    Tooting Bec	Evening	3	0	3/10	Station
    Tooting Bec	Evening	3	1	3/10	Station
    Tooting Bec	Evening	3	2	3/10	Station
    Tooting Bec	Late	1	0	1/10	Station
    Tooting Broadway	Early	1	0	1/10	Station
    Tooting Broadway	AM Peak	6	0	6/10	Station
    Tooting Broadway	AM Peak	6	1	6/10	Station
    Tooting Broadway	AM Peak	6	2	6/10	Station
    Tooting Broadway	AM Peak	6	3	6/10	Station
    Tooting Broadway	AM Peak	6	4	6/10	Station
    Tooting Broadway	AM Peak	6	5	6/10	Station
    Tooting Broadway	Inter Peak	4	0	4/10	Station
    Tooting Broadway	Inter Peak	4	1	4/10	Station
    Tooting Broadway	Inter Peak	4	2	4/10	Station
    Tooting Broadway	Inter Peak	4	3	4/10	Station
    Tooting Broadway	PM Peak	5	0	5/10	Station
    Tooting Broadway	PM Peak	5	1	5/10	Station
    Tooting Broadway	PM Peak	5	2	5/10	Station
    Tooting Broadway	PM Peak	5	3	5/10	Station
    Tooting Broadway	PM Peak	5	4	5/10	Station
    Tooting Broadway	Evening	3	0	3/10	Station
    Tooting Broadway	Evening	3	1	3/10	Station
    Tooting Broadway	Evening	3	2	3/10	Station
    Tooting Broadway	Late	1	0	1/10	Station
    Tottenham Court Road	AM Peak	5	0	5/10	Station
    Tottenham Court Road	AM Peak	5	1	5/10	Station
    Tottenham Court Road	AM Peak	5	2	5/10	Station
    Tottenham Court Road	AM Peak	5	3	5/10	Station
    Tottenham Court Road	AM Peak	5	4	5/10	Station
    Tottenham Court Road	Inter Peak	8	0	8/10	Station
    Tottenham Court Road	Inter Peak	8	1	8/10	Station
    Tottenham Court Road	Inter Peak	8	2	8/10	Station
    Tottenham Court Road	Inter Peak	8	3	8/10	Station
    Tottenham Court Road	Inter Peak	8	4	8/10	Station
    Tottenham Court Road	Inter Peak	8	5	8/10	Station
    Tottenham Court Road	Inter Peak	8	6	8/10	Station
    Tottenham Court Road	Inter Peak	8	7	8/10	Station
    Tottenham Court Road	PM Peak	8	0	8/10	Station
    Tottenham Court Road	PM Peak	8	1	8/10	Station
    Tottenham Court Road	PM Peak	8	2	8/10	Station
    Tottenham Court Road	PM Peak	8	3	8/10	Station
    Tottenham Court Road	PM Peak	8	4	8/10	Station
    Tottenham Court Road	PM Peak	8	5	8/10	Station
    Tottenham Court Road	PM Peak	8	6	8/10	Station
    Tottenham Court Road	PM Peak	8	7	8/10	Station
    Tottenham Court Road	Evening	4	0	4/10	Station
    Tottenham Court Road	Evening	4	1	4/10	Station
    Tottenham Court Road	Evening	4	2	4/10	Station
    Tottenham Court Road	Evening	4	3	4/10	Station
    Tottenham Court Road	Late	3	0	3/10	Station
    Tottenham Court Road	Late	3	1	3/10	Station
    Tottenham Court Road	Late	3	2	3/10	Station
    Tottenham Hale	Early	1	0	1/10	Station
    Tottenham Hale	AM Peak	7	0	7/10	Station
    Tottenham Hale	AM Peak	7	1	7/10	Station
    Tottenham Hale	AM Peak	7	2	7/10	Station
    Tottenham Hale	AM Peak	7	3	7/10	Station
    Tottenham Hale	AM Peak	7	4	7/10	Station
    Tottenham Hale	AM Peak	7	5	7/10	Station
    Tottenham Hale	AM Peak	7	6	7/10	Station
    Tottenham Hale	Inter Peak	6	0	6/10	Station
    Tottenham Hale	Inter Peak	6	1	6/10	Station
    Tottenham Hale	Inter Peak	6	2	6/10	Station
    Tottenham Hale	Inter Peak	6	3	6/10	Station
    Tottenham Hale	Inter Peak	6	4	6/10	Station
    Tottenham Hale	Inter Peak	6	5	6/10	Station
    Tottenham Hale	PM Peak	7	0	7/10	Station
    Tottenham Hale	PM Peak	7	1	7/10	Station
    Tottenham Hale	PM Peak	7	2	7/10	Station
    Tottenham Hale	PM Peak	7	3	7/10	Station
    Tottenham Hale	PM Peak	7	4	7/10	Station
    Tottenham Hale	PM Peak	7	5	7/10	Station
    Tottenham Hale	PM Peak	7	6	7/10	Station
    Tottenham Hale	Evening	3	0	3/10	Station
    Tottenham Hale	Evening	3	1	3/10	Station
    Tottenham Hale	Evening	3	2	3/10	Station
    Tottenham Hale	Late	1	0	1/10	Station
    Totteridge & Whetstone	Early	1	0	1/10	Station
    Totteridge & Whetstone	AM Peak	5	0	5/10	Station
    Totteridge & Whetstone	AM Peak	5	1	5/10	Station
    Totteridge & Whetstone	AM Peak	5	2	5/10	Station
    Totteridge & Whetstone	AM Peak	5	3	5/10	Station
    Totteridge & Whetstone	AM Peak	5	4	5/10	Station
    Totteridge & Whetstone	Inter Peak	3	0	3/10	Station
    Totteridge & Whetstone	Inter Peak	3	1	3/10	Station
    Totteridge & Whetstone	Inter Peak	3	2	3/10	Station
    Totteridge & Whetstone	PM Peak	4	0	4/10	Station
    Totteridge & Whetstone	PM Peak	4	1	4/10	Station
    Totteridge & Whetstone	PM Peak	4	2	4/10	Station
    Totteridge & Whetstone	PM Peak	4	3	4/10	Station
    Totteridge & Whetstone	Evening	2	0	2/10	Station
    Totteridge & Whetstone	Evening	2	1	2/10	Station
    Totteridge & Whetstone	Late	1	0	1/10	Station
    Tower Hill	Early	1	0	1/10	Station
    Tower Hill	AM Peak	5	0	5/10	Station
    Tower Hill	AM Peak	5	1	5/10	Station
    Tower Hill	AM Peak	5	2	5/10	Station
    Tower Hill	AM Peak	5	3	5/10	Station
    Tower Hill	AM Peak	5	4	5/10	Station
    Tower Hill	Inter Peak	6	0	6/10	Station
    Tower Hill	Inter Peak	6	1	6/10	Station
    Tower Hill	Inter Peak	6	2	6/10	Station
    Tower Hill	Inter Peak	6	3	6/10	Station
    Tower Hill	Inter Peak	6	4	6/10	Station
    Tower Hill	Inter Peak	6	5	6/10	Station
    Tower Hill	PM Peak	6	0	6/10	Station
    Tower Hill	PM Peak	6	1	6/10	Station
    Tower Hill	PM Peak	6	2	6/10	Station
    Tower Hill	PM Peak	6	3	6/10	Station
    Tower Hill	PM Peak	6	4	6/10	Station
    Tower Hill	PM Peak	6	5	6/10	Station
    Tower Hill	Evening	2	0	2/10	Station
    Tower Hill	Evening	2	1	2/10	Station
    Tufnell Park	Early	1	0	1/10	Station
    Tufnell Park	AM Peak	8	0	8/10	Station
    Tufnell Park	AM Peak	8	1	8/10	Station
    Tufnell Park	AM Peak	8	2	8/10	Station
    Tufnell Park	AM Peak	8	3	8/10	Station
    Tufnell Park	AM Peak	8	4	8/10	Station
    Tufnell Park	AM Peak	8	5	8/10	Station
    Tufnell Park	AM Peak	8	6	8/10	Station
    Tufnell Park	AM Peak	8	7	8/10	Station
    Tufnell Park	Inter Peak	7	0	7/10	Station
    Tufnell Park	Inter Peak	7	1	7/10	Station
    Tufnell Park	Inter Peak	7	2	7/10	Station
    Tufnell Park	Inter Peak	7	3	7/10	Station
    Tufnell Park	Inter Peak	7	4	7/10	Station
    Tufnell Park	Inter Peak	7	5	7/10	Station
    Tufnell Park	Inter Peak	7	6	7/10	Station
    Tufnell Park	PM Peak	7	0	7/10	Station
    Tufnell Park	PM Peak	7	1	7/10	Station
    Tufnell Park	PM Peak	7	2	7/10	Station
    Tufnell Park	PM Peak	7	3	7/10	Station
    Tufnell Park	PM Peak	7	4	7/10	Station
    Tufnell Park	PM Peak	7	5	7/10	Station
    Tufnell Park	PM Peak	7	6	7/10	Station
    Tufnell Park	Evening	5	0	5/10	Station
    Tufnell Park	Evening	5	1	5/10	Station
    Tufnell Park	Evening	5	2	5/10	Station
    Tufnell Park	Evening	5	3	5/10	Station
    Tufnell Park	Evening	5	4	5/10	Station
    Tufnell Park	Late	3	0	3/10	Station
    Tufnell Park	Late	3	1	3/10	Station
    Tufnell Park	Late	3	2	3/10	Station
    Turnham Green	Early	1	0	1/10	Station
    Turnham Green	AM Peak	6	0	6/10	Station
    Turnham Green	AM Peak	6	1	6/10	Station
    Turnham Green	AM Peak	6	2	6/10	Station
    Turnham Green	AM Peak	6	3	6/10	Station
    Turnham Green	AM Peak	6	4	6/10	Station
    Turnham Green	AM Peak	6	5	6/10	Station
    Turnham Green	Inter Peak	5	0	5/10	Station
    Turnham Green	Inter Peak	5	1	5/10	Station
    Turnham Green	Inter Peak	5	2	5/10	Station
    Turnham Green	Inter Peak	5	3	5/10	Station
    Turnham Green	Inter Peak	5	4	5/10	Station
    Turnham Green	PM Peak	6	0	6/10	Station
    Turnham Green	PM Peak	6	1	6/10	Station
    Turnham Green	PM Peak	6	2	6/10	Station
    Turnham Green	PM Peak	6	3	6/10	Station
    Turnham Green	PM Peak	6	4	6/10	Station
    Turnham Green	PM Peak	6	5	6/10	Station
    Turnham Green	Evening	3	0	3/10	Station
    Turnham Green	Evening	3	1	3/10	Station
    Turnham Green	Evening	3	2	3/10	Station
    Turnham Green	Late	2	0	2/10	Station
    Turnham Green	Late	2	1	2/10	Station
    Turnpike Lane	Early	1	0	1/10	Station
    Turnpike Lane	AM Peak	6	0	6/10	Station
    Turnpike Lane	AM Peak	6	1	6/10	Station
    Turnpike Lane	AM Peak	6	2	6/10	Station
    Turnpike Lane	AM Peak	6	3	6/10	Station
    Turnpike Lane	AM Peak	6	4	6/10	Station
    Turnpike Lane	AM Peak	6	5	6/10	Station
    Turnpike Lane	Inter Peak	6	0	6/10	Station
    Turnpike Lane	Inter Peak	6	1	6/10	Station
    Turnpike Lane	Inter Peak	6	2	6/10	Station
    Turnpike Lane	Inter Peak	6	3	6/10	Station
    Turnpike Lane	Inter Peak	6	4	6/10	Station
    Turnpike Lane	Inter Peak	6	5	6/10	Station
    Turnpike Lane	PM Peak	6	0	6/10	Station
    Turnpike Lane	PM Peak	6	1	6/10	Station
    Turnpike Lane	PM Peak	6	2	6/10	Station
    Turnpike Lane	PM Peak	6	3	6/10	Station
    Turnpike Lane	PM Peak	6	4	6/10	Station
    Turnpike Lane	PM Peak	6	5	6/10	Station
    Turnpike Lane	Evening	4	0	4/10	Station
    Turnpike Lane	Evening	4	1	4/10	Station
    Turnpike Lane	Evening	4	2	4/10	Station
    Turnpike Lane	Evening	4	3	4/10	Station
    Turnpike Lane	Late	2	0	2/10	Station
    Turnpike Lane	Late	2	1	2/10	Station
    Upminster	Early	1	0	1/10	Station
    Upminster	AM Peak	5	0	5/10	Station
    Upminster	AM Peak	5	1	5/10	Station
    Upminster	AM Peak	5	2	5/10	Station
    Upminster	AM Peak	5	3	5/10	Station
    Upminster	AM Peak	5	4	5/10	Station
    Upminster	Inter Peak	3	0	3/10	Station
    Upminster	Inter Peak	3	1	3/10	Station
    Upminster	Inter Peak	3	2	3/10	Station
    Upminster	PM Peak	5	0	5/10	Station
    Upminster	PM Peak	5	1	5/10	Station
    Upminster	PM Peak	5	2	5/10	Station
    Upminster	PM Peak	5	3	5/10	Station
    Upminster	PM Peak	5	4	5/10	Station
    Upminster	Evening	2	0	2/10	Station
    Upminster	Evening	2	1	2/10	Station
    Upminster	Late	1	0	1/10	Station
    Upminster Bridge	Early	1	0	1/10	Station
    Upminster Bridge	AM Peak	5	0	5/10	Station
    Upminster Bridge	AM Peak	5	1	5/10	Station
    Upminster Bridge	AM Peak	5	2	5/10	Station
    Upminster Bridge	AM Peak	5	3	5/10	Station
    Upminster Bridge	AM Peak	5	4	5/10	Station
    Upminster Bridge	Inter Peak	4	0	4/10	Station
    Upminster Bridge	Inter Peak	4	1	4/10	Station
    Upminster Bridge	Inter Peak	4	2	4/10	Station
    Upminster Bridge	Inter Peak	4	3	4/10	Station
    Upminster Bridge	PM Peak	3	0	3/10	Station
    Upminster Bridge	PM Peak	3	1	3/10	Station
    Upminster Bridge	PM Peak	3	2	3/10	Station
    Upminster Bridge	Evening	1	0	1/10	Station
    Upney	Early	2	0	2/10	Station
    Upney	Early	2	1	2/10	Station
    Upney	AM Peak	6	0	6/10	Station
    Upney	AM Peak	6	1	6/10	Station
    Upney	AM Peak	6	2	6/10	Station
    Upney	AM Peak	6	3	6/10	Station
    Upney	AM Peak	6	4	6/10	Station
    Upney	AM Peak	6	5	6/10	Station
    Upney	Inter Peak	5	0	5/10	Station
    Upney	Inter Peak	5	1	5/10	Station
    Upney	Inter Peak	5	2	5/10	Station
    Upney	Inter Peak	5	3	5/10	Station
    Upney	Inter Peak	5	4	5/10	Station
    Upney	PM Peak	5	0	5/10	Station
    Upney	PM Peak	5	1	5/10	Station
    Upney	PM Peak	5	2	5/10	Station
    Upney	PM Peak	5	3	5/10	Station
    Upney	PM Peak	5	4	5/10	Station
    Upney	Evening	2	0	2/10	Station
    Upney	Evening	2	1	2/10	Station
    Upney	Late	1	0	1/10	Station
    Upton Park	Early	2	0	2/10	Station
    Upton Park	Early	2	1	2/10	Station
    Upton Park	AM Peak	6	0	6/10	Station
    Upton Park	AM Peak	6	1	6/10	Station
    Upton Park	AM Peak	6	2	6/10	Station
    Upton Park	AM Peak	6	3	6/10	Station
    Upton Park	AM Peak	6	4	6/10	Station
    Upton Park	AM Peak	6	5	6/10	Station
    Upton Park	Inter Peak	7	0	7/10	Station
    Upton Park	Inter Peak	7	1	7/10	Station
    Upton Park	Inter Peak	7	2	7/10	Station
    Upton Park	Inter Peak	7	3	7/10	Station
    Upton Park	Inter Peak	7	4	7/10	Station
    Upton Park	Inter Peak	7	5	7/10	Station
    Upton Park	Inter Peak	7	6	7/10	Station
    Upton Park	PM Peak	7	0	7/10	Station
    Upton Park	PM Peak	7	1	7/10	Station
    Upton Park	PM Peak	7	2	7/10	Station
    Upton Park	PM Peak	7	3	7/10	Station
    Upton Park	PM Peak	7	4	7/10	Station
    Upton Park	PM Peak	7	5	7/10	Station
    Upton Park	PM Peak	7	6	7/10	Station
    Upton Park	Evening	3	0	3/10	Station
    Upton Park	Evening	3	1	3/10	Station
    Upton Park	Evening	3	2	3/10	Station
    Upton Park	Late	1	0	1/10	Station
    Uxbridge	Early	1	0	1/10	Station
    Uxbridge	AM Peak	4	0	4/10	Station
    Uxbridge	AM Peak	4	1	4/10	Station
    Uxbridge	AM Peak	4	2	4/10	Station
    Uxbridge	AM Peak	4	3	4/10	Station
    Uxbridge	Inter Peak	5	0	5/10	Station
    Uxbridge	Inter Peak	5	1	5/10	Station
    Uxbridge	Inter Peak	5	2	5/10	Station
    Uxbridge	Inter Peak	5	3	5/10	Station
    Uxbridge	Inter Peak	5	4	5/10	Station
    Uxbridge	PM Peak	5	0	5/10	Station
    Uxbridge	PM Peak	5	1	5/10	Station
    Uxbridge	PM Peak	5	2	5/10	Station
    Uxbridge	PM Peak	5	3	5/10	Station
    Uxbridge	PM Peak	5	4	5/10	Station
    Uxbridge	Evening	2	0	2/10	Station
    Uxbridge	Evening	2	1	2/10	Station
    Uxbridge	Late	1	0	1/10	Station
    Vauxhall	Early	1	0	1/10	Station
    Vauxhall	AM Peak	7	0	7/10	Station
    Vauxhall	AM Peak	7	1	7/10	Station
    Vauxhall	AM Peak	7	2	7/10	Station
    Vauxhall	AM Peak	7	3	7/10	Station
    Vauxhall	AM Peak	7	4	7/10	Station
    Vauxhall	AM Peak	7	5	7/10	Station
    Vauxhall	AM Peak	7	6	7/10	Station
    Vauxhall	Inter Peak	5	0	5/10	Station
    Vauxhall	Inter Peak	5	1	5/10	Station
    Vauxhall	Inter Peak	5	2	5/10	Station
    Vauxhall	Inter Peak	5	3	5/10	Station
    Vauxhall	Inter Peak	5	4	5/10	Station
    Vauxhall	PM Peak	7	0	7/10	Station
    Vauxhall	PM Peak	7	1	7/10	Station
    Vauxhall	PM Peak	7	2	7/10	Station
    Vauxhall	PM Peak	7	3	7/10	Station
    Vauxhall	PM Peak	7	4	7/10	Station
    Vauxhall	PM Peak	7	5	7/10	Station
    Vauxhall	PM Peak	7	6	7/10	Station
    Vauxhall	Evening	3	0	3/10	Station
    Vauxhall	Evening	3	1	3/10	Station
    Vauxhall	Evening	3	2	3/10	Station
    Vauxhall	Late	1	0	1/10	Station
    Victoria	Early	1	0	1/10	Station
    Victoria	AM Peak	7	0	7/10	Station
    Victoria	AM Peak	7	1	7/10	Station
    Victoria	AM Peak	7	2	7/10	Station
    Victoria	AM Peak	7	3	7/10	Station
    Victoria	AM Peak	7	4	7/10	Station
    Victoria	AM Peak	7	5	7/10	Station
    Victoria	AM Peak	7	6	7/10	Station
    Victoria	Inter Peak	8	0	8/10	Station
    Victoria	Inter Peak	8	1	8/10	Station
    Victoria	Inter Peak	8	2	8/10	Station
    Victoria	Inter Peak	8	3	8/10	Station
    Victoria	Inter Peak	8	4	8/10	Station
    Victoria	Inter Peak	8	5	8/10	Station
    Victoria	Inter Peak	8	6	8/10	Station
    Victoria	Inter Peak	8	7	8/10	Station
    Victoria	PM Peak	8	0	8/10	Station
    Victoria	PM Peak	8	1	8/10	Station
    Victoria	PM Peak	8	2	8/10	Station
    Victoria	PM Peak	8	3	8/10	Station
    Victoria	PM Peak	8	4	8/10	Station
    Victoria	PM Peak	8	5	8/10	Station
    Victoria	PM Peak	8	6	8/10	Station
    Victoria	PM Peak	8	7	8/10	Station
    Victoria	Evening	4	0	4/10	Station
    Victoria	Evening	4	1	4/10	Station
    Victoria	Evening	4	2	4/10	Station
    Victoria	Evening	4	3	4/10	Station
    Victoria	Late	2	0	2/10	Station
    Victoria	Late	2	1	2/10	Station
    Walthamstow Central	Early	1	0	1/10	Station
    Walthamstow Central	AM Peak	5	0	5/10	Station
    Walthamstow Central	AM Peak	5	1	5/10	Station
    Walthamstow Central	AM Peak	5	2	5/10	Station
    Walthamstow Central	AM Peak	5	3	5/10	Station
    Walthamstow Central	AM Peak	5	4	5/10	Station
    Walthamstow Central	Inter Peak	4	0	4/10	Station
    Walthamstow Central	Inter Peak	4	1	4/10	Station
    Walthamstow Central	Inter Peak	4	2	4/10	Station
    Walthamstow Central	Inter Peak	4	3	4/10	Station
    Walthamstow Central	PM Peak	6	0	6/10	Station
    Walthamstow Central	PM Peak	6	1	6/10	Station
    Walthamstow Central	PM Peak	6	2	6/10	Station
    Walthamstow Central	PM Peak	6	3	6/10	Station
    Walthamstow Central	PM Peak	6	4	6/10	Station
    Walthamstow Central	PM Peak	6	5	6/10	Station
    Walthamstow Central	Evening	3	0	3/10	Station
    Walthamstow Central	Evening	3	1	3/10	Station
    Walthamstow Central	Evening	3	2	3/10	Station
    Walthamstow Central	Late	1	0	1/10	Station
    Wanstead	Early	1	0	1/10	Station
    Wanstead	AM Peak	6	0	6/10	Station
    Wanstead	AM Peak	6	1	6/10	Station
    Wanstead	AM Peak	6	2	6/10	Station
    Wanstead	AM Peak	6	3	6/10	Station
    Wanstead	AM Peak	6	4	6/10	Station
    Wanstead	AM Peak	6	5	6/10	Station
    Wanstead	Inter Peak	5	0	5/10	Station
    Wanstead	Inter Peak	5	1	5/10	Station
    Wanstead	Inter Peak	5	2	5/10	Station
    Wanstead	Inter Peak	5	3	5/10	Station
    Wanstead	Inter Peak	5	4	5/10	Station
    Wanstead	PM Peak	5	0	5/10	Station
    Wanstead	PM Peak	5	1	5/10	Station
    Wanstead	PM Peak	5	2	5/10	Station
    Wanstead	PM Peak	5	3	5/10	Station
    Wanstead	PM Peak	5	4	5/10	Station
    Wanstead	Evening	3	0	3/10	Station
    Wanstead	Evening	3	1	3/10	Station
    Wanstead	Evening	3	2	3/10	Station
    Wanstead	Late	1	0	1/10	Station
    Warren Street	AM Peak	8	0	8/10	Station
    Warren Street	AM Peak	8	1	8/10	Station
    Warren Street	AM Peak	8	2	8/10	Station
    Warren Street	AM Peak	8	3	8/10	Station
    Warren Street	AM Peak	8	4	8/10	Station
    Warren Street	AM Peak	8	5	8/10	Station
    Warren Street	AM Peak	8	6	8/10	Station
    Warren Street	AM Peak	8	7	8/10	Station
    Warren Street	Inter Peak	7	0	7/10	Station
    Warren Street	Inter Peak	7	1	7/10	Station
    Warren Street	Inter Peak	7	2	7/10	Station
    Warren Street	Inter Peak	7	3	7/10	Station
    Warren Street	Inter Peak	7	4	7/10	Station
    Warren Street	Inter Peak	7	5	7/10	Station
    Warren Street	Inter Peak	7	6	7/10	Station
    Warren Street	PM Peak	8	0	8/10	Station
    Warren Street	PM Peak	8	1	8/10	Station
    Warren Street	PM Peak	8	2	8/10	Station
    Warren Street	PM Peak	8	3	8/10	Station
    Warren Street	PM Peak	8	4	8/10	Station
    Warren Street	PM Peak	8	5	8/10	Station
    Warren Street	PM Peak	8	6	8/10	Station
    Warren Street	PM Peak	8	7	8/10	Station
    Warren Street	Evening	3	0	3/10	Station
    Warren Street	Evening	3	1	3/10	Station
    Warren Street	Evening	3	2	3/10	Station
    Warren Street	Late	1	0	1/10	Station
    Warwick Avenue	AM Peak	6	0	6/10	Station
    Warwick Avenue	AM Peak	6	1	6/10	Station
    Warwick Avenue	AM Peak	6	2	6/10	Station
    Warwick Avenue	AM Peak	6	3	6/10	Station
    Warwick Avenue	AM Peak	6	4	6/10	Station
    Warwick Avenue	AM Peak	6	5	6/10	Station
    Warwick Avenue	Inter Peak	4	0	4/10	Station
    Warwick Avenue	Inter Peak	4	1	4/10	Station
    Warwick Avenue	Inter Peak	4	2	4/10	Station
    Warwick Avenue	Inter Peak	4	3	4/10	Station
    Warwick Avenue	PM Peak	5	0	5/10	Station
    Warwick Avenue	PM Peak	5	1	5/10	Station
    Warwick Avenue	PM Peak	5	2	5/10	Station
    Warwick Avenue	PM Peak	5	3	5/10	Station
    Warwick Avenue	PM Peak	5	4	5/10	Station
    Warwick Avenue	Evening	3	0	3/10	Station
    Warwick Avenue	Evening	3	1	3/10	Station
    Warwick Avenue	Evening	3	2	3/10	Station
    Warwick Avenue	Late	1	0	1/10	Station
    Waterloo	Early	1	0	1/10	Station
    Waterloo	AM Peak	8	0	8/10	Station
    Waterloo	AM Peak	8	1	8/10	Station
    Waterloo	AM Peak	8	2	8/10	Station
    Waterloo	AM Peak	8	3	8/10	Station
    Waterloo	AM Peak	8	4	8/10	Station
    Waterloo	AM Peak	8	5	8/10	Station
    Waterloo	AM Peak	8	6	8/10	Station
    Waterloo	AM Peak	8	7	8/10	Station
    Waterloo	Inter Peak	6	0	6/10	Station
    Waterloo	Inter Peak	6	1	6/10	Station
    Waterloo	Inter Peak	6	2	6/10	Station
    Waterloo	Inter Peak	6	3	6/10	Station
    Waterloo	Inter Peak	6	4	6/10	Station
    Waterloo	Inter Peak	6	5	6/10	Station
    Waterloo	PM Peak	8	0	8/10	Station
    Waterloo	PM Peak	8	1	8/10	Station
    Waterloo	PM Peak	8	2	8/10	Station
    Waterloo	PM Peak	8	3	8/10	Station
    Waterloo	PM Peak	8	4	8/10	Station
    Waterloo	PM Peak	8	5	8/10	Station
    Waterloo	PM Peak	8	6	8/10	Station
    Waterloo	PM Peak	8	7	8/10	Station
    Waterloo	Evening	3	0	3/10	Station
    Waterloo	Evening	3	1	3/10	Station
    Waterloo	Evening	3	2	3/10	Station
    Waterloo	Late	1	0	1/10	Station
    Watford	Early	1	0	1/10	Station
    Watford	AM Peak	5	0	5/10	Station
    Watford	AM Peak	5	1	5/10	Station
    Watford	AM Peak	5	2	5/10	Station
    Watford	AM Peak	5	3	5/10	Station
    Watford	AM Peak	5	4	5/10	Station
    Watford	Inter Peak	3	0	3/10	Station
    Watford	Inter Peak	3	1	3/10	Station
    Watford	Inter Peak	3	2	3/10	Station
    Watford	PM Peak	4	0	4/10	Station
    Watford	PM Peak	4	1	4/10	Station
    Watford	PM Peak	4	2	4/10	Station
    Watford	PM Peak	4	3	4/10	Station
    Watford	Evening	2	0	2/10	Station
    Watford	Evening	2	1	2/10	Station
    Watford	Late	1	0	1/10	Station
    Wembley Central	Early	2	0	2/10	Station
    Wembley Central	Early	2	1	2/10	Station
    Wembley Central	AM Peak	7	0	7/10	Station
    Wembley Central	AM Peak	7	1	7/10	Station
    Wembley Central	AM Peak	7	2	7/10	Station
    Wembley Central	AM Peak	7	3	7/10	Station
    Wembley Central	AM Peak	7	4	7/10	Station
    Wembley Central	AM Peak	7	5	7/10	Station
    Wembley Central	AM Peak	7	6	7/10	Station
    Wembley Central	Inter Peak	9	0	9/10	Station
    Wembley Central	Inter Peak	9	1	9/10	Station
    Wembley Central	Inter Peak	9	2	9/10	Station
    Wembley Central	Inter Peak	9	3	9/10	Station
    Wembley Central	Inter Peak	9	4	9/10	Station
    Wembley Central	Inter Peak	9	5	9/10	Station
    Wembley Central	Inter Peak	9	6	9/10	Station
    Wembley Central	Inter Peak	9	7	9/10	Station
    Wembley Central	Inter Peak	9	8	9/10	Station
    Wembley Central	PM Peak	9	0	9/10	Station
    Wembley Central	PM Peak	9	1	9/10	Station
    Wembley Central	PM Peak	9	2	9/10	Station
    Wembley Central	PM Peak	9	3	9/10	Station
    Wembley Central	PM Peak	9	4	9/10	Station
    Wembley Central	PM Peak	9	5	9/10	Station
    Wembley Central	PM Peak	9	6	9/10	Station
    Wembley Central	PM Peak	9	7	9/10	Station
    Wembley Central	PM Peak	9	8	9/10	Station
    Wembley Central	Evening	4	0	4/10	Station
    Wembley Central	Evening	4	1	4/10	Station
    Wembley Central	Evening	4	2	4/10	Station
    Wembley Central	Evening	4	3	4/10	Station
    Wembley Central	Late	1	0	1/10	Station
    Wembley Park	Early	2	0	2/10	Station
    Wembley Park	Early	2	1	2/10	Station
    Wembley Park	AM Peak	8	0	8/10	Station
    Wembley Park	AM Peak	8	1	8/10	Station
    Wembley Park	AM Peak	8	2	8/10	Station
    Wembley Park	AM Peak	8	3	8/10	Station
    Wembley Park	AM Peak	8	4	8/10	Station
    Wembley Park	AM Peak	8	5	8/10	Station
    Wembley Park	AM Peak	8	6	8/10	Station
    Wembley Park	AM Peak	8	7	8/10	Station
    Wembley Park	Inter Peak	8	0	8/10	Station
    Wembley Park	Inter Peak	8	1	8/10	Station
    Wembley Park	Inter Peak	8	2	8/10	Station
    Wembley Park	Inter Peak	8	3	8/10	Station
    Wembley Park	Inter Peak	8	4	8/10	Station
    Wembley Park	Inter Peak	8	5	8/10	Station
    Wembley Park	Inter Peak	8	6	8/10	Station
    Wembley Park	Inter Peak	8	7	8/10	Station
    Wembley Park	PM Peak	9	0	9/10	Station
    Wembley Park	PM Peak	9	1	9/10	Station
    Wembley Park	PM Peak	9	2	9/10	Station
    Wembley Park	PM Peak	9	3	9/10	Station
    Wembley Park	PM Peak	9	4	9/10	Station
    Wembley Park	PM Peak	9	5	9/10	Station
    Wembley Park	PM Peak	9	6	9/10	Station
    Wembley Park	PM Peak	9	7	9/10	Station
    Wembley Park	PM Peak	9	8	9/10	Station
    Wembley Park	Evening	4	0	4/10	Station
    Wembley Park	Evening	4	1	4/10	Station
    Wembley Park	Evening	4	2	4/10	Station
    Wembley Park	Evening	4	3	4/10	Station
    Wembley Park	Late	2	0	2/10	Station
    Wembley Park	Late	2	1	2/10	Station
    West Acton	Early	1	0	1/10	Station
    West Acton	AM Peak	6	0	6/10	Station
    West Acton	AM Peak	6	1	6/10	Station
    West Acton	AM Peak	6	2	6/10	Station
    West Acton	AM Peak	6	3	6/10	Station
    West Acton	AM Peak	6	4	6/10	Station
    West Acton	AM Peak	6	5	6/10	Station
    West Acton	Inter Peak	5	0	5/10	Station
    West Acton	Inter Peak	5	1	5/10	Station
    West Acton	Inter Peak	5	2	5/10	Station
    West Acton	Inter Peak	5	3	5/10	Station
    West Acton	Inter Peak	5	4	5/10	Station
    West Acton	PM Peak	5	0	5/10	Station
    West Acton	PM Peak	5	1	5/10	Station
    West Acton	PM Peak	5	2	5/10	Station
    West Acton	PM Peak	5	3	5/10	Station
    West Acton	PM Peak	5	4	5/10	Station
    West Acton	Evening	3	0	3/10	Station
    West Acton	Evening	3	1	3/10	Station
    West Acton	Evening	3	2	3/10	Station
    West Acton	Late	1	0	1/10	Station
    West Brompton	Early	1	0	1/10	Station
    West Brompton	AM Peak	6	0	6/10	Station
    West Brompton	AM Peak	6	1	6/10	Station
    West Brompton	AM Peak	6	2	6/10	Station
    West Brompton	AM Peak	6	3	6/10	Station
    West Brompton	AM Peak	6	4	6/10	Station
    West Brompton	AM Peak	6	5	6/10	Station
    West Brompton	Inter Peak	5	0	5/10	Station
    West Brompton	Inter Peak	5	1	5/10	Station
    West Brompton	Inter Peak	5	2	5/10	Station
    West Brompton	Inter Peak	5	3	5/10	Station
    West Brompton	Inter Peak	5	4	5/10	Station
    West Brompton	PM Peak	6	0	6/10	Station
    West Brompton	PM Peak	6	1	6/10	Station
    West Brompton	PM Peak	6	2	6/10	Station
    West Brompton	PM Peak	6	3	6/10	Station
    West Brompton	PM Peak	6	4	6/10	Station
    West Brompton	PM Peak	6	5	6/10	Station
    West Brompton	Evening	2	0	2/10	Station
    West Brompton	Evening	2	1	2/10	Station
    West Brompton	Late	1	0	1/10	Station
    West Finchley	Early	1	0	1/10	Station
    West Finchley	AM Peak	6	0	6/10	Station
    West Finchley	AM Peak	6	1	6/10	Station
    West Finchley	AM Peak	6	2	6/10	Station
    West Finchley	AM Peak	6	3	6/10	Station
    West Finchley	AM Peak	6	4	6/10	Station
    West Finchley	AM Peak	6	5	6/10	Station
    West Finchley	Inter Peak	3	0	3/10	Station
    West Finchley	Inter Peak	3	1	3/10	Station
    West Finchley	Inter Peak	3	2	3/10	Station
    West Finchley	PM Peak	4	0	4/10	Station
    West Finchley	PM Peak	4	1	4/10	Station
    West Finchley	PM Peak	4	2	4/10	Station
    West Finchley	PM Peak	4	3	4/10	Station
    West Finchley	Evening	2	0	2/10	Station
    West Finchley	Evening	2	1	2/10	Station
    West Finchley	Late	1	0	1/10	Station
    West Ham	Early	2	0	2/10	Station
    West Ham	Early	2	1	2/10	Station
    West Ham	AM Peak	7	0	7/10	Station
    West Ham	AM Peak	7	1	7/10	Station
    West Ham	AM Peak	7	2	7/10	Station
    West Ham	AM Peak	7	3	7/10	Station
    West Ham	AM Peak	7	4	7/10	Station
    West Ham	AM Peak	7	5	7/10	Station
    West Ham	AM Peak	7	6	7/10	Station
    West Ham	Inter Peak	6	0	6/10	Station
    West Ham	Inter Peak	6	1	6/10	Station
    West Ham	Inter Peak	6	2	6/10	Station
    West Ham	Inter Peak	6	3	6/10	Station
    West Ham	Inter Peak	6	4	6/10	Station
    West Ham	Inter Peak	6	5	6/10	Station
    West Ham	PM Peak	7	0	7/10	Station
    West Ham	PM Peak	7	1	7/10	Station
    West Ham	PM Peak	7	2	7/10	Station
    West Ham	PM Peak	7	3	7/10	Station
    West Ham	PM Peak	7	4	7/10	Station
    West Ham	PM Peak	7	5	7/10	Station
    West Ham	PM Peak	7	6	7/10	Station
    West Ham	Evening	4	0	4/10	Station
    West Ham	Evening	4	1	4/10	Station
    West Ham	Evening	4	2	4/10	Station
    West Ham	Evening	4	3	4/10	Station
    West Ham	Late	2	0	2/10	Station
    West Ham	Late	2	1	2/10	Station
    West Hampstead	Early	1	0	1/10	Station
    West Hampstead	AM Peak	6	0	6/10	Station
    West Hampstead	AM Peak	6	1	6/10	Station
    West Hampstead	AM Peak	6	2	6/10	Station
    West Hampstead	AM Peak	6	3	6/10	Station
    West Hampstead	AM Peak	6	4	6/10	Station
    West Hampstead	AM Peak	6	5	6/10	Station
    West Hampstead	Inter Peak	3	0	3/10	Station
    West Hampstead	Inter Peak	3	1	3/10	Station
    West Hampstead	Inter Peak	3	2	3/10	Station
    West Hampstead	PM Peak	4	0	4/10	Station
    West Hampstead	PM Peak	4	1	4/10	Station
    West Hampstead	PM Peak	4	2	4/10	Station
    West Hampstead	PM Peak	4	3	4/10	Station
    West Hampstead	Evening	2	0	2/10	Station
    West Hampstead	Evening	2	1	2/10	Station
    West Hampstead	Late	1	0	1/10	Station
    West Harrow	Early	1	0	1/10	Station
    West Harrow	AM Peak	5	0	5/10	Station
    West Harrow	AM Peak	5	1	5/10	Station
    West Harrow	AM Peak	5	2	5/10	Station
    West Harrow	AM Peak	5	3	5/10	Station
    West Harrow	AM Peak	5	4	5/10	Station
    West Harrow	Inter Peak	3	0	3/10	Station
    West Harrow	Inter Peak	3	1	3/10	Station
    West Harrow	Inter Peak	3	2	3/10	Station
    West Harrow	PM Peak	6	0	6/10	Station
    West Harrow	PM Peak	6	1	6/10	Station
    West Harrow	PM Peak	6	2	6/10	Station
    West Harrow	PM Peak	6	3	6/10	Station
    West Harrow	PM Peak	6	4	6/10	Station
    West Harrow	PM Peak	6	5	6/10	Station
    West Harrow	Evening	3	0	3/10	Station
    West Harrow	Evening	3	1	3/10	Station
    West Harrow	Evening	3	2	3/10	Station
    West Harrow	Late	1	0	1/10	Station
    West Kensington	Early	1	0	1/10	Station
    West Kensington	AM Peak	6	0	6/10	Station
    West Kensington	AM Peak	6	1	6/10	Station
    West Kensington	AM Peak	6	2	6/10	Station
    West Kensington	AM Peak	6	3	6/10	Station
    West Kensington	AM Peak	6	4	6/10	Station
    West Kensington	AM Peak	6	5	6/10	Station
    West Kensington	Inter Peak	6	0	6/10	Station
    West Kensington	Inter Peak	6	1	6/10	Station
    West Kensington	Inter Peak	6	2	6/10	Station
    West Kensington	Inter Peak	6	3	6/10	Station
    West Kensington	Inter Peak	6	4	6/10	Station
    West Kensington	Inter Peak	6	5	6/10	Station
    West Kensington	PM Peak	6	0	6/10	Station
    West Kensington	PM Peak	6	1	6/10	Station
    West Kensington	PM Peak	6	2	6/10	Station
    West Kensington	PM Peak	6	3	6/10	Station
    West Kensington	PM Peak	6	4	6/10	Station
    West Kensington	PM Peak	6	5	6/10	Station
    West Kensington	Evening	3	0	3/10	Station
    West Kensington	Evening	3	1	3/10	Station
    West Kensington	Evening	3	2	3/10	Station
    West Kensington	Late	1	0	1/10	Station
    West Ruislip	Early	1	0	1/10	Station
    West Ruislip	AM Peak	5	0	5/10	Station
    West Ruislip	AM Peak	5	1	5/10	Station
    West Ruislip	AM Peak	5	2	5/10	Station
    West Ruislip	AM Peak	5	3	5/10	Station
    West Ruislip	AM Peak	5	4	5/10	Station
    West Ruislip	Inter Peak	3	0	3/10	Station
    West Ruislip	Inter Peak	3	1	3/10	Station
    West Ruislip	Inter Peak	3	2	3/10	Station
    West Ruislip	PM Peak	5	0	5/10	Station
    West Ruislip	PM Peak	5	1	5/10	Station
    West Ruislip	PM Peak	5	2	5/10	Station
    West Ruislip	PM Peak	5	3	5/10	Station
    West Ruislip	PM Peak	5	4	5/10	Station
    West Ruislip	Evening	2	0	2/10	Station
    West Ruislip	Evening	2	1	2/10	Station
    West Ruislip	Late	1	0	1/10	Station
    Westbourne Park	Early	1	0	1/10	Station
    Westbourne Park	AM Peak	8	0	8/10	Station
    Westbourne Park	AM Peak	8	1	8/10	Station
    Westbourne Park	AM Peak	8	2	8/10	Station
    Westbourne Park	AM Peak	8	3	8/10	Station
    Westbourne Park	AM Peak	8	4	8/10	Station
    Westbourne Park	AM Peak	8	5	8/10	Station
    Westbourne Park	AM Peak	8	6	8/10	Station
    Westbourne Park	AM Peak	8	7	8/10	Station
    Westbourne Park	Inter Peak	7	0	7/10	Station
    Westbourne Park	Inter Peak	7	1	7/10	Station
    Westbourne Park	Inter Peak	7	2	7/10	Station
    Westbourne Park	Inter Peak	7	3	7/10	Station
    Westbourne Park	Inter Peak	7	4	7/10	Station
    Westbourne Park	Inter Peak	7	5	7/10	Station
    Westbourne Park	Inter Peak	7	6	7/10	Station
    Westbourne Park	PM Peak	7	0	7/10	Station
    Westbourne Park	PM Peak	7	1	7/10	Station
    Westbourne Park	PM Peak	7	2	7/10	Station
    Westbourne Park	PM Peak	7	3	7/10	Station
    Westbourne Park	PM Peak	7	4	7/10	Station
    Westbourne Park	PM Peak	7	5	7/10	Station
    Westbourne Park	PM Peak	7	6	7/10	Station
    Westbourne Park	Evening	4	0	4/10	Station
    Westbourne Park	Evening	4	1	4/10	Station
    Westbourne Park	Evening	4	2	4/10	Station
    Westbourne Park	Evening	4	3	4/10	Station
    Westbourne Park	Late	1	0	1/10	Station
    Westminster	AM Peak	5	0	5/10	Station
    Westminster	AM Peak	5	1	5/10	Station
    Westminster	AM Peak	5	2	5/10	Station
    Westminster	AM Peak	5	3	5/10	Station
    Westminster	AM Peak	5	4	5/10	Station
    Westminster	Inter Peak	7	0	7/10	Station
    Westminster	Inter Peak	7	1	7/10	Station
    Westminster	Inter Peak	7	2	7/10	Station
    Westminster	Inter Peak	7	3	7/10	Station
    Westminster	Inter Peak	7	4	7/10	Station
    Westminster	Inter Peak	7	5	7/10	Station
    Westminster	Inter Peak	7	6	7/10	Station
    Westminster	PM Peak	6	0	6/10	Station
    Westminster	PM Peak	6	1	6/10	Station
    Westminster	PM Peak	6	2	6/10	Station
    Westminster	PM Peak	6	3	6/10	Station
    Westminster	PM Peak	6	4	6/10	Station
    Westminster	PM Peak	6	5	6/10	Station
    Westminster	Evening	2	0	2/10	Station
    Westminster	Evening	2	1	2/10	Station
    Westminster	Late	1	0	1/10	Station
    White City	Early	1	0	1/10	Station
    White City	AM Peak	6	0	6/10	Station
    White City	AM Peak	6	1	6/10	Station
    White City	AM Peak	6	2	6/10	Station
    White City	AM Peak	6	3	6/10	Station
    White City	AM Peak	6	4	6/10	Station
    White City	AM Peak	6	5	6/10	Station
    White City	Inter Peak	4	0	4/10	Station
    White City	Inter Peak	4	1	4/10	Station
    White City	Inter Peak	4	2	4/10	Station
    White City	Inter Peak	4	3	4/10	Station
    White City	PM Peak	5	0	5/10	Station
    White City	PM Peak	5	1	5/10	Station
    White City	PM Peak	5	2	5/10	Station
    White City	PM Peak	5	3	5/10	Station
    White City	PM Peak	5	4	5/10	Station
    White City	Evening	2	0	2/10	Station
    White City	Evening	2	1	2/10	Station
    White City	Late	1	0	1/10	Station
    Whitechapel	Early	1	0	1/10	Station
    Whitechapel	AM Peak	5	0	5/10	Station
    Whitechapel	AM Peak	5	1	5/10	Station
    Whitechapel	AM Peak	5	2	5/10	Station
    Whitechapel	AM Peak	5	3	5/10	Station
    Whitechapel	AM Peak	5	4	5/10	Station
    Whitechapel	Inter Peak	6	0	6/10	Station
    Whitechapel	Inter Peak	6	1	6/10	Station
    Whitechapel	Inter Peak	6	2	6/10	Station
    Whitechapel	Inter Peak	6	3	6/10	Station
    Whitechapel	Inter Peak	6	4	6/10	Station
    Whitechapel	Inter Peak	6	5	6/10	Station
    Whitechapel	PM Peak	5	0	5/10	Station
    Whitechapel	PM Peak	5	1	5/10	Station
    Whitechapel	PM Peak	5	2	5/10	Station
    Whitechapel	PM Peak	5	3	5/10	Station
    Whitechapel	PM Peak	5	4	5/10	Station
    Whitechapel	Evening	3	0	3/10	Station
    Whitechapel	Evening	3	1	3/10	Station
    Whitechapel	Evening	3	2	3/10	Station
    Whitechapel	Late	1	0	1/10	Station
    Willesden Green	Early	1	0	1/10	Station
    Willesden Green	AM Peak	6	0	6/10	Station
    Willesden Green	AM Peak	6	1	6/10	Station
    Willesden Green	AM Peak	6	2	6/10	Station
    Willesden Green	AM Peak	6	3	6/10	Station
    Willesden Green	AM Peak	6	4	6/10	Station
    Willesden Green	AM Peak	6	5	6/10	Station
    Willesden Green	Inter Peak	5	0	5/10	Station
    Willesden Green	Inter Peak	5	1	5/10	Station
    Willesden Green	Inter Peak	5	2	5/10	Station
    Willesden Green	Inter Peak	5	3	5/10	Station
    Willesden Green	Inter Peak	5	4	5/10	Station
    Willesden Green	PM Peak	5	0	5/10	Station
    Willesden Green	PM Peak	5	1	5/10	Station
    Willesden Green	PM Peak	5	2	5/10	Station
    Willesden Green	PM Peak	5	3	5/10	Station
    Willesden Green	PM Peak	5	4	5/10	Station
    Willesden Green	Evening	3	0	3/10	Station
    Willesden Green	Evening	3	1	3/10	Station
    Willesden Green	Evening	3	2	3/10	Station
    Willesden Green	Late	2	0	2/10	Station
    Willesden Green	Late	2	1	2/10	Station
    Willesden Junction	Early	1	0	1/10	Station
    Willesden Junction	AM Peak	6	0	6/10	Station
    Willesden Junction	AM Peak	6	1	6/10	Station
    Willesden Junction	AM Peak	6	2	6/10	Station
    Willesden Junction	AM Peak	6	3	6/10	Station
    Willesden Junction	AM Peak	6	4	6/10	Station
    Willesden Junction	AM Peak	6	5	6/10	Station
    Willesden Junction	Inter Peak	5	0	5/10	Station
    Willesden Junction	Inter Peak	5	1	5/10	Station
    Willesden Junction	Inter Peak	5	2	5/10	Station
    Willesden Junction	Inter Peak	5	3	5/10	Station
    Willesden Junction	Inter Peak	5	4	5/10	Station
    Willesden Junction	PM Peak	5	0	5/10	Station
    Willesden Junction	PM Peak	5	1	5/10	Station
    Willesden Junction	PM Peak	5	2	5/10	Station
    Willesden Junction	PM Peak	5	3	5/10	Station
    Willesden Junction	PM Peak	5	4	5/10	Station
    Willesden Junction	Evening	2	0	2/10	Station
    Willesden Junction	Evening	2	1	2/10	Station
    Willesden Junction	Late	1	0	1/10	Station
    Wimbledon	Early	1	0	1/10	Station
    Wimbledon	AM Peak	4	0	4/10	Station
    Wimbledon	AM Peak	4	1	4/10	Station
    Wimbledon	AM Peak	4	2	4/10	Station
    Wimbledon	AM Peak	4	3	4/10	Station
    Wimbledon	Inter Peak	3	0	3/10	Station
    Wimbledon	Inter Peak	3	1	3/10	Station
    Wimbledon	Inter Peak	3	2	3/10	Station
    Wimbledon	PM Peak	5	0	5/10	Station
    Wimbledon	PM Peak	5	1	5/10	Station
    Wimbledon	PM Peak	5	2	5/10	Station
    Wimbledon	PM Peak	5	3	5/10	Station
    Wimbledon	PM Peak	5	4	5/10	Station
    Wimbledon	Evening	2	0	2/10	Station
    Wimbledon	Evening	2	1	2/10	Station
    Wimbledon	Late	1	0	1/10	Station
    Wimbledon Park	Early	1	0	1/10	Station
    Wimbledon Park	AM Peak	5	0	5/10	Station
    Wimbledon Park	AM Peak	5	1	5/10	Station
    Wimbledon Park	AM Peak	5	2	5/10	Station
    Wimbledon Park	AM Peak	5	3	5/10	Station
    Wimbledon Park	AM Peak	5	4	5/10	Station
    Wimbledon Park	Inter Peak	4	0	4/10	Station
    Wimbledon Park	Inter Peak	4	1	4/10	Station
    Wimbledon Park	Inter Peak	4	2	4/10	Station
    Wimbledon Park	Inter Peak	4	3	4/10	Station
    Wimbledon Park	PM Peak	4	0	4/10	Station
    Wimbledon Park	PM Peak	4	1	4/10	Station
    Wimbledon Park	PM Peak	4	2	4/10	Station
    Wimbledon Park	PM Peak	4	3	4/10	Station
    Wimbledon Park	Evening	2	0	2/10	Station
    Wimbledon Park	Evening	2	1	2/10	Station
    Wimbledon Park	Late	1	0	1/10	Station
    Wood Green	Early	1	0	1/10	Station
    Wood Green	AM Peak	5	0	5/10	Station
    Wood Green	AM Peak	5	1	5/10	Station
    Wood Green	AM Peak	5	2	5/10	Station
    Wood Green	AM Peak	5	3	5/10	Station
    Wood Green	AM Peak	5	4	5/10	Station
    Wood Green	Inter Peak	5	0	5/10	Station
    Wood Green	Inter Peak	5	1	5/10	Station
    Wood Green	Inter Peak	5	2	5/10	Station
    Wood Green	Inter Peak	5	3	5/10	Station
    Wood Green	Inter Peak	5	4	5/10	Station
    Wood Green	PM Peak	6	0	6/10	Station
    Wood Green	PM Peak	6	1	6/10	Station
    Wood Green	PM Peak	6	2	6/10	Station
    Wood Green	PM Peak	6	3	6/10	Station
    Wood Green	PM Peak	6	4	6/10	Station
    Wood Green	PM Peak	6	5	6/10	Station
    Wood Green	Evening	3	0	3/10	Station
    Wood Green	Evening	3	1	3/10	Station
    Wood Green	Evening	3	2	3/10	Station
    Wood Green	Late	2	0	2/10	Station
    Wood Green	Late	2	1	2/10	Station
    Wood Lane	AM Peak	5	0	5/10	Station
    Wood Lane	AM Peak	5	1	5/10	Station
    Wood Lane	AM Peak	5	2	5/10	Station
    Wood Lane	AM Peak	5	3	5/10	Station
    Wood Lane	AM Peak	5	4	5/10	Station
    Wood Lane	Inter Peak	6	0	6/10	Station
    Wood Lane	Inter Peak	6	1	6/10	Station
    Wood Lane	Inter Peak	6	2	6/10	Station
    Wood Lane	Inter Peak	6	3	6/10	Station
    Wood Lane	Inter Peak	6	4	6/10	Station
    Wood Lane	Inter Peak	6	5	6/10	Station
    Wood Lane	PM Peak	6	0	6/10	Station
    Wood Lane	PM Peak	6	1	6/10	Station
    Wood Lane	PM Peak	6	2	6/10	Station
    Wood Lane	PM Peak	6	3	6/10	Station
    Wood Lane	PM Peak	6	4	6/10	Station
    Wood Lane	PM Peak	6	5	6/10	Station
    Wood Lane	Evening	2	0	2/10	Station
    Wood Lane	Evening	2	1	2/10	Station
    Wood Lane	Late	1	0	1/10	Station
    Woodford	Early	1	0	1/10	Station
    Woodford	AM Peak	6	0	6/10	Station
    Woodford	AM Peak	6	1	6/10	Station
    Woodford	AM Peak	6	2	6/10	Station
    Woodford	AM Peak	6	3	6/10	Station
    Woodford	AM Peak	6	4	6/10	Station
    Woodford	AM Peak	6	5	6/10	Station
    Woodford	Inter Peak	4	0	4/10	Station
    Woodford	Inter Peak	4	1	4/10	Station
    Woodford	Inter Peak	4	2	4/10	Station
    Woodford	Inter Peak	4	3	4/10	Station
    Woodford	PM Peak	5	0	5/10	Station
    Woodford	PM Peak	5	1	5/10	Station
    Woodford	PM Peak	5	2	5/10	Station
    Woodford	PM Peak	5	3	5/10	Station
    Woodford	PM Peak	5	4	5/10	Station
    Woodford	Evening	2	0	2/10	Station
    Woodford	Evening	2	1	2/10	Station
    Woodford	Late	1	0	1/10	Station
    Woodside Park	Early	1	0	1/10	Station
    Woodside Park	AM Peak	5	0	5/10	Station
    Woodside Park	AM Peak	5	1	5/10	Station
    Woodside Park	AM Peak	5	2	5/10	Station
    Woodside Park	AM Peak	5	3	5/10	Station
    Woodside Park	AM Peak	5	4	5/10	Station
    Woodside Park	Inter Peak	3	0	3/10	Station
    Woodside Park	Inter Peak	3	1	3/10	Station
    Woodside Park	Inter Peak	3	2	3/10	Station
    Woodside Park	PM Peak	5	0	5/10	Station
    Woodside Park	PM Peak	5	1	5/10	Station
    Woodside Park	PM Peak	5	2	5/10	Station
    Woodside Park	PM Peak	5	3	5/10	Station
    Woodside Park	PM Peak	5	4	5/10	Station
    Woodside Park	Evening	2	0	2/10	Station
    Woodside Park	Evening	2	1	2/10	Station
    Woodside Park	Late	1	0	1/10	Station
    BackEarly	Early	10	0	10/10	Background
    BackEarly	Early	10	1	10/10	Background
    BackEarly	Early	10	2	10/10	Background
    BackEarly	Early	10	3	10/10	Background
    BackEarly	Early	10	4	10/10	Background
    BackEarly	Early	10	5	10/10	Background
    BackEarly	Early	10	6	10/10	Background
    BackEarly	Early	10	7	10/10	Background
    BackEarly	Early	10	8	10/10	Background
    BackEarly	Early	10	9	10/10	Background
    BackAM	AM Peak	10	0	10/10	Background
    BackAM	AM Peak	10	1	10/10	Background
    BackAM	AM Peak	10	2	10/10	Background
    BackAM	AM Peak	10	3	10/10	Background
    BackAM	AM Peak	10	4	10/10	Background
    BackAM	AM Peak	10	5	10/10	Background
    BackAM	AM Peak	10	6	10/10	Background
    BackAM	AM Peak	10	7	10/10	Background
    BackAM	AM Peak	10	8	10/10	Background
    BackAM	AM Peak	10	9	10/10	Background
    BackInter	Inter Peak	10	0	10/10	Background
    BackInter	Inter Peak	10	1	10/10	Background
    BackInter	Inter Peak	10	2	10/10	Background
    BackInter	Inter Peak	10	3	10/10	Background
    BackInter	Inter Peak	10	4	10/10	Background
    BackInter	Inter Peak	10	5	10/10	Background
    BackInter	Inter Peak	10	6	10/10	Background
    BackInter	Inter Peak	10	7	10/10	Background
    BackInter	Inter Peak	10	8	10/10	Background
    BackInter	Inter Peak	10	9	10/10	Background
    BackPM	PM Peak	10	0	10/10	Background
    BackPM	PM Peak	10	1	10/10	Background
    BackPM	PM Peak	10	2	10/10	Background
    BackPM	PM Peak	10	3	10/10	Background
    BackPM	PM Peak	10	4	10/10	Background
    BackPM	PM Peak	10	5	10/10	Background
    BackPM	PM Peak	10	6	10/10	Background
    BackPM	PM Peak	10	7	10/10	Background
    BackPM	PM Peak	10	8	10/10	Background
    BackPM	PM Peak	10	9	10/10	Background
    BackEvening	Evening	10	0	10/10	Background
    BackEvening	Evening	10	1	10/10	Background
    BackEvening	Evening	10	2	10/10	Background
    BackEvening	Evening	10	3	10/10	Background
    BackEvening	Evening	10	4	10/10	Background
    BackEvening	Evening	10	5	10/10	Background
    BackEvening	Evening	10	6	10/10	Background
    BackEvening	Evening	10	7	10/10	Background
    BackEvening	Evening	10	8	10/10	Background
    BackEvening	Evening	10	9	10/10	Background
    BackLate	Late	10	0	10/10	Background
    BackLate	Late	10	1	10/10	Background
    BackLate	Late	10	2	10/10	Background
    BackLate	Late	10	3	10/10	Background
    BackLate	Late	10	4	10/10	Background
    BackLate	Late	10	5	10/10	Background
    BackLate	Late	10	6	10/10	Background
    BackLate	Late	10	7	10/10	Background
    BackLate	Late	10	8	10/10	Background
    BackLate	Late	10	9	10/10	Background"""
            |> fromDelimited '\t'
```

```elm{l=hidden}
listOfTimes : List String
listOfTimes =
    [ "Please select time"
    , "0200-0230"
    , "0230-0300"
    , "0300-0330"
    , "0330-0400"
    , "0400-0430"
    , "0430-0500"
    , "0500-0530"
    , "0530-0600"
    , "0600-0630"
    , "0630-0700"
    , "0700-0730"
    , "0730-0800"
    , "0800-0830"
    , "0830-0900"
    , "0900-0930"
    , "0930-1000"
    , "1000-1030"
    , "1030-1100"
    , "1100-1130"
    , "1130-1200"
    , "1200-1230"
    , "1230-1300"
    , "1300-1330"
    , "1330-1400"
    , "1400-1430"
    , "1430-1500"
    , "1500-1530"
    , "1530-1600"
    , "1600-1630"
    , "1630-1700"
    , "1700-1730"
    , "1730-1800"
    , "1800-1830"
    , "1830-1900"
    , "1900-1930"
    , "1930-2000"
    , "2000-2030"
    , "2030-2100"
    , "2100-2130"
    , "2130-2200"
    , "2200-2230"
    , "2230-2300"
    , "2300-2330"
    , "2330-2400"
    , "0000-0030"
    , "0030-0100"
    , "0100-0130"
    , "0130-0200"
    ]


londonTubeFlow : Table
londonTubeFlow =
    """object	time	count	open
Acton Town	0430-0500	0	0
Acton Town	0500-0530	57	1
Acton Town	0530-0600	126	1
Acton Town	0600-0630	241	1
Acton Town	0630-0700	449	1
Acton Town	0700-0730	807	1
Acton Town	0730-0800	1069	1
Acton Town	0800-0830	1233	1
Acton Town	0830-0900	1026	1
Acton Town	0900-0930	677	1
Acton Town	0930-1000	454	1
Acton Town	1000-1030	350	1
Acton Town	1030-1100	314	1
Acton Town	1100-1130	326	1
Acton Town	1130-1200	305	1
Acton Town	1200-1230	333	1
Acton Town	1230-1300	331	1
Acton Town	1300-1330	344	1
Acton Town	1330-1400	353	1
Acton Town	1400-1430	365	1
Acton Town	1430-1500	375	1
Acton Town	1500-1530	481	1
Acton Town	1530-1600	590	1
Acton Town	1600-1630	661	1
Acton Town	1630-1700	690	1
Acton Town	1700-1730	803	1
Acton Town	1730-1800	882	1
Acton Town	1800-1830	880	1
Acton Town	1830-1900	777	1
Acton Town	1900-1930	614	1
Acton Town	1930-2000	472	1
Acton Town	2000-2030	370	1
Acton Town	2030-2100	323	1
Acton Town	2100-2130	292	1
Acton Town	2130-2200	273	1
Acton Town	2200-2230	277	1
Acton Town	2230-2300	265	1
Acton Town	2300-2330	244	1
Acton Town	2330-2400	199	1
Acton Town	0000-0030	141	1
Acton Town	0030-0100	92	1
Acton Town	0100-0130	36	1
Acton Town	0130-0200	16	1
Acton Town	0200-0230	0	0
Acton Town	0230-0300	0	0
Acton Town	0300-0330	0	0
Acton Town	0330-0400	0	0
Acton Town	0400-0430	0	0
Aldgate	0430-0500	0	0
Aldgate	0500-0530	34	1
Aldgate	0530-0600	35	1
Aldgate	0600-0630	146	1
Aldgate	0630-0700	389	1
Aldgate	0700-0730	787	1
Aldgate	0730-0800	1248	1
Aldgate	0800-0830	1941	1
Aldgate	0830-0900	2664	1
Aldgate	0900-0930	2251	1
Aldgate	0930-1000	1348	1
Aldgate	1000-1030	744	1
Aldgate	1030-1100	581	1
Aldgate	1100-1130	479	1
Aldgate	1130-1200	446	1
Aldgate	1200-1230	501	1
Aldgate	1230-1300	534	1
Aldgate	1300-1330	536	1
Aldgate	1330-1400	535	1
Aldgate	1400-1430	521	1
Aldgate	1430-1500	528	1
Aldgate	1500-1530	598	1
Aldgate	1530-1600	711	1
Aldgate	1600-1630	994	1
Aldgate	1630-1700	1321	1
Aldgate	1700-1730	2066	1
Aldgate	1730-1800	2367	1
Aldgate	1800-1830	1944	1
Aldgate	1830-1900	1242	1
Aldgate	1900-1930	806	1
Aldgate	1930-2000	540	1
Aldgate	2000-2030	403	1
Aldgate	2030-2100	357	1
Aldgate	2100-2130	322	1
Aldgate	2130-2200	275	1
Aldgate	2200-2230	252	1
Aldgate	2230-2300	233	1
Aldgate	2300-2330	190	1
Aldgate	2330-2400	142	1
Aldgate	0000-0030	71	1
Aldgate	0030-0100	21	1
Aldgate	0100-0130	0	1
Aldgate	0130-0200	0	1
Aldgate	0200-0230	0	0
Aldgate	0230-0300	0	0
Aldgate	0300-0330	0	0
Aldgate	0330-0400	0	0
Aldgate	0400-0430	0	0
Aldgate East	0430-0500	0	0
Aldgate East	0500-0530	31	1
Aldgate East	0530-0600	99	1
Aldgate East	0600-0630	172	1
Aldgate East	0630-0700	386	1
Aldgate East	0700-0730	691	1
Aldgate East	0730-0800	1191	1
Aldgate East	0800-0830	1874	1
Aldgate East	0830-0900	2733	1
Aldgate East	0900-0930	2563	1
Aldgate East	0930-1000	1826	1
Aldgate East	1000-1030	1175	1
Aldgate East	1030-1100	956	1
Aldgate East	1100-1130	859	1
Aldgate East	1130-1200	870	1
Aldgate East	1200-1230	920	1
Aldgate East	1230-1300	962	1
Aldgate East	1300-1330	997	1
Aldgate East	1330-1400	1008	1
Aldgate East	1400-1430	976	1
Aldgate East	1430-1500	997	1
Aldgate East	1500-1530	1055	1
Aldgate East	1530-1600	1153	1
Aldgate East	1600-1630	1342	1
Aldgate East	1630-1700	1602	1
Aldgate East	1700-1730	2178	1
Aldgate East	1730-1800	2508	1
Aldgate East	1800-1830	2443	1
Aldgate East	1830-1900	1888	1
Aldgate East	1900-1930	1373	1
Aldgate East	1930-2000	1038	1
Aldgate East	2000-2030	862	1
Aldgate East	2030-2100	771	1
Aldgate East	2100-2130	738	1
Aldgate East	2130-2200	639	1
Aldgate East	2200-2230	602	1
Aldgate East	2230-2300	584	1
Aldgate East	2300-2330	523	1
Aldgate East	2330-2400	422	1
Aldgate East	0000-0030	263	1
Aldgate East	0030-0100	112	1
Aldgate East	0100-0130	16	1
Aldgate East	0130-0200	0	1
Aldgate East	0200-0230	0	0
Aldgate East	0230-0300	0	0
Aldgate East	0300-0330	0	0
Aldgate East	0330-0400	0	0
Aldgate East	0400-0430	0	0
Alperton	0430-0500	0	0
Alperton	0500-0530	51	1
Alperton	0530-0600	104	1
Alperton	0600-0630	199	1
Alperton	0630-0700	333	1
Alperton	0700-0730	458	1
Alperton	0730-0800	487	1
Alperton	0800-0830	545	1
Alperton	0830-0900	458	1
Alperton	0900-0930	309	1
Alperton	0930-1000	213	1
Alperton	1000-1030	177	1
Alperton	1030-1100	160	1
Alperton	1100-1130	150	1
Alperton	1130-1200	152	1
Alperton	1200-1230	157	1
Alperton	1230-1300	168	1
Alperton	1300-1330	173	1
Alperton	1330-1400	185	1
Alperton	1400-1430	179	1
Alperton	1430-1500	200	1
Alperton	1500-1530	213	1
Alperton	1530-1600	288	1
Alperton	1600-1630	318	1
Alperton	1630-1700	368	1
Alperton	1700-1730	479	1
Alperton	1730-1800	557	1
Alperton	1800-1830	529	1
Alperton	1830-1900	418	1
Alperton	1900-1930	320	1
Alperton	1930-2000	231	1
Alperton	2000-2030	164	1
Alperton	2030-2100	142	1
Alperton	2100-2130	124	1
Alperton	2130-2200	104	1
Alperton	2200-2230	103	1
Alperton	2230-2300	105	1
Alperton	2300-2330	98	1
Alperton	2330-2400	76	1
Alperton	0000-0030	51	1
Alperton	0030-0100	25	1
Alperton	0100-0130	5	1
Alperton	0130-0200	0	1
Alperton	0200-0230	0	0
Alperton	0230-0300	0	0
Alperton	0300-0330	0	0
Alperton	0330-0400	0	0
Alperton	0400-0430	0	0
Amersham	0430-0500	0	0
Amersham	0500-0530	23	1
Amersham	0530-0600	80	1
Amersham	0600-0630	171	1
Amersham	0630-0700	286	1
Amersham	0700-0730	524	1
Amersham	0730-0800	698	1
Amersham	0800-0830	545	1
Amersham	0830-0900	325	1
Amersham	0900-0930	178	1
Amersham	0930-1000	144	1
Amersham	1000-1030	100	1
Amersham	1030-1100	94	1
Amersham	1100-1130	85	1
Amersham	1130-1200	76	1
Amersham	1200-1230	80	1
Amersham	1230-1300	83	1
Amersham	1300-1330	83	1
Amersham	1330-1400	79	1
Amersham	1400-1430	83	1
Amersham	1430-1500	104	1
Amersham	1500-1530	114	1
Amersham	1530-1600	288	1
Amersham	1600-1630	285	1
Amersham	1630-1700	271	1
Amersham	1700-1730	296	1
Amersham	1730-1800	309	1
Amersham	1800-1830	414	1
Amersham	1830-1900	425	1
Amersham	1900-1930	339	1
Amersham	1930-2000	266	1
Amersham	2000-2030	175	1
Amersham	2030-2100	142	1
Amersham	2100-2130	109	1
Amersham	2130-2200	108	1
Amersham	2200-2230	90	1
Amersham	2230-2300	93	1
Amersham	2300-2330	100	1
Amersham	2330-2400	99	1
Amersham	0000-0030	71	1
Amersham	0030-0100	32	1
Amersham	0100-0130	6	1
Amersham	0130-0200	0	1
Amersham	0200-0230	0	0
Amersham	0230-0300	0	0
Amersham	0300-0330	0	0
Amersham	0330-0400	0	0
Amersham	0400-0430	0	0
Angel	0430-0500	0	0
Angel	0500-0530	0	1
Angel	0530-0600	68	1
Angel	0600-0630	238	1
Angel	0630-0700	483	1
Angel	0700-0730	940	1
Angel	0730-0800	1624	1
Angel	0800-0830	2363	1
Angel	0830-0900	3481	1
Angel	0900-0930	3312	1
Angel	0930-1000	2413	1
Angel	1000-1030	1577	1
Angel	1030-1100	1417	1
Angel	1100-1130	1188	1
Angel	1130-1200	1234	1
Angel	1200-1230	1314	1
Angel	1230-1300	1359	1
Angel	1300-1330	1399	1
Angel	1330-1400	1309	1
Angel	1400-1430	1245	1
Angel	1430-1500	1334	1
Angel	1500-1530	1427	1
Angel	1530-1600	1562	1
Angel	1600-1630	1907	1
Angel	1630-1700	2287	1
Angel	1700-1730	2777	1
Angel	1730-1800	3229	1
Angel	1800-1830	3387	1
Angel	1830-1900	2869	1
Angel	1900-1930	2223	1
Angel	1930-2000	1600	1
Angel	2000-2030	1311	1
Angel	2030-2100	1212	1
Angel	2100-2130	1073	1
Angel	2130-2200	998	1
Angel	2200-2230	1070	1
Angel	2230-2300	1084	1
Angel	2300-2330	935	1
Angel	2330-2400	716	1
Angel	0000-0030	421	1
Angel	0030-0100	117	1
Angel	0100-0130	9	1
Angel	0130-0200	0	1
Angel	0200-0230	0	0
Angel	0230-0300	0	0
Angel	0300-0330	0	0
Angel	0330-0400	0	0
Angel	0400-0430	0	0
Archway	0430-0500	0	0
Archway	0500-0530	13	1
Archway	0530-0600	92	1
Archway	0600-0630	227	1
Archway	0630-0700	438	1
Archway	0700-0730	848	1
Archway	0730-0800	1387	1
Archway	0800-0830	1858	1
Archway	0830-0900	1844	1
Archway	0900-0930	1392	1
Archway	0930-1000	924	1
Archway	1000-1030	725	1
Archway	1030-1100	612	1
Archway	1100-1130	559	1
Archway	1130-1200	543	1
Archway	1200-1230	557	1
Archway	1230-1300	569	1
Archway	1300-1330	575	1
Archway	1330-1400	568	1
Archway	1400-1430	553	1
Archway	1430-1500	576	1
Archway	1500-1530	673	1
Archway	1530-1600	728	1
Archway	1600-1630	897	1
Archway	1630-1700	1078	1
Archway	1700-1730	1200	1
Archway	1730-1800	1352	1
Archway	1800-1830	1372	1
Archway	1830-1900	1269	1
Archway	1900-1930	1020	1
Archway	1930-2000	779	1
Archway	2000-2030	648	1
Archway	2030-2100	535	1
Archway	2100-2130	477	1
Archway	2130-2200	449	1
Archway	2200-2230	431	1
Archway	2230-2300	435	1
Archway	2300-2330	398	1
Archway	2330-2400	308	1
Archway	0000-0030	212	1
Archway	0030-0100	111	1
Archway	0100-0130	37	1
Archway	0130-0200	23	1
Archway	0200-0230	0	0
Archway	0230-0300	0	0
Archway	0300-0330	0	0
Archway	0330-0400	0	0
Archway	0400-0430	0	0
Arnos Grove	0430-0500	0	0
Arnos Grove	0500-0530	56	1
Arnos Grove	0530-0600	105	1
Arnos Grove	0600-0630	247	1
Arnos Grove	0630-0700	383	1
Arnos Grove	0700-0730	560	1
Arnos Grove	0730-0800	750	1
Arnos Grove	0800-0830	939	1
Arnos Grove	0830-0900	743	1
Arnos Grove	0900-0930	547	1
Arnos Grove	0930-1000	359	1
Arnos Grove	1000-1030	283	1
Arnos Grove	1030-1100	253	1
Arnos Grove	1100-1130	246	1
Arnos Grove	1130-1200	238	1
Arnos Grove	1200-1230	246	1
Arnos Grove	1230-1300	242	1
Arnos Grove	1300-1330	248	1
Arnos Grove	1330-1400	246	1
Arnos Grove	1400-1430	259	1
Arnos Grove	1430-1500	283	1
Arnos Grove	1500-1530	324	1
Arnos Grove	1530-1600	361	1
Arnos Grove	1600-1630	425	1
Arnos Grove	1630-1700	497	1
Arnos Grove	1700-1730	610	1
Arnos Grove	1730-1800	690	1
Arnos Grove	1800-1830	693	1
Arnos Grove	1830-1900	606	1
Arnos Grove	1900-1930	484	1
Arnos Grove	1930-2000	368	1
Arnos Grove	2000-2030	282	1
Arnos Grove	2030-2100	247	1
Arnos Grove	2100-2130	214	1
Arnos Grove	2130-2200	202	1
Arnos Grove	2200-2230	214	1
Arnos Grove	2230-2300	215	1
Arnos Grove	2300-2330	172	1
Arnos Grove	2330-2400	138	1
Arnos Grove	0000-0030	101	1
Arnos Grove	0030-0100	67	1
Arnos Grove	0100-0130	25	1
Arnos Grove	0130-0200	7	1
Arnos Grove	0200-0230	0	0
Arnos Grove	0230-0300	0	0
Arnos Grove	0300-0330	0	0
Arnos Grove	0330-0400	0	0
Arnos Grove	0400-0430	0	0
Arsenal	0430-0500	0	0
Arsenal	0500-0530	8	1
Arsenal	0530-0600	27	1
Arsenal	0600-0630	57	1
Arsenal	0630-0700	114	1
Arsenal	0700-0730	229	1
Arsenal	0730-0800	444	1
Arsenal	0800-0830	664	1
Arsenal	0830-0900	655	1
Arsenal	0900-0930	449	1
Arsenal	0930-1000	259	1
Arsenal	1000-1030	182	1
Arsenal	1030-1100	160	1
Arsenal	1100-1130	146	1
Arsenal	1130-1200	155	1
Arsenal	1200-1230	161	1
Arsenal	1230-1300	154	1
Arsenal	1300-1330	157	1
Arsenal	1330-1400	150	1
Arsenal	1400-1430	144	1
Arsenal	1430-1500	151	1
Arsenal	1500-1530	167	1
Arsenal	1530-1600	182	1
Arsenal	1600-1630	214	1
Arsenal	1630-1700	245	1
Arsenal	1700-1730	313	1
Arsenal	1730-1800	353	1
Arsenal	1800-1830	401	1
Arsenal	1830-1900	375	1
Arsenal	1900-1930	315	1
Arsenal	1930-2000	241	1
Arsenal	2000-2030	191	1
Arsenal	2030-2100	162	1
Arsenal	2100-2130	153	1
Arsenal	2130-2200	149	1
Arsenal	2200-2230	139	1
Arsenal	2230-2300	145	1
Arsenal	2300-2330	129	1
Arsenal	2330-2400	97	1
Arsenal	0000-0030	67	1
Arsenal	0030-0100	30	1
Arsenal	0100-0130	9	1
Arsenal	0130-0200	8	1
Arsenal	0200-0230	0	0
Arsenal	0230-0300	0	0
Arsenal	0300-0330	0	0
Arsenal	0330-0400	0	0
Arsenal	0400-0430	0	0
Baker Street	0430-0500	0	0
Baker Street	0500-0530	65	1
Baker Street	0530-0600	211	1
Baker Street	0600-0630	447	1
Baker Street	0630-0700	938	1
Baker Street	0700-0730	1830	1
Baker Street	0730-0800	3219	1
Baker Street	0800-0830	4807	1
Baker Street	0830-0900	5636	1
Baker Street	0900-0930	4571	1
Baker Street	0930-1000	3289	1
Baker Street	1000-1030	2464	1
Baker Street	1030-1100	2329	1
Baker Street	1100-1130	2058	1
Baker Street	1130-1200	2163	1
Baker Street	1200-1230	2262	1
Baker Street	1230-1300	2382	1
Baker Street	1300-1330	2354	1
Baker Street	1330-1400	2376	1
Baker Street	1400-1430	2302	1
Baker Street	1430-1500	2292	1
Baker Street	1500-1530	2434	1
Baker Street	1530-1600	2840	1
Baker Street	1600-1630	3238	1
Baker Street	1630-1700	3507	1
Baker Street	1700-1730	4575	1
Baker Street	1730-1800	5242	1
Baker Street	1800-1830	4837	1
Baker Street	1830-1900	3732	1
Baker Street	1900-1930	2656	1
Baker Street	1930-2000	1957	1
Baker Street	2000-2030	1571	1
Baker Street	2030-2100	1366	1
Baker Street	2100-2130	1207	1
Baker Street	2130-2200	1033	1
Baker Street	2200-2230	987	1
Baker Street	2230-2300	870	1
Baker Street	2300-2330	792	1
Baker Street	2330-2400	611	1
Baker Street	0000-0030	363	1
Baker Street	0030-0100	159	1
Baker Street	0100-0130	41	1
Baker Street	0130-0200	16	1
Baker Street	0200-0230	0	0
Baker Street	0230-0300	0	0
Baker Street	0300-0330	0	0
Baker Street	0330-0400	0	0
Baker Street	0400-0430	0	0
Balham	0430-0500	0	0
Balham	0500-0530	37	1
Balham	0530-0600	123	1
Balham	0600-0630	451	1
Balham	0630-0700	972	1
Balham	0700-0730	1689	1
Balham	0730-0800	2791	1
Balham	0800-0830	3264	1
Balham	0830-0900	2817	1
Balham	0900-0930	1918	1
Balham	0930-1000	1083	1
Balham	1000-1030	756	1
Balham	1030-1100	652	1
Balham	1100-1130	625	1
Balham	1130-1200	606	1
Balham	1200-1230	621	1
Balham	1230-1300	636	1
Balham	1300-1330	643	1
Balham	1330-1400	642	1
Balham	1400-1430	641	1
Balham	1430-1500	684	1
Balham	1500-1530	816	1
Balham	1530-1600	888	1
Balham	1600-1630	1094	1
Balham	1630-1700	1390	1
Balham	1700-1730	1771	1
Balham	1730-1800	2309	1
Balham	1800-1830	2511	1
Balham	1830-1900	2333	1
Balham	1900-1930	1856	1
Balham	1930-2000	1409	1
Balham	2000-2030	1049	1
Balham	2030-2100	884	1
Balham	2100-2130	785	1
Balham	2130-2200	749	1
Balham	2200-2230	730	1
Balham	2230-2300	716	1
Balham	2300-2330	657	1
Balham	2330-2400	562	1
Balham	0000-0030	332	1
Balham	0030-0100	177	1
Balham	0100-0130	64	1
Balham	0130-0200	28	1
Balham	0200-0230	0	0
Balham	0230-0300	0	0
Balham	0300-0330	0	0
Balham	0330-0400	0	0
Balham	0400-0430	0	0
Bank & Monument	0430-0500	0	0
Bank & Monument	0500-0530	31	1
Bank & Monument	0530-0600	360	1
Bank & Monument	0600-0630	1258	1
Bank & Monument	0630-0700	3447	1
Bank & Monument	0700-0730	5992	1
Bank & Monument	0730-0800	10265	1
Bank & Monument	0800-0830	14491	1
Bank & Monument	0830-0900	17965	1
Bank & Monument	0900-0930	14968	1
Bank & Monument	0930-1000	8105	1
Bank & Monument	1000-1030	4603	1
Bank & Monument	1030-1100	4047	1
Bank & Monument	1100-1130	3507	1
Bank & Monument	1130-1200	3799	1
Bank & Monument	1200-1230	4149	1
Bank & Monument	1230-1300	4116	1
Bank & Monument	1300-1330	3937	1
Bank & Monument	1330-1400	3998	1
Bank & Monument	1400-1430	3962	1
Bank & Monument	1430-1500	4085	1
Bank & Monument	1500-1530	4363	1
Bank & Monument	1530-1600	4724	1
Bank & Monument	1600-1630	6061	1
Bank & Monument	1630-1700	8194	1
Bank & Monument	1700-1730	13286	1
Bank & Monument	1730-1800	15248	1
Bank & Monument	1800-1830	14024	1
Bank & Monument	1830-1900	10768	1
Bank & Monument	1900-1930	7333	1
Bank & Monument	1930-2000	4870	1
Bank & Monument	2000-2030	3569	1
Bank & Monument	2030-2100	2841	1
Bank & Monument	2100-2130	2522	1
Bank & Monument	2130-2200	2224	1
Bank & Monument	2200-2230	1967	1
Bank & Monument	2230-2300	1693	1
Bank & Monument	2300-2330	1507	1
Bank & Monument	2330-2400	1070	1
Bank & Monument	0000-0030	580	1
Bank & Monument	0030-0100	202	1
Bank & Monument	0100-0130	84	1
Bank & Monument	0130-0200	41	1
Bank & Monument	0200-0230	0	0
Bank & Monument	0230-0300	0	0
Bank & Monument	0300-0330	0	0
Bank & Monument	0330-0400	0	0
Bank & Monument	0400-0430	0	0
Barbican	0430-0500	0	0
Barbican	0500-0530	15	1
Barbican	0530-0600	73	1
Barbican	0600-0630	175	1
Barbican	0630-0700	440	1
Barbican	0700-0730	768	1
Barbican	0730-0800	1286	1
Barbican	0800-0830	2004	1
Barbican	0830-0900	2854	1
Barbican	0900-0930	2757	1
Barbican	0930-1000	1892	1
Barbican	1000-1030	1122	1
Barbican	1030-1100	965	1
Barbican	1100-1130	774	1
Barbican	1130-1200	793	1
Barbican	1200-1230	851	1
Barbican	1230-1300	889	1
Barbican	1300-1330	894	1
Barbican	1330-1400	886	1
Barbican	1400-1430	871	1
Barbican	1430-1500	874	1
Barbican	1500-1530	983	1
Barbican	1530-1600	1094	1
Barbican	1600-1630	1442	1
Barbican	1630-1700	1635	1
Barbican	1700-1730	2211	1
Barbican	1730-1800	2582	1
Barbican	1800-1830	2270	1
Barbican	1830-1900	1666	1
Barbican	1900-1930	1224	1
Barbican	1930-2000	809	1
Barbican	2000-2030	657	1
Barbican	2030-2100	521	1
Barbican	2100-2130	483	1
Barbican	2130-2200	644	1
Barbican	2200-2230	608	1
Barbican	2230-2300	504	1
Barbican	2300-2330	342	1
Barbican	2330-2400	211	1
Barbican	0000-0030	97	1
Barbican	0030-0100	25	1
Barbican	0100-0130	1	1
Barbican	0130-0200	0	1
Barbican	0200-0230	0	0
Barbican	0230-0300	0	0
Barbican	0300-0330	0	0
Barbican	0330-0400	0	0
Barbican	0400-0430	0	0
Barking	0430-0500	0	0
Barking	0500-0530	475	1
Barking	0530-0600	994	1
Barking	0600-0630	1933	1
Barking	0630-0700	2436	1
Barking	0700-0730	2510	1
Barking	0730-0800	2616	1
Barking	0800-0830	2905	1
Barking	0830-0900	2465	1
Barking	0900-0930	1930	1
Barking	0930-1000	1441	1
Barking	1000-1030	1122	1
Barking	1030-1100	976	1
Barking	1100-1130	960	1
Barking	1130-1200	926	1
Barking	1200-1230	942	1
Barking	1230-1300	976	1
Barking	1300-1330	1017	1
Barking	1330-1400	1032	1
Barking	1400-1430	1083	1
Barking	1430-1500	1171	1
Barking	1500-1530	1270	1
Barking	1530-1600	1590	1
Barking	1600-1630	1927	1
Barking	1630-1700	2293	1
Barking	1700-1730	2740	1
Barking	1730-1800	2922	1
Barking	1800-1830	2926	1
Barking	1830-1900	2480	1
Barking	1900-1930	1868	1
Barking	1930-2000	1392	1
Barking	2000-2030	1136	1
Barking	2030-2100	969	1
Barking	2100-2130	864	1
Barking	2130-2200	763	1
Barking	2200-2230	667	1
Barking	2230-2300	568	1
Barking	2300-2330	438	1
Barking	2330-2400	383	1
Barking	0000-0030	257	1
Barking	0030-0100	150	1
Barking	0100-0130	58	1
Barking	0130-0200	4	1
Barking	0200-0230	0	0
Barking	0230-0300	0	0
Barking	0300-0330	0	0
Barking	0330-0400	0	0
Barking	0400-0430	0	0
Barkingside	0430-0500	0	0
Barkingside	0500-0530	33	1
Barkingside	0530-0600	91	1
Barkingside	0600-0630	167	1
Barkingside	0630-0700	245	1
Barkingside	0700-0730	247	1
Barkingside	0730-0800	331	1
Barkingside	0800-0830	450	1
Barkingside	0830-0900	319	1
Barkingside	0900-0930	158	1
Barkingside	0930-1000	107	1
Barkingside	1000-1030	81	1
Barkingside	1030-1100	64	1
Barkingside	1100-1130	59	1
Barkingside	1130-1200	56	1
Barkingside	1200-1230	61	1
Barkingside	1230-1300	63	1
Barkingside	1300-1330	67	1
Barkingside	1330-1400	65	1
Barkingside	1400-1430	74	1
Barkingside	1430-1500	91	1
Barkingside	1500-1530	134	1
Barkingside	1530-1600	134	1
Barkingside	1600-1630	157	1
Barkingside	1630-1700	199	1
Barkingside	1700-1730	259	1
Barkingside	1730-1800	291	1
Barkingside	1800-1830	284	1
Barkingside	1830-1900	263	1
Barkingside	1900-1930	201	1
Barkingside	1930-2000	134	1
Barkingside	2000-2030	89	1
Barkingside	2030-2100	72	1
Barkingside	2100-2130	65	1
Barkingside	2130-2200	53	1
Barkingside	2200-2230	53	1
Barkingside	2230-2300	47	1
Barkingside	2300-2330	42	1
Barkingside	2330-2400	34	1
Barkingside	0000-0030	22	1
Barkingside	0030-0100	14	1
Barkingside	0100-0130	5	1
Barkingside	0130-0200	3	1
Barkingside	0200-0230	0	0
Barkingside	0230-0300	0	0
Barkingside	0300-0330	0	0
Barkingside	0330-0400	0	0
Barkingside	0400-0430	0	0
Barons Court	0430-0500	0	0
Barons Court	0500-0530	12	1
Barons Court	0530-0600	45	1
Barons Court	0600-0630	123	1
Barons Court	0630-0700	255	1
Barons Court	0700-0730	551	1
Barons Court	0730-0800	1026	1
Barons Court	0800-0830	1674	1
Barons Court	0830-0900	1945	1
Barons Court	0900-0930	1449	1
Barons Court	0930-1000	926	1
Barons Court	1000-1030	572	1
Barons Court	1030-1100	457	1
Barons Court	1100-1130	417	1
Barons Court	1130-1200	398	1
Barons Court	1200-1230	445	1
Barons Court	1230-1300	461	1
Barons Court	1300-1330	473	1
Barons Court	1330-1400	439	1
Barons Court	1400-1430	425	1
Barons Court	1430-1500	443	1
Barons Court	1500-1530	529	1
Barons Court	1530-1600	559	1
Barons Court	1600-1630	705	1
Barons Court	1630-1700	793	1
Barons Court	1700-1730	1028	1
Barons Court	1730-1800	1158	1
Barons Court	1800-1830	1097	1
Barons Court	1830-1900	926	1
Barons Court	1900-1930	675	1
Barons Court	1930-2000	504	1
Barons Court	2000-2030	405	1
Barons Court	2030-2100	365	1
Barons Court	2100-2130	348	1
Barons Court	2130-2200	305	1
Barons Court	2200-2230	289	1
Barons Court	2230-2300	282	1
Barons Court	2300-2330	238	1
Barons Court	2330-2400	181	1
Barons Court	0000-0030	116	1
Barons Court	0030-0100	63	1
Barons Court	0100-0130	26	1
Barons Court	0130-0200	19	1
Barons Court	0200-0230	0	0
Barons Court	0230-0300	0	0
Barons Court	0300-0330	0	0
Barons Court	0330-0400	0	0
Barons Court	0400-0430	0	0
Bayswater	0430-0500	0	0
Bayswater	0500-0530	18	1
Bayswater	0530-0600	29	1
Bayswater	0600-0630	50	1
Bayswater	0630-0700	106	1
Bayswater	0700-0730	184	1
Bayswater	0730-0800	288	1
Bayswater	0800-0830	396	1
Bayswater	0830-0900	459	1
Bayswater	0900-0930	506	1
Bayswater	0930-1000	505	1
Bayswater	1000-1030	447	1
Bayswater	1030-1100	394	1
Bayswater	1100-1130	333	1
Bayswater	1130-1200	308	1
Bayswater	1200-1230	325	1
Bayswater	1230-1300	307	1
Bayswater	1300-1330	336	1
Bayswater	1330-1400	339	1
Bayswater	1400-1430	366	1
Bayswater	1430-1500	377	1
Bayswater	1500-1530	387	1
Bayswater	1530-1600	414	1
Bayswater	1600-1630	436	1
Bayswater	1630-1700	478	1
Bayswater	1700-1730	520	1
Bayswater	1730-1800	565	1
Bayswater	1800-1830	588	1
Bayswater	1830-1900	565	1
Bayswater	1900-1930	476	1
Bayswater	1930-2000	394	1
Bayswater	2000-2030	345	1
Bayswater	2030-2100	319	1
Bayswater	2100-2130	298	1
Bayswater	2130-2200	267	1
Bayswater	2200-2230	280	1
Bayswater	2230-2300	293	1
Bayswater	2300-2330	268	1
Bayswater	2330-2400	183	1
Bayswater	0000-0030	86	1
Bayswater	0030-0100	20	1
Bayswater	0100-0130	0	1
Bayswater	0130-0200	0	1
Bayswater	0200-0230	0	0
Bayswater	0230-0300	0	0
Bayswater	0300-0330	0	0
Bayswater	0330-0400	0	0
Bayswater	0400-0430	0	0
Becontree	0430-0500	0	0
Becontree	0500-0530	110	1
Becontree	0530-0600	234	1
Becontree	0600-0630	501	1
Becontree	0630-0700	543	1
Becontree	0700-0730	549	1
Becontree	0730-0800	618	1
Becontree	0800-0830	660	1
Becontree	0830-0900	462	1
Becontree	0900-0930	347	1
Becontree	0930-1000	242	1
Becontree	1000-1030	197	1
Becontree	1030-1100	183	1
Becontree	1100-1130	187	1
Becontree	1130-1200	168	1
Becontree	1200-1230	176	1
Becontree	1230-1300	175	1
Becontree	1300-1330	184	1
Becontree	1330-1400	194	1
Becontree	1400-1430	208	1
Becontree	1430-1500	238	1
Becontree	1500-1530	274	1
Becontree	1530-1600	361	1
Becontree	1600-1630	405	1
Becontree	1630-1700	490	1
Becontree	1700-1730	546	1
Becontree	1730-1800	574	1
Becontree	1800-1830	589	1
Becontree	1830-1900	492	1
Becontree	1900-1930	344	1
Becontree	1930-2000	267	1
Becontree	2000-2030	213	1
Becontree	2030-2100	172	1
Becontree	2100-2130	159	1
Becontree	2130-2200	135	1
Becontree	2200-2230	112	1
Becontree	2230-2300	100	1
Becontree	2300-2330	90	1
Becontree	2330-2400	80	1
Becontree	0000-0030	50	1
Becontree	0030-0100	28	1
Becontree	0100-0130	14	1
Becontree	0130-0200	1	1
Becontree	0200-0230	0	0
Becontree	0230-0300	0	0
Becontree	0300-0330	0	0
Becontree	0330-0400	0	0
Becontree	0400-0430	0	0
Belsize Park	0430-0500	0	0
Belsize Park	0500-0530	5	1
Belsize Park	0530-0600	30	1
Belsize Park	0600-0630	104	1
Belsize Park	0630-0700	230	1
Belsize Park	0700-0730	518	1
Belsize Park	0730-0800	823	1
Belsize Park	0800-0830	1064	1
Belsize Park	0830-0900	1218	1
Belsize Park	0900-0930	967	1
Belsize Park	0930-1000	652	1
Belsize Park	1000-1030	509	1
Belsize Park	1030-1100	463	1
Belsize Park	1100-1130	448	1
Belsize Park	1130-1200	447	1
Belsize Park	1200-1230	459	1
Belsize Park	1230-1300	496	1
Belsize Park	1300-1330	497	1
Belsize Park	1330-1400	504	1
Belsize Park	1400-1430	476	1
Belsize Park	1430-1500	497	1
Belsize Park	1500-1530	545	1
Belsize Park	1530-1600	619	1
Belsize Park	1600-1630	700	1
Belsize Park	1630-1700	784	1
Belsize Park	1700-1730	907	1
Belsize Park	1730-1800	858	1
Belsize Park	1800-1830	841	1
Belsize Park	1830-1900	761	1
Belsize Park	1900-1930	658	1
Belsize Park	1930-2000	537	1
Belsize Park	2000-2030	474	1
Belsize Park	2030-2100	369	1
Belsize Park	2100-2130	309	1
Belsize Park	2130-2200	266	1
Belsize Park	2200-2230	250	1
Belsize Park	2230-2300	239	1
Belsize Park	2300-2330	204	1
Belsize Park	2330-2400	174	1
Belsize Park	0000-0030	108	1
Belsize Park	0030-0100	47	1
Belsize Park	0100-0130	11	1
Belsize Park	0130-0200	7	1
Belsize Park	0200-0230	0	0
Belsize Park	0230-0300	0	0
Belsize Park	0300-0330	0	0
Belsize Park	0330-0400	0	0
Belsize Park	0400-0430	0	0
Bermondsey	0430-0500	0	0
Bermondsey	0500-0530	59	1
Bermondsey	0530-0600	207	1
Bermondsey	0600-0630	408	1
Bermondsey	0630-0700	730	1
Bermondsey	0700-0730	1137	1
Bermondsey	0730-0800	1509	1
Bermondsey	0800-0830	1894	1
Bermondsey	0830-0900	1974	1
Bermondsey	0900-0930	1546	1
Bermondsey	0930-1000	1000	1
Bermondsey	1000-1030	644	1
Bermondsey	1030-1100	556	1
Bermondsey	1100-1130	498	1
Bermondsey	1130-1200	493	1
Bermondsey	1200-1230	499	1
Bermondsey	1230-1300	509	1
Bermondsey	1300-1330	515	1
Bermondsey	1330-1400	529	1
Bermondsey	1400-1430	551	1
Bermondsey	1430-1500	599	1
Bermondsey	1500-1530	697	1
Bermondsey	1530-1600	844	1
Bermondsey	1600-1630	971	1
Bermondsey	1630-1700	1131	1
Bermondsey	1700-1730	1382	1
Bermondsey	1730-1800	1647	1
Bermondsey	1800-1830	1766	1
Bermondsey	1830-1900	1525	1
Bermondsey	1900-1930	1164	1
Bermondsey	1930-2000	907	1
Bermondsey	2000-2030	754	1
Bermondsey	2030-2100	654	1
Bermondsey	2100-2130	596	1
Bermondsey	2130-2200	551	1
Bermondsey	2200-2230	516	1
Bermondsey	2230-2300	491	1
Bermondsey	2300-2330	427	1
Bermondsey	2330-2400	348	1
Bermondsey	0000-0030	224	1
Bermondsey	0030-0100	116	1
Bermondsey	0100-0130	38	1
Bermondsey	0130-0200	18	1
Bermondsey	0200-0230	0	0
Bermondsey	0230-0300	0	0
Bermondsey	0300-0330	0	0
Bermondsey	0330-0400	0	0
Bermondsey	0400-0430	0	0
Bethnal Green	0430-0500	0	0
Bethnal Green	0500-0530	12	1
Bethnal Green	0530-0600	158	1
Bethnal Green	0600-0630	456	1
Bethnal Green	0630-0700	736	1
Bethnal Green	0700-0730	1210	1
Bethnal Green	0730-0800	1690	1
Bethnal Green	0800-0830	2116	1
Bethnal Green	0830-0900	2119	1
Bethnal Green	0900-0930	2036	1
Bethnal Green	0930-1000	1581	1
Bethnal Green	1000-1030	1095	1
Bethnal Green	1030-1100	960	1
Bethnal Green	1100-1130	888	1
Bethnal Green	1130-1200	885	1
Bethnal Green	1200-1230	869	1
Bethnal Green	1230-1300	921	1
Bethnal Green	1300-1330	947	1
Bethnal Green	1330-1400	947	1
Bethnal Green	1400-1430	966	1
Bethnal Green	1430-1500	1032	1
Bethnal Green	1500-1530	1138	1
Bethnal Green	1530-1600	1291	1
Bethnal Green	1600-1630	1433	1
Bethnal Green	1630-1700	1594	1
Bethnal Green	1700-1730	1813	1
Bethnal Green	1730-1800	2069	1
Bethnal Green	1800-1830	2245	1
Bethnal Green	1830-1900	2149	1
Bethnal Green	1900-1930	1731	1
Bethnal Green	1930-2000	1374	1
Bethnal Green	2000-2030	1114	1
Bethnal Green	2030-2100	963	1
Bethnal Green	2100-2130	910	1
Bethnal Green	2130-2200	885	1
Bethnal Green	2200-2230	869	1
Bethnal Green	2230-2300	852	1
Bethnal Green	2300-2330	789	1
Bethnal Green	2330-2400	636	1
Bethnal Green	0000-0030	429	1
Bethnal Green	0030-0100	219	1
Bethnal Green	0100-0130	85	1
Bethnal Green	0130-0200	47	1
Bethnal Green	0200-0230	0	0
Bethnal Green	0230-0300	0	0
Bethnal Green	0300-0330	0	0
Bethnal Green	0330-0400	0	0
Bethnal Green	0400-0430	0	0
Blackfriars	0430-0500	0	0
Blackfriars	0500-0530	18	1
Blackfriars	0530-0600	98	1
Blackfriars	0600-0630	281	1
Blackfriars	0630-0700	682	1
Blackfriars	0700-0730	1283	1
Blackfriars	0730-0800	2137	1
Blackfriars	0800-0830	3443	1
Blackfriars	0830-0900	4481	1
Blackfriars	0900-0930	3935	1
Blackfriars	0930-1000	2148	1
Blackfriars	1000-1030	1122	1
Blackfriars	1030-1100	927	1
Blackfriars	1100-1130	804	1
Blackfriars	1130-1200	811	1
Blackfriars	1200-1230	869	1
Blackfriars	1230-1300	892	1
Blackfriars	1300-1330	881	1
Blackfriars	1330-1400	874	1
Blackfriars	1400-1430	850	1
Blackfriars	1430-1500	879	1
Blackfriars	1500-1530	991	1
Blackfriars	1530-1600	1164	1
Blackfriars	1600-1630	1523	1
Blackfriars	1630-1700	1835	1
Blackfriars	1700-1730	3030	1
Blackfriars	1730-1800	3696	1
Blackfriars	1800-1830	3184	1
Blackfriars	1830-1900	2258	1
Blackfriars	1900-1930	1520	1
Blackfriars	1930-2000	1000	1
Blackfriars	2000-2030	747	1
Blackfriars	2030-2100	583	1
Blackfriars	2100-2130	508	1
Blackfriars	2130-2200	466	1
Blackfriars	2200-2230	435	1
Blackfriars	2230-2300	370	1
Blackfriars	2300-2330	334	1
Blackfriars	2330-2400	217	1
Blackfriars	0000-0030	118	1
Blackfriars	0030-0100	42	1
Blackfriars	0100-0130	1	1
Blackfriars	0130-0200	0	1
Blackfriars	0200-0230	0	0
Blackfriars	0230-0300	0	0
Blackfriars	0300-0330	0	0
Blackfriars	0330-0400	0	0
Blackfriars	0400-0430	0	0
Blackhorse Road	0430-0500	0	0
Blackhorse Road	0500-0530	115	1
Blackhorse Road	0530-0600	288	1
Blackhorse Road	0600-0630	568	1
Blackhorse Road	0630-0700	1028	1
Blackhorse Road	0700-0730	1297	1
Blackhorse Road	0730-0800	1329	1
Blackhorse Road	0800-0830	1766	1
Blackhorse Road	0830-0900	1541	1
Blackhorse Road	0900-0930	1183	1
Blackhorse Road	0930-1000	704	1
Blackhorse Road	1000-1030	505	1
Blackhorse Road	1030-1100	421	1
Blackhorse Road	1100-1130	405	1
Blackhorse Road	1130-1200	377	1
Blackhorse Road	1200-1230	386	1
Blackhorse Road	1230-1300	399	1
Blackhorse Road	1300-1330	419	1
Blackhorse Road	1330-1400	420	1
Blackhorse Road	1400-1430	432	1
Blackhorse Road	1430-1500	476	1
Blackhorse Road	1500-1530	532	1
Blackhorse Road	1530-1600	619	1
Blackhorse Road	1600-1630	801	1
Blackhorse Road	1630-1700	1017	1
Blackhorse Road	1700-1730	1285	1
Blackhorse Road	1730-1800	1470	1
Blackhorse Road	1800-1830	1418	1
Blackhorse Road	1830-1900	1283	1
Blackhorse Road	1900-1930	975	1
Blackhorse Road	1930-2000	712	1
Blackhorse Road	2000-2030	576	1
Blackhorse Road	2030-2100	528	1
Blackhorse Road	2100-2130	459	1
Blackhorse Road	2130-2200	451	1
Blackhorse Road	2200-2230	436	1
Blackhorse Road	2230-2300	431	1
Blackhorse Road	2300-2330	380	1
Blackhorse Road	2330-2400	348	1
Blackhorse Road	0000-0030	227	1
Blackhorse Road	0030-0100	126	1
Blackhorse Road	0100-0130	55	1
Blackhorse Road	0130-0200	16	1
Blackhorse Road	0200-0230	0	0
Blackhorse Road	0230-0300	0	0
Blackhorse Road	0300-0330	0	0
Blackhorse Road	0330-0400	0	0
Blackhorse Road	0400-0430	0	0
Bond Street	0430-0500	0	0
Bond Street	0500-0530	48	1
Bond Street	0530-0600	253	1
Bond Street	0600-0630	544	1
Bond Street	0630-0700	1166	1
Bond Street	0700-0730	1745	1
Bond Street	0730-0800	2920	1
Bond Street	0800-0830	3949	1
Bond Street	0830-0900	5735	1
Bond Street	0900-0930	5148	1
Bond Street	0930-1000	3632	1
Bond Street	1000-1030	2762	1
Bond Street	1030-1100	2833	1
Bond Street	1100-1130	2672	1
Bond Street	1130-1200	2928	1
Bond Street	1200-1230	3239	1
Bond Street	1230-1300	3492	1
Bond Street	1300-1330	3392	1
Bond Street	1330-1400	3524	1
Bond Street	1400-1430	3431	1
Bond Street	1430-1500	3497	1
Bond Street	1500-1530	3594	1
Bond Street	1530-1600	3907	1
Bond Street	1600-1630	4324	1
Bond Street	1630-1700	4960	1
Bond Street	1700-1730	6268	1
Bond Street	1730-1800	7622	1
Bond Street	1800-1830	7415	1
Bond Street	1830-1900	5810	1
Bond Street	1900-1930	4259	1
Bond Street	1930-2000	3059	1
Bond Street	2000-2030	2609	1
Bond Street	2030-2100	2105	1
Bond Street	2100-2130	1941	1
Bond Street	2130-2200	1689	1
Bond Street	2200-2230	1478	1
Bond Street	2230-2300	1216	1
Bond Street	2300-2330	912	1
Bond Street	2330-2400	643	1
Bond Street	0000-0030	412	1
Bond Street	0030-0100	146	1
Bond Street	0100-0130	51	1
Bond Street	0130-0200	28	1
Bond Street	0200-0230	0	0
Bond Street	0230-0300	0	0
Bond Street	0300-0330	0	0
Bond Street	0330-0400	0	0
Bond Street	0400-0430	0	0
Borough	0430-0500	0	0
Borough	0500-0530	4	1
Borough	0530-0600	31	1
Borough	0600-0630	83	1
Borough	0630-0700	200	1
Borough	0700-0730	326	1
Borough	0730-0800	549	1
Borough	0800-0830	898	1
Borough	0830-0900	1298	1
Borough	0900-0930	1222	1
Borough	0930-1000	854	1
Borough	1000-1030	505	1
Borough	1030-1100	423	1
Borough	1100-1130	374	1
Borough	1130-1200	366	1
Borough	1200-1230	382	1
Borough	1230-1300	406	1
Borough	1300-1330	417	1
Borough	1330-1400	429	1
Borough	1400-1430	394	1
Borough	1430-1500	415	1
Borough	1500-1530	454	1
Borough	1530-1600	512	1
Borough	1600-1630	609	1
Borough	1630-1700	721	1
Borough	1700-1730	910	1
Borough	1730-1800	1064	1
Borough	1800-1830	993	1
Borough	1830-1900	769	1
Borough	1900-1930	573	1
Borough	1930-2000	428	1
Borough	2000-2030	350	1
Borough	2030-2100	309	1
Borough	2100-2130	286	1
Borough	2130-2200	265	1
Borough	2200-2230	273	1
Borough	2230-2300	254	1
Borough	2300-2330	223	1
Borough	2330-2400	152	1
Borough	0000-0030	93	1
Borough	0030-0100	29	1
Borough	0100-0130	0	1
Borough	0130-0200	0	1
Borough	0200-0230	0	0
Borough	0230-0300	0	0
Borough	0300-0330	0	0
Borough	0330-0400	0	0
Borough	0400-0430	0	0
Boston Manor	0430-0500	0	0
Boston Manor	0500-0530	29	1
Boston Manor	0530-0600	43	1
Boston Manor	0600-0630	96	1
Boston Manor	0630-0700	141	1
Boston Manor	0700-0730	254	1
Boston Manor	0730-0800	438	1
Boston Manor	0800-0830	643	1
Boston Manor	0830-0900	528	1
Boston Manor	0900-0930	329	1
Boston Manor	0930-1000	198	1
Boston Manor	1000-1030	143	1
Boston Manor	1030-1100	118	1
Boston Manor	1100-1130	116	1
Boston Manor	1130-1200	109	1
Boston Manor	1200-1230	111	1
Boston Manor	1230-1300	121	1
Boston Manor	1300-1330	122	1
Boston Manor	1330-1400	120	1
Boston Manor	1400-1430	124	1
Boston Manor	1430-1500	133	1
Boston Manor	1500-1530	180	1
Boston Manor	1530-1600	212	1
Boston Manor	1600-1630	233	1
Boston Manor	1630-1700	271	1
Boston Manor	1700-1730	335	1
Boston Manor	1730-1800	351	1
Boston Manor	1800-1830	325	1
Boston Manor	1830-1900	282	1
Boston Manor	1900-1930	212	1
Boston Manor	1930-2000	159	1
Boston Manor	2000-2030	123	1
Boston Manor	2030-2100	108	1
Boston Manor	2100-2130	100	1
Boston Manor	2130-2200	93	1
Boston Manor	2200-2230	96	1
Boston Manor	2230-2300	91	1
Boston Manor	2300-2330	85	1
Boston Manor	2330-2400	59	1
Boston Manor	0000-0030	39	1
Boston Manor	0030-0100	21	1
Boston Manor	0100-0130	12	1
Boston Manor	0130-0200	4	1
Boston Manor	0200-0230	0	0
Boston Manor	0230-0300	0	0
Boston Manor	0300-0330	0	0
Boston Manor	0330-0400	0	0
Boston Manor	0400-0430	0	0
Bounds Green	0430-0500	0	0
Bounds Green	0500-0530	72	1
Bounds Green	0530-0600	164	1
Bounds Green	0600-0630	381	1
Bounds Green	0630-0700	612	1
Bounds Green	0700-0730	792	1
Bounds Green	0730-0800	987	1
Bounds Green	0800-0830	1283	1
Bounds Green	0830-0900	1110	1
Bounds Green	0900-0930	856	1
Bounds Green	0930-1000	543	1
Bounds Green	1000-1030	388	1
Bounds Green	1030-1100	329	1
Bounds Green	1100-1130	318	1
Bounds Green	1130-1200	292	1
Bounds Green	1200-1230	300	1
Bounds Green	1230-1300	298	1
Bounds Green	1300-1330	312	1
Bounds Green	1330-1400	311	1
Bounds Green	1400-1430	315	1
Bounds Green	1430-1500	344	1
Bounds Green	1500-1530	395	1
Bounds Green	1530-1600	440	1
Bounds Green	1600-1630	526	1
Bounds Green	1630-1700	632	1
Bounds Green	1700-1730	758	1
Bounds Green	1730-1800	912	1
Bounds Green	1800-1830	992	1
Bounds Green	1830-1900	883	1
Bounds Green	1900-1930	721	1
Bounds Green	1930-2000	556	1
Bounds Green	2000-2030	429	1
Bounds Green	2030-2100	367	1
Bounds Green	2100-2130	328	1
Bounds Green	2130-2200	301	1
Bounds Green	2200-2230	315	1
Bounds Green	2230-2300	312	1
Bounds Green	2300-2330	280	1
Bounds Green	2330-2400	240	1
Bounds Green	0000-0030	168	1
Bounds Green	0030-0100	102	1
Bounds Green	0100-0130	28	1
Bounds Green	0130-0200	13	1
Bounds Green	0200-0230	0	0
Bounds Green	0230-0300	0	0
Bounds Green	0300-0330	0	0
Bounds Green	0330-0400	0	0
Bounds Green	0400-0430	0	0
Bow Road	0430-0500	0	0
Bow Road	0500-0530	35	1
Bow Road	0530-0600	89	1
Bow Road	0600-0630	200	1
Bow Road	0630-0700	337	1
Bow Road	0700-0730	511	1
Bow Road	0730-0800	832	1
Bow Road	0800-0830	1283	1
Bow Road	0830-0900	1237	1
Bow Road	0900-0930	803	1
Bow Road	0930-1000	496	1
Bow Road	1000-1030	356	1
Bow Road	1030-1100	307	1
Bow Road	1100-1130	298	1
Bow Road	1130-1200	280	1
Bow Road	1200-1230	269	1
Bow Road	1230-1300	277	1
Bow Road	1300-1330	289	1
Bow Road	1330-1400	284	1
Bow Road	1400-1430	301	1
Bow Road	1430-1500	336	1
Bow Road	1500-1530	425	1
Bow Road	1530-1600	449	1
Bow Road	1600-1630	484	1
Bow Road	1630-1700	537	1
Bow Road	1700-1730	626	1
Bow Road	1730-1800	726	1
Bow Road	1800-1830	820	1
Bow Road	1830-1900	804	1
Bow Road	1900-1930	640	1
Bow Road	1930-2000	481	1
Bow Road	2000-2030	391	1
Bow Road	2030-2100	349	1
Bow Road	2100-2130	309	1
Bow Road	2130-2200	309	1
Bow Road	2200-2230	300	1
Bow Road	2230-2300	287	1
Bow Road	2300-2330	276	1
Bow Road	2330-2400	237	1
Bow Road	0000-0030	175	1
Bow Road	0030-0100	97	1
Bow Road	0100-0130	22	1
Bow Road	0130-0200	0	1
Bow Road	0200-0230	0	0
Bow Road	0230-0300	0	0
Bow Road	0300-0330	0	0
Bow Road	0330-0400	0	0
Bow Road	0400-0430	0	0
Brent Cross	0430-0500	0	0
Brent Cross	0500-0530	10	1
Brent Cross	0530-0600	45	1
Brent Cross	0600-0630	134	1
Brent Cross	0630-0700	202	1
Brent Cross	0700-0730	248	1
Brent Cross	0730-0800	333	1
Brent Cross	0800-0830	499	1
Brent Cross	0830-0900	453	1
Brent Cross	0900-0930	280	1
Brent Cross	0930-1000	203	1
Brent Cross	1000-1030	160	1
Brent Cross	1030-1100	144	1
Brent Cross	1100-1130	133	1
Brent Cross	1130-1200	132	1
Brent Cross	1200-1230	142	1
Brent Cross	1230-1300	156	1
Brent Cross	1300-1330	171	1
Brent Cross	1330-1400	165	1
Brent Cross	1400-1430	168	1
Brent Cross	1430-1500	180	1
Brent Cross	1500-1530	195	1
Brent Cross	1530-1600	228	1
Brent Cross	1600-1630	268	1
Brent Cross	1630-1700	289	1
Brent Cross	1700-1730	351	1
Brent Cross	1730-1800	432	1
Brent Cross	1800-1830	398	1
Brent Cross	1830-1900	330	1
Brent Cross	1900-1930	249	1
Brent Cross	1930-2000	194	1
Brent Cross	2000-2030	169	1
Brent Cross	2030-2100	134	1
Brent Cross	2100-2130	110	1
Brent Cross	2130-2200	102	1
Brent Cross	2200-2230	105	1
Brent Cross	2230-2300	108	1
Brent Cross	2300-2330	86	1
Brent Cross	2330-2400	66	1
Brent Cross	0000-0030	52	1
Brent Cross	0030-0100	31	1
Brent Cross	0100-0130	10	1
Brent Cross	0130-0200	6	1
Brent Cross	0200-0230	0	0
Brent Cross	0230-0300	0	0
Brent Cross	0300-0330	0	0
Brent Cross	0330-0400	0	0
Brent Cross	0400-0430	0	0
Brixton	0430-0500	0	0
Brixton	0500-0530	207	1
Brixton	0530-0600	512	1
Brixton	0600-0630	1062	1
Brixton	0630-0700	1959	1
Brixton	0700-0730	3305	1
Brixton	0730-0800	4653	1
Brixton	0800-0830	6401	1
Brixton	0830-0900	6295	1
Brixton	0900-0930	4374	1
Brixton	0930-1000	2744	1
Brixton	1000-1030	1783	1
Brixton	1030-1100	1542	1
Brixton	1100-1130	1402	1
Brixton	1130-1200	1393	1
Brixton	1200-1230	1398	1
Brixton	1230-1300	1458	1
Brixton	1300-1330	1503	1
Brixton	1330-1400	1531	1
Brixton	1400-1430	1556	1
Brixton	1430-1500	1645	1
Brixton	1500-1530	1724	1
Brixton	1530-1600	1968	1
Brixton	1600-1630	2446	1
Brixton	1630-1700	2947	1
Brixton	1700-1730	3641	1
Brixton	1730-1800	4528	1
Brixton	1800-1830	5112	1
Brixton	1830-1900	5055	1
Brixton	1900-1930	4218	1
Brixton	1930-2000	3222	1
Brixton	2000-2030	2514	1
Brixton	2030-2100	2082	1
Brixton	2100-2130	1871	1
Brixton	2130-2200	1755	1
Brixton	2200-2230	1906	1
Brixton	2230-2300	2666	1
Brixton	2300-2330	2289	1
Brixton	2330-2400	1440	1
Brixton	0000-0030	986	1
Brixton	0030-0100	443	1
Brixton	0100-0130	223	1
Brixton	0130-0200	91	1
Brixton	0200-0230	0	0
Brixton	0230-0300	0	0
Brixton	0300-0330	0	0
Brixton	0330-0400	0	0
Brixton	0400-0430	0	0
Bromley-by-Bow	0430-0500	0	0
Bromley-by-Bow	0500-0530	43	1
Bromley-by-Bow	0530-0600	88	1
Bromley-by-Bow	0600-0630	175	1
Bromley-by-Bow	0630-0700	256	1
Bromley-by-Bow	0700-0730	428	1
Bromley-by-Bow	0730-0800	664	1
Bromley-by-Bow	0800-0830	883	1
Bromley-by-Bow	0830-0900	704	1
Bromley-by-Bow	0900-0930	463	1
Bromley-by-Bow	0930-1000	323	1
Bromley-by-Bow	1000-1030	251	1
Bromley-by-Bow	1030-1100	218	1
Bromley-by-Bow	1100-1130	201	1
Bromley-by-Bow	1130-1200	185	1
Bromley-by-Bow	1200-1230	179	1
Bromley-by-Bow	1230-1300	191	1
Bromley-by-Bow	1300-1330	200	1
Bromley-by-Bow	1330-1400	201	1
Bromley-by-Bow	1400-1430	212	1
Bromley-by-Bow	1430-1500	230	1
Bromley-by-Bow	1500-1530	296	1
Bromley-by-Bow	1530-1600	341	1
Bromley-by-Bow	1600-1630	425	1
Bromley-by-Bow	1630-1700	511	1
Bromley-by-Bow	1700-1730	541	1
Bromley-by-Bow	1730-1800	586	1
Bromley-by-Bow	1800-1830	587	1
Bromley-by-Bow	1830-1900	537	1
Bromley-by-Bow	1900-1930	438	1
Bromley-by-Bow	1930-2000	325	1
Bromley-by-Bow	2000-2030	252	1
Bromley-by-Bow	2030-2100	214	1
Bromley-by-Bow	2100-2130	189	1
Bromley-by-Bow	2130-2200	176	1
Bromley-by-Bow	2200-2230	163	1
Bromley-by-Bow	2230-2300	154	1
Bromley-by-Bow	2300-2330	146	1
Bromley-by-Bow	2330-2400	118	1
Bromley-by-Bow	0000-0030	91	1
Bromley-by-Bow	0030-0100	51	1
Bromley-by-Bow	0100-0130	8	1
Bromley-by-Bow	0130-0200	0	1
Bromley-by-Bow	0200-0230	0	0
Bromley-by-Bow	0230-0300	0	0
Bromley-by-Bow	0300-0330	0	0
Bromley-by-Bow	0330-0400	0	0
Bromley-by-Bow	0400-0430	0	0
Buckhurst Hill	0430-0500	0	0
Buckhurst Hill	0500-0530	21	1
Buckhurst Hill	0530-0600	61	1
Buckhurst Hill	0600-0630	137	1
Buckhurst Hill	0630-0700	219	1
Buckhurst Hill	0700-0730	360	1
Buckhurst Hill	0730-0800	563	1
Buckhurst Hill	0800-0830	601	1
Buckhurst Hill	0830-0900	374	1
Buckhurst Hill	0900-0930	225	1
Buckhurst Hill	0930-1000	155	1
Buckhurst Hill	1000-1030	113	1
Buckhurst Hill	1030-1100	98	1
Buckhurst Hill	1100-1130	93	1
Buckhurst Hill	1130-1200	91	1
Buckhurst Hill	1200-1230	97	1
Buckhurst Hill	1230-1300	99	1
Buckhurst Hill	1300-1330	105	1
Buckhurst Hill	1330-1400	106	1
Buckhurst Hill	1400-1430	111	1
Buckhurst Hill	1430-1500	122	1
Buckhurst Hill	1500-1530	166	1
Buckhurst Hill	1530-1600	192	1
Buckhurst Hill	1600-1630	216	1
Buckhurst Hill	1630-1700	260	1
Buckhurst Hill	1700-1730	345	1
Buckhurst Hill	1730-1800	423	1
Buckhurst Hill	1800-1830	464	1
Buckhurst Hill	1830-1900	405	1
Buckhurst Hill	1900-1930	318	1
Buckhurst Hill	1930-2000	210	1
Buckhurst Hill	2000-2030	146	1
Buckhurst Hill	2030-2100	110	1
Buckhurst Hill	2100-2130	95	1
Buckhurst Hill	2130-2200	83	1
Buckhurst Hill	2200-2230	80	1
Buckhurst Hill	2230-2300	91	1
Buckhurst Hill	2300-2330	79	1
Buckhurst Hill	2330-2400	67	1
Buckhurst Hill	0000-0030	41	1
Buckhurst Hill	0030-0100	28	1
Buckhurst Hill	0100-0130	9	1
Buckhurst Hill	0130-0200	4	1
Buckhurst Hill	0200-0230	0	0
Buckhurst Hill	0230-0300	0	0
Buckhurst Hill	0300-0330	0	0
Buckhurst Hill	0330-0400	0	0
Buckhurst Hill	0400-0430	0	0
Burnt Oak	0430-0500	0	0
Burnt Oak	0500-0530	61	1
Burnt Oak	0530-0600	218	1
Burnt Oak	0600-0630	519	1
Burnt Oak	0630-0700	673	1
Burnt Oak	0700-0730	634	1
Burnt Oak	0730-0800	742	1
Burnt Oak	0800-0830	914	1
Burnt Oak	0830-0900	757	1
Burnt Oak	0900-0930	438	1
Burnt Oak	0930-1000	300	1
Burnt Oak	1000-1030	241	1
Burnt Oak	1030-1100	212	1
Burnt Oak	1100-1130	205	1
Burnt Oak	1130-1200	202	1
Burnt Oak	1200-1230	215	1
Burnt Oak	1230-1300	244	1
Burnt Oak	1300-1330	250	1
Burnt Oak	1330-1400	233	1
Burnt Oak	1400-1430	239	1
Burnt Oak	1430-1500	274	1
Burnt Oak	1500-1530	300	1
Burnt Oak	1530-1600	377	1
Burnt Oak	1600-1630	441	1
Burnt Oak	1630-1700	513	1
Burnt Oak	1700-1730	706	1
Burnt Oak	1730-1800	806	1
Burnt Oak	1800-1830	764	1
Burnt Oak	1830-1900	674	1
Burnt Oak	1900-1930	467	1
Burnt Oak	1930-2000	325	1
Burnt Oak	2000-2030	245	1
Burnt Oak	2030-2100	209	1
Burnt Oak	2100-2130	180	1
Burnt Oak	2130-2200	154	1
Burnt Oak	2200-2230	143	1
Burnt Oak	2230-2300	126	1
Burnt Oak	2300-2330	109	1
Burnt Oak	2330-2400	101	1
Burnt Oak	0000-0030	74	1
Burnt Oak	0030-0100	53	1
Burnt Oak	0100-0130	18	1
Burnt Oak	0130-0200	5	1
Burnt Oak	0200-0230	0	0
Burnt Oak	0230-0300	0	0
Burnt Oak	0300-0330	0	0
Burnt Oak	0330-0400	0	0
Burnt Oak	0400-0430	0	0
Caledonian Road	0430-0500	0	0
Caledonian Road	0500-0530	16	1
Caledonian Road	0530-0600	69	1
Caledonian Road	0600-0630	163	1
Caledonian Road	0630-0700	285	1
Caledonian Road	0700-0730	497	1
Caledonian Road	0730-0800	713	1
Caledonian Road	0800-0830	933	1
Caledonian Road	0830-0900	1047	1
Caledonian Road	0900-0930	843	1
Caledonian Road	0930-1000	627	1
Caledonian Road	1000-1030	420	1
Caledonian Road	1030-1100	398	1
Caledonian Road	1100-1130	314	1
Caledonian Road	1130-1200	327	1
Caledonian Road	1200-1230	337	1
Caledonian Road	1230-1300	362	1
Caledonian Road	1300-1330	360	1
Caledonian Road	1330-1400	373	1
Caledonian Road	1400-1430	359	1
Caledonian Road	1430-1500	380	1
Caledonian Road	1500-1530	401	1
Caledonian Road	1530-1600	457	1
Caledonian Road	1600-1630	563	1
Caledonian Road	1630-1700	636	1
Caledonian Road	1700-1730	804	1
Caledonian Road	1730-1800	873	1
Caledonian Road	1800-1830	829	1
Caledonian Road	1830-1900	715	1
Caledonian Road	1900-1930	607	1
Caledonian Road	1930-2000	461	1
Caledonian Road	2000-2030	384	1
Caledonian Road	2030-2100	356	1
Caledonian Road	2100-2130	325	1
Caledonian Road	2130-2200	340	1
Caledonian Road	2200-2230	333	1
Caledonian Road	2230-2300	314	1
Caledonian Road	2300-2330	237	1
Caledonian Road	2330-2400	191	1
Caledonian Road	0000-0030	129	1
Caledonian Road	0030-0100	60	1
Caledonian Road	0100-0130	14	1
Caledonian Road	0130-0200	16	1
Caledonian Road	0200-0230	0	0
Caledonian Road	0230-0300	0	0
Caledonian Road	0300-0330	0	0
Caledonian Road	0330-0400	0	0
Caledonian Road	0400-0430	0	0
Camden Town	0430-0500	0	0
Camden Town	0500-0530	0	1
Camden Town	0530-0600	97	1
Camden Town	0600-0630	275	1
Camden Town	0630-0700	576	1
Camden Town	0700-0730	1026	1
Camden Town	0730-0800	1318	1
Camden Town	0800-0830	1704	1
Camden Town	0830-0900	2377	1
Camden Town	0900-0930	2324	1
Camden Town	0930-1000	1973	1
Camden Town	1000-1030	1439	1
Camden Town	1030-1100	1316	1
Camden Town	1100-1130	1296	1
Camden Town	1130-1200	1399	1
Camden Town	1200-1230	1510	1
Camden Town	1230-1300	1621	1
Camden Town	1300-1330	1757	1
Camden Town	1330-1400	1810	1
Camden Town	1400-1430	1824	1
Camden Town	1430-1500	1898	1
Camden Town	1500-1530	1964	1
Camden Town	1530-1600	2088	1
Camden Town	1600-1630	2313	1
Camden Town	1630-1700	2464	1
Camden Town	1700-1730	2774	1
Camden Town	1730-1800	3224	1
Camden Town	1800-1830	3427	1
Camden Town	1830-1900	2769	1
Camden Town	1900-1930	2113	1
Camden Town	1930-2000	1609	1
Camden Town	2000-2030	1293	1
Camden Town	2030-2100	1053	1
Camden Town	2100-2130	943	1
Camden Town	2130-2200	901	1
Camden Town	2200-2230	1019	1
Camden Town	2230-2300	1200	1
Camden Town	2300-2330	1215	1
Camden Town	2330-2400	1064	1
Camden Town	0000-0030	759	1
Camden Town	0030-0100	292	1
Camden Town	0100-0130	131	1
Camden Town	0130-0200	74	1
Camden Town	0200-0230	0	0
Camden Town	0230-0300	0	0
Camden Town	0300-0330	0	0
Camden Town	0330-0400	0	0
Camden Town	0400-0430	0	0
Canada Water	0430-0500	0	0
Canada Water	0500-0530	96	1
Canada Water	0530-0600	272	1
Canada Water	0600-0630	437	1
Canada Water	0630-0700	823	1
Canada Water	0700-0730	1481	1
Canada Water	0730-0800	1972	1
Canada Water	0800-0830	2596	1
Canada Water	0830-0900	2504	1
Canada Water	0900-0930	1889	1
Canada Water	0930-1000	1220	1
Canada Water	1000-1030	820	1
Canada Water	1030-1100	737	1
Canada Water	1100-1130	677	1
Canada Water	1130-1200	682	1
Canada Water	1200-1230	704	1
Canada Water	1230-1300	743	1
Canada Water	1300-1330	752	1
Canada Water	1330-1400	762	1
Canada Water	1400-1430	759	1
Canada Water	1430-1500	804	1
Canada Water	1500-1530	856	1
Canada Water	1530-1600	974	1
Canada Water	1600-1630	1222	1
Canada Water	1630-1700	1447	1
Canada Water	1700-1730	1809	1
Canada Water	1730-1800	2193	1
Canada Water	1800-1830	2366	1
Canada Water	1830-1900	2149	1
Canada Water	1900-1930	1673	1
Canada Water	1930-2000	1369	1
Canada Water	2000-2030	1089	1
Canada Water	2030-2100	946	1
Canada Water	2100-2130	848	1
Canada Water	2130-2200	808	1
Canada Water	2200-2230	762	1
Canada Water	2230-2300	725	1
Canada Water	2300-2330	671	1
Canada Water	2330-2400	554	1
Canada Water	0000-0030	396	1
Canada Water	0030-0100	236	1
Canada Water	0100-0130	86	1
Canada Water	0130-0200	45	1
Canada Water	0200-0230	0	0
Canada Water	0230-0300	0	0
Canada Water	0300-0330	0	0
Canada Water	0330-0400	0	0
Canada Water	0400-0430	0	0
Canary Wharf	0430-0500	0	0
Canary Wharf	0500-0530	177	1
Canary Wharf	0530-0600	697	1
Canary Wharf	0600-0630	1418	1
Canary Wharf	0630-0700	3183	1
Canary Wharf	0700-0730	5394	1
Canary Wharf	0730-0800	8046	1
Canary Wharf	0800-0830	11441	1
Canary Wharf	0830-0900	14387	1
Canary Wharf	0900-0930	11927	1
Canary Wharf	0930-1000	6231	1
Canary Wharf	1000-1030	3182	1
Canary Wharf	1030-1100	2408	1
Canary Wharf	1100-1130	2168	1
Canary Wharf	1130-1200	2297	1
Canary Wharf	1200-1230	2335	1
Canary Wharf	1230-1300	2345	1
Canary Wharf	1300-1330	2277	1
Canary Wharf	1330-1400	2283	1
Canary Wharf	1400-1430	2359	1
Canary Wharf	1430-1500	2456	1
Canary Wharf	1500-1530	2803	1
Canary Wharf	1530-1600	3484	1
Canary Wharf	1600-1630	5049	1
Canary Wharf	1630-1700	6871	1
Canary Wharf	1700-1730	10939	1
Canary Wharf	1730-1800	11329	1
Canary Wharf	1800-1830	10887	1
Canary Wharf	1830-1900	8675	1
Canary Wharf	1900-1930	6245	1
Canary Wharf	1930-2000	4342	1
Canary Wharf	2000-2030	3295	1
Canary Wharf	2030-2100	2521	1
Canary Wharf	2100-2130	2073	1
Canary Wharf	2130-2200	1804	1
Canary Wharf	2200-2230	1613	1
Canary Wharf	2230-2300	1451	1
Canary Wharf	2300-2330	1271	1
Canary Wharf	2330-2400	927	1
Canary Wharf	0000-0030	522	1
Canary Wharf	0030-0100	235	1
Canary Wharf	0100-0130	79	1
Canary Wharf	0130-0200	40	1
Canary Wharf	0200-0230	0	0
Canary Wharf	0230-0300	0	0
Canary Wharf	0300-0330	0	0
Canary Wharf	0330-0400	0	0
Canary Wharf	0400-0430	0	0
Canning Town	0430-0500	0	0
Canning Town	0500-0530	265	1
Canning Town	0530-0600	537	1
Canning Town	0600-0630	968	1
Canning Town	0630-0700	1598	1
Canning Town	0700-0730	1980	1
Canning Town	0730-0800	1842	1
Canning Town	0800-0830	2066	1
Canning Town	0830-0900	1778	1
Canning Town	0900-0930	1339	1
Canning Town	0930-1000	920	1
Canning Town	1000-1030	715	1
Canning Town	1030-1100	649	1
Canning Town	1100-1130	622	1
Canning Town	1130-1200	578	1
Canning Town	1200-1230	588	1
Canning Town	1230-1300	603	1
Canning Town	1300-1330	635	1
Canning Town	1330-1400	643	1
Canning Town	1400-1430	695	1
Canning Town	1430-1500	753	1
Canning Town	1500-1530	850	1
Canning Town	1530-1600	982	1
Canning Town	1600-1630	1258	1
Canning Town	1630-1700	1495	1
Canning Town	1700-1730	1812	1
Canning Town	1730-1800	2020	1
Canning Town	1800-1830	2058	1
Canning Town	1830-1900	1742	1
Canning Town	1900-1930	1330	1
Canning Town	1930-2000	1057	1
Canning Town	2000-2030	859	1
Canning Town	2030-2100	786	1
Canning Town	2100-2130	731	1
Canning Town	2130-2200	652	1
Canning Town	2200-2230	606	1
Canning Town	2230-2300	603	1
Canning Town	2300-2330	568	1
Canning Town	2330-2400	486	1
Canning Town	0000-0030	325	1
Canning Town	0030-0100	234	1
Canning Town	0100-0130	106	1
Canning Town	0130-0200	50	1
Canning Town	0200-0230	0	0
Canning Town	0230-0300	0	0
Canning Town	0300-0330	0	0
Canning Town	0330-0400	0	0
Canning Town	0400-0430	0	0
Cannon Street	0430-0500	0	0
Cannon Street	0500-0530	8	1
Cannon Street	0530-0600	78	1
Cannon Street	0600-0630	279	1
Cannon Street	0630-0700	599	1
Cannon Street	0700-0730	1092	1
Cannon Street	0730-0800	1766	1
Cannon Street	0800-0830	2437	1
Cannon Street	0830-0900	2824	1
Cannon Street	0900-0930	2413	1
Cannon Street	0930-1000	1296	1
Cannon Street	1000-1030	771	1
Cannon Street	1030-1100	596	1
Cannon Street	1100-1130	527	1
Cannon Street	1130-1200	549	1
Cannon Street	1200-1230	607	1
Cannon Street	1230-1300	610	1
Cannon Street	1300-1330	578	1
Cannon Street	1330-1400	575	1
Cannon Street	1400-1430	575	1
Cannon Street	1430-1500	575	1
Cannon Street	1500-1530	618	1
Cannon Street	1530-1600	761	1
Cannon Street	1600-1630	1009	1
Cannon Street	1630-1700	1225	1
Cannon Street	1700-1730	1901	1
Cannon Street	1730-1800	2151	1
Cannon Street	1800-1830	1973	1
Cannon Street	1830-1900	1509	1
Cannon Street	1900-1930	992	1
Cannon Street	1930-2000	675	1
Cannon Street	2000-2030	496	1
Cannon Street	2030-2100	391	1
Cannon Street	2100-2130	336	1
Cannon Street	2130-2200	310	1
Cannon Street	2200-2230	287	1
Cannon Street	2230-2300	252	1
Cannon Street	2300-2330	217	1
Cannon Street	2330-2400	152	1
Cannon Street	0000-0030	72	1
Cannon Street	0030-0100	15	1
Cannon Street	0100-0130	0	1
Cannon Street	0130-0200	0	1
Cannon Street	0200-0230	0	0
Cannon Street	0230-0300	0	0
Cannon Street	0300-0330	0	0
Cannon Street	0330-0400	0	0
Cannon Street	0400-0430	0	0
Canons Park	0430-0500	0	0
Canons Park	0500-0530	31	1
Canons Park	0530-0600	103	1
Canons Park	0600-0630	228	1
Canons Park	0630-0700	326	1
Canons Park	0700-0730	448	1
Canons Park	0730-0800	639	1
Canons Park	0800-0830	716	1
Canons Park	0830-0900	498	1
Canons Park	0900-0930	303	1
Canons Park	0930-1000	212	1
Canons Park	1000-1030	159	1
Canons Park	1030-1100	134	1
Canons Park	1100-1130	130	1
Canons Park	1130-1200	119	1
Canons Park	1200-1230	121	1
Canons Park	1230-1300	127	1
Canons Park	1300-1330	129	1
Canons Park	1330-1400	131	1
Canons Park	1400-1430	133	1
Canons Park	1430-1500	160	1
Canons Park	1500-1530	170	1
Canons Park	1530-1600	235	1
Canons Park	1600-1630	303	1
Canons Park	1630-1700	334	1
Canons Park	1700-1730	420	1
Canons Park	1730-1800	532	1
Canons Park	1800-1830	568	1
Canons Park	1830-1900	542	1
Canons Park	1900-1930	378	1
Canons Park	1930-2000	272	1
Canons Park	2000-2030	201	1
Canons Park	2030-2100	146	1
Canons Park	2100-2130	125	1
Canons Park	2130-2200	121	1
Canons Park	2200-2230	124	1
Canons Park	2230-2300	119	1
Canons Park	2300-2330	87	1
Canons Park	2330-2400	68	1
Canons Park	0000-0030	46	1
Canons Park	0030-0100	25	1
Canons Park	0100-0130	10	1
Canons Park	0130-0200	4	1
Canons Park	0200-0230	0	0
Canons Park	0230-0300	0	0
Canons Park	0300-0330	0	0
Canons Park	0330-0400	0	0
Canons Park	0400-0430	0	0
Chalfont & Latimer	0430-0500	0	0
Chalfont & Latimer	0500-0530	9	1
Chalfont & Latimer	0530-0600	45	1
Chalfont & Latimer	0600-0630	128	1
Chalfont & Latimer	0630-0700	206	1
Chalfont & Latimer	0700-0730	399	1
Chalfont & Latimer	0730-0800	577	1
Chalfont & Latimer	0800-0830	481	1
Chalfont & Latimer	0830-0900	186	1
Chalfont & Latimer	0900-0930	116	1
Chalfont & Latimer	0930-1000	85	1
Chalfont & Latimer	1000-1030	64	1
Chalfont & Latimer	1030-1100	63	1
Chalfont & Latimer	1100-1130	56	1
Chalfont & Latimer	1130-1200	49	1
Chalfont & Latimer	1200-1230	52	1
Chalfont & Latimer	1230-1300	58	1
Chalfont & Latimer	1300-1330	60	1
Chalfont & Latimer	1330-1400	70	1
Chalfont & Latimer	1400-1430	59	1
Chalfont & Latimer	1430-1500	57	1
Chalfont & Latimer	1500-1530	185	1
Chalfont & Latimer	1530-1600	276	1
Chalfont & Latimer	1600-1630	170	1
Chalfont & Latimer	1630-1700	192	1
Chalfont & Latimer	1700-1730	257	1
Chalfont & Latimer	1730-1800	254	1
Chalfont & Latimer	1800-1830	272	1
Chalfont & Latimer	1830-1900	257	1
Chalfont & Latimer	1900-1930	269	1
Chalfont & Latimer	1930-2000	160	1
Chalfont & Latimer	2000-2030	96	1
Chalfont & Latimer	2030-2100	90	1
Chalfont & Latimer	2100-2130	75	1
Chalfont & Latimer	2130-2200	90	1
Chalfont & Latimer	2200-2230	81	1
Chalfont & Latimer	2230-2300	97	1
Chalfont & Latimer	2300-2330	64	1
Chalfont & Latimer	2330-2400	49	1
Chalfont & Latimer	0000-0030	30	1
Chalfont & Latimer	0030-0100	16	1
Chalfont & Latimer	0100-0130	2	1
Chalfont & Latimer	0130-0200	0	1
Chalfont & Latimer	0200-0230	0	0
Chalfont & Latimer	0230-0300	0	0
Chalfont & Latimer	0300-0330	0	0
Chalfont & Latimer	0330-0400	0	0
Chalfont & Latimer	0400-0430	0	0
Chalk Farm	0430-0500	0	0
Chalk Farm	0500-0530	0	1
Chalk Farm	0530-0600	33	1
Chalk Farm	0600-0630	86	1
Chalk Farm	0630-0700	186	1
Chalk Farm	0700-0730	363	1
Chalk Farm	0730-0800	603	1
Chalk Farm	0800-0830	828	1
Chalk Farm	0830-0900	919	1
Chalk Farm	0900-0930	709	1
Chalk Farm	0930-1000	551	1
Chalk Farm	1000-1030	379	1
Chalk Farm	1030-1100	317	1
Chalk Farm	1100-1130	291	1
Chalk Farm	1130-1200	292	1
Chalk Farm	1200-1230	305	1
Chalk Farm	1230-1300	322	1
Chalk Farm	1300-1330	327	1
Chalk Farm	1330-1400	331	1
Chalk Farm	1400-1430	328	1
Chalk Farm	1430-1500	333	1
Chalk Farm	1500-1530	382	1
Chalk Farm	1530-1600	422	1
Chalk Farm	1600-1630	486	1
Chalk Farm	1630-1700	575	1
Chalk Farm	1700-1730	661	1
Chalk Farm	1730-1800	811	1
Chalk Farm	1800-1830	927	1
Chalk Farm	1830-1900	866	1
Chalk Farm	1900-1930	712	1
Chalk Farm	1930-2000	544	1
Chalk Farm	2000-2030	431	1
Chalk Farm	2030-2100	347	1
Chalk Farm	2100-2130	320	1
Chalk Farm	2130-2200	285	1
Chalk Farm	2200-2230	368	1
Chalk Farm	2230-2300	496	1
Chalk Farm	2300-2330	411	1
Chalk Farm	2330-2400	246	1
Chalk Farm	0000-0030	136	1
Chalk Farm	0030-0100	47	1
Chalk Farm	0100-0130	16	1
Chalk Farm	0130-0200	8	1
Chalk Farm	0200-0230	0	0
Chalk Farm	0230-0300	0	0
Chalk Farm	0300-0330	0	0
Chalk Farm	0330-0400	0	0
Chalk Farm	0400-0430	0	0
Chancery Lane	0430-0500	0	0
Chancery Lane	0500-0530	0	1
Chancery Lane	0530-0600	111	1
Chancery Lane	0600-0630	337	1
Chancery Lane	0630-0700	636	1
Chancery Lane	0700-0730	1082	1
Chancery Lane	0730-0800	1903	1
Chancery Lane	0800-0830	3077	1
Chancery Lane	0830-0900	4666	1
Chancery Lane	0900-0930	5091	1
Chancery Lane	0930-1000	3251	1
Chancery Lane	1000-1030	1795	1
Chancery Lane	1030-1100	1414	1
Chancery Lane	1100-1130	1245	1
Chancery Lane	1130-1200	1322	1
Chancery Lane	1200-1230	1517	1
Chancery Lane	1230-1300	1598	1
Chancery Lane	1300-1330	1582	1
Chancery Lane	1330-1400	1566	1
Chancery Lane	1400-1430	1465	1
Chancery Lane	1430-1500	1419	1
Chancery Lane	1500-1530	1465	1
Chancery Lane	1530-1600	1707	1
Chancery Lane	1600-1630	2162	1
Chancery Lane	1630-1700	2598	1
Chancery Lane	1700-1730	3322	1
Chancery Lane	1730-1800	3845	1
Chancery Lane	1800-1830	3434	1
Chancery Lane	1830-1900	2562	1
Chancery Lane	1900-1930	1777	1
Chancery Lane	1930-2000	1200	1
Chancery Lane	2000-2030	929	1
Chancery Lane	2030-2100	796	1
Chancery Lane	2100-2130	674	1
Chancery Lane	2130-2200	552	1
Chancery Lane	2200-2230	502	1
Chancery Lane	2230-2300	397	1
Chancery Lane	2300-2330	352	1
Chancery Lane	2330-2400	247	1
Chancery Lane	0000-0030	154	1
Chancery Lane	0030-0100	57	1
Chancery Lane	0100-0130	36	1
Chancery Lane	0130-0200	18	1
Chancery Lane	0200-0230	0	0
Chancery Lane	0230-0300	0	0
Chancery Lane	0300-0330	0	0
Chancery Lane	0330-0400	0	0
Chancery Lane	0400-0430	0	0
Charing Cross	0430-0500	0	0
Charing Cross	0500-0530	15	1
Charing Cross	0530-0600	124	1
Charing Cross	0600-0630	309	1
Charing Cross	0630-0700	730	1
Charing Cross	0700-0730	1248	1
Charing Cross	0730-0800	1761	1
Charing Cross	0800-0830	2422	1
Charing Cross	0830-0900	3050	1
Charing Cross	0900-0930	2597	1
Charing Cross	0930-1000	1876	1
Charing Cross	1000-1030	1403	1
Charing Cross	1030-1100	1283	1
Charing Cross	1100-1130	1139	1
Charing Cross	1130-1200	1209	1
Charing Cross	1200-1230	1268	1
Charing Cross	1230-1300	1315	1
Charing Cross	1300-1330	1301	1
Charing Cross	1330-1400	1351	1
Charing Cross	1400-1430	1375	1
Charing Cross	1430-1500	1403	1
Charing Cross	1500-1530	1535	1
Charing Cross	1530-1600	1776	1
Charing Cross	1600-1630	2144	1
Charing Cross	1630-1700	2553	1
Charing Cross	1700-1730	3293	1
Charing Cross	1730-1800	3776	1
Charing Cross	1800-1830	3485	1
Charing Cross	1830-1900	2747	1
Charing Cross	1900-1930	1983	1
Charing Cross	1930-2000	1334	1
Charing Cross	2000-2030	1135	1
Charing Cross	2030-2100	1026	1
Charing Cross	2100-2130	998	1
Charing Cross	2130-2200	1013	1
Charing Cross	2200-2230	1316	1
Charing Cross	2230-2300	1123	1
Charing Cross	2300-2330	819	1
Charing Cross	2330-2400	580	1
Charing Cross	0000-0030	275	1
Charing Cross	0030-0100	80	1
Charing Cross	0100-0130	26	1
Charing Cross	0130-0200	15	1
Charing Cross	0200-0230	0	0
Charing Cross	0230-0300	0	0
Charing Cross	0300-0330	0	0
Charing Cross	0330-0400	0	0
Charing Cross	0400-0430	0	0
Chesham	0430-0500	0	0
Chesham	0500-0530	15	1
Chesham	0530-0600	52	1
Chesham	0600-0630	114	1
Chesham	0630-0700	193	1
Chesham	0700-0730	306	1
Chesham	0730-0800	323	1
Chesham	0800-0830	277	1
Chesham	0830-0900	145	1
Chesham	0900-0930	77	1
Chesham	0930-1000	67	1
Chesham	1000-1030	45	1
Chesham	1030-1100	44	1
Chesham	1100-1130	40	1
Chesham	1130-1200	38	1
Chesham	1200-1230	42	1
Chesham	1230-1300	37	1
Chesham	1300-1330	41	1
Chesham	1330-1400	45	1
Chesham	1400-1430	45	1
Chesham	1430-1500	51	1
Chesham	1500-1530	45	1
Chesham	1530-1600	147	1
Chesham	1600-1630	145	1
Chesham	1630-1700	136	1
Chesham	1700-1730	152	1
Chesham	1730-1800	143	1
Chesham	1800-1830	185	1
Chesham	1830-1900	190	1
Chesham	1900-1930	176	1
Chesham	1930-2000	121	1
Chesham	2000-2030	68	1
Chesham	2030-2100	52	1
Chesham	2100-2130	39	1
Chesham	2130-2200	33	1
Chesham	2200-2230	36	1
Chesham	2230-2300	34	1
Chesham	2300-2330	33	1
Chesham	2330-2400	27	1
Chesham	0000-0030	22	1
Chesham	0030-0100	15	1
Chesham	0100-0130	7	1
Chesham	0130-0200	3	1
Chesham	0200-0230	0	0
Chesham	0230-0300	0	0
Chesham	0300-0330	0	0
Chesham	0330-0400	0	0
Chesham	0400-0430	0	0
Chigwell	0430-0500	0	0
Chigwell	0500-0530	4	1
Chigwell	0530-0600	6	1
Chigwell	0600-0630	24	1
Chigwell	0630-0700	65	1
Chigwell	0700-0730	118	1
Chigwell	0730-0800	197	1
Chigwell	0800-0830	223	1
Chigwell	0830-0900	82	1
Chigwell	0900-0930	28	1
Chigwell	0930-1000	29	1
Chigwell	1000-1030	22	1
Chigwell	1030-1100	20	1
Chigwell	1100-1130	21	1
Chigwell	1130-1200	20	1
Chigwell	1200-1230	18	1
Chigwell	1230-1300	20	1
Chigwell	1300-1330	19	1
Chigwell	1330-1400	26	1
Chigwell	1400-1430	20	1
Chigwell	1430-1500	23	1
Chigwell	1500-1530	43	1
Chigwell	1530-1600	72	1
Chigwell	1600-1630	74	1
Chigwell	1630-1700	71	1
Chigwell	1700-1730	63	1
Chigwell	1730-1800	89	1
Chigwell	1800-1830	73	1
Chigwell	1830-1900	72	1
Chigwell	1900-1930	51	1
Chigwell	1930-2000	40	1
Chigwell	2000-2030	23	1
Chigwell	2030-2100	20	1
Chigwell	2100-2130	12	1
Chigwell	2130-2200	14	1
Chigwell	2200-2230	10	1
Chigwell	2230-2300	11	1
Chigwell	2300-2330	9	1
Chigwell	2330-2400	10	1
Chigwell	0000-0030	6	1
Chigwell	0030-0100	0	1
Chigwell	0100-0130	0	1
Chigwell	0130-0200	0	1
Chigwell	0200-0230	0	0
Chigwell	0230-0300	0	0
Chigwell	0300-0330	0	0
Chigwell	0330-0400	0	0
Chigwell	0400-0430	0	0
Chiswick Park	0430-0500	0	0
Chiswick Park	0500-0530	10	1
Chiswick Park	0530-0600	23	1
Chiswick Park	0600-0630	47	1
Chiswick Park	0630-0700	106	1
Chiswick Park	0700-0730	257	1
Chiswick Park	0730-0800	469	1
Chiswick Park	0800-0830	527	1
Chiswick Park	0830-0900	512	1
Chiswick Park	0900-0930	372	1
Chiswick Park	0930-1000	243	1
Chiswick Park	1000-1030	149	1
Chiswick Park	1030-1100	125	1
Chiswick Park	1100-1130	116	1
Chiswick Park	1130-1200	118	1
Chiswick Park	1200-1230	111	1
Chiswick Park	1230-1300	118	1
Chiswick Park	1300-1330	118	1
Chiswick Park	1330-1400	123	1
Chiswick Park	1400-1430	126	1
Chiswick Park	1430-1500	126	1
Chiswick Park	1500-1530	143	1
Chiswick Park	1530-1600	166	1
Chiswick Park	1600-1630	227	1
Chiswick Park	1630-1700	299	1
Chiswick Park	1700-1730	376	1
Chiswick Park	1730-1800	412	1
Chiswick Park	1800-1830	401	1
Chiswick Park	1830-1900	326	1
Chiswick Park	1900-1930	250	1
Chiswick Park	1930-2000	189	1
Chiswick Park	2000-2030	137	1
Chiswick Park	2030-2100	108	1
Chiswick Park	2100-2130	96	1
Chiswick Park	2130-2200	83	1
Chiswick Park	2200-2230	87	1
Chiswick Park	2230-2300	81	1
Chiswick Park	2300-2330	66	1
Chiswick Park	2330-2400	54	1
Chiswick Park	0000-0030	40	1
Chiswick Park	0030-0100	22	1
Chiswick Park	0100-0130	4	1
Chiswick Park	0130-0200	0	1
Chiswick Park	0200-0230	0	0
Chiswick Park	0230-0300	0	0
Chiswick Park	0300-0330	0	0
Chiswick Park	0330-0400	0	0
Chiswick Park	0400-0430	0	0
Chorleywood	0430-0500	0	0
Chorleywood	0500-0530	5	1
Chorleywood	0530-0600	15	1
Chorleywood	0600-0630	56	1
Chorleywood	0630-0700	113	1
Chorleywood	0700-0730	142	1
Chorleywood	0730-0800	219	1
Chorleywood	0800-0830	159	1
Chorleywood	0830-0900	77	1
Chorleywood	0900-0930	63	1
Chorleywood	0930-1000	45	1
Chorleywood	1000-1030	32	1
Chorleywood	1030-1100	39	1
Chorleywood	1100-1130	34	1
Chorleywood	1130-1200	30	1
Chorleywood	1200-1230	30	1
Chorleywood	1230-1300	32	1
Chorleywood	1300-1330	41	1
Chorleywood	1330-1400	31	1
Chorleywood	1400-1430	43	1
Chorleywood	1430-1500	60	1
Chorleywood	1500-1530	42	1
Chorleywood	1530-1600	127	1
Chorleywood	1600-1630	100	1
Chorleywood	1630-1700	84	1
Chorleywood	1700-1730	81	1
Chorleywood	1730-1800	149	1
Chorleywood	1800-1830	129	1
Chorleywood	1830-1900	119	1
Chorleywood	1900-1930	87	1
Chorleywood	1930-2000	56	1
Chorleywood	2000-2030	82	1
Chorleywood	2030-2100	45	1
Chorleywood	2100-2130	42	1
Chorleywood	2130-2200	38	1
Chorleywood	2200-2230	30	1
Chorleywood	2230-2300	20	1
Chorleywood	2300-2330	30	1
Chorleywood	2330-2400	31	1
Chorleywood	0000-0030	18	1
Chorleywood	0030-0100	12	1
Chorleywood	0100-0130	2	1
Chorleywood	0130-0200	0	1
Chorleywood	0200-0230	0	0
Chorleywood	0230-0300	0	0
Chorleywood	0300-0330	0	0
Chorleywood	0330-0400	0	0
Chorleywood	0400-0430	0	0
Clapham Common	0430-0500	0	0
Clapham Common	0500-0530	29	1
Clapham Common	0530-0600	121	1
Clapham Common	0600-0630	323	1
Clapham Common	0630-0700	585	1
Clapham Common	0700-0730	1017	1
Clapham Common	0730-0800	1566	1
Clapham Common	0800-0830	1625	1
Clapham Common	0830-0900	1636	1
Clapham Common	0900-0930	1296	1
Clapham Common	0930-1000	804	1
Clapham Common	1000-1030	535	1
Clapham Common	1030-1100	454	1
Clapham Common	1100-1130	435	1
Clapham Common	1130-1200	451	1
Clapham Common	1200-1230	482	1
Clapham Common	1230-1300	494	1
Clapham Common	1300-1330	512	1
Clapham Common	1330-1400	510	1
Clapham Common	1400-1430	487	1
Clapham Common	1430-1500	507	1
Clapham Common	1500-1530	592	1
Clapham Common	1530-1600	668	1
Clapham Common	1600-1630	762	1
Clapham Common	1630-1700	926	1
Clapham Common	1700-1730	1181	1
Clapham Common	1730-1800	1627	1
Clapham Common	1800-1830	1817	1
Clapham Common	1830-1900	1763	1
Clapham Common	1900-1930	1462	1
Clapham Common	1930-2000	1094	1
Clapham Common	2000-2030	879	1
Clapham Common	2030-2100	752	1
Clapham Common	2100-2130	653	1
Clapham Common	2130-2200	625	1
Clapham Common	2200-2230	628	1
Clapham Common	2230-2300	600	1
Clapham Common	2300-2330	557	1
Clapham Common	2330-2400	489	1
Clapham Common	0000-0030	310	1
Clapham Common	0030-0100	166	1
Clapham Common	0100-0130	64	1
Clapham Common	0130-0200	37	1
Clapham Common	0200-0230	0	0
Clapham Common	0230-0300	0	0
Clapham Common	0300-0330	0	0
Clapham Common	0330-0400	0	0
Clapham Common	0400-0430	0	0
Clapham North	0430-0500	0	0
Clapham North	0500-0530	20	1
Clapham North	0530-0600	75	1
Clapham North	0600-0630	208	1
Clapham North	0630-0700	419	1
Clapham North	0700-0730	783	1
Clapham North	0730-0800	1117	1
Clapham North	0800-0830	968	1
Clapham North	0830-0900	955	1
Clapham North	0900-0930	849	1
Clapham North	0930-1000	552	1
Clapham North	1000-1030	351	1
Clapham North	1030-1100	292	1
Clapham North	1100-1130	278	1
Clapham North	1130-1200	273	1
Clapham North	1200-1230	275	1
Clapham North	1230-1300	286	1
Clapham North	1300-1330	289	1
Clapham North	1330-1400	291	1
Clapham North	1400-1430	288	1
Clapham North	1430-1500	298	1
Clapham North	1500-1530	322	1
Clapham North	1530-1600	377	1
Clapham North	1600-1630	470	1
Clapham North	1630-1700	602	1
Clapham North	1700-1730	784	1
Clapham North	1730-1800	1062	1
Clapham North	1800-1830	1221	1
Clapham North	1830-1900	1181	1
Clapham North	1900-1930	978	1
Clapham North	1930-2000	747	1
Clapham North	2000-2030	604	1
Clapham North	2030-2100	495	1
Clapham North	2100-2130	472	1
Clapham North	2130-2200	449	1
Clapham North	2200-2230	445	1
Clapham North	2230-2300	444	1
Clapham North	2300-2330	397	1
Clapham North	2330-2400	327	1
Clapham North	0000-0030	214	1
Clapham North	0030-0100	119	1
Clapham North	0100-0130	41	1
Clapham North	0130-0200	20	1
Clapham North	0200-0230	0	0
Clapham North	0230-0300	0	0
Clapham North	0300-0330	0	0
Clapham North	0330-0400	0	0
Clapham North	0400-0430	0	0
Clapham South	0430-0500	0	0
Clapham South	0500-0530	32	1
Clapham South	0530-0600	101	1
Clapham South	0600-0630	310	1
Clapham South	0630-0700	627	1
Clapham South	0700-0730	1202	1
Clapham South	0730-0800	2115	1
Clapham South	0800-0830	1999	1
Clapham South	0830-0900	1599	1
Clapham South	0900-0930	1134	1
Clapham South	0930-1000	609	1
Clapham South	1000-1030	446	1
Clapham South	1030-1100	375	1
Clapham South	1100-1130	352	1
Clapham South	1130-1200	337	1
Clapham South	1200-1230	338	1
Clapham South	1230-1300	353	1
Clapham South	1300-1330	369	1
Clapham South	1330-1400	331	1
Clapham South	1400-1430	353	1
Clapham South	1430-1500	368	1
Clapham South	1500-1530	443	1
Clapham South	1530-1600	505	1
Clapham South	1600-1630	590	1
Clapham South	1630-1700	709	1
Clapham South	1700-1730	881	1
Clapham South	1730-1800	1228	1
Clapham South	1800-1830	1463	1
Clapham South	1830-1900	1449	1
Clapham South	1900-1930	1242	1
Clapham South	1930-2000	919	1
Clapham South	2000-2030	714	1
Clapham South	2030-2100	587	1
Clapham South	2100-2130	506	1
Clapham South	2130-2200	461	1
Clapham South	2200-2230	445	1
Clapham South	2230-2300	433	1
Clapham South	2300-2330	402	1
Clapham South	2330-2400	322	1
Clapham South	0000-0030	218	1
Clapham South	0030-0100	106	1
Clapham South	0100-0130	31	1
Clapham South	0130-0200	20	1
Clapham South	0200-0230	0	0
Clapham South	0230-0300	0	0
Clapham South	0300-0330	0	0
Clapham South	0330-0400	0	0
Clapham South	0400-0430	0	0
Cockfosters	0430-0500	0	0
Cockfosters	0500-0530	23	1
Cockfosters	0530-0600	37	1
Cockfosters	0600-0630	96	1
Cockfosters	0630-0700	138	1
Cockfosters	0700-0730	202	1
Cockfosters	0730-0800	284	1
Cockfosters	0800-0830	320	1
Cockfosters	0830-0900	243	1
Cockfosters	0900-0930	184	1
Cockfosters	0930-1000	167	1
Cockfosters	1000-1030	136	1
Cockfosters	1030-1100	117	1
Cockfosters	1100-1130	116	1
Cockfosters	1130-1200	111	1
Cockfosters	1200-1230	113	1
Cockfosters	1230-1300	108	1
Cockfosters	1300-1330	113	1
Cockfosters	1330-1400	113	1
Cockfosters	1400-1430	116	1
Cockfosters	1430-1500	118	1
Cockfosters	1500-1530	140	1
Cockfosters	1530-1600	164	1
Cockfosters	1600-1630	196	1
Cockfosters	1630-1700	229	1
Cockfosters	1700-1730	265	1
Cockfosters	1730-1800	265	1
Cockfosters	1800-1830	272	1
Cockfosters	1830-1900	232	1
Cockfosters	1900-1930	184	1
Cockfosters	1930-2000	143	1
Cockfosters	2000-2030	116	1
Cockfosters	2030-2100	88	1
Cockfosters	2100-2130	77	1
Cockfosters	2130-2200	72	1
Cockfosters	2200-2230	76	1
Cockfosters	2230-2300	77	1
Cockfosters	2300-2330	72	1
Cockfosters	2330-2400	60	1
Cockfosters	0000-0030	38	1
Cockfosters	0030-0100	19	1
Cockfosters	0100-0130	9	1
Cockfosters	0130-0200	5	1
Cockfosters	0200-0230	0	0
Cockfosters	0230-0300	0	0
Cockfosters	0300-0330	0	0
Cockfosters	0330-0400	0	0
Cockfosters	0400-0430	0	0
Colindale	0430-0500	0	0
Colindale	0500-0530	48	1
Colindale	0530-0600	147	1
Colindale	0600-0630	408	1
Colindale	0630-0700	716	1
Colindale	0700-0730	1063	1
Colindale	0730-0800	1303	1
Colindale	0800-0830	1567	1
Colindale	0830-0900	1214	1
Colindale	0900-0930	804	1
Colindale	0930-1000	551	1
Colindale	1000-1030	440	1
Colindale	1030-1100	370	1
Colindale	1100-1130	345	1
Colindale	1130-1200	322	1
Colindale	1200-1230	352	1
Colindale	1230-1300	356	1
Colindale	1300-1330	388	1
Colindale	1330-1400	422	1
Colindale	1400-1430	423	1
Colindale	1430-1500	473	1
Colindale	1500-1530	501	1
Colindale	1530-1600	619	1
Colindale	1600-1630	711	1
Colindale	1630-1700	814	1
Colindale	1700-1730	997	1
Colindale	1730-1800	1149	1
Colindale	1800-1830	1111	1
Colindale	1830-1900	960	1
Colindale	1900-1930	730	1
Colindale	1930-2000	550	1
Colindale	2000-2030	446	1
Colindale	2030-2100	399	1
Colindale	2100-2130	353	1
Colindale	2130-2200	330	1
Colindale	2200-2230	296	1
Colindale	2230-2300	281	1
Colindale	2300-2330	229	1
Colindale	2330-2400	197	1
Colindale	0000-0030	151	1
Colindale	0030-0100	95	1
Colindale	0100-0130	37	1
Colindale	0130-0200	16	1
Colindale	0200-0230	0	0
Colindale	0230-0300	0	0
Colindale	0300-0330	0	0
Colindale	0330-0400	0	0
Colindale	0400-0430	0	0
Colliers Wood	0430-0500	0	0
Colliers Wood	0500-0530	83	1
Colliers Wood	0530-0600	140	1
Colliers Wood	0600-0630	357	1
Colliers Wood	0630-0700	643	1
Colliers Wood	0700-0730	918	1
Colliers Wood	0730-0800	1248	1
Colliers Wood	0800-0830	1469	1
Colliers Wood	0830-0900	1125	1
Colliers Wood	0900-0930	727	1
Colliers Wood	0930-1000	463	1
Colliers Wood	1000-1030	344	1
Colliers Wood	1030-1100	307	1
Colliers Wood	1100-1130	305	1
Colliers Wood	1130-1200	294	1
Colliers Wood	1200-1230	303	1
Colliers Wood	1230-1300	310	1
Colliers Wood	1300-1330	325	1
Colliers Wood	1330-1400	319	1
Colliers Wood	1400-1430	335	1
Colliers Wood	1430-1500	362	1
Colliers Wood	1500-1530	412	1
Colliers Wood	1530-1600	456	1
Colliers Wood	1600-1630	544	1
Colliers Wood	1630-1700	676	1
Colliers Wood	1700-1730	837	1
Colliers Wood	1730-1800	1031	1
Colliers Wood	1800-1830	1085	1
Colliers Wood	1830-1900	1001	1
Colliers Wood	1900-1930	777	1
Colliers Wood	1930-2000	581	1
Colliers Wood	2000-2030	426	1
Colliers Wood	2030-2100	372	1
Colliers Wood	2100-2130	338	1
Colliers Wood	2130-2200	316	1
Colliers Wood	2200-2230	288	1
Colliers Wood	2230-2300	298	1
Colliers Wood	2300-2330	271	1
Colliers Wood	2330-2400	233	1
Colliers Wood	0000-0030	162	1
Colliers Wood	0030-0100	94	1
Colliers Wood	0100-0130	32	1
Colliers Wood	0130-0200	18	1
Colliers Wood	0200-0230	0	0
Colliers Wood	0230-0300	0	0
Colliers Wood	0300-0330	0	0
Colliers Wood	0330-0400	0	0
Colliers Wood	0400-0430	0	0
Covent Garden	0430-0500	0	0
Covent Garden	0500-0530	2	1
Covent Garden	0530-0600	37	1
Covent Garden	0600-0630	86	1
Covent Garden	0630-0700	222	1
Covent Garden	0700-0730	341	1
Covent Garden	0730-0800	576	1
Covent Garden	0800-0830	791	1
Covent Garden	0830-0900	1171	1
Covent Garden	0900-0930	1367	1
Covent Garden	0930-1000	1252	1
Covent Garden	1000-1030	1001	1
Covent Garden	1030-1100	1034	1
Covent Garden	1100-1130	1040	1
Covent Garden	1130-1200	1149	1
Covent Garden	1200-1230	1225	1
Covent Garden	1230-1300	1315	1
Covent Garden	1300-1330	1337	1
Covent Garden	1330-1400	1356	1
Covent Garden	1400-1430	1411	1
Covent Garden	1430-1500	1462	1
Covent Garden	1500-1530	1472	1
Covent Garden	1530-1600	1639	1
Covent Garden	1600-1630	1745	1
Covent Garden	1630-1700	1940	1
Covent Garden	1700-1730	2280	1
Covent Garden	1730-1800	2587	1
Covent Garden	1800-1830	2728	1
Covent Garden	1830-1900	2461	1
Covent Garden	1900-1930	2028	1
Covent Garden	1930-2000	1345	1
Covent Garden	2000-2030	1134	1
Covent Garden	2030-2100	955	1
Covent Garden	2100-2130	932	1
Covent Garden	2130-2200	937	1
Covent Garden	2200-2230	1646	1
Covent Garden	2230-2300	1276	1
Covent Garden	2300-2330	769	1
Covent Garden	2330-2400	566	1
Covent Garden	0000-0030	492	1
Covent Garden	0030-0100	102	1
Covent Garden	0100-0130	32	1
Covent Garden	0130-0200	13	1
Covent Garden	0200-0230	0	0
Covent Garden	0230-0300	0	0
Covent Garden	0300-0330	0	0
Covent Garden	0330-0400	0	0
Covent Garden	0400-0430	0	0
Croxley	0430-0500	0	0
Croxley	0500-0530	14	1
Croxley	0530-0600	28	1
Croxley	0600-0630	78	1
Croxley	0630-0700	138	1
Croxley	0700-0730	231	1
Croxley	0730-0800	384	1
Croxley	0800-0830	363	1
Croxley	0830-0900	191	1
Croxley	0900-0930	89	1
Croxley	0930-1000	65	1
Croxley	1000-1030	38	1
Croxley	1030-1100	33	1
Croxley	1100-1130	33	1
Croxley	1130-1200	35	1
Croxley	1200-1230	37	1
Croxley	1230-1300	37	1
Croxley	1300-1330	35	1
Croxley	1330-1400	38	1
Croxley	1400-1430	44	1
Croxley	1430-1500	40	1
Croxley	1500-1530	74	1
Croxley	1530-1600	198	1
Croxley	1600-1630	148	1
Croxley	1630-1700	145	1
Croxley	1700-1730	164	1
Croxley	1730-1800	190	1
Croxley	1800-1830	223	1
Croxley	1830-1900	203	1
Croxley	1900-1930	151	1
Croxley	1930-2000	98	1
Croxley	2000-2030	70	1
Croxley	2030-2100	44	1
Croxley	2100-2130	33	1
Croxley	2130-2200	35	1
Croxley	2200-2230	34	1
Croxley	2230-2300	30	1
Croxley	2300-2330	34	1
Croxley	2330-2400	27	1
Croxley	0000-0030	19	1
Croxley	0030-0100	11	1
Croxley	0100-0130	1	1
Croxley	0130-0200	0	1
Croxley	0200-0230	0	0
Croxley	0230-0300	0	0
Croxley	0300-0330	0	0
Croxley	0330-0400	0	0
Croxley	0400-0430	0	0
Dagenham East	0430-0500	0	0
Dagenham East	0500-0530	78	1
Dagenham East	0530-0600	205	1
Dagenham East	0600-0630	376	1
Dagenham East	0630-0700	455	1
Dagenham East	0700-0730	494	1
Dagenham East	0730-0800	583	1
Dagenham East	0800-0830	580	1
Dagenham East	0830-0900	392	1
Dagenham East	0900-0930	291	1
Dagenham East	0930-1000	202	1
Dagenham East	1000-1030	158	1
Dagenham East	1030-1100	146	1
Dagenham East	1100-1130	137	1
Dagenham East	1130-1200	144	1
Dagenham East	1200-1230	149	1
Dagenham East	1230-1300	150	1
Dagenham East	1300-1330	152	1
Dagenham East	1330-1400	158	1
Dagenham East	1400-1430	176	1
Dagenham East	1430-1500	189	1
Dagenham East	1500-1530	223	1
Dagenham East	1530-1600	332	1
Dagenham East	1600-1630	344	1
Dagenham East	1630-1700	418	1
Dagenham East	1700-1730	434	1
Dagenham East	1730-1800	463	1
Dagenham East	1800-1830	448	1
Dagenham East	1830-1900	367	1
Dagenham East	1900-1930	287	1
Dagenham East	1930-2000	208	1
Dagenham East	2000-2030	177	1
Dagenham East	2030-2100	140	1
Dagenham East	2100-2130	119	1
Dagenham East	2130-2200	111	1
Dagenham East	2200-2230	99	1
Dagenham East	2230-2300	85	1
Dagenham East	2300-2330	74	1
Dagenham East	2330-2400	62	1
Dagenham East	0000-0030	38	1
Dagenham East	0030-0100	21	1
Dagenham East	0100-0130	10	1
Dagenham East	0130-0200	0	1
Dagenham East	0200-0230	0	0
Dagenham East	0230-0300	0	0
Dagenham East	0300-0330	0	0
Dagenham East	0330-0400	0	0
Dagenham East	0400-0430	0	0
Dagenham Heathway	0430-0500	0	0
Dagenham Heathway	0500-0530	168	1
Dagenham Heathway	0530-0600	402	1
Dagenham Heathway	0600-0630	803	1
Dagenham Heathway	0630-0700	863	1
Dagenham Heathway	0700-0730	862	1
Dagenham Heathway	0730-0800	929	1
Dagenham Heathway	0800-0830	970	1
Dagenham Heathway	0830-0900	781	1
Dagenham Heathway	0900-0930	613	1
Dagenham Heathway	0930-1000	449	1
Dagenham Heathway	1000-1030	374	1
Dagenham Heathway	1030-1100	346	1
Dagenham Heathway	1100-1130	337	1
Dagenham Heathway	1130-1200	340	1
Dagenham Heathway	1200-1230	340	1
Dagenham Heathway	1230-1300	365	1
Dagenham Heathway	1300-1330	370	1
Dagenham Heathway	1330-1400	365	1
Dagenham Heathway	1400-1430	384	1
Dagenham Heathway	1430-1500	435	1
Dagenham Heathway	1500-1530	487	1
Dagenham Heathway	1530-1600	633	1
Dagenham Heathway	1600-1630	727	1
Dagenham Heathway	1630-1700	844	1
Dagenham Heathway	1700-1730	905	1
Dagenham Heathway	1730-1800	886	1
Dagenham Heathway	1800-1830	897	1
Dagenham Heathway	1830-1900	786	1
Dagenham Heathway	1900-1930	594	1
Dagenham Heathway	1930-2000	417	1
Dagenham Heathway	2000-2030	326	1
Dagenham Heathway	2030-2100	291	1
Dagenham Heathway	2100-2130	251	1
Dagenham Heathway	2130-2200	206	1
Dagenham Heathway	2200-2230	179	1
Dagenham Heathway	2230-2300	164	1
Dagenham Heathway	2300-2330	142	1
Dagenham Heathway	2330-2400	128	1
Dagenham Heathway	0000-0030	86	1
Dagenham Heathway	0030-0100	47	1
Dagenham Heathway	0100-0130	17	1
Dagenham Heathway	0130-0200	2	1
Dagenham Heathway	0200-0230	0	0
Dagenham Heathway	0230-0300	0	0
Dagenham Heathway	0300-0330	0	0
Dagenham Heathway	0330-0400	0	0
Dagenham Heathway	0400-0430	0	0
Debden	0430-0500	0	0
Debden	0500-0530	32	1
Debden	0530-0600	81	1
Debden	0600-0630	187	1
Debden	0630-0700	266	1
Debden	0700-0730	393	1
Debden	0730-0800	610	1
Debden	0800-0830	579	1
Debden	0830-0900	427	1
Debden	0900-0930	386	1
Debden	0930-1000	248	1
Debden	1000-1030	136	1
Debden	1030-1100	130	1
Debden	1100-1130	128	1
Debden	1130-1200	109	1
Debden	1200-1230	114	1
Debden	1230-1300	177	1
Debden	1300-1330	169	1
Debden	1330-1400	143	1
Debden	1400-1430	122	1
Debden	1430-1500	164	1
Debden	1500-1530	245	1
Debden	1530-1600	291	1
Debden	1600-1630	291	1
Debden	1630-1700	373	1
Debden	1700-1730	448	1
Debden	1730-1800	437	1
Debden	1800-1830	433	1
Debden	1830-1900	318	1
Debden	1900-1930	232	1
Debden	1930-2000	146	1
Debden	2000-2030	101	1
Debden	2030-2100	78	1
Debden	2100-2130	79	1
Debden	2130-2200	68	1
Debden	2200-2230	63	1
Debden	2230-2300	62	1
Debden	2300-2330	60	1
Debden	2330-2400	49	1
Debden	0000-0030	34	1
Debden	0030-0100	23	1
Debden	0100-0130	9	1
Debden	0130-0200	0	1
Debden	0200-0230	0	0
Debden	0230-0300	0	0
Debden	0300-0330	0	0
Debden	0330-0400	0	0
Debden	0400-0430	0	0
Dollis Hill	0430-0500	0	0
Dollis Hill	0500-0530	41	1
Dollis Hill	0530-0600	103	1
Dollis Hill	0600-0630	199	1
Dollis Hill	0630-0700	336	1
Dollis Hill	0700-0730	491	1
Dollis Hill	0730-0800	670	1
Dollis Hill	0800-0830	811	1
Dollis Hill	0830-0900	769	1
Dollis Hill	0900-0930	514	1
Dollis Hill	0930-1000	315	1
Dollis Hill	1000-1030	268	1
Dollis Hill	1030-1100	232	1
Dollis Hill	1100-1130	226	1
Dollis Hill	1130-1200	210	1
Dollis Hill	1200-1230	218	1
Dollis Hill	1230-1300	235	1
Dollis Hill	1300-1330	244	1
Dollis Hill	1330-1400	242	1
Dollis Hill	1400-1430	255	1
Dollis Hill	1430-1500	298	1
Dollis Hill	1500-1530	335	1
Dollis Hill	1530-1600	388	1
Dollis Hill	1600-1630	458	1
Dollis Hill	1630-1700	525	1
Dollis Hill	1700-1730	597	1
Dollis Hill	1730-1800	599	1
Dollis Hill	1800-1830	588	1
Dollis Hill	1830-1900	531	1
Dollis Hill	1900-1930	427	1
Dollis Hill	1930-2000	313	1
Dollis Hill	2000-2030	260	1
Dollis Hill	2030-2100	232	1
Dollis Hill	2100-2130	202	1
Dollis Hill	2130-2200	193	1
Dollis Hill	2200-2230	177	1
Dollis Hill	2230-2300	170	1
Dollis Hill	2300-2330	149	1
Dollis Hill	2330-2400	137	1
Dollis Hill	0000-0030	102	1
Dollis Hill	0030-0100	61	1
Dollis Hill	0100-0130	14	1
Dollis Hill	0130-0200	7	1
Dollis Hill	0200-0230	0	0
Dollis Hill	0230-0300	0	0
Dollis Hill	0300-0330	0	0
Dollis Hill	0330-0400	0	0
Dollis Hill	0400-0430	0	0
Ealing Broadway	0430-0500	0	0
Ealing Broadway	0500-0530	125	1
Ealing Broadway	0530-0600	292	1
Ealing Broadway	0600-0630	738	1
Ealing Broadway	0630-0700	1358	1
Ealing Broadway	0700-0730	2082	1
Ealing Broadway	0730-0800	3026	1
Ealing Broadway	0800-0830	3552	1
Ealing Broadway	0830-0900	3028	1
Ealing Broadway	0900-0930	2059	1
Ealing Broadway	0930-1000	1367	1
Ealing Broadway	1000-1030	1042	1
Ealing Broadway	1030-1100	898	1
Ealing Broadway	1100-1130	902	1
Ealing Broadway	1130-1200	867	1
Ealing Broadway	1200-1230	909	1
Ealing Broadway	1230-1300	943	1
Ealing Broadway	1300-1330	980	1
Ealing Broadway	1330-1400	964	1
Ealing Broadway	1400-1430	999	1
Ealing Broadway	1430-1500	1034	1
Ealing Broadway	1500-1530	1099	1
Ealing Broadway	1530-1600	1275	1
Ealing Broadway	1600-1630	1681	1
Ealing Broadway	1630-1700	2016	1
Ealing Broadway	1700-1730	2470	1
Ealing Broadway	1730-1800	2780	1
Ealing Broadway	1800-1830	2751	1
Ealing Broadway	1830-1900	2453	1
Ealing Broadway	1900-1930	1843	1
Ealing Broadway	1930-2000	1377	1
Ealing Broadway	2000-2030	1046	1
Ealing Broadway	2030-2100	854	1
Ealing Broadway	2100-2130	763	1
Ealing Broadway	2130-2200	676	1
Ealing Broadway	2200-2230	679	1
Ealing Broadway	2230-2300	597	1
Ealing Broadway	2300-2330	528	1
Ealing Broadway	2330-2400	408	1
Ealing Broadway	0000-0030	258	1
Ealing Broadway	0030-0100	165	1
Ealing Broadway	0100-0130	73	1
Ealing Broadway	0130-0200	35	1
Ealing Broadway	0200-0230	0	0
Ealing Broadway	0230-0300	0	0
Ealing Broadway	0300-0330	0	0
Ealing Broadway	0330-0400	0	0
Ealing Broadway	0400-0430	0	0
Ealing Common	0430-0500	0	0
Ealing Common	0500-0530	20	1
Ealing Common	0530-0600	43	1
Ealing Common	0600-0630	119	1
Ealing Common	0630-0700	228	1
Ealing Common	0700-0730	408	1
Ealing Common	0730-0800	601	1
Ealing Common	0800-0830	731	1
Ealing Common	0830-0900	568	1
Ealing Common	0900-0930	369	1
Ealing Common	0930-1000	245	1
Ealing Common	1000-1030	183	1
Ealing Common	1030-1100	154	1
Ealing Common	1100-1130	158	1
Ealing Common	1130-1200	144	1
Ealing Common	1200-1230	153	1
Ealing Common	1230-1300	160	1
Ealing Common	1300-1330	171	1
Ealing Common	1330-1400	174	1
Ealing Common	1400-1430	172	1
Ealing Common	1430-1500	178	1
Ealing Common	1500-1530	217	1
Ealing Common	1530-1600	270	1
Ealing Common	1600-1630	321	1
Ealing Common	1630-1700	387	1
Ealing Common	1700-1730	468	1
Ealing Common	1730-1800	521	1
Ealing Common	1800-1830	532	1
Ealing Common	1830-1900	467	1
Ealing Common	1900-1930	351	1
Ealing Common	1930-2000	246	1
Ealing Common	2000-2030	198	1
Ealing Common	2030-2100	171	1
Ealing Common	2100-2130	151	1
Ealing Common	2130-2200	145	1
Ealing Common	2200-2230	144	1
Ealing Common	2230-2300	133	1
Ealing Common	2300-2330	122	1
Ealing Common	2330-2400	89	1
Ealing Common	0000-0030	62	1
Ealing Common	0030-0100	36	1
Ealing Common	0100-0130	9	1
Ealing Common	0130-0200	0	1
Ealing Common	0200-0230	0	0
Ealing Common	0230-0300	0	0
Ealing Common	0300-0330	0	0
Ealing Common	0330-0400	0	0
Ealing Common	0400-0430	0	0
Earl's Court	0430-0500	0	0
Earl's Court	0500-0530	70	1
Earl's Court	0530-0600	160	1
Earl's Court	0600-0630	444	1
Earl's Court	0630-0700	898	1
Earl's Court	0700-0730	1714	1
Earl's Court	0730-0800	2526	1
Earl's Court	0800-0830	2994	1
Earl's Court	0830-0900	3034	1
Earl's Court	0900-0930	2452	1
Earl's Court	0930-1000	2003	1
Earl's Court	1000-1030	1622	1
Earl's Court	1030-1100	1488	1
Earl's Court	1100-1130	1356	1
Earl's Court	1130-1200	1270	1
Earl's Court	1200-1230	1238	1
Earl's Court	1230-1300	1233	1
Earl's Court	1300-1330	1267	1
Earl's Court	1330-1400	1304	1
Earl's Court	1400-1430	1318	1
Earl's Court	1430-1500	1409	1
Earl's Court	1500-1530	1551	1
Earl's Court	1530-1600	1701	1
Earl's Court	1600-1630	1932	1
Earl's Court	1630-1700	2132	1
Earl's Court	1700-1730	2537	1
Earl's Court	1730-1800	2708	1
Earl's Court	1800-1830	2815	1
Earl's Court	1830-1900	2523	1
Earl's Court	1900-1930	2072	1
Earl's Court	1930-2000	1618	1
Earl's Court	2000-2030	1367	1
Earl's Court	2030-2100	1173	1
Earl's Court	2100-2130	1071	1
Earl's Court	2130-2200	992	1
Earl's Court	2200-2230	1035	1
Earl's Court	2230-2300	1074	1
Earl's Court	2300-2330	871	1
Earl's Court	2330-2400	706	1
Earl's Court	0000-0030	440	1
Earl's Court	0030-0100	205	1
Earl's Court	0100-0130	67	1
Earl's Court	0130-0200	31	1
Earl's Court	0200-0230	0	0
Earl's Court	0230-0300	0	0
Earl's Court	0300-0330	0	0
Earl's Court	0330-0400	0	0
Earl's Court	0400-0430	0	0
East Acton	0430-0500	0	0
East Acton	0500-0530	21	1
East Acton	0530-0600	78	1
East Acton	0600-0630	166	1
East Acton	0630-0700	328	1
East Acton	0700-0730	521	1
East Acton	0730-0800	679	1
East Acton	0800-0830	828	1
East Acton	0830-0900	743	1
East Acton	0900-0930	509	1
East Acton	0930-1000	330	1
East Acton	1000-1030	271	1
East Acton	1030-1100	238	1
East Acton	1100-1130	228	1
East Acton	1130-1200	212	1
East Acton	1200-1230	218	1
East Acton	1230-1300	224	1
East Acton	1300-1330	241	1
East Acton	1330-1400	235	1
East Acton	1400-1430	253	1
East Acton	1430-1500	267	1
East Acton	1500-1530	303	1
East Acton	1530-1600	385	1
East Acton	1600-1630	459	1
East Acton	1630-1700	538	1
East Acton	1700-1730	655	1
East Acton	1730-1800	613	1
East Acton	1800-1830	569	1
East Acton	1830-1900	491	1
East Acton	1900-1930	396	1
East Acton	1930-2000	316	1
East Acton	2000-2030	266	1
East Acton	2030-2100	224	1
East Acton	2100-2130	181	1
East Acton	2130-2200	171	1
East Acton	2200-2230	163	1
East Acton	2230-2300	156	1
East Acton	2300-2330	144	1
East Acton	2330-2400	137	1
East Acton	0000-0030	101	1
East Acton	0030-0100	63	1
East Acton	0100-0130	18	1
East Acton	0130-0200	9	1
East Acton	0200-0230	0	0
East Acton	0230-0300	0	0
East Acton	0300-0330	0	0
East Acton	0330-0400	0	0
East Acton	0400-0430	0	0
East Finchley	0430-0500	0	0
East Finchley	0500-0530	21	1
East Finchley	0530-0600	89	1
East Finchley	0600-0630	220	1
East Finchley	0630-0700	424	1
East Finchley	0700-0730	843	1
East Finchley	0730-0800	1365	1
East Finchley	0800-0830	1796	1
East Finchley	0830-0900	1565	1
East Finchley	0900-0930	1101	1
East Finchley	0930-1000	652	1
East Finchley	1000-1030	459	1
East Finchley	1030-1100	388	1
East Finchley	1100-1130	373	1
East Finchley	1130-1200	359	1
East Finchley	1200-1230	364	1
East Finchley	1230-1300	368	1
East Finchley	1300-1330	381	1
East Finchley	1330-1400	371	1
East Finchley	1400-1430	382	1
East Finchley	1430-1500	416	1
East Finchley	1500-1530	458	1
East Finchley	1530-1600	537	1
East Finchley	1600-1630	659	1
East Finchley	1630-1700	797	1
East Finchley	1700-1730	980	1
East Finchley	1730-1800	1155	1
East Finchley	1800-1830	1278	1
East Finchley	1830-1900	1161	1
East Finchley	1900-1930	925	1
East Finchley	1930-2000	657	1
East Finchley	2000-2030	500	1
East Finchley	2030-2100	410	1
East Finchley	2100-2130	371	1
East Finchley	2130-2200	345	1
East Finchley	2200-2230	339	1
East Finchley	2230-2300	352	1
East Finchley	2300-2330	312	1
East Finchley	2330-2400	233	1
East Finchley	0000-0030	147	1
East Finchley	0030-0100	75	1
East Finchley	0100-0130	24	1
East Finchley	0130-0200	9	1
East Finchley	0200-0230	0	0
East Finchley	0230-0300	0	0
East Finchley	0300-0330	0	0
East Finchley	0330-0400	0	0
East Finchley	0400-0430	0	0
East Ham	0430-0500	0	0
East Ham	0500-0530	299	1
East Ham	0530-0600	723	1
East Ham	0600-0630	1589	1
East Ham	0630-0700	2131	1
East Ham	0700-0730	1817	1
East Ham	0730-0800	1828	1
East Ham	0800-0830	2280	1
East Ham	0830-0900	1947	1
East Ham	0900-0930	1513	1
East Ham	0930-1000	1074	1
East Ham	1000-1030	850	1
East Ham	1030-1100	758	1
East Ham	1100-1130	759	1
East Ham	1130-1200	736	1
East Ham	1200-1230	735	1
East Ham	1230-1300	778	1
East Ham	1300-1330	823	1
East Ham	1330-1400	850	1
East Ham	1400-1430	874	1
East Ham	1430-1500	973	1
East Ham	1500-1530	1053	1
East Ham	1530-1600	1248	1
East Ham	1600-1630	1447	1
East Ham	1630-1700	1736	1
East Ham	1700-1730	2044	1
East Ham	1730-1800	2400	1
East Ham	1800-1830	2371	1
East Ham	1830-1900	2140	1
East Ham	1900-1930	1601	1
East Ham	1930-2000	1188	1
East Ham	2000-2030	938	1
East Ham	2030-2100	794	1
East Ham	2100-2130	679	1
East Ham	2130-2200	591	1
East Ham	2200-2230	467	1
East Ham	2230-2300	456	1
East Ham	2300-2330	396	1
East Ham	2330-2400	382	1
East Ham	0000-0030	260	1
East Ham	0030-0100	159	1
East Ham	0100-0130	67	1
East Ham	0130-0200	0	1
East Ham	0200-0230	0	0
East Ham	0230-0300	0	0
East Ham	0300-0330	0	0
East Ham	0330-0400	0	0
East Ham	0400-0430	0	0
East Putney	0430-0500	0	0
East Putney	0500-0530	15	1
East Putney	0530-0600	52	1
East Putney	0600-0630	139	1
East Putney	0630-0700	381	1
East Putney	0700-0730	859	1
East Putney	0730-0800	1430	1
East Putney	0800-0830	1603	1
East Putney	0830-0900	1300	1
East Putney	0900-0930	792	1
East Putney	0930-1000	453	1
East Putney	1000-1030	347	1
East Putney	1030-1100	279	1
East Putney	1100-1130	274	1
East Putney	1130-1200	279	1
East Putney	1200-1230	272	1
East Putney	1230-1300	275	1
East Putney	1300-1330	295	1
East Putney	1330-1400	289	1
East Putney	1400-1430	282	1
East Putney	1430-1500	286	1
East Putney	1500-1530	328	1
East Putney	1530-1600	460	1
East Putney	1600-1630	516	1
East Putney	1630-1700	664	1
East Putney	1700-1730	810	1
East Putney	1730-1800	1010	1
East Putney	1800-1830	1093	1
East Putney	1830-1900	1055	1
East Putney	1900-1930	810	1
East Putney	1930-2000	577	1
East Putney	2000-2030	417	1
East Putney	2030-2100	336	1
East Putney	2100-2130	313	1
East Putney	2130-2200	306	1
East Putney	2200-2230	277	1
East Putney	2230-2300	253	1
East Putney	2300-2330	233	1
East Putney	2330-2400	190	1
East Putney	0000-0030	144	1
East Putney	0030-0100	74	1
East Putney	0100-0130	13	1
East Putney	0130-0200	0	1
East Putney	0200-0230	0	0
East Putney	0230-0300	0	0
East Putney	0300-0330	0	0
East Putney	0330-0400	0	0
East Putney	0400-0430	0	0
Eastcote	0430-0500	0	0
Eastcote	0500-0530	26	1
Eastcote	0530-0600	70	1
Eastcote	0600-0630	179	1
Eastcote	0630-0700	297	1
Eastcote	0700-0730	483	1
Eastcote	0730-0800	686	1
Eastcote	0800-0830	696	1
Eastcote	0830-0900	514	1
Eastcote	0900-0930	320	1
Eastcote	0930-1000	227	1
Eastcote	1000-1030	183	1
Eastcote	1030-1100	167	1
Eastcote	1100-1130	162	1
Eastcote	1130-1200	169	1
Eastcote	1200-1230	171	1
Eastcote	1230-1300	167	1
Eastcote	1300-1330	173	1
Eastcote	1330-1400	172	1
Eastcote	1400-1430	186	1
Eastcote	1430-1500	210	1
Eastcote	1500-1530	224	1
Eastcote	1530-1600	282	1
Eastcote	1600-1630	310	1
Eastcote	1630-1700	364	1
Eastcote	1700-1730	449	1
Eastcote	1730-1800	501	1
Eastcote	1800-1830	542	1
Eastcote	1830-1900	506	1
Eastcote	1900-1930	372	1
Eastcote	1930-2000	237	1
Eastcote	2000-2030	172	1
Eastcote	2030-2100	127	1
Eastcote	2100-2130	116	1
Eastcote	2130-2200	103	1
Eastcote	2200-2230	101	1
Eastcote	2230-2300	97	1
Eastcote	2300-2330	82	1
Eastcote	2330-2400	65	1
Eastcote	0000-0030	35	1
Eastcote	0030-0100	21	1
Eastcote	0100-0130	13	1
Eastcote	0130-0200	0	1
Eastcote	0200-0230	0	0
Eastcote	0230-0300	0	0
Eastcote	0300-0330	0	0
Eastcote	0330-0400	0	0
Eastcote	0400-0430	0	0
Edgware	0430-0500	0	0
Edgware	0500-0530	34	1
Edgware	0530-0600	117	1
Edgware	0600-0630	315	1
Edgware	0630-0700	486	1
Edgware	0700-0730	656	1
Edgware	0730-0800	959	1
Edgware	0800-0830	1148	1
Edgware	0830-0900	870	1
Edgware	0900-0930	602	1
Edgware	0930-1000	460	1
Edgware	1000-1030	346	1
Edgware	1030-1100	305	1
Edgware	1100-1130	302	1
Edgware	1130-1200	297	1
Edgware	1200-1230	316	1
Edgware	1230-1300	343	1
Edgware	1300-1330	353	1
Edgware	1330-1400	365	1
Edgware	1400-1430	354	1
Edgware	1430-1500	378	1
Edgware	1500-1530	405	1
Edgware	1530-1600	467	1
Edgware	1600-1630	553	1
Edgware	1630-1700	597	1
Edgware	1700-1730	690	1
Edgware	1730-1800	797	1
Edgware	1800-1830	819	1
Edgware	1830-1900	720	1
Edgware	1900-1930	542	1
Edgware	1930-2000	393	1
Edgware	2000-2030	300	1
Edgware	2030-2100	245	1
Edgware	2100-2130	215	1
Edgware	2130-2200	191	1
Edgware	2200-2230	180	1
Edgware	2230-2300	182	1
Edgware	2300-2330	154	1
Edgware	2330-2400	117	1
Edgware	0000-0030	79	1
Edgware	0030-0100	40	1
Edgware	0100-0130	22	1
Edgware	0130-0200	5	1
Edgware	0200-0230	0	0
Edgware	0230-0300	0	0
Edgware	0300-0330	0	0
Edgware	0330-0400	0	0
Edgware	0400-0430	0	0
Edgware Road (Bak)	0430-0500	0	0
Edgware Road (Bak)	0500-0530	0	1
Edgware Road (Bak)	0530-0600	20	1
Edgware Road (Bak)	0600-0630	58	1
Edgware Road (Bak)	0630-0700	171	1
Edgware Road (Bak)	0700-0730	337	1
Edgware Road (Bak)	0730-0800	473	1
Edgware Road (Bak)	0800-0830	706	1
Edgware Road (Bak)	0830-0900	966	1
Edgware Road (Bak)	0900-0930	734	1
Edgware Road (Bak)	0930-1000	480	1
Edgware Road (Bak)	1000-1030	379	1
Edgware Road (Bak)	1030-1100	376	1
Edgware Road (Bak)	1100-1130	276	1
Edgware Road (Bak)	1130-1200	278	1
Edgware Road (Bak)	1200-1230	324	1
Edgware Road (Bak)	1230-1300	335	1
Edgware Road (Bak)	1300-1330	328	1
Edgware Road (Bak)	1330-1400	341	1
Edgware Road (Bak)	1400-1430	343	1
Edgware Road (Bak)	1430-1500	333	1
Edgware Road (Bak)	1500-1530	374	1
Edgware Road (Bak)	1530-1600	458	1
Edgware Road (Bak)	1600-1630	532	1
Edgware Road (Bak)	1630-1700	613	1
Edgware Road (Bak)	1700-1730	818	1
Edgware Road (Bak)	1730-1800	966	1
Edgware Road (Bak)	1800-1830	792	1
Edgware Road (Bak)	1830-1900	558	1
Edgware Road (Bak)	1900-1930	427	1
Edgware Road (Bak)	1930-2000	322	1
Edgware Road (Bak)	2000-2030	266	1
Edgware Road (Bak)	2030-2100	239	1
Edgware Road (Bak)	2100-2130	224	1
Edgware Road (Bak)	2130-2200	204	1
Edgware Road (Bak)	2200-2230	201	1
Edgware Road (Bak)	2230-2300	196	1
Edgware Road (Bak)	2300-2330	167	1
Edgware Road (Bak)	2330-2400	123	1
Edgware Road (Bak)	0000-0030	69	1
Edgware Road (Bak)	0030-0100	23	1
Edgware Road (Bak)	0100-0130	0	1
Edgware Road (Bak)	0130-0200	0	1
Edgware Road (Bak)	0200-0230	0	0
Edgware Road (Bak)	0230-0300	0	0
Edgware Road (Bak)	0300-0330	0	0
Edgware Road (Bak)	0330-0400	0	0
Edgware Road (Bak)	0400-0430	0	0
Edgware Road (Cir)	0430-0500	0	0
Edgware Road (Cir)	0500-0530	28	1
Edgware Road (Cir)	0530-0600	60	1
Edgware Road (Cir)	0600-0630	115	1
Edgware Road (Cir)	0630-0700	244	1
Edgware Road (Cir)	0700-0730	473	1
Edgware Road (Cir)	0730-0800	833	1
Edgware Road (Cir)	0800-0830	1284	1
Edgware Road (Cir)	0830-0900	1526	1
Edgware Road (Cir)	0900-0930	1174	1
Edgware Road (Cir)	0930-1000	814	1
Edgware Road (Cir)	1000-1030	580	1
Edgware Road (Cir)	1030-1100	528	1
Edgware Road (Cir)	1100-1130	470	1
Edgware Road (Cir)	1130-1200	468	1
Edgware Road (Cir)	1200-1230	507	1
Edgware Road (Cir)	1230-1300	521	1
Edgware Road (Cir)	1300-1330	521	1
Edgware Road (Cir)	1330-1400	545	1
Edgware Road (Cir)	1400-1430	541	1
Edgware Road (Cir)	1430-1500	544	1
Edgware Road (Cir)	1500-1530	584	1
Edgware Road (Cir)	1530-1600	688	1
Edgware Road (Cir)	1600-1630	793	1
Edgware Road (Cir)	1630-1700	906	1
Edgware Road (Cir)	1700-1730	1237	1
Edgware Road (Cir)	1730-1800	1404	1
Edgware Road (Cir)	1800-1830	1257	1
Edgware Road (Cir)	1830-1900	971	1
Edgware Road (Cir)	1900-1930	697	1
Edgware Road (Cir)	1930-2000	529	1
Edgware Road (Cir)	2000-2030	438	1
Edgware Road (Cir)	2030-2100	373	1
Edgware Road (Cir)	2100-2130	333	1
Edgware Road (Cir)	2130-2200	302	1
Edgware Road (Cir)	2200-2230	291	1
Edgware Road (Cir)	2230-2300	256	1
Edgware Road (Cir)	2300-2330	219	1
Edgware Road (Cir)	2330-2400	157	1
Edgware Road (Cir)	0000-0030	92	1
Edgware Road (Cir)	0030-0100	52	1
Edgware Road (Cir)	0100-0130	11	1
Edgware Road (Cir)	0130-0200	0	1
Edgware Road (Cir)	0200-0230	0	0
Edgware Road (Cir)	0230-0300	0	0
Edgware Road (Cir)	0300-0330	0	0
Edgware Road (Cir)	0330-0400	0	0
Edgware Road (Cir)	0400-0430	0	0
Elephant & Castle	0430-0500	0	0
Elephant & Castle	0500-0530	46	1
Elephant & Castle	0530-0600	200	1
Elephant & Castle	0600-0630	500	1
Elephant & Castle	0630-0700	1057	1
Elephant & Castle	0700-0730	2045	1
Elephant & Castle	0730-0800	2501	1
Elephant & Castle	0800-0830	3310	1
Elephant & Castle	0830-0900	4271	1
Elephant & Castle	0900-0930	3814	1
Elephant & Castle	0930-1000	3084	1
Elephant & Castle	1000-1030	2125	1
Elephant & Castle	1030-1100	1758	1
Elephant & Castle	1100-1130	1470	1
Elephant & Castle	1130-1200	1316	1
Elephant & Castle	1200-1230	1373	1
Elephant & Castle	1230-1300	1500	1
Elephant & Castle	1300-1330	1532	1
Elephant & Castle	1330-1400	1533	1
Elephant & Castle	1400-1430	1462	1
Elephant & Castle	1430-1500	1494	1
Elephant & Castle	1500-1530	1711	1
Elephant & Castle	1530-1600	1989	1
Elephant & Castle	1600-1630	2446	1
Elephant & Castle	1630-1700	2812	1
Elephant & Castle	1700-1730	3209	1
Elephant & Castle	1730-1800	3127	1
Elephant & Castle	1800-1830	3018	1
Elephant & Castle	1830-1900	2571	1
Elephant & Castle	1900-1930	2021	1
Elephant & Castle	1930-2000	1653	1
Elephant & Castle	2000-2030	1396	1
Elephant & Castle	2030-2100	1261	1
Elephant & Castle	2100-2130	1175	1
Elephant & Castle	2130-2200	1095	1
Elephant & Castle	2200-2230	1038	1
Elephant & Castle	2230-2300	1019	1
Elephant & Castle	2300-2330	950	1
Elephant & Castle	2330-2400	765	1
Elephant & Castle	0000-0030	442	1
Elephant & Castle	0030-0100	151	1
Elephant & Castle	0100-0130	4	1
Elephant & Castle	0130-0200	0	1
Elephant & Castle	0200-0230	0	0
Elephant & Castle	0230-0300	0	0
Elephant & Castle	0300-0330	0	0
Elephant & Castle	0330-0400	0	0
Elephant & Castle	0400-0430	0	0
Elm Park	0430-0500	0	0
Elm Park	0500-0530	78	1
Elm Park	0530-0600	183	1
Elm Park	0600-0630	356	1
Elm Park	0630-0700	495	1
Elm Park	0700-0730	652	1
Elm Park	0730-0800	857	1
Elm Park	0800-0830	869	1
Elm Park	0830-0900	516	1
Elm Park	0900-0930	281	1
Elm Park	0930-1000	200	1
Elm Park	1000-1030	157	1
Elm Park	1030-1100	147	1
Elm Park	1100-1130	131	1
Elm Park	1130-1200	123	1
Elm Park	1200-1230	128	1
Elm Park	1230-1300	136	1
Elm Park	1300-1330	138	1
Elm Park	1330-1400	148	1
Elm Park	1400-1430	154	1
Elm Park	1430-1500	168	1
Elm Park	1500-1530	186	1
Elm Park	1530-1600	298	1
Elm Park	1600-1630	340	1
Elm Park	1630-1700	415	1
Elm Park	1700-1730	491	1
Elm Park	1730-1800	573	1
Elm Park	1800-1830	627	1
Elm Park	1830-1900	482	1
Elm Park	1900-1930	321	1
Elm Park	1930-2000	221	1
Elm Park	2000-2030	177	1
Elm Park	2030-2100	140	1
Elm Park	2100-2130	120	1
Elm Park	2130-2200	102	1
Elm Park	2200-2230	89	1
Elm Park	2230-2300	94	1
Elm Park	2300-2330	89	1
Elm Park	2330-2400	78	1
Elm Park	0000-0030	59	1
Elm Park	0030-0100	25	1
Elm Park	0100-0130	15	1
Elm Park	0130-0200	3	1
Elm Park	0200-0230	0	0
Elm Park	0230-0300	0	0
Elm Park	0300-0330	0	0
Elm Park	0330-0400	0	0
Elm Park	0400-0430	0	0
Embankment	0430-0500	0	0
Embankment	0500-0530	26	1
Embankment	0530-0600	125	1
Embankment	0600-0630	318	1
Embankment	0630-0700	709	1
Embankment	0700-0730	1295	1
Embankment	0730-0800	2019	1
Embankment	0800-0830	2789	1
Embankment	0830-0900	3520	1
Embankment	0900-0930	3356	1
Embankment	0930-1000	2257	1
Embankment	1000-1030	1510	1
Embankment	1030-1100	1349	1
Embankment	1100-1130	1212	1
Embankment	1130-1200	1320	1
Embankment	1200-1230	1449	1
Embankment	1230-1300	1464	1
Embankment	1300-1330	1427	1
Embankment	1330-1400	1477	1
Embankment	1400-1430	1441	1
Embankment	1430-1500	1545	1
Embankment	1500-1530	1665	1
Embankment	1530-1600	1893	1
Embankment	1600-1630	2312	1
Embankment	1630-1700	2709	1
Embankment	1700-1730	3537	1
Embankment	1730-1800	4305	1
Embankment	1800-1830	4154	1
Embankment	1830-1900	3238	1
Embankment	1900-1930	2276	1
Embankment	1930-2000	1485	1
Embankment	2000-2030	1237	1
Embankment	2030-2100	1091	1
Embankment	2100-2130	1116	1
Embankment	2130-2200	1447	1
Embankment	2200-2230	1719	1
Embankment	2230-2300	1434	1
Embankment	2300-2330	1120	1
Embankment	2330-2400	708	1
Embankment	0000-0030	355	1
Embankment	0030-0100	104	1
Embankment	0100-0130	28	1
Embankment	0130-0200	14	1
Embankment	0200-0230	0	0
Embankment	0230-0300	0	0
Embankment	0300-0330	0	0
Embankment	0330-0400	0	0
Embankment	0400-0430	0	0
Epping	0430-0500	0	0
Epping	0500-0530	78	1
Epping	0530-0600	186	1
Epping	0600-0630	440	1
Epping	0630-0700	700	1
Epping	0700-0730	911	1
Epping	0730-0800	1029	1
Epping	0800-0830	770	1
Epping	0830-0900	419	1
Epping	0900-0930	245	1
Epping	0930-1000	215	1
Epping	1000-1030	169	1
Epping	1030-1100	155	1
Epping	1100-1130	183	1
Epping	1130-1200	151	1
Epping	1200-1230	148	1
Epping	1230-1300	152	1
Epping	1300-1330	155	1
Epping	1330-1400	157	1
Epping	1400-1430	174	1
Epping	1430-1500	184	1
Epping	1500-1530	231	1
Epping	1530-1600	311	1
Epping	1600-1630	392	1
Epping	1630-1700	559	1
Epping	1700-1730	619	1
Epping	1730-1800	620	1
Epping	1800-1830	643	1
Epping	1830-1900	642	1
Epping	1900-1930	453	1
Epping	1930-2000	291	1
Epping	2000-2030	202	1
Epping	2030-2100	154	1
Epping	2100-2130	138	1
Epping	2130-2200	118	1
Epping	2200-2230	120	1
Epping	2230-2300	120	1
Epping	2300-2330	134	1
Epping	2330-2400	125	1
Epping	0000-0030	95	1
Epping	0030-0100	60	1
Epping	0100-0130	22	1
Epping	0130-0200	3	1
Epping	0200-0230	0	0
Epping	0230-0300	0	0
Epping	0300-0330	0	0
Epping	0330-0400	0	0
Epping	0400-0430	0	0
Euston	0430-0500	0	0
Euston	0500-0530	38	1
Euston	0530-0600	255	1
Euston	0600-0630	748	1
Euston	0630-0700	1879	1
Euston	0700-0730	3411	1
Euston	0730-0800	4744	1
Euston	0800-0830	5844	1
Euston	0830-0900	6347	1
Euston	0900-0930	5559	1
Euston	0930-1000	4387	1
Euston	1000-1030	3467	1
Euston	1030-1100	3341	1
Euston	1100-1130	2751	1
Euston	1130-1200	2973	1
Euston	1200-1230	3212	1
Euston	1230-1300	3192	1
Euston	1300-1330	3229	1
Euston	1330-1400	3150	1
Euston	1400-1430	3131	1
Euston	1430-1500	3029	1
Euston	1500-1530	3287	1
Euston	1530-1600	3659	1
Euston	1600-1630	4483	1
Euston	1630-1700	5205	1
Euston	1700-1730	6169	1
Euston	1730-1800	7132	1
Euston	1800-1830	6728	1
Euston	1830-1900	5445	1
Euston	1900-1930	4087	1
Euston	1930-2000	3353	1
Euston	2000-2030	2921	1
Euston	2030-2100	2478	1
Euston	2100-2130	2258	1
Euston	2130-2200	1784	1
Euston	2200-2230	1673	1
Euston	2230-2300	1473	1
Euston	2300-2330	1167	1
Euston	2330-2400	842	1
Euston	0000-0030	452	1
Euston	0030-0100	159	1
Euston	0100-0130	67	1
Euston	0130-0200	32	1
Euston	0200-0230	0	0
Euston	0230-0300	0	0
Euston	0300-0330	0	0
Euston	0330-0400	0	0
Euston	0400-0430	0	0
Euston Square	0430-0500	0	0
Euston Square	0500-0530	28	1
Euston Square	0530-0600	91	1
Euston Square	0600-0630	179	1
Euston Square	0630-0700	526	1
Euston Square	0700-0730	1012	1
Euston Square	0730-0800	1708	1
Euston Square	0800-0830	2457	1
Euston Square	0830-0900	3501	1
Euston Square	0900-0930	2966	1
Euston Square	0930-1000	1961	1
Euston Square	1000-1030	1325	1
Euston Square	1030-1100	1277	1
Euston Square	1100-1130	998	1
Euston Square	1130-1200	923	1
Euston Square	1200-1230	994	1
Euston Square	1230-1300	1077	1
Euston Square	1300-1330	1101	1
Euston Square	1330-1400	1118	1
Euston Square	1400-1430	1047	1
Euston Square	1430-1500	990	1
Euston Square	1500-1530	1121	1
Euston Square	1530-1600	1314	1
Euston Square	1600-1630	1768	1
Euston Square	1630-1700	2086	1
Euston Square	1700-1730	2932	1
Euston Square	1730-1800	3298	1
Euston Square	1800-1830	2812	1
Euston Square	1830-1900	1984	1
Euston Square	1900-1930	1394	1
Euston Square	1930-2000	1052	1
Euston Square	2000-2030	887	1
Euston Square	2030-2100	762	1
Euston Square	2100-2130	679	1
Euston Square	2130-2200	487	1
Euston Square	2200-2230	421	1
Euston Square	2230-2300	348	1
Euston Square	2300-2330	274	1
Euston Square	2330-2400	187	1
Euston Square	0000-0030	99	1
Euston Square	0030-0100	32	1
Euston Square	0100-0130	3	1
Euston Square	0130-0200	0	1
Euston Square	0200-0230	0	0
Euston Square	0230-0300	0	0
Euston Square	0300-0330	0	0
Euston Square	0330-0400	0	0
Euston Square	0400-0430	0	0
Fairlop	0430-0500	0	0
Fairlop	0500-0530	15	1
Fairlop	0530-0600	62	1
Fairlop	0600-0630	124	1
Fairlop	0630-0700	170	1
Fairlop	0700-0730	195	1
Fairlop	0730-0800	308	1
Fairlop	0800-0830	341	1
Fairlop	0830-0900	173	1
Fairlop	0900-0930	108	1
Fairlop	0930-1000	66	1
Fairlop	1000-1030	50	1
Fairlop	1030-1100	43	1
Fairlop	1100-1130	46	1
Fairlop	1130-1200	45	1
Fairlop	1200-1230	44	1
Fairlop	1230-1300	43	1
Fairlop	1300-1330	61	1
Fairlop	1330-1400	64	1
Fairlop	1400-1430	62	1
Fairlop	1430-1500	56	1
Fairlop	1500-1530	88	1
Fairlop	1530-1600	101	1
Fairlop	1600-1630	108	1
Fairlop	1630-1700	140	1
Fairlop	1700-1730	180	1
Fairlop	1730-1800	205	1
Fairlop	1800-1830	228	1
Fairlop	1830-1900	193	1
Fairlop	1900-1930	154	1
Fairlop	1930-2000	93	1
Fairlop	2000-2030	74	1
Fairlop	2030-2100	58	1
Fairlop	2100-2130	51	1
Fairlop	2130-2200	40	1
Fairlop	2200-2230	39	1
Fairlop	2230-2300	39	1
Fairlop	2300-2330	32	1
Fairlop	2330-2400	27	1
Fairlop	0000-0030	18	1
Fairlop	0030-0100	10	1
Fairlop	0100-0130	3	1
Fairlop	0130-0200	2	1
Fairlop	0200-0230	0	0
Fairlop	0230-0300	0	0
Fairlop	0300-0330	0	0
Fairlop	0330-0400	0	0
Fairlop	0400-0430	0	0
Farringdon	0430-0500	0	0
Farringdon	0500-0530	32	1
Farringdon	0530-0600	155	1
Farringdon	0600-0630	295	1
Farringdon	0630-0700	656	1
Farringdon	0700-0730	1062	1
Farringdon	0730-0800	2486	1
Farringdon	0800-0830	3947	1
Farringdon	0830-0900	6351	1
Farringdon	0900-0930	6505	1
Farringdon	0930-1000	3831	1
Farringdon	1000-1030	1883	1
Farringdon	1030-1100	1287	1
Farringdon	1100-1130	1051	1
Farringdon	1130-1200	1080	1
Farringdon	1200-1230	1150	1
Farringdon	1230-1300	1220	1
Farringdon	1300-1330	1215	1
Farringdon	1330-1400	1208	1
Farringdon	1400-1430	1130	1
Farringdon	1430-1500	1145	1
Farringdon	1500-1530	1184	1
Farringdon	1530-1600	1535	1
Farringdon	1600-1630	2138	1
Farringdon	1630-1700	2855	1
Farringdon	1700-1730	4294	1
Farringdon	1730-1800	5896	1
Farringdon	1800-1830	5179	1
Farringdon	1830-1900	3374	1
Farringdon	1900-1930	2242	1
Farringdon	1930-2000	1502	1
Farringdon	2000-2030	1077	1
Farringdon	2030-2100	892	1
Farringdon	2100-2130	735	1
Farringdon	2130-2200	661	1
Farringdon	2200-2230	645	1
Farringdon	2230-2300	576	1
Farringdon	2300-2330	608	1
Farringdon	2330-2400	516	1
Farringdon	0000-0030	262	1
Farringdon	0030-0100	70	1
Farringdon	0100-0130	7	1
Farringdon	0130-0200	1	1
Farringdon	0200-0230	0	0
Farringdon	0230-0300	0	0
Farringdon	0300-0330	0	0
Farringdon	0330-0400	0	0
Farringdon	0400-0430	0	0
Finchley Central	0430-0500	0	0
Finchley Central	0500-0530	23	1
Finchley Central	0530-0600	89	1
Finchley Central	0600-0630	190	1
Finchley Central	0630-0700	464	1
Finchley Central	0700-0730	908	1
Finchley Central	0730-0800	1432	1
Finchley Central	0800-0830	1782	1
Finchley Central	0830-0900	1508	1
Finchley Central	0900-0930	1006	1
Finchley Central	0930-1000	631	1
Finchley Central	1000-1030	460	1
Finchley Central	1030-1100	403	1
Finchley Central	1100-1130	365	1
Finchley Central	1130-1200	387	1
Finchley Central	1200-1230	374	1
Finchley Central	1230-1300	387	1
Finchley Central	1300-1330	407	1
Finchley Central	1330-1400	398	1
Finchley Central	1400-1430	403	1
Finchley Central	1430-1500	410	1
Finchley Central	1500-1530	491	1
Finchley Central	1530-1600	566	1
Finchley Central	1600-1630	740	1
Finchley Central	1630-1700	830	1
Finchley Central	1700-1730	1076	1
Finchley Central	1730-1800	1305	1
Finchley Central	1800-1830	1243	1
Finchley Central	1830-1900	1128	1
Finchley Central	1900-1930	815	1
Finchley Central	1930-2000	576	1
Finchley Central	2000-2030	430	1
Finchley Central	2030-2100	387	1
Finchley Central	2100-2130	385	1
Finchley Central	2130-2200	331	1
Finchley Central	2200-2230	313	1
Finchley Central	2230-2300	281	1
Finchley Central	2300-2330	232	1
Finchley Central	2330-2400	239	1
Finchley Central	0000-0030	175	1
Finchley Central	0030-0100	94	1
Finchley Central	0100-0130	32	1
Finchley Central	0130-0200	8	1
Finchley Central	0200-0230	0	0
Finchley Central	0230-0300	0	0
Finchley Central	0300-0330	0	0
Finchley Central	0330-0400	0	0
Finchley Central	0400-0430	0	0
Finchley Road	0430-0500	0	0
Finchley Road	0500-0530	21	1
Finchley Road	0530-0600	101	1
Finchley Road	0600-0630	207	1
Finchley Road	0630-0700	484	1
Finchley Road	0700-0730	875	1
Finchley Road	0730-0800	1359	1
Finchley Road	0800-0830	1818	1
Finchley Road	0830-0900	1706	1
Finchley Road	0900-0930	1186	1
Finchley Road	0930-1000	882	1
Finchley Road	1000-1030	641	1
Finchley Road	1030-1100	556	1
Finchley Road	1100-1130	519	1
Finchley Road	1130-1200	531	1
Finchley Road	1200-1230	553	1
Finchley Road	1230-1300	586	1
Finchley Road	1300-1330	605	1
Finchley Road	1330-1400	620	1
Finchley Road	1400-1430	605	1
Finchley Road	1430-1500	621	1
Finchley Road	1500-1530	717	1
Finchley Road	1530-1600	813	1
Finchley Road	1600-1630	1068	1
Finchley Road	1630-1700	1178	1
Finchley Road	1700-1730	1335	1
Finchley Road	1730-1800	1584	1
Finchley Road	1800-1830	1707	1
Finchley Road	1830-1900	1539	1
Finchley Road	1900-1930	1177	1
Finchley Road	1930-2000	862	1
Finchley Road	2000-2030	660	1
Finchley Road	2030-2100	546	1
Finchley Road	2100-2130	486	1
Finchley Road	2130-2200	446	1
Finchley Road	2200-2230	420	1
Finchley Road	2230-2300	374	1
Finchley Road	2300-2330	315	1
Finchley Road	2330-2400	279	1
Finchley Road	0000-0030	178	1
Finchley Road	0030-0100	67	1
Finchley Road	0100-0130	14	1
Finchley Road	0130-0200	8	1
Finchley Road	0200-0230	0	0
Finchley Road	0230-0300	0	0
Finchley Road	0300-0330	0	0
Finchley Road	0330-0400	0	0
Finchley Road	0400-0430	0	0
Finsbury Park	0430-0500	7	1
Finsbury Park	0500-0530	164	1
Finsbury Park	0530-0600	463	1
Finsbury Park	0600-0630	991	1
Finsbury Park	0630-0700	1846	1
Finsbury Park	0700-0730	3286	1
Finsbury Park	0730-0800	4861	1
Finsbury Park	0800-0830	6051	1
Finsbury Park	0830-0900	5420	1
Finsbury Park	0900-0930	4229	1
Finsbury Park	0930-1000	3061	1
Finsbury Park	1000-1030	1950	1
Finsbury Park	1030-1100	1673	1
Finsbury Park	1100-1130	1543	1
Finsbury Park	1130-1200	1516	1
Finsbury Park	1200-1230	1594	1
Finsbury Park	1230-1300	1614	1
Finsbury Park	1300-1330	1623	1
Finsbury Park	1330-1400	1695	1
Finsbury Park	1400-1430	1699	1
Finsbury Park	1430-1500	1758	1
Finsbury Park	1500-1530	1894	1
Finsbury Park	1530-1600	2221	1
Finsbury Park	1600-1630	2743	1
Finsbury Park	1630-1700	3541	1
Finsbury Park	1700-1730	4073	1
Finsbury Park	1730-1800	4871	1
Finsbury Park	1800-1830	5244	1
Finsbury Park	1830-1900	4681	1
Finsbury Park	1900-1930	3637	1
Finsbury Park	1930-2000	2675	1
Finsbury Park	2000-2030	2187	1
Finsbury Park	2030-2100	1859	1
Finsbury Park	2100-2130	1855	1
Finsbury Park	2130-2200	1796	1
Finsbury Park	2200-2230	1865	1
Finsbury Park	2230-2300	1711	1
Finsbury Park	2300-2330	1404	1
Finsbury Park	2330-2400	1033	1
Finsbury Park	0000-0030	604	1
Finsbury Park	0030-0100	293	1
Finsbury Park	0100-0130	96	1
Finsbury Park	0130-0200	64	1
Finsbury Park	0200-0230	0	0
Finsbury Park	0230-0300	0	0
Finsbury Park	0300-0330	0	0
Finsbury Park	0330-0400	0	0
Finsbury Park	0400-0430	0	0
Fulham Broadway	0430-0500	0	0
Fulham Broadway	0500-0530	11	1
Fulham Broadway	0530-0600	35	1
Fulham Broadway	0600-0630	122	1
Fulham Broadway	0630-0700	313	1
Fulham Broadway	0700-0730	741	1
Fulham Broadway	0730-0800	1293	1
Fulham Broadway	0800-0830	1752	1
Fulham Broadway	0830-0900	1755	1
Fulham Broadway	0900-0930	1153	1
Fulham Broadway	0930-1000	839	1
Fulham Broadway	1000-1030	681	1
Fulham Broadway	1030-1100	599	1
Fulham Broadway	1100-1130	580	1
Fulham Broadway	1130-1200	609	1
Fulham Broadway	1200-1230	625	1
Fulham Broadway	1230-1300	630	1
Fulham Broadway	1300-1330	649	1
Fulham Broadway	1330-1400	669	1
Fulham Broadway	1400-1430	696	1
Fulham Broadway	1430-1500	701	1
Fulham Broadway	1500-1530	793	1
Fulham Broadway	1530-1600	1183	1
Fulham Broadway	1600-1630	990	1
Fulham Broadway	1630-1700	1114	1
Fulham Broadway	1700-1730	1366	1
Fulham Broadway	1730-1800	1446	1
Fulham Broadway	1800-1830	1595	1
Fulham Broadway	1830-1900	1406	1
Fulham Broadway	1900-1930	1151	1
Fulham Broadway	1930-2000	850	1
Fulham Broadway	2000-2030	647	1
Fulham Broadway	2030-2100	519	1
Fulham Broadway	2100-2130	442	1
Fulham Broadway	2130-2200	445	1
Fulham Broadway	2200-2230	383	1
Fulham Broadway	2230-2300	464	1
Fulham Broadway	2300-2330	485	1
Fulham Broadway	2330-2400	365	1
Fulham Broadway	0000-0030	177	1
Fulham Broadway	0030-0100	55	1
Fulham Broadway	0100-0130	6	1
Fulham Broadway	0130-0200	0	1
Fulham Broadway	0200-0230	0	0
Fulham Broadway	0230-0300	0	0
Fulham Broadway	0300-0330	0	0
Fulham Broadway	0330-0400	0	0
Fulham Broadway	0400-0430	0	0
Gants Hill	0430-0500	0	0
Gants Hill	0500-0530	105	1
Gants Hill	0530-0600	286	1
Gants Hill	0600-0630	518	1
Gants Hill	0630-0700	744	1
Gants Hill	0700-0730	881	1
Gants Hill	0730-0800	1176	1
Gants Hill	0800-0830	1524	1
Gants Hill	0830-0900	1131	1
Gants Hill	0900-0930	767	1
Gants Hill	0930-1000	535	1
Gants Hill	1000-1030	418	1
Gants Hill	1030-1100	338	1
Gants Hill	1100-1130	324	1
Gants Hill	1130-1200	294	1
Gants Hill	1200-1230	309	1
Gants Hill	1230-1300	319	1
Gants Hill	1300-1330	341	1
Gants Hill	1330-1400	333	1
Gants Hill	1400-1430	346	1
Gants Hill	1430-1500	379	1
Gants Hill	1500-1530	401	1
Gants Hill	1530-1600	515	1
Gants Hill	1600-1630	590	1
Gants Hill	1630-1700	756	1
Gants Hill	1700-1730	952	1
Gants Hill	1730-1800	1114	1
Gants Hill	1800-1830	1239	1
Gants Hill	1830-1900	1091	1
Gants Hill	1900-1930	842	1
Gants Hill	1930-2000	619	1
Gants Hill	2000-2030	454	1
Gants Hill	2030-2100	422	1
Gants Hill	2100-2130	341	1
Gants Hill	2130-2200	280	1
Gants Hill	2200-2230	261	1
Gants Hill	2230-2300	238	1
Gants Hill	2300-2330	201	1
Gants Hill	2330-2400	183	1
Gants Hill	0000-0030	113	1
Gants Hill	0030-0100	77	1
Gants Hill	0100-0130	24	1
Gants Hill	0130-0200	16	1
Gants Hill	0200-0230	0	0
Gants Hill	0230-0300	0	0
Gants Hill	0300-0330	0	0
Gants Hill	0330-0400	0	0
Gants Hill	0400-0430	0	0
Gloucester Road	0430-0500	0	0
Gloucester Road	0500-0530	18	1
Gloucester Road	0530-0600	76	1
Gloucester Road	0600-0630	223	1
Gloucester Road	0630-0700	490	1
Gloucester Road	0700-0730	861	1
Gloucester Road	0730-0800	1528	1
Gloucester Road	0800-0830	1856	1
Gloucester Road	0830-0900	2141	1
Gloucester Road	0900-0930	1856	1
Gloucester Road	0930-1000	1487	1
Gloucester Road	1000-1030	1186	1
Gloucester Road	1030-1100	1121	1
Gloucester Road	1100-1130	1004	1
Gloucester Road	1130-1200	946	1
Gloucester Road	1200-1230	930	1
Gloucester Road	1230-1300	936	1
Gloucester Road	1300-1330	949	1
Gloucester Road	1330-1400	975	1
Gloucester Road	1400-1430	964	1
Gloucester Road	1430-1500	1036	1
Gloucester Road	1500-1530	1136	1
Gloucester Road	1530-1600	1300	1
Gloucester Road	1600-1630	1526	1
Gloucester Road	1630-1700	1690	1
Gloucester Road	1700-1730	1948	1
Gloucester Road	1730-1800	1976	1
Gloucester Road	1800-1830	1999	1
Gloucester Road	1830-1900	1701	1
Gloucester Road	1900-1930	1408	1
Gloucester Road	1930-2000	1100	1
Gloucester Road	2000-2030	957	1
Gloucester Road	2030-2100	787	1
Gloucester Road	2100-2130	699	1
Gloucester Road	2130-2200	675	1
Gloucester Road	2200-2230	704	1
Gloucester Road	2230-2300	731	1
Gloucester Road	2300-2330	603	1
Gloucester Road	2330-2400	415	1
Gloucester Road	0000-0030	230	1
Gloucester Road	0030-0100	82	1
Gloucester Road	0100-0130	20	1
Gloucester Road	0130-0200	13	1
Gloucester Road	0200-0230	0	0
Gloucester Road	0230-0300	0	0
Gloucester Road	0300-0330	0	0
Gloucester Road	0330-0400	0	0
Gloucester Road	0400-0430	0	0
Golders Green	0430-0500	0	0
Golders Green	0500-0530	23	1
Golders Green	0530-0600	119	1
Golders Green	0600-0630	264	1
Golders Green	0630-0700	420	1
Golders Green	0700-0730	765	1
Golders Green	0730-0800	1243	1
Golders Green	0800-0830	1585	1
Golders Green	0830-0900	1475	1
Golders Green	0900-0930	1068	1
Golders Green	0930-1000	775	1
Golders Green	1000-1030	598	1
Golders Green	1030-1100	513	1
Golders Green	1100-1130	498	1
Golders Green	1130-1200	494	1
Golders Green	1200-1230	523	1
Golders Green	1230-1300	540	1
Golders Green	1300-1330	575	1
Golders Green	1330-1400	550	1
Golders Green	1400-1430	574	1
Golders Green	1430-1500	586	1
Golders Green	1500-1530	656	1
Golders Green	1530-1600	748	1
Golders Green	1600-1630	844	1
Golders Green	1630-1700	901	1
Golders Green	1700-1730	1081	1
Golders Green	1730-1800	1251	1
Golders Green	1800-1830	1264	1
Golders Green	1830-1900	1124	1
Golders Green	1900-1930	922	1
Golders Green	1930-2000	722	1
Golders Green	2000-2030	553	1
Golders Green	2030-2100	497	1
Golders Green	2100-2130	435	1
Golders Green	2130-2200	403	1
Golders Green	2200-2230	388	1
Golders Green	2230-2300	381	1
Golders Green	2300-2330	310	1
Golders Green	2330-2400	262	1
Golders Green	0000-0030	192	1
Golders Green	0030-0100	116	1
Golders Green	0100-0130	42	1
Golders Green	0130-0200	12	1
Golders Green	0200-0230	0	0
Golders Green	0230-0300	0	0
Golders Green	0300-0330	0	0
Golders Green	0330-0400	0	0
Golders Green	0400-0430	0	0
Goldhawk Road	0430-0500	0	0
Goldhawk Road	0500-0530	8	1
Goldhawk Road	0530-0600	20	1
Goldhawk Road	0600-0630	51	1
Goldhawk Road	0630-0700	107	1
Goldhawk Road	0700-0730	184	1
Goldhawk Road	0730-0800	309	1
Goldhawk Road	0800-0830	425	1
Goldhawk Road	0830-0900	398	1
Goldhawk Road	0900-0930	309	1
Goldhawk Road	0930-1000	224	1
Goldhawk Road	1000-1030	168	1
Goldhawk Road	1030-1100	138	1
Goldhawk Road	1100-1130	133	1
Goldhawk Road	1130-1200	133	1
Goldhawk Road	1200-1230	145	1
Goldhawk Road	1230-1300	158	1
Goldhawk Road	1300-1330	162	1
Goldhawk Road	1330-1400	161	1
Goldhawk Road	1400-1430	155	1
Goldhawk Road	1430-1500	150	1
Goldhawk Road	1500-1530	169	1
Goldhawk Road	1530-1600	182	1
Goldhawk Road	1600-1630	214	1
Goldhawk Road	1630-1700	241	1
Goldhawk Road	1700-1730	268	1
Goldhawk Road	1730-1800	298	1
Goldhawk Road	1800-1830	329	1
Goldhawk Road	1830-1900	313	1
Goldhawk Road	1900-1930	244	1
Goldhawk Road	1930-2000	182	1
Goldhawk Road	2000-2030	141	1
Goldhawk Road	2030-2100	115	1
Goldhawk Road	2100-2130	107	1
Goldhawk Road	2130-2200	99	1
Goldhawk Road	2200-2230	95	1
Goldhawk Road	2230-2300	97	1
Goldhawk Road	2300-2330	87	1
Goldhawk Road	2330-2400	61	1
Goldhawk Road	0000-0030	34	1
Goldhawk Road	0030-0100	16	1
Goldhawk Road	0100-0130	2	1
Goldhawk Road	0130-0200	0	1
Goldhawk Road	0200-0230	0	0
Goldhawk Road	0230-0300	0	0
Goldhawk Road	0300-0330	0	0
Goldhawk Road	0330-0400	0	0
Goldhawk Road	0400-0430	0	0
Goodge Street	0430-0500	0	0
Goodge Street	0500-0530	0	1
Goodge Street	0530-0600	21	1
Goodge Street	0600-0630	72	1
Goodge Street	0630-0700	188	1
Goodge Street	0700-0730	353	1
Goodge Street	0730-0800	573	1
Goodge Street	0800-0830	904	1
Goodge Street	0830-0900	1336	1
Goodge Street	0900-0930	1465	1
Goodge Street	0930-1000	1181	1
Goodge Street	1000-1030	746	1
Goodge Street	1030-1100	641	1
Goodge Street	1100-1130	537	1
Goodge Street	1130-1200	516	1
Goodge Street	1200-1230	549	1
Goodge Street	1230-1300	634	1
Goodge Street	1300-1330	624	1
Goodge Street	1330-1400	631	1
Goodge Street	1400-1430	588	1
Goodge Street	1430-1500	608	1
Goodge Street	1500-1530	647	1
Goodge Street	1530-1600	720	1
Goodge Street	1600-1630	851	1
Goodge Street	1630-1700	983	1
Goodge Street	1700-1730	1331	1
Goodge Street	1730-1800	1704	1
Goodge Street	1800-1830	1599	1
Goodge Street	1830-1900	1237	1
Goodge Street	1900-1930	892	1
Goodge Street	1930-2000	636	1
Goodge Street	2000-2030	543	1
Goodge Street	2030-2100	459	1
Goodge Street	2100-2130	451	1
Goodge Street	2130-2200	328	1
Goodge Street	2200-2230	292	1
Goodge Street	2230-2300	260	1
Goodge Street	2300-2330	225	1
Goodge Street	2330-2400	156	1
Goodge Street	0000-0030	87	1
Goodge Street	0030-0100	28	1
Goodge Street	0100-0130	9	1
Goodge Street	0130-0200	6	1
Goodge Street	0200-0230	0	0
Goodge Street	0230-0300	0	0
Goodge Street	0300-0330	0	0
Goodge Street	0330-0400	0	0
Goodge Street	0400-0430	0	0
Grange Hill	0430-0500	0	0
Grange Hill	0500-0530	7	1
Grange Hill	0530-0600	13	1
Grange Hill	0600-0630	52	1
Grange Hill	0630-0700	120	1
Grange Hill	0700-0730	161	1
Grange Hill	0730-0800	228	1
Grange Hill	0800-0830	221	1
Grange Hill	0830-0900	95	1
Grange Hill	0900-0930	48	1
Grange Hill	0930-1000	38	1
Grange Hill	1000-1030	29	1
Grange Hill	1030-1100	27	1
Grange Hill	1100-1130	23	1
Grange Hill	1130-1200	24	1
Grange Hill	1200-1230	25	1
Grange Hill	1230-1300	26	1
Grange Hill	1300-1330	28	1
Grange Hill	1330-1400	35	1
Grange Hill	1400-1430	32	1
Grange Hill	1430-1500	31	1
Grange Hill	1500-1530	33	1
Grange Hill	1530-1600	56	1
Grange Hill	1600-1630	65	1
Grange Hill	1630-1700	87	1
Grange Hill	1700-1730	87	1
Grange Hill	1730-1800	133	1
Grange Hill	1800-1830	127	1
Grange Hill	1830-1900	114	1
Grange Hill	1900-1930	80	1
Grange Hill	1930-2000	60	1
Grange Hill	2000-2030	39	1
Grange Hill	2030-2100	33	1
Grange Hill	2100-2130	23	1
Grange Hill	2130-2200	25	1
Grange Hill	2200-2230	20	1
Grange Hill	2230-2300	20	1
Grange Hill	2300-2330	13	1
Grange Hill	2330-2400	10	1
Grange Hill	0000-0030	10	1
Grange Hill	0030-0100	0	1
Grange Hill	0100-0130	0	1
Grange Hill	0130-0200	0	1
Grange Hill	0200-0230	0	0
Grange Hill	0230-0300	0	0
Grange Hill	0300-0330	0	0
Grange Hill	0330-0400	0	0
Grange Hill	0400-0430	0	0
Great Portland Street	0430-0500	0	0
Great Portland Street	0500-0530	14	1
Great Portland Street	0530-0600	46	1
Great Portland Street	0600-0630	101	1
Great Portland Street	0630-0700	268	1
Great Portland Street	0700-0730	588	1
Great Portland Street	0730-0800	984	1
Great Portland Street	0800-0830	1407	1
Great Portland Street	0830-0900	2186	1
Great Portland Street	0900-0930	2024	1
Great Portland Street	0930-1000	1268	1
Great Portland Street	1000-1030	755	1
Great Portland Street	1030-1100	652	1
Great Portland Street	1100-1130	544	1
Great Portland Street	1130-1200	538	1
Great Portland Street	1200-1230	564	1
Great Portland Street	1230-1300	582	1
Great Portland Street	1300-1330	583	1
Great Portland Street	1330-1400	585	1
Great Portland Street	1400-1430	568	1
Great Portland Street	1430-1500	576	1
Great Portland Street	1500-1530	661	1
Great Portland Street	1530-1600	818	1
Great Portland Street	1600-1630	1029	1
Great Portland Street	1630-1700	1155	1
Great Portland Street	1700-1730	1563	1
Great Portland Street	1730-1800	1833	1
Great Portland Street	1800-1830	1748	1
Great Portland Street	1830-1900	1199	1
Great Portland Street	1900-1930	811	1
Great Portland Street	1930-2000	566	1
Great Portland Street	2000-2030	452	1
Great Portland Street	2030-2100	363	1
Great Portland Street	2100-2130	316	1
Great Portland Street	2130-2200	268	1
Great Portland Street	2200-2230	250	1
Great Portland Street	2230-2300	209	1
Great Portland Street	2300-2330	196	1
Great Portland Street	2330-2400	135	1
Great Portland Street	0000-0030	71	1
Great Portland Street	0030-0100	26	1
Great Portland Street	0100-0130	2	1
Great Portland Street	0130-0200	0	1
Great Portland Street	0200-0230	0	0
Great Portland Street	0230-0300	0	0
Great Portland Street	0300-0330	0	0
Great Portland Street	0330-0400	0	0
Great Portland Street	0400-0430	0	0
Green Park	0430-0500	0	0
Green Park	0500-0530	73	1
Green Park	0530-0600	473	1
Green Park	0600-0630	770	1
Green Park	0630-0700	1502	1
Green Park	0700-0730	2553	1
Green Park	0730-0800	4089	1
Green Park	0800-0830	5804	1
Green Park	0830-0900	8459	1
Green Park	0900-0930	7315	1
Green Park	0930-1000	4477	1
Green Park	1000-1030	3266	1
Green Park	1030-1100	3100	1
Green Park	1100-1130	2720	1
Green Park	1130-1200	2935	1
Green Park	1200-1230	3066	1
Green Park	1230-1300	2917	1
Green Park	1300-1330	2690	1
Green Park	1330-1400	2743	1
Green Park	1400-1430	2810	1
Green Park	1430-1500	3094	1
Green Park	1500-1530	3239	1
Green Park	1530-1600	3605	1
Green Park	1600-1630	3897	1
Green Park	1630-1700	4528	1
Green Park	1700-1730	5839	1
Green Park	1730-1800	7167	1
Green Park	1800-1830	7142	1
Green Park	1830-1900	5655	1
Green Park	1900-1930	3977	1
Green Park	1930-2000	2674	1
Green Park	2000-2030	2105	1
Green Park	2030-2100	1802	1
Green Park	2100-2130	1641	1
Green Park	2130-2200	1557	1
Green Park	2200-2230	1674	1
Green Park	2230-2300	1632	1
Green Park	2300-2330	1402	1
Green Park	2330-2400	1091	1
Green Park	0000-0030	760	1
Green Park	0030-0100	295	1
Green Park	0100-0130	118	1
Green Park	0130-0200	55	1
Green Park	0200-0230	0	0
Green Park	0230-0300	0	0
Green Park	0300-0330	0	0
Green Park	0330-0400	0	0
Green Park	0400-0430	0	0
Greenford	0430-0500	0	0
Greenford	0500-0530	71	1
Greenford	0530-0600	206	1
Greenford	0600-0630	512	1
Greenford	0630-0700	736	1
Greenford	0700-0730	806	1
Greenford	0730-0800	831	1
Greenford	0800-0830	863	1
Greenford	0830-0900	642	1
Greenford	0900-0930	480	1
Greenford	0930-1000	314	1
Greenford	1000-1030	252	1
Greenford	1030-1100	210	1
Greenford	1100-1130	214	1
Greenford	1130-1200	205	1
Greenford	1200-1230	203	1
Greenford	1230-1300	220	1
Greenford	1300-1330	235	1
Greenford	1330-1400	250	1
Greenford	1400-1430	265	1
Greenford	1430-1500	261	1
Greenford	1500-1530	272	1
Greenford	1530-1600	366	1
Greenford	1600-1630	466	1
Greenford	1630-1700	561	1
Greenford	1700-1730	758	1
Greenford	1730-1800	835	1
Greenford	1800-1830	831	1
Greenford	1830-1900	691	1
Greenford	1900-1930	525	1
Greenford	1930-2000	364	1
Greenford	2000-2030	289	1
Greenford	2030-2100	241	1
Greenford	2100-2130	205	1
Greenford	2130-2200	211	1
Greenford	2200-2230	179	1
Greenford	2230-2300	139	1
Greenford	2300-2330	131	1
Greenford	2330-2400	109	1
Greenford	0000-0030	78	1
Greenford	0030-0100	45	1
Greenford	0100-0130	16	1
Greenford	0130-0200	0	1
Greenford	0200-0230	0	0
Greenford	0230-0300	0	0
Greenford	0300-0330	0	0
Greenford	0330-0400	0	0
Greenford	0400-0430	0	0
Gunnersbury	0430-0500	0	0
Gunnersbury	0500-0530	4	1
Gunnersbury	0530-0600	35	1
Gunnersbury	0600-0630	160	1
Gunnersbury	0630-0700	385	1
Gunnersbury	0700-0730	633	1
Gunnersbury	0730-0800	1025	1
Gunnersbury	0800-0830	1366	1
Gunnersbury	0830-0900	1676	1
Gunnersbury	0900-0930	1258	1
Gunnersbury	0930-1000	659	1
Gunnersbury	1000-1030	383	1
Gunnersbury	1030-1100	276	1
Gunnersbury	1100-1130	260	1
Gunnersbury	1130-1200	268	1
Gunnersbury	1200-1230	265	1
Gunnersbury	1230-1300	263	1
Gunnersbury	1300-1330	273	1
Gunnersbury	1330-1400	265	1
Gunnersbury	1400-1430	262	1
Gunnersbury	1430-1500	275	1
Gunnersbury	1500-1530	328	1
Gunnersbury	1530-1600	404	1
Gunnersbury	1600-1630	632	1
Gunnersbury	1630-1700	806	1
Gunnersbury	1700-1730	1284	1
Gunnersbury	1730-1800	1611	1
Gunnersbury	1800-1830	1347	1
Gunnersbury	1830-1900	855	1
Gunnersbury	1900-1930	625	1
Gunnersbury	1930-2000	400	1
Gunnersbury	2000-2030	283	1
Gunnersbury	2030-2100	220	1
Gunnersbury	2100-2130	193	1
Gunnersbury	2130-2200	171	1
Gunnersbury	2200-2230	165	1
Gunnersbury	2230-2300	153	1
Gunnersbury	2300-2330	138	1
Gunnersbury	2330-2400	98	1
Gunnersbury	0000-0030	48	1
Gunnersbury	0030-0100	19	1
Gunnersbury	0100-0130	4	1
Gunnersbury	0130-0200	0	1
Gunnersbury	0200-0230	0	0
Gunnersbury	0230-0300	0	0
Gunnersbury	0300-0330	0	0
Gunnersbury	0330-0400	0	0
Gunnersbury	0400-0430	0	0
Hainault	0430-0500	0	0
Hainault	0500-0530	99	1
Hainault	0530-0600	263	1
Hainault	0600-0630	455	1
Hainault	0630-0700	652	1
Hainault	0700-0730	684	1
Hainault	0730-0800	828	1
Hainault	0800-0830	846	1
Hainault	0830-0900	488	1
Hainault	0900-0930	310	1
Hainault	0930-1000	200	1
Hainault	1000-1030	171	1
Hainault	1030-1100	154	1
Hainault	1100-1130	151	1
Hainault	1130-1200	136	1
Hainault	1200-1230	144	1
Hainault	1230-1300	149	1
Hainault	1300-1330	153	1
Hainault	1330-1400	155	1
Hainault	1400-1430	174	1
Hainault	1430-1500	187	1
Hainault	1500-1530	217	1
Hainault	1530-1600	283	1
Hainault	1600-1630	334	1
Hainault	1630-1700	448	1
Hainault	1700-1730	582	1
Hainault	1730-1800	608	1
Hainault	1800-1830	679	1
Hainault	1830-1900	632	1
Hainault	1900-1930	475	1
Hainault	1930-2000	303	1
Hainault	2000-2030	233	1
Hainault	2030-2100	199	1
Hainault	2100-2130	165	1
Hainault	2130-2200	152	1
Hainault	2200-2230	139	1
Hainault	2230-2300	132	1
Hainault	2300-2330	123	1
Hainault	2330-2400	106	1
Hainault	0000-0030	79	1
Hainault	0030-0100	54	1
Hainault	0100-0130	26	1
Hainault	0130-0200	7	1
Hainault	0200-0230	0	0
Hainault	0230-0300	0	0
Hainault	0300-0330	0	0
Hainault	0330-0400	0	0
Hainault	0400-0430	0	0
Hammersmith (Dis)	0430-0500	0	0
Hammersmith (Dis)	0500-0530	75	1
Hammersmith (Dis)	0530-0600	225	1
Hammersmith (Dis)	0600-0630	563	1
Hammersmith (Dis)	0630-0700	1192	1
Hammersmith (Dis)	0700-0730	2408	1
Hammersmith (Dis)	0730-0800	3880	1
Hammersmith (Dis)	0800-0830	4992	1
Hammersmith (Dis)	0830-0900	5515	1
Hammersmith (Dis)	0900-0930	4397	1
Hammersmith (Dis)	0930-1000	2898	1
Hammersmith (Dis)	1000-1030	1971	1
Hammersmith (Dis)	1030-1100	1671	1
Hammersmith (Dis)	1100-1130	1599	1
Hammersmith (Dis)	1130-1200	1616	1
Hammersmith (Dis)	1200-1230	1698	1
Hammersmith (Dis)	1230-1300	1775	1
Hammersmith (Dis)	1300-1330	1797	1
Hammersmith (Dis)	1330-1400	1775	1
Hammersmith (Dis)	1400-1430	1803	1
Hammersmith (Dis)	1430-1500	1844	1
Hammersmith (Dis)	1500-1530	2238	1
Hammersmith (Dis)	1530-1600	2464	1
Hammersmith (Dis)	1600-1630	3162	1
Hammersmith (Dis)	1630-1700	3563	1
Hammersmith (Dis)	1700-1730	4458	1
Hammersmith (Dis)	1730-1800	5335	1
Hammersmith (Dis)	1800-1830	5189	1
Hammersmith (Dis)	1830-1900	4269	1
Hammersmith (Dis)	1900-1930	3192	1
Hammersmith (Dis)	1930-2000	2344	1
Hammersmith (Dis)	2000-2030	1778	1
Hammersmith (Dis)	2030-2100	1485	1
Hammersmith (Dis)	2100-2130	1311	1
Hammersmith (Dis)	2130-2200	1249	1
Hammersmith (Dis)	2200-2230	1658	1
Hammersmith (Dis)	2230-2300	2236	1
Hammersmith (Dis)	2300-2330	1675	1
Hammersmith (Dis)	2330-2400	879	1
Hammersmith (Dis)	0000-0030	449	1
Hammersmith (Dis)	0030-0100	219	1
Hammersmith (Dis)	0100-0130	74	1
Hammersmith (Dis)	0130-0200	41	1
Hammersmith (Dis)	0200-0230	0	0
Hammersmith (Dis)	0230-0300	0	0
Hammersmith (Dis)	0300-0330	0	0
Hammersmith (Dis)	0330-0400	0	0
Hammersmith (Dis)	0400-0430	0	0
Hammersmith (H&C)	0430-0500	0	0
Hammersmith (H&C)	0500-0530	32	1
Hammersmith (H&C)	0530-0600	98	1
Hammersmith (H&C)	0600-0630	200	1
Hammersmith (H&C)	0630-0700	409	1
Hammersmith (H&C)	0700-0730	882	1
Hammersmith (H&C)	0730-0800	1548	1
Hammersmith (H&C)	0800-0830	2203	1
Hammersmith (H&C)	0830-0900	2238	1
Hammersmith (H&C)	0900-0930	1717	1
Hammersmith (H&C)	0930-1000	1117	1
Hammersmith (H&C)	1000-1030	770	1
Hammersmith (H&C)	1030-1100	662	1
Hammersmith (H&C)	1100-1130	686	1
Hammersmith (H&C)	1130-1200	680	1
Hammersmith (H&C)	1200-1230	719	1
Hammersmith (H&C)	1230-1300	783	1
Hammersmith (H&C)	1300-1330	798	1
Hammersmith (H&C)	1330-1400	791	1
Hammersmith (H&C)	1400-1430	778	1
Hammersmith (H&C)	1430-1500	760	1
Hammersmith (H&C)	1500-1530	908	1
Hammersmith (H&C)	1530-1600	998	1
Hammersmith (H&C)	1600-1630	1212	1
Hammersmith (H&C)	1630-1700	1332	1
Hammersmith (H&C)	1700-1730	1698	1
Hammersmith (H&C)	1730-1800	1996	1
Hammersmith (H&C)	1800-1830	1943	1
Hammersmith (H&C)	1830-1900	1599	1
Hammersmith (H&C)	1900-1930	1168	1
Hammersmith (H&C)	1930-2000	828	1
Hammersmith (H&C)	2000-2030	624	1
Hammersmith (H&C)	2030-2100	485	1
Hammersmith (H&C)	2100-2130	436	1
Hammersmith (H&C)	2130-2200	410	1
Hammersmith (H&C)	2200-2230	429	1
Hammersmith (H&C)	2230-2300	441	1
Hammersmith (H&C)	2300-2330	361	1
Hammersmith (H&C)	2330-2400	234	1
Hammersmith (H&C)	0000-0030	148	1
Hammersmith (H&C)	0030-0100	68	1
Hammersmith (H&C)	0100-0130	23	1
Hammersmith (H&C)	0130-0200	0	1
Hammersmith (H&C)	0200-0230	0	0
Hammersmith (H&C)	0230-0300	0	0
Hammersmith (H&C)	0300-0330	0	0
Hammersmith (H&C)	0330-0400	0	0
Hammersmith (H&C)	0400-0430	0	0
Hampstead	0430-0500	0	0
Hampstead	0500-0530	3	1
Hampstead	0530-0600	24	1
Hampstead	0600-0630	63	1
Hampstead	0630-0700	157	1
Hampstead	0700-0730	359	1
Hampstead	0730-0800	631	1
Hampstead	0800-0830	827	1
Hampstead	0830-0900	846	1
Hampstead	0900-0930	638	1
Hampstead	0930-1000	438	1
Hampstead	1000-1030	329	1
Hampstead	1030-1100	297	1
Hampstead	1100-1130	277	1
Hampstead	1130-1200	291	1
Hampstead	1200-1230	293	1
Hampstead	1230-1300	304	1
Hampstead	1300-1330	322	1
Hampstead	1330-1400	319	1
Hampstead	1400-1430	324	1
Hampstead	1430-1500	358	1
Hampstead	1500-1530	454	1
Hampstead	1530-1600	546	1
Hampstead	1600-1630	628	1
Hampstead	1630-1700	592	1
Hampstead	1700-1730	602	1
Hampstead	1730-1800	636	1
Hampstead	1800-1830	636	1
Hampstead	1830-1900	575	1
Hampstead	1900-1930	487	1
Hampstead	1930-2000	387	1
Hampstead	2000-2030	302	1
Hampstead	2030-2100	231	1
Hampstead	2100-2130	205	1
Hampstead	2130-2200	191	1
Hampstead	2200-2230	180	1
Hampstead	2230-2300	203	1
Hampstead	2300-2330	185	1
Hampstead	2330-2400	148	1
Hampstead	0000-0030	78	1
Hampstead	0030-0100	33	1
Hampstead	0100-0130	11	1
Hampstead	0130-0200	5	1
Hampstead	0200-0230	0	0
Hampstead	0230-0300	0	0
Hampstead	0300-0330	0	0
Hampstead	0330-0400	0	0
Hampstead	0400-0430	0	0
Hanger Lane	0430-0500	0	0
Hanger Lane	0500-0530	20	1
Hanger Lane	0530-0600	109	1
Hanger Lane	0600-0630	218	1
Hanger Lane	0630-0700	391	1
Hanger Lane	0700-0730	571	1
Hanger Lane	0730-0800	664	1
Hanger Lane	0800-0830	769	1
Hanger Lane	0830-0900	828	1
Hanger Lane	0900-0930	687	1
Hanger Lane	0930-1000	368	1
Hanger Lane	1000-1030	210	1
Hanger Lane	1030-1100	177	1
Hanger Lane	1100-1130	168	1
Hanger Lane	1130-1200	165	1
Hanger Lane	1200-1230	166	1
Hanger Lane	1230-1300	153	1
Hanger Lane	1300-1330	168	1
Hanger Lane	1330-1400	172	1
Hanger Lane	1400-1430	185	1
Hanger Lane	1430-1500	194	1
Hanger Lane	1500-1530	215	1
Hanger Lane	1530-1600	265	1
Hanger Lane	1600-1630	365	1
Hanger Lane	1630-1700	448	1
Hanger Lane	1700-1730	661	1
Hanger Lane	1730-1800	942	1
Hanger Lane	1800-1830	744	1
Hanger Lane	1830-1900	568	1
Hanger Lane	1900-1930	405	1
Hanger Lane	1930-2000	286	1
Hanger Lane	2000-2030	224	1
Hanger Lane	2030-2100	187	1
Hanger Lane	2100-2130	177	1
Hanger Lane	2130-2200	154	1
Hanger Lane	2200-2230	153	1
Hanger Lane	2230-2300	133	1
Hanger Lane	2300-2330	123	1
Hanger Lane	2330-2400	96	1
Hanger Lane	0000-0030	60	1
Hanger Lane	0030-0100	39	1
Hanger Lane	0100-0130	5	1
Hanger Lane	0130-0200	0	1
Hanger Lane	0200-0230	0	0
Hanger Lane	0230-0300	0	0
Hanger Lane	0300-0330	0	0
Hanger Lane	0330-0400	0	0
Hanger Lane	0400-0430	0	0
Harlesden	0430-0500	0	0
Harlesden	0500-0530	29	1
Harlesden	0530-0600	110	1
Harlesden	0600-0630	228	1
Harlesden	0630-0700	338	1
Harlesden	0700-0730	439	1
Harlesden	0730-0800	614	1
Harlesden	0800-0830	668	1
Harlesden	0830-0900	608	1
Harlesden	0900-0930	388	1
Harlesden	0930-1000	242	1
Harlesden	1000-1030	195	1
Harlesden	1030-1100	168	1
Harlesden	1100-1130	147	1
Harlesden	1130-1200	150	1
Harlesden	1200-1230	155	1
Harlesden	1230-1300	175	1
Harlesden	1300-1330	186	1
Harlesden	1330-1400	197	1
Harlesden	1400-1430	210	1
Harlesden	1430-1500	229	1
Harlesden	1500-1530	278	1
Harlesden	1530-1600	336	1
Harlesden	1600-1630	419	1
Harlesden	1630-1700	434	1
Harlesden	1700-1730	570	1
Harlesden	1730-1800	587	1
Harlesden	1800-1830	505	1
Harlesden	1830-1900	378	1
Harlesden	1900-1930	263	1
Harlesden	1930-2000	213	1
Harlesden	2000-2030	173	1
Harlesden	2030-2100	155	1
Harlesden	2100-2130	149	1
Harlesden	2130-2200	122	1
Harlesden	2200-2230	114	1
Harlesden	2230-2300	102	1
Harlesden	2300-2330	105	1
Harlesden	2330-2400	68	1
Harlesden	0000-0030	35	1
Harlesden	0030-0100	11	1
Harlesden	0100-0130	0	1
Harlesden	0130-0200	0	1
Harlesden	0200-0230	0	0
Harlesden	0230-0300	0	0
Harlesden	0300-0330	0	0
Harlesden	0330-0400	0	0
Harlesden	0400-0430	0	0
Harrow & Wealdstone	0430-0500	0	0
Harrow & Wealdstone	0500-0530	59	1
Harrow & Wealdstone	0530-0600	176	1
Harrow & Wealdstone	0600-0630	393	1
Harrow & Wealdstone	0630-0700	600	1
Harrow & Wealdstone	0700-0730	783	1
Harrow & Wealdstone	0730-0800	895	1
Harrow & Wealdstone	0800-0830	1049	1
Harrow & Wealdstone	0830-0900	923	1
Harrow & Wealdstone	0900-0930	580	1
Harrow & Wealdstone	0930-1000	409	1
Harrow & Wealdstone	1000-1030	277	1
Harrow & Wealdstone	1030-1100	259	1
Harrow & Wealdstone	1100-1130	247	1
Harrow & Wealdstone	1130-1200	229	1
Harrow & Wealdstone	1200-1230	232	1
Harrow & Wealdstone	1230-1300	259	1
Harrow & Wealdstone	1300-1330	284	1
Harrow & Wealdstone	1330-1400	292	1
Harrow & Wealdstone	1400-1430	289	1
Harrow & Wealdstone	1430-1500	279	1
Harrow & Wealdstone	1500-1530	330	1
Harrow & Wealdstone	1530-1600	415	1
Harrow & Wealdstone	1600-1630	509	1
Harrow & Wealdstone	1630-1700	602	1
Harrow & Wealdstone	1700-1730	825	1
Harrow & Wealdstone	1730-1800	864	1
Harrow & Wealdstone	1800-1830	918	1
Harrow & Wealdstone	1830-1900	733	1
Harrow & Wealdstone	1900-1930	522	1
Harrow & Wealdstone	1930-2000	339	1
Harrow & Wealdstone	2000-2030	275	1
Harrow & Wealdstone	2030-2100	214	1
Harrow & Wealdstone	2100-2130	174	1
Harrow & Wealdstone	2130-2200	150	1
Harrow & Wealdstone	2200-2230	131	1
Harrow & Wealdstone	2230-2300	87	1
Harrow & Wealdstone	2300-2330	95	1
Harrow & Wealdstone	2330-2400	66	1
Harrow & Wealdstone	0000-0030	43	1
Harrow & Wealdstone	0030-0100	18	1
Harrow & Wealdstone	0100-0130	0	1
Harrow & Wealdstone	0130-0200	4	1
Harrow & Wealdstone	0200-0230	0	0
Harrow & Wealdstone	0230-0300	0	0
Harrow & Wealdstone	0300-0330	0	0
Harrow & Wealdstone	0330-0400	0	0
Harrow & Wealdstone	0400-0430	0	0
Harrow-on-the-Hill	0430-0500	0	0
Harrow-on-the-Hill	0500-0530	59	1
Harrow-on-the-Hill	0530-0600	213	1
Harrow-on-the-Hill	0600-0630	576	1
Harrow-on-the-Hill	0630-0700	946	1
Harrow-on-the-Hill	0700-0730	1286	1
Harrow-on-the-Hill	0730-0800	1781	1
Harrow-on-the-Hill	0800-0830	1997	1
Harrow-on-the-Hill	0830-0900	1719	1
Harrow-on-the-Hill	0900-0930	1290	1
Harrow-on-the-Hill	0930-1000	886	1
Harrow-on-the-Hill	1000-1030	662	1
Harrow-on-the-Hill	1030-1100	622	1
Harrow-on-the-Hill	1100-1130	627	1
Harrow-on-the-Hill	1130-1200	629	1
Harrow-on-the-Hill	1200-1230	645	1
Harrow-on-the-Hill	1230-1300	672	1
Harrow-on-the-Hill	1300-1330	687	1
Harrow-on-the-Hill	1330-1400	716	1
Harrow-on-the-Hill	1400-1430	744	1
Harrow-on-the-Hill	1430-1500	797	1
Harrow-on-the-Hill	1500-1530	809	1
Harrow-on-the-Hill	1530-1600	1001	1
Harrow-on-the-Hill	1600-1630	1306	1
Harrow-on-the-Hill	1630-1700	1464	1
Harrow-on-the-Hill	1700-1730	1663	1
Harrow-on-the-Hill	1730-1800	1936	1
Harrow-on-the-Hill	1800-1830	1865	1
Harrow-on-the-Hill	1830-1900	1634	1
Harrow-on-the-Hill	1900-1930	1213	1
Harrow-on-the-Hill	1930-2000	841	1
Harrow-on-the-Hill	2000-2030	651	1
Harrow-on-the-Hill	2030-2100	514	1
Harrow-on-the-Hill	2100-2130	459	1
Harrow-on-the-Hill	2130-2200	406	1
Harrow-on-the-Hill	2200-2230	365	1
Harrow-on-the-Hill	2230-2300	378	1
Harrow-on-the-Hill	2300-2330	347	1
Harrow-on-the-Hill	2330-2400	285	1
Harrow-on-the-Hill	0000-0030	172	1
Harrow-on-the-Hill	0030-0100	90	1
Harrow-on-the-Hill	0100-0130	22	1
Harrow-on-the-Hill	0130-0200	0	1
Harrow-on-the-Hill	0200-0230	0	0
Harrow-on-the-Hill	0230-0300	0	0
Harrow-on-the-Hill	0300-0330	0	0
Harrow-on-the-Hill	0330-0400	0	0
Harrow-on-the-Hill	0400-0430	0	0
Hatton Cross	0430-0500	0	0
Hatton Cross	0500-0530	97	1
Hatton Cross	0530-0600	137	1
Hatton Cross	0600-0630	200	1
Hatton Cross	0630-0700	329	1
Hatton Cross	0700-0730	409	1
Hatton Cross	0730-0800	523	1
Hatton Cross	0800-0830	526	1
Hatton Cross	0830-0900	463	1
Hatton Cross	0900-0930	351	1
Hatton Cross	0930-1000	248	1
Hatton Cross	1000-1030	178	1
Hatton Cross	1030-1100	162	1
Hatton Cross	1100-1130	158	1
Hatton Cross	1130-1200	149	1
Hatton Cross	1200-1230	167	1
Hatton Cross	1230-1300	191	1
Hatton Cross	1300-1330	203	1
Hatton Cross	1330-1400	192	1
Hatton Cross	1400-1430	206	1
Hatton Cross	1430-1500	211	1
Hatton Cross	1500-1530	227	1
Hatton Cross	1530-1600	264	1
Hatton Cross	1600-1630	337	1
Hatton Cross	1630-1700	413	1
Hatton Cross	1700-1730	476	1
Hatton Cross	1730-1800	507	1
Hatton Cross	1800-1830	436	1
Hatton Cross	1830-1900	346	1
Hatton Cross	1900-1930	282	1
Hatton Cross	1930-2000	202	1
Hatton Cross	2000-2030	165	1
Hatton Cross	2030-2100	147	1
Hatton Cross	2100-2130	127	1
Hatton Cross	2130-2200	126	1
Hatton Cross	2200-2230	142	1
Hatton Cross	2230-2300	133	1
Hatton Cross	2300-2330	119	1
Hatton Cross	2330-2400	86	1
Hatton Cross	0000-0030	59	1
Hatton Cross	0030-0100	37	1
Hatton Cross	0100-0130	24	1
Hatton Cross	0130-0200	8	1
Hatton Cross	0200-0230	0	0
Hatton Cross	0230-0300	0	0
Hatton Cross	0300-0330	0	0
Hatton Cross	0330-0400	0	0
Hatton Cross	0400-0430	0	0
Heathrow Terminals 123	0430-0500	0	0
Heathrow Terminals 123	0500-0530	138	1
Heathrow Terminals 123	0530-0600	164	1
Heathrow Terminals 123	0600-0630	225	1
Heathrow Terminals 123	0630-0700	385	1
Heathrow Terminals 123	0700-0730	520	1
Heathrow Terminals 123	0730-0800	620	1
Heathrow Terminals 123	0800-0830	670	1
Heathrow Terminals 123	0830-0900	662	1
Heathrow Terminals 123	0900-0930	621	1
Heathrow Terminals 123	0930-1000	596	1
Heathrow Terminals 123	1000-1030	613	1
Heathrow Terminals 123	1030-1100	553	1
Heathrow Terminals 123	1100-1130	556	1
Heathrow Terminals 123	1130-1200	584	1
Heathrow Terminals 123	1200-1230	620	1
Heathrow Terminals 123	1230-1300	643	1
Heathrow Terminals 123	1300-1330	707	1
Heathrow Terminals 123	1330-1400	725	1
Heathrow Terminals 123	1400-1430	708	1
Heathrow Terminals 123	1430-1500	660	1
Heathrow Terminals 123	1500-1530	651	1
Heathrow Terminals 123	1530-1600	665	1
Heathrow Terminals 123	1600-1630	699	1
Heathrow Terminals 123	1630-1700	789	1
Heathrow Terminals 123	1700-1730	859	1
Heathrow Terminals 123	1730-1800	847	1
Heathrow Terminals 123	1800-1830	752	1
Heathrow Terminals 123	1830-1900	714	1
Heathrow Terminals 123	1900-1930	702	1
Heathrow Terminals 123	1930-2000	562	1
Heathrow Terminals 123	2000-2030	503	1
Heathrow Terminals 123	2030-2100	394	1
Heathrow Terminals 123	2100-2130	399	1
Heathrow Terminals 123	2130-2200	410	1
Heathrow Terminals 123	2200-2230	428	1
Heathrow Terminals 123	2230-2300	270	1
Heathrow Terminals 123	2300-2330	171	1
Heathrow Terminals 123	2330-2400	90	1
Heathrow Terminals 123	0000-0030	36	1
Heathrow Terminals 123	0030-0100	23	1
Heathrow Terminals 123	0100-0130	14	1
Heathrow Terminals 123	0130-0200	5	1
Heathrow Terminals 123	0200-0230	0	0
Heathrow Terminals 123	0230-0300	0	0
Heathrow Terminals 123	0300-0330	0	0
Heathrow Terminals 123	0330-0400	0	0
Heathrow Terminals 123	0400-0430	0	0
Heathrow Terminal 4	0430-0500	0	0
Heathrow Terminal 4	0500-0530	30	1
Heathrow Terminal 4	0530-0600	45	1
Heathrow Terminal 4	0600-0630	70	1
Heathrow Terminal 4	0630-0700	140	1
Heathrow Terminal 4	0700-0730	210	1
Heathrow Terminal 4	0730-0800	219	1
Heathrow Terminal 4	0800-0830	175	1
Heathrow Terminal 4	0830-0900	147	1
Heathrow Terminal 4	0900-0930	130	1
Heathrow Terminal 4	0930-1000	129	1
Heathrow Terminal 4	1000-1030	116	1
Heathrow Terminal 4	1030-1100	120	1
Heathrow Terminal 4	1100-1130	136	1
Heathrow Terminal 4	1130-1200	155	1
Heathrow Terminal 4	1200-1230	158	1
Heathrow Terminal 4	1230-1300	185	1
Heathrow Terminal 4	1300-1330	221	1
Heathrow Terminal 4	1330-1400	215	1
Heathrow Terminal 4	1400-1430	229	1
Heathrow Terminal 4	1430-1500	215	1
Heathrow Terminal 4	1500-1530	201	1
Heathrow Terminal 4	1530-1600	190	1
Heathrow Terminal 4	1600-1630	214	1
Heathrow Terminal 4	1630-1700	267	1
Heathrow Terminal 4	1700-1730	274	1
Heathrow Terminal 4	1730-1800	263	1
Heathrow Terminal 4	1800-1830	275	1
Heathrow Terminal 4	1830-1900	246	1
Heathrow Terminal 4	1900-1930	213	1
Heathrow Terminal 4	1930-2000	197	1
Heathrow Terminal 4	2000-2030	160	1
Heathrow Terminal 4	2030-2100	123	1
Heathrow Terminal 4	2100-2130	132	1
Heathrow Terminal 4	2130-2200	113	1
Heathrow Terminal 4	2200-2230	90	1
Heathrow Terminal 4	2230-2300	52	1
Heathrow Terminal 4	2300-2330	54	1
Heathrow Terminal 4	2330-2400	24	1
Heathrow Terminal 4	0000-0030	5	1
Heathrow Terminal 4	0030-0100	0	1
Heathrow Terminal 4	0100-0130	0	1
Heathrow Terminal 4	0130-0200	0	1
Heathrow Terminal 4	0200-0230	0	0
Heathrow Terminal 4	0230-0300	0	0
Heathrow Terminal 4	0300-0330	0	0
Heathrow Terminal 4	0330-0400	0	0
Heathrow Terminal 4	0400-0430	0	0
Heathrow Terminal 5	0430-0500	0	0
Heathrow Terminal 5	0500-0530	108	1
Heathrow Terminal 5	0530-0600	182	1
Heathrow Terminal 5	0600-0630	180	1
Heathrow Terminal 5	0630-0700	242	1
Heathrow Terminal 5	0700-0730	293	1
Heathrow Terminal 5	0730-0800	356	1
Heathrow Terminal 5	0800-0830	367	1
Heathrow Terminal 5	0830-0900	373	1
Heathrow Terminal 5	0900-0930	328	1
Heathrow Terminal 5	0930-1000	317	1
Heathrow Terminal 5	1000-1030	323	1
Heathrow Terminal 5	1030-1100	312	1
Heathrow Terminal 5	1100-1130	338	1
Heathrow Terminal 5	1130-1200	363	1
Heathrow Terminal 5	1200-1230	397	1
Heathrow Terminal 5	1230-1300	432	1
Heathrow Terminal 5	1300-1330	477	1
Heathrow Terminal 5	1330-1400	459	1
Heathrow Terminal 5	1400-1430	484	1
Heathrow Terminal 5	1430-1500	430	1
Heathrow Terminal 5	1500-1530	396	1
Heathrow Terminal 5	1530-1600	369	1
Heathrow Terminal 5	1600-1630	405	1
Heathrow Terminal 5	1630-1700	463	1
Heathrow Terminal 5	1700-1730	495	1
Heathrow Terminal 5	1730-1800	489	1
Heathrow Terminal 5	1800-1830	427	1
Heathrow Terminal 5	1830-1900	356	1
Heathrow Terminal 5	1900-1930	320	1
Heathrow Terminal 5	1930-2000	252	1
Heathrow Terminal 5	2000-2030	253	1
Heathrow Terminal 5	2030-2100	277	1
Heathrow Terminal 5	2100-2130	270	1
Heathrow Terminal 5	2130-2200	266	1
Heathrow Terminal 5	2200-2230	257	1
Heathrow Terminal 5	2230-2300	159	1
Heathrow Terminal 5	2300-2330	78	1
Heathrow Terminal 5	2330-2400	34	1
Heathrow Terminal 5	0000-0030	16	1
Heathrow Terminal 5	0030-0100	9	1
Heathrow Terminal 5	0100-0130	6	1
Heathrow Terminal 5	0130-0200	1	1
Heathrow Terminal 5	0200-0230	0	0
Heathrow Terminal 5	0230-0300	0	0
Heathrow Terminal 5	0300-0330	0	0
Heathrow Terminal 5	0330-0400	0	0
Heathrow Terminal 5	0400-0430	0	0
Hendon Central	0430-0500	0	0
Hendon Central	0500-0530	37	1
Hendon Central	0530-0600	143	1
Hendon Central	0600-0630	354	1
Hendon Central	0630-0700	645	1
Hendon Central	0700-0730	819	1
Hendon Central	0730-0800	998	1
Hendon Central	0800-0830	1407	1
Hendon Central	0830-0900	1414	1
Hendon Central	0900-0930	958	1
Hendon Central	0930-1000	774	1
Hendon Central	1000-1030	636	1
Hendon Central	1030-1100	553	1
Hendon Central	1100-1130	515	1
Hendon Central	1130-1200	521	1
Hendon Central	1200-1230	533	1
Hendon Central	1230-1300	554	1
Hendon Central	1300-1330	587	1
Hendon Central	1330-1400	539	1
Hendon Central	1400-1430	561	1
Hendon Central	1430-1500	608	1
Hendon Central	1500-1530	707	1
Hendon Central	1530-1600	754	1
Hendon Central	1600-1630	853	1
Hendon Central	1630-1700	965	1
Hendon Central	1700-1730	1141	1
Hendon Central	1730-1800	1243	1
Hendon Central	1800-1830	1225	1
Hendon Central	1830-1900	1050	1
Hendon Central	1900-1930	807	1
Hendon Central	1930-2000	579	1
Hendon Central	2000-2030	462	1
Hendon Central	2030-2100	408	1
Hendon Central	2100-2130	351	1
Hendon Central	2130-2200	319	1
Hendon Central	2200-2230	302	1
Hendon Central	2230-2300	294	1
Hendon Central	2300-2330	253	1
Hendon Central	2330-2400	210	1
Hendon Central	0000-0030	164	1
Hendon Central	0030-0100	100	1
Hendon Central	0100-0130	32	1
Hendon Central	0130-0200	13	1
Hendon Central	0200-0230	0	0
Hendon Central	0230-0300	0	0
Hendon Central	0300-0330	0	0
Hendon Central	0330-0400	0	0
Hendon Central	0400-0430	0	0
High Barnet	0430-0500	0	0
High Barnet	0500-0530	23	1
High Barnet	0530-0600	71	1
High Barnet	0600-0630	179	1
High Barnet	0630-0700	316	1
High Barnet	0700-0730	566	1
High Barnet	0730-0800	998	1
High Barnet	0800-0830	1218	1
High Barnet	0830-0900	792	1
High Barnet	0900-0930	488	1
High Barnet	0930-1000	335	1
High Barnet	1000-1030	250	1
High Barnet	1030-1100	225	1
High Barnet	1100-1130	206	1
High Barnet	1130-1200	211	1
High Barnet	1200-1230	218	1
High Barnet	1230-1300	225	1
High Barnet	1300-1330	228	1
High Barnet	1330-1400	218	1
High Barnet	1400-1430	255	1
High Barnet	1430-1500	244	1
High Barnet	1500-1530	311	1
High Barnet	1530-1600	365	1
High Barnet	1600-1630	514	1
High Barnet	1630-1700	521	1
High Barnet	1700-1730	601	1
High Barnet	1730-1800	673	1
High Barnet	1800-1830	710	1
High Barnet	1830-1900	632	1
High Barnet	1900-1930	479	1
High Barnet	1930-2000	352	1
High Barnet	2000-2030	264	1
High Barnet	2030-2100	220	1
High Barnet	2100-2130	192	1
High Barnet	2130-2200	174	1
High Barnet	2200-2230	162	1
High Barnet	2230-2300	168	1
High Barnet	2300-2330	170	1
High Barnet	2330-2400	140	1
High Barnet	0000-0030	107	1
High Barnet	0030-0100	70	1
High Barnet	0100-0130	28	1
High Barnet	0130-0200	12	1
High Barnet	0200-0230	0	0
High Barnet	0230-0300	0	0
High Barnet	0300-0330	0	0
High Barnet	0330-0400	0	0
High Barnet	0400-0430	0	0
High Street Kensington	0430-0500	0	0
High Street Kensington	0500-0530	14	1
High Street Kensington	0530-0600	56	1
High Street Kensington	0600-0630	165	1
High Street Kensington	0630-0700	385	1
High Street Kensington	0700-0730	626	1
High Street Kensington	0730-0800	1104	1
High Street Kensington	0800-0830	1471	1
High Street Kensington	0830-0900	2064	1
High Street Kensington	0900-0930	1891	1
High Street Kensington	0930-1000	1591	1
High Street Kensington	1000-1030	1205	1
High Street Kensington	1030-1100	1059	1
High Street Kensington	1100-1130	1024	1
High Street Kensington	1130-1200	1041	1
High Street Kensington	1200-1230	1059	1
High Street Kensington	1230-1300	1104	1
High Street Kensington	1300-1330	1112	1
High Street Kensington	1330-1400	1120	1
High Street Kensington	1400-1430	1098	1
High Street Kensington	1430-1500	1129	1
High Street Kensington	1500-1530	1250	1
High Street Kensington	1530-1600	1353	1
High Street Kensington	1600-1630	1538	1
High Street Kensington	1630-1700	1708	1
High Street Kensington	1700-1730	1970	1
High Street Kensington	1730-1800	2146	1
High Street Kensington	1800-1830	2193	1
High Street Kensington	1830-1900	1676	1
High Street Kensington	1900-1930	1267	1
High Street Kensington	1930-2000	901	1
High Street Kensington	2000-2030	717	1
High Street Kensington	2030-2100	560	1
High Street Kensington	2100-2130	490	1
High Street Kensington	2130-2200	417	1
High Street Kensington	2200-2230	437	1
High Street Kensington	2230-2300	434	1
High Street Kensington	2300-2330	352	1
High Street Kensington	2330-2400	229	1
High Street Kensington	0000-0030	124	1
High Street Kensington	0030-0100	46	1
High Street Kensington	0100-0130	7	1
High Street Kensington	0130-0200	0	1
High Street Kensington	0200-0230	0	0
High Street Kensington	0230-0300	0	0
High Street Kensington	0300-0330	0	0
High Street Kensington	0330-0400	0	0
High Street Kensington	0400-0430	0	0
Highbury & Islington	0430-0500	0	0
Highbury & Islington	0500-0530	44	1
Highbury & Islington	0530-0600	164	1
Highbury & Islington	0600-0630	414	1
Highbury & Islington	0630-0700	885	1
Highbury & Islington	0700-0730	1708	1
Highbury & Islington	0730-0800	2535	1
Highbury & Islington	0800-0830	3308	1
Highbury & Islington	0830-0900	3934	1
Highbury & Islington	0900-0930	3211	1
Highbury & Islington	0930-1000	2262	1
Highbury & Islington	1000-1030	1308	1
Highbury & Islington	1030-1100	1081	1
Highbury & Islington	1100-1130	970	1
Highbury & Islington	1130-1200	979	1
Highbury & Islington	1200-1230	1013	1
Highbury & Islington	1230-1300	1084	1
Highbury & Islington	1300-1330	1098	1
Highbury & Islington	1330-1400	1088	1
Highbury & Islington	1400-1430	1032	1
Highbury & Islington	1430-1500	1143	1
Highbury & Islington	1500-1530	1263	1
Highbury & Islington	1530-1600	1498	1
Highbury & Islington	1600-1630	1981	1
Highbury & Islington	1630-1700	2334	1
Highbury & Islington	1700-1730	2744	1
Highbury & Islington	1730-1800	3100	1
Highbury & Islington	1800-1830	3402	1
Highbury & Islington	1830-1900	3085	1
Highbury & Islington	1900-1930	2441	1
Highbury & Islington	1930-2000	1758	1
Highbury & Islington	2000-2030	1364	1
Highbury & Islington	2030-2100	1140	1
Highbury & Islington	2100-2130	1004	1
Highbury & Islington	2130-2200	956	1
Highbury & Islington	2200-2230	1134	1
Highbury & Islington	2230-2300	1245	1
Highbury & Islington	2300-2330	1000	1
Highbury & Islington	2330-2400	698	1
Highbury & Islington	0000-0030	402	1
Highbury & Islington	0030-0100	169	1
Highbury & Islington	0100-0130	66	1
Highbury & Islington	0130-0200	43	1
Highbury & Islington	0200-0230	0	0
Highbury & Islington	0230-0300	0	0
Highbury & Islington	0300-0330	0	0
Highbury & Islington	0330-0400	0	0
Highbury & Islington	0400-0430	0	0
Highgate	0430-0500	0	0
Highgate	0500-0530	8	1
Highgate	0530-0600	42	1
Highgate	0600-0630	128	1
Highgate	0630-0700	310	1
Highgate	0700-0730	671	1
Highgate	0730-0800	1132	1
Highgate	0800-0830	1409	1
Highgate	0830-0900	1311	1
Highgate	0900-0930	951	1
Highgate	0930-1000	576	1
Highgate	1000-1030	371	1
Highgate	1030-1100	301	1
Highgate	1100-1130	288	1
Highgate	1130-1200	279	1
Highgate	1200-1230	285	1
Highgate	1230-1300	277	1
Highgate	1300-1330	296	1
Highgate	1330-1400	289	1
Highgate	1400-1430	282	1
Highgate	1430-1500	301	1
Highgate	1500-1530	342	1
Highgate	1530-1600	387	1
Highgate	1600-1630	519	1
Highgate	1630-1700	625	1
Highgate	1700-1730	723	1
Highgate	1730-1800	873	1
Highgate	1800-1830	993	1
Highgate	1830-1900	957	1
Highgate	1900-1930	766	1
Highgate	1930-2000	566	1
Highgate	2000-2030	423	1
Highgate	2030-2100	336	1
Highgate	2100-2130	289	1
Highgate	2130-2200	286	1
Highgate	2200-2230	285	1
Highgate	2230-2300	271	1
Highgate	2300-2330	240	1
Highgate	2330-2400	185	1
Highgate	0000-0030	120	1
Highgate	0030-0100	60	1
Highgate	0100-0130	23	1
Highgate	0130-0200	11	1
Highgate	0200-0230	0	0
Highgate	0230-0300	0	0
Highgate	0300-0330	0	0
Highgate	0330-0400	0	0
Highgate	0400-0430	0	0
Hillingdon	0430-0500	0	0
Hillingdon	0500-0530	23	1
Hillingdon	0530-0600	47	1
Hillingdon	0600-0630	116	1
Hillingdon	0630-0700	225	1
Hillingdon	0700-0730	350	1
Hillingdon	0730-0800	460	1
Hillingdon	0800-0830	425	1
Hillingdon	0830-0900	303	1
Hillingdon	0900-0930	168	1
Hillingdon	0930-1000	118	1
Hillingdon	1000-1030	95	1
Hillingdon	1030-1100	86	1
Hillingdon	1100-1130	80	1
Hillingdon	1130-1200	78	1
Hillingdon	1200-1230	82	1
Hillingdon	1230-1300	87	1
Hillingdon	1300-1330	85	1
Hillingdon	1330-1400	88	1
Hillingdon	1400-1430	91	1
Hillingdon	1430-1500	106	1
Hillingdon	1500-1530	188	1
Hillingdon	1530-1600	205	1
Hillingdon	1600-1630	177	1
Hillingdon	1630-1700	218	1
Hillingdon	1700-1730	249	1
Hillingdon	1730-1800	268	1
Hillingdon	1800-1830	285	1
Hillingdon	1830-1900	275	1
Hillingdon	1900-1930	202	1
Hillingdon	1930-2000	128	1
Hillingdon	2000-2030	100	1
Hillingdon	2030-2100	79	1
Hillingdon	2100-2130	60	1
Hillingdon	2130-2200	57	1
Hillingdon	2200-2230	60	1
Hillingdon	2230-2300	65	1
Hillingdon	2300-2330	63	1
Hillingdon	2330-2400	42	1
Hillingdon	0000-0030	26	1
Hillingdon	0030-0100	14	1
Hillingdon	0100-0130	5	1
Hillingdon	0130-0200	0	1
Hillingdon	0200-0230	0	0
Hillingdon	0230-0300	0	0
Hillingdon	0300-0330	0	0
Hillingdon	0330-0400	0	0
Hillingdon	0400-0430	0	0
Holborn	0430-0500	0	0
Holborn	0500-0530	9	1
Holborn	0530-0600	178	1
Holborn	0600-0630	440	1
Holborn	0630-0700	963	1
Holborn	0700-0730	1707	1
Holborn	0730-0800	2740	1
Holborn	0800-0830	4126	1
Holborn	0830-0900	6327	1
Holborn	0900-0930	6387	1
Holborn	0930-1000	4645	1
Holborn	1000-1030	3075	1
Holborn	1030-1100	2715	1
Holborn	1100-1130	2303	1
Holborn	1130-1200	2442	1
Holborn	1200-1230	2765	1
Holborn	1230-1300	2819	1
Holborn	1300-1330	2802	1
Holborn	1330-1400	2859	1
Holborn	1400-1430	2770	1
Holborn	1430-1500	2763	1
Holborn	1500-1530	2883	1
Holborn	1530-1600	3230	1
Holborn	1600-1630	3802	1
Holborn	1630-1700	4222	1
Holborn	1700-1730	4888	1
Holborn	1730-1800	5519	1
Holborn	1800-1830	5311	1
Holborn	1830-1900	4284	1
Holborn	1900-1930	3258	1
Holborn	1930-2000	2417	1
Holborn	2000-2030	2096	1
Holborn	2030-2100	1920	1
Holborn	2100-2130	1728	1
Holborn	2130-2200	1526	1
Holborn	2200-2230	1730	1
Holborn	2230-2300	1410	1
Holborn	2300-2330	1040	1
Holborn	2330-2400	881	1
Holborn	0000-0030	576	1
Holborn	0030-0100	186	1
Holborn	0100-0130	104	1
Holborn	0130-0200	59	1
Holborn	0200-0230	0	0
Holborn	0230-0300	0	0
Holborn	0300-0330	0	0
Holborn	0330-0400	0	0
Holborn	0400-0430	0	0
Holland Park	0430-0500	0	0
Holland Park	0500-0530	3	1
Holland Park	0530-0600	24	1
Holland Park	0600-0630	73	1
Holland Park	0630-0700	164	1
Holland Park	0700-0730	463	1
Holland Park	0730-0800	764	1
Holland Park	0800-0830	704	1
Holland Park	0830-0900	688	1
Holland Park	0900-0930	533	1
Holland Park	0930-1000	363	1
Holland Park	1000-1030	270	1
Holland Park	1030-1100	234	1
Holland Park	1100-1130	224	1
Holland Park	1130-1200	228	1
Holland Park	1200-1230	234	1
Holland Park	1230-1300	234	1
Holland Park	1300-1330	229	1
Holland Park	1330-1400	227	1
Holland Park	1400-1430	225	1
Holland Park	1430-1500	238	1
Holland Park	1500-1530	262	1
Holland Park	1530-1600	367	1
Holland Park	1600-1630	386	1
Holland Park	1630-1700	496	1
Holland Park	1700-1730	582	1
Holland Park	1730-1800	491	1
Holland Park	1800-1830	549	1
Holland Park	1830-1900	441	1
Holland Park	1900-1930	343	1
Holland Park	1930-2000	257	1
Holland Park	2000-2030	204	1
Holland Park	2030-2100	161	1
Holland Park	2100-2130	142	1
Holland Park	2130-2200	151	1
Holland Park	2200-2230	146	1
Holland Park	2230-2300	131	1
Holland Park	2300-2330	127	1
Holland Park	2330-2400	92	1
Holland Park	0000-0030	50	1
Holland Park	0030-0100	23	1
Holland Park	0100-0130	9	1
Holland Park	0130-0200	6	1
Holland Park	0200-0230	0	0
Holland Park	0230-0300	0	0
Holland Park	0300-0330	0	0
Holland Park	0330-0400	0	0
Holland Park	0400-0430	0	0
Holloway Road	0430-0500	0	0
Holloway Road	0500-0530	14	1
Holloway Road	0530-0600	54	1
Holloway Road	0600-0630	107	1
Holloway Road	0630-0700	202	1
Holloway Road	0700-0730	378	1
Holloway Road	0730-0800	612	1
Holloway Road	0800-0830	960	1
Holloway Road	0830-0900	1213	1
Holloway Road	0900-0930	1033	1
Holloway Road	0930-1000	957	1
Holloway Road	1000-1030	656	1
Holloway Road	1030-1100	520	1
Holloway Road	1100-1130	434	1
Holloway Road	1130-1200	431	1
Holloway Road	1200-1230	477	1
Holloway Road	1230-1300	542	1
Holloway Road	1300-1330	562	1
Holloway Road	1330-1400	571	1
Holloway Road	1400-1430	491	1
Holloway Road	1430-1500	464	1
Holloway Road	1500-1530	492	1
Holloway Road	1530-1600	564	1
Holloway Road	1600-1630	710	1
Holloway Road	1630-1700	847	1
Holloway Road	1700-1730	922	1
Holloway Road	1730-1800	897	1
Holloway Road	1800-1830	943	1
Holloway Road	1830-1900	846	1
Holloway Road	1900-1930	686	1
Holloway Road	1930-2000	556	1
Holloway Road	2000-2030	495	1
Holloway Road	2030-2100	502	1
Holloway Road	2100-2130	405	1
Holloway Road	2130-2200	342	1
Holloway Road	2200-2230	308	1
Holloway Road	2230-2300	317	1
Holloway Road	2300-2330	298	1
Holloway Road	2330-2400	239	1
Holloway Road	0000-0030	155	1
Holloway Road	0030-0100	73	1
Holloway Road	0100-0130	22	1
Holloway Road	0130-0200	12	1
Holloway Road	0200-0230	0	0
Holloway Road	0230-0300	0	0
Holloway Road	0300-0330	0	0
Holloway Road	0330-0400	0	0
Holloway Road	0400-0430	0	0
Hornchurch	0430-0500	0	0
Hornchurch	0500-0530	40	1
Hornchurch	0530-0600	118	1
Hornchurch	0600-0630	214	1
Hornchurch	0630-0700	285	1
Hornchurch	0700-0730	431	1
Hornchurch	0730-0800	615	1
Hornchurch	0800-0830	578	1
Hornchurch	0830-0900	336	1
Hornchurch	0900-0930	174	1
Hornchurch	0930-1000	132	1
Hornchurch	1000-1030	101	1
Hornchurch	1030-1100	98	1
Hornchurch	1100-1130	84	1
Hornchurch	1130-1200	90	1
Hornchurch	1200-1230	102	1
Hornchurch	1230-1300	103	1
Hornchurch	1300-1330	98	1
Hornchurch	1330-1400	101	1
Hornchurch	1400-1430	109	1
Hornchurch	1430-1500	132	1
Hornchurch	1500-1530	146	1
Hornchurch	1530-1600	202	1
Hornchurch	1600-1630	238	1
Hornchurch	1630-1700	294	1
Hornchurch	1700-1730	351	1
Hornchurch	1730-1800	424	1
Hornchurch	1800-1830	442	1
Hornchurch	1830-1900	342	1
Hornchurch	1900-1930	222	1
Hornchurch	1930-2000	153	1
Hornchurch	2000-2030	118	1
Hornchurch	2030-2100	85	1
Hornchurch	2100-2130	68	1
Hornchurch	2130-2200	67	1
Hornchurch	2200-2230	63	1
Hornchurch	2230-2300	67	1
Hornchurch	2300-2330	64	1
Hornchurch	2330-2400	51	1
Hornchurch	0000-0030	51	1
Hornchurch	0030-0100	29	1
Hornchurch	0100-0130	9	1
Hornchurch	0130-0200	1	1
Hornchurch	0200-0230	0	0
Hornchurch	0230-0300	0	0
Hornchurch	0300-0330	0	0
Hornchurch	0330-0400	0	0
Hornchurch	0400-0430	0	0
Hounslow Central	0430-0500	0	0
Hounslow Central	0500-0530	67	1
Hounslow Central	0530-0600	171	1
Hounslow Central	0600-0630	303	1
Hounslow Central	0630-0700	427	1
Hounslow Central	0700-0730	527	1
Hounslow Central	0730-0800	669	1
Hounslow Central	0800-0830	721	1
Hounslow Central	0830-0900	693	1
Hounslow Central	0900-0930	512	1
Hounslow Central	0930-1000	349	1
Hounslow Central	1000-1030	261	1
Hounslow Central	1030-1100	234	1
Hounslow Central	1100-1130	227	1
Hounslow Central	1130-1200	221	1
Hounslow Central	1200-1230	229	1
Hounslow Central	1230-1300	249	1
Hounslow Central	1300-1330	243	1
Hounslow Central	1330-1400	230	1
Hounslow Central	1400-1430	246	1
Hounslow Central	1430-1500	261	1
Hounslow Central	1500-1530	287	1
Hounslow Central	1530-1600	303	1
Hounslow Central	1600-1630	351	1
Hounslow Central	1630-1700	420	1
Hounslow Central	1700-1730	529	1
Hounslow Central	1730-1800	558	1
Hounslow Central	1800-1830	606	1
Hounslow Central	1830-1900	527	1
Hounslow Central	1900-1930	428	1
Hounslow Central	1930-2000	313	1
Hounslow Central	2000-2030	239	1
Hounslow Central	2030-2100	193	1
Hounslow Central	2100-2130	163	1
Hounslow Central	2130-2200	142	1
Hounslow Central	2200-2230	152	1
Hounslow Central	2230-2300	130	1
Hounslow Central	2300-2330	109	1
Hounslow Central	2330-2400	89	1
Hounslow Central	0000-0030	60	1
Hounslow Central	0030-0100	39	1
Hounslow Central	0100-0130	19	1
Hounslow Central	0130-0200	6	1
Hounslow Central	0200-0230	0	0
Hounslow Central	0230-0300	0	0
Hounslow Central	0300-0330	0	0
Hounslow Central	0330-0400	0	0
Hounslow Central	0400-0430	0	0
Hounslow East	0430-0500	0	0
Hounslow East	0500-0530	75	1
Hounslow East	0530-0600	178	1
Hounslow East	0600-0630	289	1
Hounslow East	0630-0700	448	1
Hounslow East	0700-0730	518	1
Hounslow East	0730-0800	605	1
Hounslow East	0800-0830	662	1
Hounslow East	0830-0900	549	1
Hounslow East	0900-0930	388	1
Hounslow East	0930-1000	266	1
Hounslow East	1000-1030	215	1
Hounslow East	1030-1100	200	1
Hounslow East	1100-1130	196	1
Hounslow East	1130-1200	191	1
Hounslow East	1200-1230	203	1
Hounslow East	1230-1300	229	1
Hounslow East	1300-1330	233	1
Hounslow East	1330-1400	227	1
Hounslow East	1400-1430	231	1
Hounslow East	1430-1500	253	1
Hounslow East	1500-1530	250	1
Hounslow East	1530-1600	299	1
Hounslow East	1600-1630	353	1
Hounslow East	1630-1700	443	1
Hounslow East	1700-1730	531	1
Hounslow East	1730-1800	606	1
Hounslow East	1800-1830	628	1
Hounslow East	1830-1900	575	1
Hounslow East	1900-1930	464	1
Hounslow East	1930-2000	341	1
Hounslow East	2000-2030	286	1
Hounslow East	2030-2100	225	1
Hounslow East	2100-2130	203	1
Hounslow East	2130-2200	181	1
Hounslow East	2200-2230	166	1
Hounslow East	2230-2300	164	1
Hounslow East	2300-2330	140	1
Hounslow East	2330-2400	116	1
Hounslow East	0000-0030	85	1
Hounslow East	0030-0100	49	1
Hounslow East	0100-0130	26	1
Hounslow East	0130-0200	6	1
Hounslow East	0200-0230	0	0
Hounslow East	0230-0300	0	0
Hounslow East	0300-0330	0	0
Hounslow East	0330-0400	0	0
Hounslow East	0400-0430	0	0
Hounslow West	0430-0500	0	0
Hounslow West	0500-0530	103	1
Hounslow West	0530-0600	176	1
Hounslow West	0600-0630	271	1
Hounslow West	0630-0700	353	1
Hounslow West	0700-0730	435	1
Hounslow West	0730-0800	580	1
Hounslow West	0800-0830	563	1
Hounslow West	0830-0900	399	1
Hounslow West	0900-0930	295	1
Hounslow West	0930-1000	248	1
Hounslow West	1000-1030	217	1
Hounslow West	1030-1100	188	1
Hounslow West	1100-1130	182	1
Hounslow West	1130-1200	171	1
Hounslow West	1200-1230	195	1
Hounslow West	1230-1300	223	1
Hounslow West	1300-1330	221	1
Hounslow West	1330-1400	209	1
Hounslow West	1400-1430	232	1
Hounslow West	1430-1500	239	1
Hounslow West	1500-1530	235	1
Hounslow West	1530-1600	240	1
Hounslow West	1600-1630	267	1
Hounslow West	1630-1700	323	1
Hounslow West	1700-1730	401	1
Hounslow West	1730-1800	464	1
Hounslow West	1800-1830	485	1
Hounslow West	1830-1900	462	1
Hounslow West	1900-1930	390	1
Hounslow West	1930-2000	297	1
Hounslow West	2000-2030	234	1
Hounslow West	2030-2100	201	1
Hounslow West	2100-2130	184	1
Hounslow West	2130-2200	167	1
Hounslow West	2200-2230	192	1
Hounslow West	2230-2300	171	1
Hounslow West	2300-2330	138	1
Hounslow West	2330-2400	106	1
Hounslow West	0000-0030	74	1
Hounslow West	0030-0100	43	1
Hounslow West	0100-0130	23	1
Hounslow West	0130-0200	8	1
Hounslow West	0200-0230	0	0
Hounslow West	0230-0300	0	0
Hounslow West	0300-0330	0	0
Hounslow West	0330-0400	0	0
Hounslow West	0400-0430	0	0
Hyde Park Corner	0430-0500	0	0
Hyde Park Corner	0500-0530	0	1
Hyde Park Corner	0530-0600	32	1
Hyde Park Corner	0600-0630	71	1
Hyde Park Corner	0630-0700	149	1
Hyde Park Corner	0700-0730	371	1
Hyde Park Corner	0730-0800	562	1
Hyde Park Corner	0800-0830	439	1
Hyde Park Corner	0830-0900	598	1
Hyde Park Corner	0900-0930	586	1
Hyde Park Corner	0930-1000	461	1
Hyde Park Corner	1000-1030	392	1
Hyde Park Corner	1030-1100	370	1
Hyde Park Corner	1100-1130	404	1
Hyde Park Corner	1130-1200	432	1
Hyde Park Corner	1200-1230	473	1
Hyde Park Corner	1230-1300	456	1
Hyde Park Corner	1300-1330	416	1
Hyde Park Corner	1330-1400	418	1
Hyde Park Corner	1400-1430	442	1
Hyde Park Corner	1430-1500	454	1
Hyde Park Corner	1500-1530	472	1
Hyde Park Corner	1530-1600	520	1
Hyde Park Corner	1600-1630	583	1
Hyde Park Corner	1630-1700	705	1
Hyde Park Corner	1700-1730	798	1
Hyde Park Corner	1730-1800	778	1
Hyde Park Corner	1800-1830	800	1
Hyde Park Corner	1830-1900	677	1
Hyde Park Corner	1900-1930	492	1
Hyde Park Corner	1930-2000	403	1
Hyde Park Corner	2000-2030	342	1
Hyde Park Corner	2030-2100	286	1
Hyde Park Corner	2100-2130	279	1
Hyde Park Corner	2130-2200	263	1
Hyde Park Corner	2200-2230	310	1
Hyde Park Corner	2230-2300	212	1
Hyde Park Corner	2300-2330	156	1
Hyde Park Corner	2330-2400	108	1
Hyde Park Corner	0000-0030	70	1
Hyde Park Corner	0030-0100	17	1
Hyde Park Corner	0100-0130	5	1
Hyde Park Corner	0130-0200	5	1
Hyde Park Corner	0200-0230	0	0
Hyde Park Corner	0230-0300	0	0
Hyde Park Corner	0300-0330	0	0
Hyde Park Corner	0330-0400	0	0
Hyde Park Corner	0400-0430	0	0
Ickenham	0430-0500	0	0
Ickenham	0500-0530	12	1
Ickenham	0530-0600	24	1
Ickenham	0600-0630	62	1
Ickenham	0630-0700	135	1
Ickenham	0700-0730	199	1
Ickenham	0730-0800	242	1
Ickenham	0800-0830	284	1
Ickenham	0830-0900	198	1
Ickenham	0900-0930	93	1
Ickenham	0930-1000	79	1
Ickenham	1000-1030	70	1
Ickenham	1030-1100	62	1
Ickenham	1100-1130	58	1
Ickenham	1130-1200	61	1
Ickenham	1200-1230	62	1
Ickenham	1230-1300	61	1
Ickenham	1300-1330	63	1
Ickenham	1330-1400	63	1
Ickenham	1400-1430	64	1
Ickenham	1430-1500	71	1
Ickenham	1500-1530	87	1
Ickenham	1530-1600	189	1
Ickenham	1600-1630	136	1
Ickenham	1630-1700	151	1
Ickenham	1700-1730	182	1
Ickenham	1730-1800	198	1
Ickenham	1800-1830	192	1
Ickenham	1830-1900	175	1
Ickenham	1900-1930	136	1
Ickenham	1930-2000	85	1
Ickenham	2000-2030	56	1
Ickenham	2030-2100	46	1
Ickenham	2100-2130	40	1
Ickenham	2130-2200	40	1
Ickenham	2200-2230	47	1
Ickenham	2230-2300	45	1
Ickenham	2300-2330	39	1
Ickenham	2330-2400	29	1
Ickenham	0000-0030	19	1
Ickenham	0030-0100	11	1
Ickenham	0100-0130	4	1
Ickenham	0130-0200	0	1
Ickenham	0200-0230	0	0
Ickenham	0230-0300	0	0
Ickenham	0300-0330	0	0
Ickenham	0330-0400	0	0
Ickenham	0400-0430	0	0
Kennington	0430-0500	0	0
Kennington	0500-0530	13	1
Kennington	0530-0600	63	1
Kennington	0600-0630	143	1
Kennington	0630-0700	286	1
Kennington	0700-0730	556	1
Kennington	0730-0800	761	1
Kennington	0800-0830	1030	1
Kennington	0830-0900	1178	1
Kennington	0900-0930	829	1
Kennington	0930-1000	554	1
Kennington	1000-1030	367	1
Kennington	1030-1100	297	1
Kennington	1100-1130	256	1
Kennington	1130-1200	256	1
Kennington	1200-1230	267	1
Kennington	1230-1300	278	1
Kennington	1300-1330	280	1
Kennington	1330-1400	277	1
Kennington	1400-1430	278	1
Kennington	1430-1500	294	1
Kennington	1500-1530	329	1
Kennington	1530-1600	379	1
Kennington	1600-1630	455	1
Kennington	1630-1700	564	1
Kennington	1700-1730	684	1
Kennington	1730-1800	758	1
Kennington	1800-1830	856	1
Kennington	1830-1900	786	1
Kennington	1900-1930	631	1
Kennington	1930-2000	493	1
Kennington	2000-2030	406	1
Kennington	2030-2100	366	1
Kennington	2100-2130	344	1
Kennington	2130-2200	327	1
Kennington	2200-2230	337	1
Kennington	2230-2300	328	1
Kennington	2300-2330	276	1
Kennington	2330-2400	227	1
Kennington	0000-0030	167	1
Kennington	0030-0100	86	1
Kennington	0100-0130	33	1
Kennington	0130-0200	24	1
Kennington	0200-0230	0	0
Kennington	0230-0300	0	0
Kennington	0300-0330	0	0
Kennington	0330-0400	0	0
Kennington	0400-0430	0	0
Kensal Green	0430-0500	0	0
Kensal Green	0500-0530	13	1
Kensal Green	0530-0600	38	1
Kensal Green	0600-0630	72	1
Kensal Green	0630-0700	133	1
Kensal Green	0700-0730	277	1
Kensal Green	0730-0800	467	1
Kensal Green	0800-0830	645	1
Kensal Green	0830-0900	636	1
Kensal Green	0900-0930	413	1
Kensal Green	0930-1000	267	1
Kensal Green	1000-1030	188	1
Kensal Green	1030-1100	158	1
Kensal Green	1100-1130	147	1
Kensal Green	1130-1200	140	1
Kensal Green	1200-1230	141	1
Kensal Green	1230-1300	141	1
Kensal Green	1300-1330	138	1
Kensal Green	1330-1400	143	1
Kensal Green	1400-1430	145	1
Kensal Green	1430-1500	155	1
Kensal Green	1500-1530	174	1
Kensal Green	1530-1600	201	1
Kensal Green	1600-1630	224	1
Kensal Green	1630-1700	282	1
Kensal Green	1700-1730	330	1
Kensal Green	1730-1800	383	1
Kensal Green	1800-1830	389	1
Kensal Green	1830-1900	373	1
Kensal Green	1900-1930	295	1
Kensal Green	1930-2000	231	1
Kensal Green	2000-2030	174	1
Kensal Green	2030-2100	155	1
Kensal Green	2100-2130	142	1
Kensal Green	2130-2200	135	1
Kensal Green	2200-2230	115	1
Kensal Green	2230-2300	124	1
Kensal Green	2300-2330	105	1
Kensal Green	2330-2400	95	1
Kensal Green	0000-0030	64	1
Kensal Green	0030-0100	21	1
Kensal Green	0100-0130	0	1
Kensal Green	0130-0200	0	1
Kensal Green	0200-0230	0	0
Kensal Green	0230-0300	0	0
Kensal Green	0300-0330	0	0
Kensal Green	0330-0400	0	0
Kensal Green	0400-0430	0	0
Kensington (Olympia)	0430-0500	0	0
Kensington (Olympia)	0500-0530	0	1
Kensington (Olympia)	0530-0600	0	1
Kensington (Olympia)	0600-0630	0	1
Kensington (Olympia)	0630-0700	0	1
Kensington (Olympia)	0700-0730	51	1
Kensington (Olympia)	0730-0800	80	1
Kensington (Olympia)	0800-0830	126	1
Kensington (Olympia)	0830-0900	113	1
Kensington (Olympia)	0900-0930	109	1
Kensington (Olympia)	0930-1000	120	1
Kensington (Olympia)	1000-1030	128	1
Kensington (Olympia)	1030-1100	118	1
Kensington (Olympia)	1100-1130	102	1
Kensington (Olympia)	1130-1200	117	1
Kensington (Olympia)	1200-1230	55	1
Kensington (Olympia)	1230-1300	212	1
Kensington (Olympia)	1300-1330	109	1
Kensington (Olympia)	1330-1400	128	1
Kensington (Olympia)	1400-1430	93	1
Kensington (Olympia)	1430-1500	165	1
Kensington (Olympia)	1500-1530	122	1
Kensington (Olympia)	1530-1600	133	1
Kensington (Olympia)	1600-1630	121	1
Kensington (Olympia)	1630-1700	110	1
Kensington (Olympia)	1700-1730	174	1
Kensington (Olympia)	1730-1800	69	1
Kensington (Olympia)	1800-1830	89	1
Kensington (Olympia)	1830-1900	70	1
Kensington (Olympia)	1900-1930	105	1
Kensington (Olympia)	1930-2000	79	1
Kensington (Olympia)	2000-2030	69	1
Kensington (Olympia)	2030-2100	56	1
Kensington (Olympia)	2100-2130	31	1
Kensington (Olympia)	2130-2200	66	1
Kensington (Olympia)	2200-2230	43	1
Kensington (Olympia)	2230-2300	31	1
Kensington (Olympia)	2300-2330	36	1
Kensington (Olympia)	2330-2400	26	1
Kensington (Olympia)	0000-0030	0	1
Kensington (Olympia)	0030-0100	0	1
Kensington (Olympia)	0100-0130	0	1
Kensington (Olympia)	0130-0200	0	1
Kensington (Olympia)	0200-0230	0	0
Kensington (Olympia)	0230-0300	0	0
Kensington (Olympia)	0300-0330	0	0
Kensington (Olympia)	0330-0400	0	0
Kensington (Olympia)	0400-0430	0	0
Kentish Town	0430-0500	0	0
Kentish Town	0500-0530	4	1
Kentish Town	0530-0600	60	1
Kentish Town	0600-0630	158	1
Kentish Town	0630-0700	329	1
Kentish Town	0700-0730	604	1
Kentish Town	0730-0800	1010	1
Kentish Town	0800-0830	1458	1
Kentish Town	0830-0900	1744	1
Kentish Town	0900-0930	1368	1
Kentish Town	0930-1000	897	1
Kentish Town	1000-1030	591	1
Kentish Town	1030-1100	478	1
Kentish Town	1100-1130	427	1
Kentish Town	1130-1200	433	1
Kentish Town	1200-1230	446	1
Kentish Town	1230-1300	478	1
Kentish Town	1300-1330	484	1
Kentish Town	1330-1400	486	1
Kentish Town	1400-1430	472	1
Kentish Town	1430-1500	506	1
Kentish Town	1500-1530	565	1
Kentish Town	1530-1600	655	1
Kentish Town	1600-1630	741	1
Kentish Town	1630-1700	867	1
Kentish Town	1700-1730	1165	1
Kentish Town	1730-1800	1526	1
Kentish Town	1800-1830	1547	1
Kentish Town	1830-1900	1341	1
Kentish Town	1900-1930	1019	1
Kentish Town	1930-2000	746	1
Kentish Town	2000-2030	602	1
Kentish Town	2030-2100	477	1
Kentish Town	2100-2130	434	1
Kentish Town	2130-2200	395	1
Kentish Town	2200-2230	439	1
Kentish Town	2230-2300	682	1
Kentish Town	2300-2330	539	1
Kentish Town	2330-2400	316	1
Kentish Town	0000-0030	190	1
Kentish Town	0030-0100	74	1
Kentish Town	0100-0130	23	1
Kentish Town	0130-0200	21	1
Kentish Town	0200-0230	0	0
Kentish Town	0230-0300	0	0
Kentish Town	0300-0330	0	0
Kentish Town	0330-0400	0	0
Kentish Town	0400-0430	0	0
Kenton	0430-0500	0	0
Kenton	0500-0530	22	1
Kenton	0530-0600	93	1
Kenton	0600-0630	202	1
Kenton	0630-0700	285	1
Kenton	0700-0730	307	1
Kenton	0730-0800	378	1
Kenton	0800-0830	474	1
Kenton	0830-0900	314	1
Kenton	0900-0930	205	1
Kenton	0930-1000	145	1
Kenton	1000-1030	122	1
Kenton	1030-1100	106	1
Kenton	1100-1130	96	1
Kenton	1130-1200	78	1
Kenton	1200-1230	91	1
Kenton	1230-1300	95	1
Kenton	1300-1330	112	1
Kenton	1330-1400	104	1
Kenton	1400-1430	110	1
Kenton	1430-1500	127	1
Kenton	1500-1530	156	1
Kenton	1530-1600	269	1
Kenton	1600-1630	262	1
Kenton	1630-1700	252	1
Kenton	1700-1730	350	1
Kenton	1730-1800	352	1
Kenton	1800-1830	373	1
Kenton	1830-1900	282	1
Kenton	1900-1930	210	1
Kenton	1930-2000	132	1
Kenton	2000-2030	106	1
Kenton	2030-2100	89	1
Kenton	2100-2130	82	1
Kenton	2130-2200	58	1
Kenton	2200-2230	59	1
Kenton	2230-2300	49	1
Kenton	2300-2330	47	1
Kenton	2330-2400	37	1
Kenton	0000-0030	22	1
Kenton	0030-0100	5	1
Kenton	0100-0130	0	1
Kenton	0130-0200	0	1
Kenton	0200-0230	0	0
Kenton	0230-0300	0	0
Kenton	0300-0330	0	0
Kenton	0330-0400	0	0
Kenton	0400-0430	0	0
Kew Gardens	0430-0500	0	0
Kew Gardens	0500-0530	7	1
Kew Gardens	0530-0600	29	1
Kew Gardens	0600-0630	82	1
Kew Gardens	0630-0700	220	1
Kew Gardens	0700-0730	455	1
Kew Gardens	0730-0800	708	1
Kew Gardens	0800-0830	731	1
Kew Gardens	0830-0900	601	1
Kew Gardens	0900-0930	460	1
Kew Gardens	0930-1000	341	1
Kew Gardens	1000-1030	289	1
Kew Gardens	1030-1100	260	1
Kew Gardens	1100-1130	265	1
Kew Gardens	1130-1200	269	1
Kew Gardens	1200-1230	271	1
Kew Gardens	1230-1300	262	1
Kew Gardens	1300-1330	262	1
Kew Gardens	1330-1400	251	1
Kew Gardens	1400-1430	273	1
Kew Gardens	1430-1500	289	1
Kew Gardens	1500-1530	343	1
Kew Gardens	1530-1600	385	1
Kew Gardens	1600-1630	514	1
Kew Gardens	1630-1700	588	1
Kew Gardens	1700-1730	596	1
Kew Gardens	1730-1800	626	1
Kew Gardens	1800-1830	701	1
Kew Gardens	1830-1900	606	1
Kew Gardens	1900-1930	531	1
Kew Gardens	1930-2000	384	1
Kew Gardens	2000-2030	303	1
Kew Gardens	2030-2100	248	1
Kew Gardens	2100-2130	217	1
Kew Gardens	2130-2200	179	1
Kew Gardens	2200-2230	160	1
Kew Gardens	2230-2300	143	1
Kew Gardens	2300-2330	135	1
Kew Gardens	2330-2400	92	1
Kew Gardens	0000-0030	59	1
Kew Gardens	0030-0100	19	1
Kew Gardens	0100-0130	5	1
Kew Gardens	0130-0200	0	1
Kew Gardens	0200-0230	0	0
Kew Gardens	0230-0300	0	0
Kew Gardens	0300-0330	0	0
Kew Gardens	0330-0400	0	0
Kew Gardens	0400-0430	0	0
Kilburn	0430-0500	0	0
Kilburn	0500-0530	70	1
Kilburn	0530-0600	150	1
Kilburn	0600-0630	322	1
Kilburn	0630-0700	587	1
Kilburn	0700-0730	898	1
Kilburn	0730-0800	1190	1
Kilburn	0800-0830	1613	1
Kilburn	0830-0900	1463	1
Kilburn	0900-0930	1021	1
Kilburn	0930-1000	699	1
Kilburn	1000-1030	517	1
Kilburn	1030-1100	483	1
Kilburn	1100-1130	456	1
Kilburn	1130-1200	442	1
Kilburn	1200-1230	435	1
Kilburn	1230-1300	450	1
Kilburn	1300-1330	459	1
Kilburn	1330-1400	466	1
Kilburn	1400-1430	479	1
Kilburn	1430-1500	520	1
Kilburn	1500-1530	585	1
Kilburn	1530-1600	662	1
Kilburn	1600-1630	787	1
Kilburn	1630-1700	892	1
Kilburn	1700-1730	1037	1
Kilburn	1730-1800	1216	1
Kilburn	1800-1830	1320	1
Kilburn	1830-1900	1192	1
Kilburn	1900-1930	922	1
Kilburn	1930-2000	729	1
Kilburn	2000-2030	611	1
Kilburn	2030-2100	525	1
Kilburn	2100-2130	484	1
Kilburn	2130-2200	469	1
Kilburn	2200-2230	452	1
Kilburn	2230-2300	446	1
Kilburn	2300-2330	392	1
Kilburn	2330-2400	335	1
Kilburn	0000-0030	249	1
Kilburn	0030-0100	130	1
Kilburn	0100-0130	35	1
Kilburn	0130-0200	18	1
Kilburn	0200-0230	0	0
Kilburn	0230-0300	0	0
Kilburn	0300-0330	0	0
Kilburn	0330-0400	0	0
Kilburn	0400-0430	0	0
Kilburn Park	0430-0500	0	0
Kilburn Park	0500-0530	5	1
Kilburn Park	0530-0600	36	1
Kilburn Park	0600-0630	90	1
Kilburn Park	0630-0700	153	1
Kilburn Park	0700-0730	279	1
Kilburn Park	0730-0800	408	1
Kilburn Park	0800-0830	568	1
Kilburn Park	0830-0900	551	1
Kilburn Park	0900-0930	393	1
Kilburn Park	0930-1000	290	1
Kilburn Park	1000-1030	235	1
Kilburn Park	1030-1100	210	1
Kilburn Park	1100-1130	208	1
Kilburn Park	1130-1200	205	1
Kilburn Park	1200-1230	208	1
Kilburn Park	1230-1300	207	1
Kilburn Park	1300-1330	210	1
Kilburn Park	1330-1400	214	1
Kilburn Park	1400-1430	218	1
Kilburn Park	1430-1500	238	1
Kilburn Park	1500-1530	259	1
Kilburn Park	1530-1600	293	1
Kilburn Park	1600-1630	330	1
Kilburn Park	1630-1700	363	1
Kilburn Park	1700-1730	395	1
Kilburn Park	1730-1800	452	1
Kilburn Park	1800-1830	489	1
Kilburn Park	1830-1900	449	1
Kilburn Park	1900-1930	361	1
Kilburn Park	1930-2000	280	1
Kilburn Park	2000-2030	245	1
Kilburn Park	2030-2100	204	1
Kilburn Park	2100-2130	184	1
Kilburn Park	2130-2200	175	1
Kilburn Park	2200-2230	171	1
Kilburn Park	2230-2300	164	1
Kilburn Park	2300-2330	134	1
Kilburn Park	2330-2400	119	1
Kilburn Park	0000-0030	75	1
Kilburn Park	0030-0100	33	1
Kilburn Park	0100-0130	0	1
Kilburn Park	0130-0200	0	1
Kilburn Park	0200-0230	0	0
Kilburn Park	0230-0300	0	0
Kilburn Park	0300-0330	0	0
Kilburn Park	0330-0400	0	0
Kilburn Park	0400-0430	0	0
King's Cross St. Pancras	0430-0500	0	0
King's Cross St. Pancras	0500-0530	149	1
King's Cross St. Pancras	0530-0600	708	1
King's Cross St. Pancras	0600-0630	1708	1
King's Cross St. Pancras	0630-0700	3687	1
King's Cross St. Pancras	0700-0730	6191	1
King's Cross St. Pancras	0730-0800	9817	1
King's Cross St. Pancras	0800-0830	12938	1
King's Cross St. Pancras	0830-0900	15311	1
King's Cross St. Pancras	0900-0930	14218	1
King's Cross St. Pancras	0930-1000	10514	1
King's Cross St. Pancras	1000-1030	8139	1
King's Cross St. Pancras	1030-1100	7665	1
King's Cross St. Pancras	1100-1130	6594	1
King's Cross St. Pancras	1130-1200	6674	1
King's Cross St. Pancras	1200-1230	6693	1
King's Cross St. Pancras	1230-1300	6939	1
King's Cross St. Pancras	1300-1330	6951	1
King's Cross St. Pancras	1330-1400	6954	1
King's Cross St. Pancras	1400-1430	7030	1
King's Cross St. Pancras	1430-1500	7255	1
King's Cross St. Pancras	1500-1530	7662	1
King's Cross St. Pancras	1530-1600	8543	1
King's Cross St. Pancras	1600-1630	10507	1
King's Cross St. Pancras	1630-1700	11927	1
King's Cross St. Pancras	1700-1730	14248	1
King's Cross St. Pancras	1730-1800	15857	1
King's Cross St. Pancras	1800-1830	15052	1
King's Cross St. Pancras	1830-1900	12327	1
King's Cross St. Pancras	1900-1930	9282	1
King's Cross St. Pancras	1930-2000	7068	1
King's Cross St. Pancras	2000-2030	5872	1
King's Cross St. Pancras	2030-2100	4992	1
King's Cross St. Pancras	2100-2130	4880	1
King's Cross St. Pancras	2130-2200	4469	1
King's Cross St. Pancras	2200-2230	4291	1
King's Cross St. Pancras	2230-2300	4322	1
King's Cross St. Pancras	2300-2330	3650	1
King's Cross St. Pancras	2330-2400	2468	1
King's Cross St. Pancras	0000-0030	1422	1
King's Cross St. Pancras	0030-0100	654	1
King's Cross St. Pancras	0100-0130	255	1
King's Cross St. Pancras	0130-0200	131	1
King's Cross St. Pancras	0200-0230	0	0
King's Cross St. Pancras	0230-0300	0	0
King's Cross St. Pancras	0300-0330	0	0
King's Cross St. Pancras	0330-0400	0	0
King's Cross St. Pancras	0400-0430	0	0
Kingsbury	0430-0500	0	0
Kingsbury	0500-0530	43	1
Kingsbury	0530-0600	214	1
Kingsbury	0600-0630	581	1
Kingsbury	0630-0700	803	1
Kingsbury	0700-0730	701	1
Kingsbury	0730-0800	884	1
Kingsbury	0800-0830	1103	1
Kingsbury	0830-0900	679	1
Kingsbury	0900-0930	440	1
Kingsbury	0930-1000	332	1
Kingsbury	1000-1030	279	1
Kingsbury	1030-1100	255	1
Kingsbury	1100-1130	269	1
Kingsbury	1130-1200	252	1
Kingsbury	1200-1230	246	1
Kingsbury	1230-1300	266	1
Kingsbury	1300-1330	273	1
Kingsbury	1330-1400	312	1
Kingsbury	1400-1430	275	1
Kingsbury	1430-1500	323	1
Kingsbury	1500-1530	318	1
Kingsbury	1530-1600	615	1
Kingsbury	1600-1630	573	1
Kingsbury	1630-1700	595	1
Kingsbury	1700-1730	729	1
Kingsbury	1730-1800	897	1
Kingsbury	1800-1830	952	1
Kingsbury	1830-1900	877	1
Kingsbury	1900-1930	587	1
Kingsbury	1930-2000	380	1
Kingsbury	2000-2030	293	1
Kingsbury	2030-2100	225	1
Kingsbury	2100-2130	186	1
Kingsbury	2130-2200	164	1
Kingsbury	2200-2230	162	1
Kingsbury	2230-2300	145	1
Kingsbury	2300-2330	104	1
Kingsbury	2330-2400	88	1
Kingsbury	0000-0030	60	1
Kingsbury	0030-0100	32	1
Kingsbury	0100-0130	14	1
Kingsbury	0130-0200	5	1
Kingsbury	0200-0230	0	0
Kingsbury	0230-0300	0	0
Kingsbury	0300-0330	0	0
Kingsbury	0330-0400	0	0
Kingsbury	0400-0430	0	0
Knightsbridge	0430-0500	0	0
Knightsbridge	0500-0530	0	1
Knightsbridge	0530-0600	59	1
Knightsbridge	0600-0630	143	1
Knightsbridge	0630-0700	303	1
Knightsbridge	0700-0730	515	1
Knightsbridge	0730-0800	1324	1
Knightsbridge	0800-0830	1236	1
Knightsbridge	0830-0900	1655	1
Knightsbridge	0900-0930	1544	1
Knightsbridge	0930-1000	1429	1
Knightsbridge	1000-1030	1215	1
Knightsbridge	1030-1100	1344	1
Knightsbridge	1100-1130	1345	1
Knightsbridge	1130-1200	1524	1
Knightsbridge	1200-1230	1656	1
Knightsbridge	1230-1300	1591	1
Knightsbridge	1300-1330	1468	1
Knightsbridge	1330-1400	1446	1
Knightsbridge	1400-1430	1551	1
Knightsbridge	1430-1500	1650	1
Knightsbridge	1500-1530	1775	1
Knightsbridge	1530-1600	1893	1
Knightsbridge	1600-1630	2082	1
Knightsbridge	1630-1700	2273	1
Knightsbridge	1700-1730	2505	1
Knightsbridge	1730-1800	2639	1
Knightsbridge	1800-1830	2673	1
Knightsbridge	1830-1900	2134	1
Knightsbridge	1900-1930	1744	1
Knightsbridge	1930-2000	1333	1
Knightsbridge	2000-2030	861	1
Knightsbridge	2030-2100	700	1
Knightsbridge	2100-2130	1026	1
Knightsbridge	2130-2200	650	1
Knightsbridge	2200-2230	475	1
Knightsbridge	2230-2300	364	1
Knightsbridge	2300-2330	326	1
Knightsbridge	2330-2400	221	1
Knightsbridge	0000-0030	130	1
Knightsbridge	0030-0100	22	1
Knightsbridge	0100-0130	7	1
Knightsbridge	0130-0200	5	1
Knightsbridge	0200-0230	0	0
Knightsbridge	0230-0300	0	0
Knightsbridge	0300-0330	0	0
Knightsbridge	0330-0400	0	0
Knightsbridge	0400-0430	0	0
Ladbroke Grove	0430-0500	0	0
Ladbroke Grove	0500-0530	18	1
Ladbroke Grove	0530-0600	38	1
Ladbroke Grove	0600-0630	81	1
Ladbroke Grove	0630-0700	184	1
Ladbroke Grove	0700-0730	420	1
Ladbroke Grove	0730-0800	786	1
Ladbroke Grove	0800-0830	995	1
Ladbroke Grove	0830-0900	1163	1
Ladbroke Grove	0900-0930	845	1
Ladbroke Grove	0930-1000	633	1
Ladbroke Grove	1000-1030	427	1
Ladbroke Grove	1030-1100	389	1
Ladbroke Grove	1100-1130	388	1
Ladbroke Grove	1130-1200	404	1
Ladbroke Grove	1200-1230	420	1
Ladbroke Grove	1230-1300	420	1
Ladbroke Grove	1300-1330	452	1
Ladbroke Grove	1330-1400	444	1
Ladbroke Grove	1400-1430	411	1
Ladbroke Grove	1430-1500	413	1
Ladbroke Grove	1500-1530	523	1
Ladbroke Grove	1530-1600	605	1
Ladbroke Grove	1600-1630	688	1
Ladbroke Grove	1630-1700	769	1
Ladbroke Grove	1700-1730	861	1
Ladbroke Grove	1730-1800	863	1
Ladbroke Grove	1800-1830	883	1
Ladbroke Grove	1830-1900	741	1
Ladbroke Grove	1900-1930	560	1
Ladbroke Grove	1930-2000	418	1
Ladbroke Grove	2000-2030	352	1
Ladbroke Grove	2030-2100	283	1
Ladbroke Grove	2100-2130	253	1
Ladbroke Grove	2130-2200	229	1
Ladbroke Grove	2200-2230	194	1
Ladbroke Grove	2230-2300	189	1
Ladbroke Grove	2300-2330	206	1
Ladbroke Grove	2330-2400	140	1
Ladbroke Grove	0000-0030	81	1
Ladbroke Grove	0030-0100	32	1
Ladbroke Grove	0100-0130	4	1
Ladbroke Grove	0130-0200	0	1
Ladbroke Grove	0200-0230	0	0
Ladbroke Grove	0230-0300	0	0
Ladbroke Grove	0300-0330	0	0
Ladbroke Grove	0330-0400	0	0
Ladbroke Grove	0400-0430	0	0
Lambeth North	0430-0500	0	0
Lambeth North	0500-0530	5	1
Lambeth North	0530-0600	21	1
Lambeth North	0600-0630	51	1
Lambeth North	0630-0700	112	1
Lambeth North	0700-0730	181	1
Lambeth North	0730-0800	288	1
Lambeth North	0800-0830	402	1
Lambeth North	0830-0900	483	1
Lambeth North	0900-0930	423	1
Lambeth North	0930-1000	382	1
Lambeth North	1000-1030	317	1
Lambeth North	1030-1100	279	1
Lambeth North	1100-1130	236	1
Lambeth North	1130-1200	237	1
Lambeth North	1200-1230	245	1
Lambeth North	1230-1300	261	1
Lambeth North	1300-1330	271	1
Lambeth North	1330-1400	271	1
Lambeth North	1400-1430	271	1
Lambeth North	1430-1500	292	1
Lambeth North	1500-1530	309	1
Lambeth North	1530-1600	337	1
Lambeth North	1600-1630	400	1
Lambeth North	1630-1700	438	1
Lambeth North	1700-1730	481	1
Lambeth North	1730-1800	516	1
Lambeth North	1800-1830	483	1
Lambeth North	1830-1900	389	1
Lambeth North	1900-1930	306	1
Lambeth North	1930-2000	241	1
Lambeth North	2000-2030	200	1
Lambeth North	2030-2100	185	1
Lambeth North	2100-2130	211	1
Lambeth North	2130-2200	193	1
Lambeth North	2200-2230	168	1
Lambeth North	2230-2300	166	1
Lambeth North	2300-2330	129	1
Lambeth North	2330-2400	83	1
Lambeth North	0000-0030	52	1
Lambeth North	0030-0100	15	1
Lambeth North	0100-0130	0	1
Lambeth North	0130-0200	0	1
Lambeth North	0200-0230	0	0
Lambeth North	0230-0300	0	0
Lambeth North	0300-0330	0	0
Lambeth North	0330-0400	0	0
Lambeth North	0400-0430	0	0
Lancaster Gate	0430-0500	0	0
Lancaster Gate	0500-0530	5	1
Lancaster Gate	0530-0600	34	1
Lancaster Gate	0600-0630	107	1
Lancaster Gate	0630-0700	241	1
Lancaster Gate	0700-0730	474	1
Lancaster Gate	0730-0800	791	1
Lancaster Gate	0800-0830	1035	1
Lancaster Gate	0830-0900	1162	1
Lancaster Gate	0900-0930	868	1
Lancaster Gate	0930-1000	669	1
Lancaster Gate	1000-1030	493	1
Lancaster Gate	1030-1100	442	1
Lancaster Gate	1100-1130	367	1
Lancaster Gate	1130-1200	352	1
Lancaster Gate	1200-1230	346	1
Lancaster Gate	1230-1300	345	1
Lancaster Gate	1300-1330	355	1
Lancaster Gate	1330-1400	381	1
Lancaster Gate	1400-1430	392	1
Lancaster Gate	1430-1500	427	1
Lancaster Gate	1500-1530	485	1
Lancaster Gate	1530-1600	529	1
Lancaster Gate	1600-1630	616	1
Lancaster Gate	1630-1700	701	1
Lancaster Gate	1700-1730	858	1
Lancaster Gate	1730-1800	960	1
Lancaster Gate	1800-1830	922	1
Lancaster Gate	1830-1900	795	1
Lancaster Gate	1900-1930	592	1
Lancaster Gate	1930-2000	435	1
Lancaster Gate	2000-2030	351	1
Lancaster Gate	2030-2100	314	1
Lancaster Gate	2100-2130	296	1
Lancaster Gate	2130-2200	271	1
Lancaster Gate	2200-2230	295	1
Lancaster Gate	2230-2300	334	1
Lancaster Gate	2300-2330	272	1
Lancaster Gate	2330-2400	196	1
Lancaster Gate	0000-0030	102	1
Lancaster Gate	0030-0100	43	1
Lancaster Gate	0100-0130	21	1
Lancaster Gate	0130-0200	14	1
Lancaster Gate	0200-0230	0	0
Lancaster Gate	0230-0300	0	0
Lancaster Gate	0300-0330	0	0
Lancaster Gate	0330-0400	0	0
Lancaster Gate	0400-0430	0	0
Latimer Road	0430-0500	0	0
Latimer Road	0500-0530	10	1
Latimer Road	0530-0600	16	1
Latimer Road	0600-0630	38	1
Latimer Road	0630-0700	83	1
Latimer Road	0700-0730	168	1
Latimer Road	0730-0800	336	1
Latimer Road	0800-0830	432	1
Latimer Road	0830-0900	617	1
Latimer Road	0900-0930	494	1
Latimer Road	0930-1000	287	1
Latimer Road	1000-1030	185	1
Latimer Road	1030-1100	148	1
Latimer Road	1100-1130	138	1
Latimer Road	1130-1200	145	1
Latimer Road	1200-1230	148	1
Latimer Road	1230-1300	153	1
Latimer Road	1300-1330	162	1
Latimer Road	1330-1400	159	1
Latimer Road	1400-1430	171	1
Latimer Road	1430-1500	174	1
Latimer Road	1500-1530	198	1
Latimer Road	1530-1600	225	1
Latimer Road	1600-1630	289	1
Latimer Road	1630-1700	342	1
Latimer Road	1700-1730	448	1
Latimer Road	1730-1800	529	1
Latimer Road	1800-1830	465	1
Latimer Road	1830-1900	362	1
Latimer Road	1900-1930	271	1
Latimer Road	1930-2000	201	1
Latimer Road	2000-2030	165	1
Latimer Road	2030-2100	126	1
Latimer Road	2100-2130	117	1
Latimer Road	2130-2200	98	1
Latimer Road	2200-2230	94	1
Latimer Road	2230-2300	64	1
Latimer Road	2300-2330	55	1
Latimer Road	2330-2400	41	1
Latimer Road	0000-0030	26	1
Latimer Road	0030-0100	11	1
Latimer Road	0100-0130	2	1
Latimer Road	0130-0200	0	1
Latimer Road	0200-0230	0	0
Latimer Road	0230-0300	0	0
Latimer Road	0300-0330	0	0
Latimer Road	0330-0400	0	0
Latimer Road	0400-0430	0	0
Leicester Square	0430-0500	0	0
Leicester Square	0500-0530	6	1
Leicester Square	0530-0600	153	1
Leicester Square	0600-0630	273	1
Leicester Square	0630-0700	532	1
Leicester Square	0700-0730	758	1
Leicester Square	0730-0800	1047	1
Leicester Square	0800-0830	1501	1
Leicester Square	0830-0900	2367	1
Leicester Square	0900-0930	2390	1
Leicester Square	0930-1000	2033	1
Leicester Square	1000-1030	1609	1
Leicester Square	1030-1100	1710	1
Leicester Square	1100-1130	1681	1
Leicester Square	1130-1200	1863	1
Leicester Square	1200-1230	2031	1
Leicester Square	1230-1300	2193	1
Leicester Square	1300-1330	2286	1
Leicester Square	1330-1400	2408	1
Leicester Square	1400-1430	2405	1
Leicester Square	1430-1500	2452	1
Leicester Square	1500-1530	2462	1
Leicester Square	1530-1600	2660	1
Leicester Square	1600-1630	2867	1
Leicester Square	1630-1700	3329	1
Leicester Square	1700-1730	4144	1
Leicester Square	1730-1800	5280	1
Leicester Square	1800-1830	5566	1
Leicester Square	1830-1900	5149	1
Leicester Square	1900-1930	4220	1
Leicester Square	1930-2000	3172	1
Leicester Square	2000-2030	2874	1
Leicester Square	2030-2100	2759	1
Leicester Square	2100-2130	2797	1
Leicester Square	2130-2200	3086	1
Leicester Square	2200-2230	4233	1
Leicester Square	2230-2300	3789	1
Leicester Square	2300-2330	2940	1
Leicester Square	2330-2400	2262	1
Leicester Square	0000-0030	1233	1
Leicester Square	0030-0100	420	1
Leicester Square	0100-0130	230	1
Leicester Square	0130-0200	119	1
Leicester Square	0200-0230	0	0
Leicester Square	0230-0300	0	0
Leicester Square	0300-0330	0	0
Leicester Square	0330-0400	0	0
Leicester Square	0400-0430	0	0
Leyton	0430-0500	0	0
Leyton	0500-0530	104	1
Leyton	0530-0600	434	1
Leyton	0600-0630	1035	1
Leyton	0630-0700	1548	1
Leyton	0700-0730	1841	1
Leyton	0730-0800	1747	1
Leyton	0800-0830	1998	1
Leyton	0830-0900	1747	1
Leyton	0900-0930	1362	1
Leyton	0930-1000	953	1
Leyton	1000-1030	737	1
Leyton	1030-1100	658	1
Leyton	1100-1130	666	1
Leyton	1130-1200	597	1
Leyton	1200-1230	619	1
Leyton	1230-1300	636	1
Leyton	1300-1330	653	1
Leyton	1330-1400	683	1
Leyton	1400-1430	733	1
Leyton	1430-1500	774	1
Leyton	1500-1530	837	1
Leyton	1530-1600	987	1
Leyton	1600-1630	1254	1
Leyton	1630-1700	1500	1
Leyton	1700-1730	1834	1
Leyton	1730-1800	2131	1
Leyton	1800-1830	2151	1
Leyton	1830-1900	1873	1
Leyton	1900-1930	1484	1
Leyton	1930-2000	1171	1
Leyton	2000-2030	926	1
Leyton	2030-2100	797	1
Leyton	2100-2130	695	1
Leyton	2130-2200	688	1
Leyton	2200-2230	636	1
Leyton	2230-2300	583	1
Leyton	2300-2330	516	1
Leyton	2330-2400	472	1
Leyton	0000-0030	342	1
Leyton	0030-0100	200	1
Leyton	0100-0130	52	1
Leyton	0130-0200	38	1
Leyton	0200-0230	0	0
Leyton	0230-0300	0	0
Leyton	0300-0330	0	0
Leyton	0330-0400	0	0
Leyton	0400-0430	0	0
Leytonstone	0430-0500	0	0
Leytonstone	0500-0530	116	1
Leytonstone	0530-0600	296	1
Leytonstone	0600-0630	655	1
Leytonstone	0630-0700	1019	1
Leytonstone	0700-0730	1354	1
Leytonstone	0730-0800	1628	1
Leytonstone	0800-0830	2172	1
Leytonstone	0830-0900	1891	1
Leytonstone	0900-0930	1269	1
Leytonstone	0930-1000	851	1
Leytonstone	1000-1030	661	1
Leytonstone	1030-1100	565	1
Leytonstone	1100-1130	570	1
Leytonstone	1130-1200	545	1
Leytonstone	1200-1230	539	1
Leytonstone	1230-1300	555	1
Leytonstone	1300-1330	602	1
Leytonstone	1330-1400	576	1
Leytonstone	1400-1430	592	1
Leytonstone	1430-1500	670	1
Leytonstone	1500-1530	752	1
Leytonstone	1530-1600	851	1
Leytonstone	1600-1630	1032	1
Leytonstone	1630-1700	1286	1
Leytonstone	1700-1730	1529	1
Leytonstone	1730-1800	1716	1
Leytonstone	1800-1830	1715	1
Leytonstone	1830-1900	1577	1
Leytonstone	1900-1930	1207	1
Leytonstone	1930-2000	898	1
Leytonstone	2000-2030	722	1
Leytonstone	2030-2100	638	1
Leytonstone	2100-2130	542	1
Leytonstone	2130-2200	508	1
Leytonstone	2200-2230	465	1
Leytonstone	2230-2300	444	1
Leytonstone	2300-2330	415	1
Leytonstone	2330-2400	375	1
Leytonstone	0000-0030	236	1
Leytonstone	0030-0100	143	1
Leytonstone	0100-0130	48	1
Leytonstone	0130-0200	28	1
Leytonstone	0200-0230	0	0
Leytonstone	0230-0300	0	0
Leytonstone	0300-0330	0	0
Leytonstone	0330-0400	0	0
Leytonstone	0400-0430	0	0
Liverpool Street	0430-0500	0	0
Liverpool Street	0500-0530	79	1
Liverpool Street	0530-0600	357	1
Liverpool Street	0600-0630	948	1
Liverpool Street	0630-0700	1883	1
Liverpool Street	0700-0730	6042	1
Liverpool Street	0730-0800	8536	1
Liverpool Street	0800-0830	11943	1
Liverpool Street	0830-0900	14817	1
Liverpool Street	0900-0930	12083	1
Liverpool Street	0930-1000	7592	1
Liverpool Street	1000-1030	5166	1
Liverpool Street	1030-1100	4660	1
Liverpool Street	1100-1130	4155	1
Liverpool Street	1130-1200	4214	1
Liverpool Street	1200-1230	4527	1
Liverpool Street	1230-1300	4501	1
Liverpool Street	1300-1330	4668	1
Liverpool Street	1330-1400	4602	1
Liverpool Street	1400-1430	4682	1
Liverpool Street	1430-1500	4784	1
Liverpool Street	1500-1530	5392	1
Liverpool Street	1530-1600	6094	1
Liverpool Street	1600-1630	7687	1
Liverpool Street	1630-1700	9302	1
Liverpool Street	1700-1730	12873	1
Liverpool Street	1730-1800	15048	1
Liverpool Street	1800-1830	14450	1
Liverpool Street	1830-1900	10948	1
Liverpool Street	1900-1930	7571	1
Liverpool Street	1930-2000	5341	1
Liverpool Street	2000-2030	4350	1
Liverpool Street	2030-2100	3671	1
Liverpool Street	2100-2130	1938	1
Liverpool Street	2130-2200	1795	1
Liverpool Street	2200-2230	1767	1
Liverpool Street	2230-2300	1652	1
Liverpool Street	2300-2330	1520	1
Liverpool Street	2330-2400	1149	1
Liverpool Street	0000-0030	703	1
Liverpool Street	0030-0100	297	1
Liverpool Street	0100-0130	213	1
Liverpool Street	0130-0200	125	1
Liverpool Street	0200-0230	0	0
Liverpool Street	0230-0300	0	0
Liverpool Street	0300-0330	0	0
Liverpool Street	0330-0400	0	0
Liverpool Street	0400-0430	0	0
London Bridge	0430-0500	0	0
London Bridge	0500-0530	88	1
London Bridge	0530-0600	555	1
London Bridge	0600-0630	1311	1
London Bridge	0630-0700	3119	1
London Bridge	0700-0730	5492	1
London Bridge	0730-0800	8283	1
London Bridge	0800-0830	11449	1
London Bridge	0830-0900	14740	1
London Bridge	0900-0930	13173	1
London Bridge	0930-1000	8587	1
London Bridge	1000-1030	5660	1
London Bridge	1030-1100	4729	1
London Bridge	1100-1130	4189	1
London Bridge	1130-1200	4252	1
London Bridge	1200-1230	4529	1
London Bridge	1230-1300	4718	1
London Bridge	1300-1330	4757	1
London Bridge	1330-1400	4769	1
London Bridge	1400-1430	4578	1
London Bridge	1430-1500	4681	1
London Bridge	1500-1530	4963	1
London Bridge	1530-1600	5614	1
London Bridge	1600-1630	6903	1
London Bridge	1630-1700	8370	1
London Bridge	1700-1730	10863	1
London Bridge	1730-1800	12769	1
London Bridge	1800-1830	12129	1
London Bridge	1830-1900	9410	1
London Bridge	1900-1930	6664	1
London Bridge	1930-2000	4911	1
London Bridge	2000-2030	3877	1
London Bridge	2030-2100	3383	1
London Bridge	2100-2130	3025	1
London Bridge	2130-2200	2826	1
London Bridge	2200-2230	2928	1
London Bridge	2230-2300	2667	1
London Bridge	2300-2330	2387	1
London Bridge	2330-2400	1773	1
London Bridge	0000-0030	994	1
London Bridge	0030-0100	357	1
London Bridge	0100-0130	126	1
London Bridge	0130-0200	56	1
London Bridge	0200-0230	0	0
London Bridge	0230-0300	0	0
London Bridge	0300-0330	0	0
London Bridge	0330-0400	0	0
London Bridge	0400-0430	0	0
Loughton	0430-0500	0	0
Loughton	0500-0530	35	1
Loughton	0530-0600	97	1
Loughton	0600-0630	218	1
Loughton	0630-0700	344	1
Loughton	0700-0730	582	1
Loughton	0730-0800	879	1
Loughton	0800-0830	898	1
Loughton	0830-0900	606	1
Loughton	0900-0930	367	1
Loughton	0930-1000	265	1
Loughton	1000-1030	191	1
Loughton	1030-1100	177	1
Loughton	1100-1130	165	1
Loughton	1130-1200	156	1
Loughton	1200-1230	164	1
Loughton	1230-1300	167	1
Loughton	1300-1330	173	1
Loughton	1330-1400	170	1
Loughton	1400-1430	179	1
Loughton	1430-1500	203	1
Loughton	1500-1530	296	1
Loughton	1530-1600	276	1
Loughton	1600-1630	344	1
Loughton	1630-1700	406	1
Loughton	1700-1730	520	1
Loughton	1730-1800	625	1
Loughton	1800-1830	658	1
Loughton	1830-1900	548	1
Loughton	1900-1930	436	1
Loughton	1930-2000	287	1
Loughton	2000-2030	216	1
Loughton	2030-2100	161	1
Loughton	2100-2130	136	1
Loughton	2130-2200	127	1
Loughton	2200-2230	119	1
Loughton	2230-2300	127	1
Loughton	2300-2330	115	1
Loughton	2330-2400	91	1
Loughton	0000-0030	61	1
Loughton	0030-0100	37	1
Loughton	0100-0130	17	1
Loughton	0130-0200	8	1
Loughton	0200-0230	0	0
Loughton	0230-0300	0	0
Loughton	0300-0330	0	0
Loughton	0330-0400	0	0
Loughton	0400-0430	0	0
Maida Vale	0430-0500	0	0
Maida Vale	0500-0530	3	1
Maida Vale	0530-0600	20	1
Maida Vale	0600-0630	55	1
Maida Vale	0630-0700	124	1
Maida Vale	0700-0730	291	1
Maida Vale	0730-0800	534	1
Maida Vale	0800-0830	737	1
Maida Vale	0830-0900	676	1
Maida Vale	0900-0930	442	1
Maida Vale	0930-1000	284	1
Maida Vale	1000-1030	223	1
Maida Vale	1030-1100	199	1
Maida Vale	1100-1130	185	1
Maida Vale	1130-1200	188	1
Maida Vale	1200-1230	187	1
Maida Vale	1230-1300	190	1
Maida Vale	1300-1330	185	1
Maida Vale	1330-1400	193	1
Maida Vale	1400-1430	193	1
Maida Vale	1430-1500	194	1
Maida Vale	1500-1530	251	1
Maida Vale	1530-1600	273	1
Maida Vale	1600-1630	302	1
Maida Vale	1630-1700	347	1
Maida Vale	1700-1730	411	1
Maida Vale	1730-1800	420	1
Maida Vale	1800-1830	479	1
Maida Vale	1830-1900	485	1
Maida Vale	1900-1930	416	1
Maida Vale	1930-2000	336	1
Maida Vale	2000-2030	273	1
Maida Vale	2030-2100	212	1
Maida Vale	2100-2130	197	1
Maida Vale	2130-2200	170	1
Maida Vale	2200-2230	166	1
Maida Vale	2230-2300	151	1
Maida Vale	2300-2330	129	1
Maida Vale	2330-2400	99	1
Maida Vale	0000-0030	55	1
Maida Vale	0030-0100	23	1
Maida Vale	0100-0130	0	1
Maida Vale	0130-0200	0	1
Maida Vale	0200-0230	0	0
Maida Vale	0230-0300	0	0
Maida Vale	0300-0330	0	0
Maida Vale	0330-0400	0	0
Maida Vale	0400-0430	0	0
Manor House	0430-0500	0	0
Manor House	0500-0530	61	1
Manor House	0530-0600	173	1
Manor House	0600-0630	363	1
Manor House	0630-0700	581	1
Manor House	0700-0730	847	1
Manor House	0730-0800	1122	1
Manor House	0800-0830	1432	1
Manor House	0830-0900	1325	1
Manor House	0900-0930	1102	1
Manor House	0930-1000	744	1
Manor House	1000-1030	540	1
Manor House	1030-1100	479	1
Manor House	1100-1130	482	1
Manor House	1130-1200	426	1
Manor House	1200-1230	422	1
Manor House	1230-1300	430	1
Manor House	1300-1330	439	1
Manor House	1330-1400	449	1
Manor House	1400-1430	458	1
Manor House	1430-1500	503	1
Manor House	1500-1530	551	1
Manor House	1530-1600	593	1
Manor House	1600-1630	722	1
Manor House	1630-1700	857	1
Manor House	1700-1730	960	1
Manor House	1730-1800	1133	1
Manor House	1800-1830	1236	1
Manor House	1830-1900	1182	1
Manor House	1900-1930	989	1
Manor House	1930-2000	791	1
Manor House	2000-2030	655	1
Manor House	2030-2100	600	1
Manor House	2100-2130	542	1
Manor House	2130-2200	520	1
Manor House	2200-2230	509	1
Manor House	2230-2300	503	1
Manor House	2300-2330	451	1
Manor House	2330-2400	410	1
Manor House	0000-0030	297	1
Manor House	0030-0100	160	1
Manor House	0100-0130	42	1
Manor House	0130-0200	27	1
Manor House	0200-0230	0	0
Manor House	0230-0300	0	0
Manor House	0300-0330	0	0
Manor House	0330-0400	0	0
Manor House	0400-0430	0	0
Mansion House	0430-0500	0	0
Mansion House	0500-0530	8	1
Mansion House	0530-0600	42	1
Mansion House	0600-0630	110	1
Mansion House	0630-0700	331	1
Mansion House	0700-0730	600	1
Mansion House	0730-0800	1066	1
Mansion House	0800-0830	1672	1
Mansion House	0830-0900	2071	1
Mansion House	0900-0930	1581	1
Mansion House	0930-1000	766	1
Mansion House	1000-1030	466	1
Mansion House	1030-1100	404	1
Mansion House	1100-1130	365	1
Mansion House	1130-1200	400	1
Mansion House	1200-1230	466	1
Mansion House	1230-1300	457	1
Mansion House	1300-1330	431	1
Mansion House	1330-1400	439	1
Mansion House	1400-1430	421	1
Mansion House	1430-1500	437	1
Mansion House	1500-1530	450	1
Mansion House	1530-1600	515	1
Mansion House	1600-1630	667	1
Mansion House	1630-1700	772	1
Mansion House	1700-1730	1344	1
Mansion House	1730-1800	1593	1
Mansion House	1800-1830	1508	1
Mansion House	1830-1900	1094	1
Mansion House	1900-1930	727	1
Mansion House	1930-2000	464	1
Mansion House	2000-2030	328	1
Mansion House	2030-2100	267	1
Mansion House	2100-2130	233	1
Mansion House	2130-2200	200	1
Mansion House	2200-2230	174	1
Mansion House	2230-2300	148	1
Mansion House	2300-2330	144	1
Mansion House	2330-2400	103	1
Mansion House	0000-0030	41	1
Mansion House	0030-0100	9	1
Mansion House	0100-0130	0	1
Mansion House	0130-0200	0	1
Mansion House	0200-0230	0	0
Mansion House	0230-0300	0	0
Mansion House	0300-0330	0	0
Mansion House	0330-0400	0	0
Mansion House	0400-0430	0	0
Marble Arch	0430-0500	0	0
Marble Arch	0500-0530	6	1
Marble Arch	0530-0600	68	1
Marble Arch	0600-0630	255	1
Marble Arch	0630-0700	468	1
Marble Arch	0700-0730	768	1
Marble Arch	0730-0800	1214	1
Marble Arch	0800-0830	1372	1
Marble Arch	0830-0900	1723	1
Marble Arch	0900-0930	1528	1
Marble Arch	0930-1000	1129	1
Marble Arch	1000-1030	889	1
Marble Arch	1030-1100	868	1
Marble Arch	1100-1130	811	1
Marble Arch	1130-1200	885	1
Marble Arch	1200-1230	929	1
Marble Arch	1230-1300	968	1
Marble Arch	1300-1330	954	1
Marble Arch	1330-1400	1037	1
Marble Arch	1400-1430	1080	1
Marble Arch	1430-1500	1151	1
Marble Arch	1500-1530	1221	1
Marble Arch	1530-1600	1440	1
Marble Arch	1600-1630	1565	1
Marble Arch	1630-1700	1750	1
Marble Arch	1700-1730	2071	1
Marble Arch	1730-1800	2300	1
Marble Arch	1800-1830	2313	1
Marble Arch	1830-1900	1972	1
Marble Arch	1900-1930	1556	1
Marble Arch	1930-2000	1205	1
Marble Arch	2000-2030	1044	1
Marble Arch	2030-2100	913	1
Marble Arch	2100-2130	904	1
Marble Arch	2130-2200	921	1
Marble Arch	2200-2230	1118	1
Marble Arch	2230-2300	723	1
Marble Arch	2300-2330	512	1
Marble Arch	2330-2400	355	1
Marble Arch	0000-0030	204	1
Marble Arch	0030-0100	46	1
Marble Arch	0100-0130	18	1
Marble Arch	0130-0200	9	1
Marble Arch	0200-0230	0	0
Marble Arch	0230-0300	0	0
Marble Arch	0300-0330	0	0
Marble Arch	0330-0400	0	0
Marble Arch	0400-0430	0	0
Marylebone	0430-0500	0	0
Marylebone	0500-0530	0	1
Marylebone	0530-0600	34	1
Marylebone	0600-0630	233	1
Marylebone	0630-0700	537	1
Marylebone	0700-0730	1251	1
Marylebone	0730-0800	1817	1
Marylebone	0800-0830	2492	1
Marylebone	0830-0900	2598	1
Marylebone	0900-0930	2022	1
Marylebone	0930-1000	1356	1
Marylebone	1000-1030	1151	1
Marylebone	1030-1100	1010	1
Marylebone	1100-1130	863	1
Marylebone	1130-1200	844	1
Marylebone	1200-1230	864	1
Marylebone	1230-1300	823	1
Marylebone	1300-1330	812	1
Marylebone	1330-1400	813	1
Marylebone	1400-1430	795	1
Marylebone	1430-1500	849	1
Marylebone	1500-1530	992	1
Marylebone	1530-1600	1148	1
Marylebone	1600-1630	1487	1
Marylebone	1630-1700	1715	1
Marylebone	1700-1730	2189	1
Marylebone	1730-1800	2503	1
Marylebone	1800-1830	2400	1
Marylebone	1830-1900	1906	1
Marylebone	1900-1930	1367	1
Marylebone	1930-2000	1002	1
Marylebone	2000-2030	778	1
Marylebone	2030-2100	699	1
Marylebone	2100-2130	580	1
Marylebone	2130-2200	577	1
Marylebone	2200-2230	661	1
Marylebone	2230-2300	648	1
Marylebone	2300-2330	439	1
Marylebone	2330-2400	268	1
Marylebone	0000-0030	100	1
Marylebone	0030-0100	17	1
Marylebone	0100-0130	0	1
Marylebone	0130-0200	0	1
Marylebone	0200-0230	0	0
Marylebone	0230-0300	0	0
Marylebone	0300-0330	0	0
Marylebone	0330-0400	0	0
Marylebone	0400-0430	0	0
Mile End	0430-0500	0	0
Mile End	0500-0530	65	1
Mile End	0530-0600	191	1
Mile End	0600-0630	385	1
Mile End	0630-0700	637	1
Mile End	0700-0730	1089	1
Mile End	0730-0800	1662	1
Mile End	0800-0830	2324	1
Mile End	0830-0900	2770	1
Mile End	0900-0930	2114	1
Mile End	0930-1000	1634	1
Mile End	1000-1030	1148	1
Mile End	1030-1100	1199	1
Mile End	1100-1130	1054	1
Mile End	1130-1200	1046	1
Mile End	1200-1230	1057	1
Mile End	1230-1300	1096	1
Mile End	1300-1330	1159	1
Mile End	1330-1400	1113	1
Mile End	1400-1430	1152	1
Mile End	1430-1500	1134	1
Mile End	1500-1530	1276	1
Mile End	1530-1600	1389	1
Mile End	1600-1630	1698	1
Mile End	1630-1700	1798	1
Mile End	1700-1730	2171	1
Mile End	1730-1800	2159	1
Mile End	1800-1830	2255	1
Mile End	1830-1900	1974	1
Mile End	1900-1930	1615	1
Mile End	1930-2000	1294	1
Mile End	2000-2030	1097	1
Mile End	2030-2100	957	1
Mile End	2100-2130	864	1
Mile End	2130-2200	812	1
Mile End	2200-2230	763	1
Mile End	2230-2300	723	1
Mile End	2300-2330	656	1
Mile End	2330-2400	548	1
Mile End	0000-0030	382	1
Mile End	0030-0100	219	1
Mile End	0100-0130	105	1
Mile End	0130-0200	48	1
Mile End	0200-0230	0	0
Mile End	0230-0300	0	0
Mile End	0300-0330	0	0
Mile End	0330-0400	0	0
Mile End	0400-0430	0	0
Mill Hill East	0430-0500	0	0
Mill Hill East	0500-0530	1	1
Mill Hill East	0530-0600	11	1
Mill Hill East	0600-0630	37	1
Mill Hill East	0630-0700	138	1
Mill Hill East	0700-0730	269	1
Mill Hill East	0730-0800	494	1
Mill Hill East	0800-0830	364	1
Mill Hill East	0830-0900	239	1
Mill Hill East	0900-0930	147	1
Mill Hill East	0930-1000	77	1
Mill Hill East	1000-1030	62	1
Mill Hill East	1030-1100	74	1
Mill Hill East	1100-1130	61	1
Mill Hill East	1130-1200	53	1
Mill Hill East	1200-1230	68	1
Mill Hill East	1230-1300	74	1
Mill Hill East	1300-1330	77	1
Mill Hill East	1330-1400	51	1
Mill Hill East	1400-1430	66	1
Mill Hill East	1430-1500	57	1
Mill Hill East	1500-1530	94	1
Mill Hill East	1530-1600	201	1
Mill Hill East	1600-1630	192	1
Mill Hill East	1630-1700	228	1
Mill Hill East	1700-1730	224	1
Mill Hill East	1730-1800	183	1
Mill Hill East	1800-1830	213	1
Mill Hill East	1830-1900	204	1
Mill Hill East	1900-1930	63	1
Mill Hill East	1930-2000	99	1
Mill Hill East	2000-2030	78	1
Mill Hill East	2030-2100	72	1
Mill Hill East	2100-2130	52	1
Mill Hill East	2130-2200	34	1
Mill Hill East	2200-2230	36	1
Mill Hill East	2230-2300	51	1
Mill Hill East	2300-2330	40	1
Mill Hill East	2330-2400	31	1
Mill Hill East	0000-0030	29	1
Mill Hill East	0030-0100	6	1
Mill Hill East	0100-0130	1	1
Mill Hill East	0130-0200	0	1
Mill Hill East	0200-0230	0	0
Mill Hill East	0230-0300	0	0
Mill Hill East	0300-0330	0	0
Mill Hill East	0330-0400	0	0
Mill Hill East	0400-0430	0	0
Moor Park	0430-0500	0	0
Moor Park	0500-0530	5	1
Moor Park	0530-0600	16	1
Moor Park	0600-0630	35	1
Moor Park	0630-0700	84	1
Moor Park	0700-0730	150	1
Moor Park	0730-0800	345	1
Moor Park	0800-0830	391	1
Moor Park	0830-0900	157	1
Moor Park	0900-0930	75	1
Moor Park	0930-1000	49	1
Moor Park	1000-1030	35	1
Moor Park	1030-1100	33	1
Moor Park	1100-1130	34	1
Moor Park	1130-1200	33	1
Moor Park	1200-1230	32	1
Moor Park	1230-1300	34	1
Moor Park	1300-1330	38	1
Moor Park	1330-1400	42	1
Moor Park	1400-1430	41	1
Moor Park	1430-1500	42	1
Moor Park	1500-1530	64	1
Moor Park	1530-1600	189	1
Moor Park	1600-1630	160	1
Moor Park	1630-1700	158	1
Moor Park	1700-1730	167	1
Moor Park	1730-1800	161	1
Moor Park	1800-1830	156	1
Moor Park	1830-1900	126	1
Moor Park	1900-1930	101	1
Moor Park	1930-2000	70	1
Moor Park	2000-2030	50	1
Moor Park	2030-2100	37	1
Moor Park	2100-2130	30	1
Moor Park	2130-2200	27	1
Moor Park	2200-2230	26	1
Moor Park	2230-2300	28	1
Moor Park	2300-2330	23	1
Moor Park	2330-2400	15	1
Moor Park	0000-0030	10	1
Moor Park	0030-0100	5	1
Moor Park	0100-0130	1	1
Moor Park	0130-0200	0	1
Moor Park	0200-0230	0	0
Moor Park	0230-0300	0	0
Moor Park	0300-0330	0	0
Moor Park	0330-0400	0	0
Moor Park	0400-0430	0	0
Moorgate	0430-0500	4	1
Moorgate	0500-0530	106	1
Moorgate	0530-0600	313	1
Moorgate	0600-0630	711	1
Moorgate	0630-0700	1664	1
Moorgate	0700-0730	2915	1
Moorgate	0730-0800	5345	1
Moorgate	0800-0830	7619	1
Moorgate	0830-0900	9419	1
Moorgate	0900-0930	7422	1
Moorgate	0930-1000	3883	1
Moorgate	1000-1030	2082	1
Moorgate	1030-1100	1652	1
Moorgate	1100-1130	1410	1
Moorgate	1130-1200	1522	1
Moorgate	1200-1230	1626	1
Moorgate	1230-1300	1598	1
Moorgate	1300-1330	1584	1
Moorgate	1330-1400	1548	1
Moorgate	1400-1430	1530	1
Moorgate	1430-1500	1549	1
Moorgate	1500-1530	1634	1
Moorgate	1530-1600	1938	1
Moorgate	1600-1630	2725	1
Moorgate	1630-1700	3576	1
Moorgate	1700-1730	6110	1
Moorgate	1730-1800	7308	1
Moorgate	1800-1830	6647	1
Moorgate	1830-1900	4724	1
Moorgate	1900-1930	3034	1
Moorgate	1930-2000	1817	1
Moorgate	2000-2030	1345	1
Moorgate	2030-2100	1054	1
Moorgate	2100-2130	909	1
Moorgate	2130-2200	831	1
Moorgate	2200-2230	685	1
Moorgate	2230-2300	566	1
Moorgate	2300-2330	483	1
Moorgate	2330-2400	339	1
Moorgate	0000-0030	174	1
Moorgate	0030-0100	40	1
Moorgate	0100-0130	0	1
Moorgate	0130-0200	1	1
Moorgate	0200-0230	0	0
Moorgate	0230-0300	0	0
Moorgate	0300-0330	0	0
Moorgate	0330-0400	0	0
Moorgate	0400-0430	0	0
Morden	0430-0500	0	0
Morden	0500-0530	224	1
Morden	0530-0600	330	1
Morden	0600-0630	698	1
Morden	0630-0700	1242	1
Morden	0700-0730	1720	1
Morden	0730-0800	2106	1
Morden	0800-0830	2231	1
Morden	0830-0900	1674	1
Morden	0900-0930	1118	1
Morden	0930-1000	718	1
Morden	1000-1030	547	1
Morden	1030-1100	466	1
Morden	1100-1130	463	1
Morden	1130-1200	462	1
Morden	1200-1230	462	1
Morden	1230-1300	496	1
Morden	1300-1330	496	1
Morden	1330-1400	499	1
Morden	1400-1430	521	1
Morden	1430-1500	557	1
Morden	1500-1530	598	1
Morden	1530-1600	739	1
Morden	1600-1630	939	1
Morden	1630-1700	1216	1
Morden	1700-1730	1440	1
Morden	1730-1800	1624	1
Morden	1800-1830	1647	1
Morden	1830-1900	1434	1
Morden	1900-1930	1085	1
Morden	1930-2000	783	1
Morden	2000-2030	597	1
Morden	2030-2100	528	1
Morden	2100-2130	463	1
Morden	2130-2200	414	1
Morden	2200-2230	390	1
Morden	2230-2300	414	1
Morden	2300-2330	413	1
Morden	2330-2400	364	1
Morden	0000-0030	270	1
Morden	0030-0100	159	1
Morden	0100-0130	74	1
Morden	0130-0200	23	1
Morden	0200-0230	0	0
Morden	0230-0300	0	0
Morden	0300-0330	0	0
Morden	0330-0400	0	0
Morden	0400-0430	0	0
Mornington Crescent	0430-0500	0	0
Mornington Crescent	0500-0530	0	1
Mornington Crescent	0530-0600	18	1
Mornington Crescent	0600-0630	53	1
Mornington Crescent	0630-0700	147	1
Mornington Crescent	0700-0730	272	1
Mornington Crescent	0730-0800	423	1
Mornington Crescent	0800-0830	717	1
Mornington Crescent	0830-0900	1226	1
Mornington Crescent	0900-0930	1028	1
Mornington Crescent	0930-1000	574	1
Mornington Crescent	1000-1030	320	1
Mornington Crescent	1030-1100	244	1
Mornington Crescent	1100-1130	215	1
Mornington Crescent	1130-1200	212	1
Mornington Crescent	1200-1230	235	1
Mornington Crescent	1230-1300	261	1
Mornington Crescent	1300-1330	264	1
Mornington Crescent	1330-1400	246	1
Mornington Crescent	1400-1430	245	1
Mornington Crescent	1430-1500	255	1
Mornington Crescent	1500-1530	283	1
Mornington Crescent	1530-1600	340	1
Mornington Crescent	1600-1630	443	1
Mornington Crescent	1630-1700	553	1
Mornington Crescent	1700-1730	850	1
Mornington Crescent	1730-1800	1198	1
Mornington Crescent	1800-1830	945	1
Mornington Crescent	1830-1900	649	1
Mornington Crescent	1900-1930	496	1
Mornington Crescent	1930-2000	361	1
Mornington Crescent	2000-2030	272	1
Mornington Crescent	2030-2100	233	1
Mornington Crescent	2100-2130	218	1
Mornington Crescent	2130-2200	225	1
Mornington Crescent	2200-2230	275	1
Mornington Crescent	2230-2300	298	1
Mornington Crescent	2300-2330	247	1
Mornington Crescent	2330-2400	149	1
Mornington Crescent	0000-0030	94	1
Mornington Crescent	0030-0100	42	1
Mornington Crescent	0100-0130	22	1
Mornington Crescent	0130-0200	13	1
Mornington Crescent	0200-0230	0	0
Mornington Crescent	0230-0300	0	0
Mornington Crescent	0300-0330	0	0
Mornington Crescent	0330-0400	0	0
Mornington Crescent	0400-0430	0	0
Neasden	0430-0500	0	0
Neasden	0500-0530	39	1
Neasden	0530-0600	119	1
Neasden	0600-0630	277	1
Neasden	0630-0700	501	1
Neasden	0700-0730	590	1
Neasden	0730-0800	655	1
Neasden	0800-0830	727	1
Neasden	0830-0900	602	1
Neasden	0900-0930	427	1
Neasden	0930-1000	280	1
Neasden	1000-1030	231	1
Neasden	1030-1100	196	1
Neasden	1100-1130	197	1
Neasden	1130-1200	174	1
Neasden	1200-1230	181	1
Neasden	1230-1300	192	1
Neasden	1300-1330	198	1
Neasden	1330-1400	198	1
Neasden	1400-1430	209	1
Neasden	1430-1500	238	1
Neasden	1500-1530	271	1
Neasden	1530-1600	331	1
Neasden	1600-1630	410	1
Neasden	1630-1700	516	1
Neasden	1700-1730	584	1
Neasden	1730-1800	663	1
Neasden	1800-1830	630	1
Neasden	1830-1900	510	1
Neasden	1900-1930	352	1
Neasden	1930-2000	257	1
Neasden	2000-2030	207	1
Neasden	2030-2100	172	1
Neasden	2100-2130	147	1
Neasden	2130-2200	133	1
Neasden	2200-2230	141	1
Neasden	2230-2300	132	1
Neasden	2300-2330	110	1
Neasden	2330-2400	98	1
Neasden	0000-0030	76	1
Neasden	0030-0100	47	1
Neasden	0100-0130	11	1
Neasden	0130-0200	5	1
Neasden	0200-0230	0	0
Neasden	0230-0300	0	0
Neasden	0300-0330	0	0
Neasden	0330-0400	0	0
Neasden	0400-0430	0	0
Newbury Park	0430-0500	0	0
Newbury Park	0500-0530	120	1
Newbury Park	0530-0600	309	1
Newbury Park	0600-0630	638	1
Newbury Park	0630-0700	835	1
Newbury Park	0700-0730	837	1
Newbury Park	0730-0800	1060	1
Newbury Park	0800-0830	1250	1
Newbury Park	0830-0900	845	1
Newbury Park	0900-0930	547	1
Newbury Park	0930-1000	368	1
Newbury Park	1000-1030	293	1
Newbury Park	1030-1100	248	1
Newbury Park	1100-1130	236	1
Newbury Park	1130-1200	216	1
Newbury Park	1200-1230	232	1
Newbury Park	1230-1300	237	1
Newbury Park	1300-1330	234	1
Newbury Park	1330-1400	241	1
Newbury Park	1400-1430	253	1
Newbury Park	1430-1500	277	1
Newbury Park	1500-1530	335	1
Newbury Park	1530-1600	426	1
Newbury Park	1600-1630	476	1
Newbury Park	1630-1700	627	1
Newbury Park	1700-1730	750	1
Newbury Park	1730-1800	863	1
Newbury Park	1800-1830	903	1
Newbury Park	1830-1900	793	1
Newbury Park	1900-1930	627	1
Newbury Park	1930-2000	438	1
Newbury Park	2000-2030	317	1
Newbury Park	2030-2100	284	1
Newbury Park	2100-2130	256	1
Newbury Park	2130-2200	222	1
Newbury Park	2200-2230	193	1
Newbury Park	2230-2300	176	1
Newbury Park	2300-2330	175	1
Newbury Park	2330-2400	154	1
Newbury Park	0000-0030	99	1
Newbury Park	0030-0100	54	1
Newbury Park	0100-0130	16	1
Newbury Park	0130-0200	17	1
Newbury Park	0200-0230	0	0
Newbury Park	0230-0300	0	0
Newbury Park	0300-0330	0	0
Newbury Park	0330-0400	0	0
Newbury Park	0400-0430	0	0
North Acton	0430-0500	0	0
North Acton	0500-0530	24	1
North Acton	0530-0600	105	1
North Acton	0600-0630	297	1
North Acton	0630-0700	550	1
North Acton	0700-0730	716	1
North Acton	0730-0800	1038	1
North Acton	0800-0830	1527	1
North Acton	0830-0900	1607	1
North Acton	0900-0930	1220	1
North Acton	0930-1000	655	1
North Acton	1000-1030	472	1
North Acton	1030-1100	370	1
North Acton	1100-1130	338	1
North Acton	1130-1200	315	1
North Acton	1200-1230	324	1
North Acton	1230-1300	340	1
North Acton	1300-1330	371	1
North Acton	1330-1400	360	1
North Acton	1400-1430	369	1
North Acton	1430-1500	370	1
North Acton	1500-1530	416	1
North Acton	1530-1600	483	1
North Acton	1600-1630	674	1
North Acton	1630-1700	837	1
North Acton	1700-1730	1160	1
North Acton	1730-1800	1309	1
North Acton	1800-1830	1222	1
North Acton	1830-1900	946	1
North Acton	1900-1930	710	1
North Acton	1930-2000	540	1
North Acton	2000-2030	450	1
North Acton	2030-2100	356	1
North Acton	2100-2130	314	1
North Acton	2130-2200	286	1
North Acton	2200-2230	270	1
North Acton	2230-2300	244	1
North Acton	2300-2330	208	1
North Acton	2330-2400	187	1
North Acton	0000-0030	124	1
North Acton	0030-0100	68	1
North Acton	0100-0130	27	1
North Acton	0130-0200	14	1
North Acton	0200-0230	0	0
North Acton	0230-0300	0	0
North Acton	0300-0330	0	0
North Acton	0330-0400	0	0
North Acton	0400-0430	0	0
North Ealing	0430-0500	0	0
North Ealing	0500-0530	2	1
North Ealing	0530-0600	10	1
North Ealing	0600-0630	18	1
North Ealing	0630-0700	42	1
North Ealing	0700-0730	80	1
North Ealing	0730-0800	147	1
North Ealing	0800-0830	231	1
North Ealing	0830-0900	186	1
North Ealing	0900-0930	92	1
North Ealing	0930-1000	62	1
North Ealing	1000-1030	49	1
North Ealing	1030-1100	42	1
North Ealing	1100-1130	37	1
North Ealing	1130-1200	38	1
North Ealing	1200-1230	39	1
North Ealing	1230-1300	40	1
North Ealing	1300-1330	50	1
North Ealing	1330-1400	40	1
North Ealing	1400-1430	42	1
North Ealing	1430-1500	42	1
North Ealing	1500-1530	120	1
North Ealing	1530-1600	201	1
North Ealing	1600-1630	82	1
North Ealing	1630-1700	90	1
North Ealing	1700-1730	91	1
North Ealing	1730-1800	109	1
North Ealing	1800-1830	118	1
North Ealing	1830-1900	101	1
North Ealing	1900-1930	78	1
North Ealing	1930-2000	58	1
North Ealing	2000-2030	46	1
North Ealing	2030-2100	40	1
North Ealing	2100-2130	36	1
North Ealing	2130-2200	30	1
North Ealing	2200-2230	31	1
North Ealing	2230-2300	34	1
North Ealing	2300-2330	35	1
North Ealing	2330-2400	23	1
North Ealing	0000-0030	15	1
North Ealing	0030-0100	6	1
North Ealing	0100-0130	1	1
North Ealing	0130-0200	0	1
North Ealing	0200-0230	0	0
North Ealing	0230-0300	0	0
North Ealing	0300-0330	0	0
North Ealing	0330-0400	0	0
North Ealing	0400-0430	0	0
North Greenwich	0430-0500	0	0
North Greenwich	0500-0530	299	1
North Greenwich	0530-0600	635	1
North Greenwich	0600-0630	1167	1
North Greenwich	0630-0700	1938	1
North Greenwich	0700-0730	2783	1
North Greenwich	0730-0800	3126	1
North Greenwich	0800-0830	3622	1
North Greenwich	0830-0900	3561	1
North Greenwich	0900-0930	2827	1
North Greenwich	0930-1000	2195	1
North Greenwich	1000-1030	1538	1
North Greenwich	1030-1100	1403	1
North Greenwich	1100-1130	1492	1
North Greenwich	1130-1200	1429	1
North Greenwich	1200-1230	1334	1
North Greenwich	1230-1300	1311	1
North Greenwich	1300-1330	1318	1
North Greenwich	1330-1400	1343	1
North Greenwich	1400-1430	1318	1
North Greenwich	1430-1500	1409	1
North Greenwich	1500-1530	1568	1
North Greenwich	1530-1600	2097	1
North Greenwich	1600-1630	2834	1
North Greenwich	1630-1700	3355	1
North Greenwich	1700-1730	3877	1
North Greenwich	1730-1800	4405	1
North Greenwich	1800-1830	4504	1
North Greenwich	1830-1900	3906	1
North Greenwich	1900-1930	3012	1
North Greenwich	1930-2000	2273	1
North Greenwich	2000-2030	1739	1
North Greenwich	2030-2100	1419	1
North Greenwich	2100-2130	1344	1
North Greenwich	2130-2200	1406	1
North Greenwich	2200-2230	1660	1
North Greenwich	2230-2300	2426	1
North Greenwich	2300-2330	2486	1
North Greenwich	2330-2400	1445	1
North Greenwich	0000-0030	671	1
North Greenwich	0030-0100	313	1
North Greenwich	0100-0130	121	1
North Greenwich	0130-0200	47	1
North Greenwich	0200-0230	0	0
North Greenwich	0230-0300	0	0
North Greenwich	0300-0330	0	0
North Greenwich	0330-0400	0	0
North Greenwich	0400-0430	0	0
North Harrow	0430-0500	0	0
North Harrow	0500-0530	6	1
North Harrow	0530-0600	62	1
North Harrow	0600-0630	132	1
North Harrow	0630-0700	175	1
North Harrow	0700-0730	294	1
North Harrow	0730-0800	525	1
North Harrow	0800-0830	530	1
North Harrow	0830-0900	341	1
North Harrow	0900-0930	200	1
North Harrow	0930-1000	122	1
North Harrow	1000-1030	96	1
North Harrow	1030-1100	85	1
North Harrow	1100-1130	79	1
North Harrow	1130-1200	79	1
North Harrow	1200-1230	80	1
North Harrow	1230-1300	85	1
North Harrow	1300-1330	90	1
North Harrow	1330-1400	89	1
North Harrow	1400-1430	90	1
North Harrow	1430-1500	100	1
North Harrow	1500-1530	110	1
North Harrow	1530-1600	163	1
North Harrow	1600-1630	220	1
North Harrow	1630-1700	244	1
North Harrow	1700-1730	277	1
North Harrow	1730-1800	333	1
North Harrow	1800-1830	367	1
North Harrow	1830-1900	349	1
North Harrow	1900-1930	263	1
North Harrow	1930-2000	172	1
North Harrow	2000-2030	122	1
North Harrow	2030-2100	95	1
North Harrow	2100-2130	75	1
North Harrow	2130-2200	70	1
North Harrow	2200-2230	69	1
North Harrow	2230-2300	91	1
North Harrow	2300-2330	67	1
North Harrow	2330-2400	53	1
North Harrow	0000-0030	33	1
North Harrow	0030-0100	15	1
North Harrow	0100-0130	2	1
North Harrow	0130-0200	0	1
North Harrow	0200-0230	0	0
North Harrow	0230-0300	0	0
North Harrow	0300-0330	0	0
North Harrow	0330-0400	0	0
North Harrow	0400-0430	0	0
North Wembley	0430-0500	0	0
North Wembley	0500-0530	21	1
North Wembley	0530-0600	72	1
North Wembley	0600-0630	135	1
North Wembley	0630-0700	210	1
North Wembley	0700-0730	244	1
North Wembley	0730-0800	360	1
North Wembley	0800-0830	396	1
North Wembley	0830-0900	253	1
North Wembley	0900-0930	167	1
North Wembley	0930-1000	119	1
North Wembley	1000-1030	100	1
North Wembley	1030-1100	86	1
North Wembley	1100-1130	85	1
North Wembley	1130-1200	77	1
North Wembley	1200-1230	87	1
North Wembley	1230-1300	84	1
North Wembley	1300-1330	93	1
North Wembley	1330-1400	99	1
North Wembley	1400-1430	108	1
North Wembley	1430-1500	126	1
North Wembley	1500-1530	131	1
North Wembley	1530-1600	169	1
North Wembley	1600-1630	197	1
North Wembley	1630-1700	201	1
North Wembley	1700-1730	276	1
North Wembley	1730-1800	271	1
North Wembley	1800-1830	281	1
North Wembley	1830-1900	232	1
North Wembley	1900-1930	214	1
North Wembley	1930-2000	142	1
North Wembley	2000-2030	110	1
North Wembley	2030-2100	84	1
North Wembley	2100-2130	74	1
North Wembley	2130-2200	66	1
North Wembley	2200-2230	67	1
North Wembley	2230-2300	54	1
North Wembley	2300-2330	47	1
North Wembley	2330-2400	39	1
North Wembley	0000-0030	27	1
North Wembley	0030-0100	6	1
North Wembley	0100-0130	0	1
North Wembley	0130-0200	0	1
North Wembley	0200-0230	0	0
North Wembley	0230-0300	0	0
North Wembley	0300-0330	0	0
North Wembley	0330-0400	0	0
North Wembley	0400-0430	0	0
Northfields	0430-0500	0	0
Northfields	0500-0530	47	1
Northfields	0530-0600	74	1
Northfields	0600-0630	159	1
Northfields	0630-0700	335	1
Northfields	0700-0730	565	1
Northfields	0730-0800	811	1
Northfields	0800-0830	953	1
Northfields	0830-0900	716	1
Northfields	0900-0930	454	1
Northfields	0930-1000	268	1
Northfields	1000-1030	212	1
Northfields	1030-1100	195	1
Northfields	1100-1130	176	1
Northfields	1130-1200	167	1
Northfields	1200-1230	159	1
Northfields	1230-1300	164	1
Northfields	1300-1330	176	1
Northfields	1330-1400	179	1
Northfields	1400-1430	193	1
Northfields	1430-1500	199	1
Northfields	1500-1530	232	1
Northfields	1530-1600	370	1
Northfields	1600-1630	393	1
Northfields	1630-1700	466	1
Northfields	1700-1730	586	1
Northfields	1730-1800	645	1
Northfields	1800-1830	641	1
Northfields	1830-1900	585	1
Northfields	1900-1930	465	1
Northfields	1930-2000	335	1
Northfields	2000-2030	244	1
Northfields	2030-2100	202	1
Northfields	2100-2130	185	1
Northfields	2130-2200	187	1
Northfields	2200-2230	184	1
Northfields	2230-2300	187	1
Northfields	2300-2330	175	1
Northfields	2330-2400	143	1
Northfields	0000-0030	103	1
Northfields	0030-0100	60	1
Northfields	0100-0130	21	1
Northfields	0130-0200	8	1
Northfields	0200-0230	0	0
Northfields	0230-0300	0	0
Northfields	0300-0330	0	0
Northfields	0330-0400	0	0
Northfields	0400-0430	0	0
Northolt	0430-0500	0	0
Northolt	0500-0530	101	1
Northolt	0530-0600	246	1
Northolt	0600-0630	490	1
Northolt	0630-0700	723	1
Northolt	0700-0730	796	1
Northolt	0730-0800	934	1
Northolt	0800-0830	995	1
Northolt	0830-0900	667	1
Northolt	0900-0930	493	1
Northolt	0930-1000	370	1
Northolt	1000-1030	287	1
Northolt	1030-1100	251	1
Northolt	1100-1130	242	1
Northolt	1130-1200	221	1
Northolt	1200-1230	236	1
Northolt	1230-1300	242	1
Northolt	1300-1330	265	1
Northolt	1330-1400	263	1
Northolt	1400-1430	287	1
Northolt	1430-1500	289	1
Northolt	1500-1530	342	1
Northolt	1530-1600	423	1
Northolt	1600-1630	526	1
Northolt	1630-1700	597	1
Northolt	1700-1730	765	1
Northolt	1730-1800	841	1
Northolt	1800-1830	856	1
Northolt	1830-1900	750	1
Northolt	1900-1930	615	1
Northolt	1930-2000	438	1
Northolt	2000-2030	331	1
Northolt	2030-2100	282	1
Northolt	2100-2130	232	1
Northolt	2130-2200	226	1
Northolt	2200-2230	205	1
Northolt	2230-2300	182	1
Northolt	2300-2330	159	1
Northolt	2330-2400	138	1
Northolt	0000-0030	96	1
Northolt	0030-0100	49	1
Northolt	0100-0130	20	1
Northolt	0130-0200	0	1
Northolt	0200-0230	0	0
Northolt	0230-0300	0	0
Northolt	0300-0330	0	0
Northolt	0330-0400	0	0
Northolt	0400-0430	0	0
Northwick Park	0430-0500	0	0
Northwick Park	0500-0530	20	1
Northwick Park	0530-0600	111	1
Northwick Park	0600-0630	301	1
Northwick Park	0630-0700	411	1
Northwick Park	0700-0730	542	1
Northwick Park	0730-0800	740	1
Northwick Park	0800-0830	949	1
Northwick Park	0830-0900	822	1
Northwick Park	0900-0930	547	1
Northwick Park	0930-1000	450	1
Northwick Park	1000-1030	379	1
Northwick Park	1030-1100	336	1
Northwick Park	1100-1130	301	1
Northwick Park	1130-1200	244	1
Northwick Park	1200-1230	256	1
Northwick Park	1230-1300	299	1
Northwick Park	1300-1330	342	1
Northwick Park	1330-1400	338	1
Northwick Park	1400-1430	312	1
Northwick Park	1430-1500	313	1
Northwick Park	1500-1530	341	1
Northwick Park	1530-1600	422	1
Northwick Park	1600-1630	551	1
Northwick Park	1630-1700	657	1
Northwick Park	1700-1730	805	1
Northwick Park	1730-1800	751	1
Northwick Park	1800-1830	739	1
Northwick Park	1830-1900	653	1
Northwick Park	1900-1930	470	1
Northwick Park	1930-2000	340	1
Northwick Park	2000-2030	284	1
Northwick Park	2030-2100	241	1
Northwick Park	2100-2130	197	1
Northwick Park	2130-2200	172	1
Northwick Park	2200-2230	147	1
Northwick Park	2230-2300	130	1
Northwick Park	2300-2330	105	1
Northwick Park	2330-2400	94	1
Northwick Park	0000-0030	75	1
Northwick Park	0030-0100	38	1
Northwick Park	0100-0130	7	1
Northwick Park	0130-0200	0	1
Northwick Park	0200-0230	0	0
Northwick Park	0230-0300	0	0
Northwick Park	0300-0330	0	0
Northwick Park	0330-0400	0	0
Northwick Park	0400-0430	0	0
Northwood	0430-0500	0	0
Northwood	0500-0530	8	1
Northwood	0530-0600	54	1
Northwood	0600-0630	135	1
Northwood	0630-0700	240	1
Northwood	0700-0730	436	1
Northwood	0730-0800	852	1
Northwood	0800-0830	1066	1
Northwood	0830-0900	582	1
Northwood	0900-0930	317	1
Northwood	0930-1000	248	1
Northwood	1000-1030	184	1
Northwood	1030-1100	166	1
Northwood	1100-1130	159	1
Northwood	1130-1200	151	1
Northwood	1200-1230	142	1
Northwood	1230-1300	140	1
Northwood	1300-1330	142	1
Northwood	1330-1400	139	1
Northwood	1400-1430	148	1
Northwood	1430-1500	167	1
Northwood	1500-1530	209	1
Northwood	1530-1600	372	1
Northwood	1600-1630	523	1
Northwood	1630-1700	367	1
Northwood	1700-1730	407	1
Northwood	1730-1800	447	1
Northwood	1800-1830	468	1
Northwood	1830-1900	443	1
Northwood	1900-1930	341	1
Northwood	1930-2000	245	1
Northwood	2000-2030	185	1
Northwood	2030-2100	124	1
Northwood	2100-2130	114	1
Northwood	2130-2200	108	1
Northwood	2200-2230	102	1
Northwood	2230-2300	100	1
Northwood	2300-2330	91	1
Northwood	2330-2400	62	1
Northwood	0000-0030	43	1
Northwood	0030-0100	23	1
Northwood	0100-0130	6	1
Northwood	0130-0200	0	1
Northwood	0200-0230	0	0
Northwood	0230-0300	0	0
Northwood	0300-0330	0	0
Northwood	0330-0400	0	0
Northwood	0400-0430	0	0
Northwood Hills	0430-0500	0	0
Northwood Hills	0500-0530	8	1
Northwood Hills	0530-0600	60	1
Northwood Hills	0600-0630	132	1
Northwood Hills	0630-0700	202	1
Northwood Hills	0700-0730	285	1
Northwood Hills	0730-0800	533	1
Northwood Hills	0800-0830	565	1
Northwood Hills	0830-0900	325	1
Northwood Hills	0900-0930	194	1
Northwood Hills	0930-1000	130	1
Northwood Hills	1000-1030	109	1
Northwood Hills	1030-1100	107	1
Northwood Hills	1100-1130	100	1
Northwood Hills	1130-1200	93	1
Northwood Hills	1200-1230	89	1
Northwood Hills	1230-1300	99	1
Northwood Hills	1300-1330	114	1
Northwood Hills	1330-1400	111	1
Northwood Hills	1400-1430	109	1
Northwood Hills	1430-1500	141	1
Northwood Hills	1500-1530	185	1
Northwood Hills	1530-1600	227	1
Northwood Hills	1600-1630	237	1
Northwood Hills	1630-1700	264	1
Northwood Hills	1700-1730	288	1
Northwood Hills	1730-1800	289	1
Northwood Hills	1800-1830	322	1
Northwood Hills	1830-1900	298	1
Northwood Hills	1900-1930	226	1
Northwood Hills	1930-2000	168	1
Northwood Hills	2000-2030	127	1
Northwood Hills	2030-2100	92	1
Northwood Hills	2100-2130	82	1
Northwood Hills	2130-2200	73	1
Northwood Hills	2200-2230	67	1
Northwood Hills	2230-2300	70	1
Northwood Hills	2300-2330	61	1
Northwood Hills	2330-2400	46	1
Northwood Hills	0000-0030	35	1
Northwood Hills	0030-0100	20	1
Northwood Hills	0100-0130	2	1
Northwood Hills	0130-0200	0	1
Northwood Hills	0200-0230	0	0
Northwood Hills	0230-0300	0	0
Northwood Hills	0300-0330	0	0
Northwood Hills	0330-0400	0	0
Northwood Hills	0400-0430	0	0
Notting Hill Gate	0430-0500	0	0
Notting Hill Gate	0500-0530	20	1
Notting Hill Gate	0530-0600	84	1
Notting Hill Gate	0600-0630	263	1
Notting Hill Gate	0630-0700	588	1
Notting Hill Gate	0700-0730	1348	1
Notting Hill Gate	0730-0800	2053	1
Notting Hill Gate	0800-0830	2154	1
Notting Hill Gate	0830-0900	2428	1
Notting Hill Gate	0900-0930	2008	1
Notting Hill Gate	0930-1000	1564	1
Notting Hill Gate	1000-1030	1137	1
Notting Hill Gate	1030-1100	1058	1
Notting Hill Gate	1100-1130	1011	1
Notting Hill Gate	1130-1200	1011	1
Notting Hill Gate	1200-1230	1049	1
Notting Hill Gate	1230-1300	1075	1
Notting Hill Gate	1300-1330	1086	1
Notting Hill Gate	1330-1400	1066	1
Notting Hill Gate	1400-1430	1081	1
Notting Hill Gate	1430-1500	1133	1
Notting Hill Gate	1500-1530	1230	1
Notting Hill Gate	1530-1600	1353	1
Notting Hill Gate	1600-1630	1526	1
Notting Hill Gate	1630-1700	1770	1
Notting Hill Gate	1700-1730	2102	1
Notting Hill Gate	1730-1800	2274	1
Notting Hill Gate	1800-1830	2532	1
Notting Hill Gate	1830-1900	2186	1
Notting Hill Gate	1900-1930	1706	1
Notting Hill Gate	1930-2000	1275	1
Notting Hill Gate	2000-2030	1011	1
Notting Hill Gate	2030-2100	835	1
Notting Hill Gate	2100-2130	758	1
Notting Hill Gate	2130-2200	686	1
Notting Hill Gate	2200-2230	617	1
Notting Hill Gate	2230-2300	592	1
Notting Hill Gate	2300-2330	564	1
Notting Hill Gate	2330-2400	477	1
Notting Hill Gate	0000-0030	287	1
Notting Hill Gate	0030-0100	122	1
Notting Hill Gate	0100-0130	46	1
Notting Hill Gate	0130-0200	22	1
Notting Hill Gate	0200-0230	0	0
Notting Hill Gate	0230-0300	0	0
Notting Hill Gate	0300-0330	0	0
Notting Hill Gate	0330-0400	0	0
Notting Hill Gate	0400-0430	0	0
Oakwood	0430-0500	0	0
Oakwood	0500-0530	43	1
Oakwood	0530-0600	55	1
Oakwood	0600-0630	112	1
Oakwood	0630-0700	199	1
Oakwood	0700-0730	321	1
Oakwood	0730-0800	468	1
Oakwood	0800-0830	539	1
Oakwood	0830-0900	411	1
Oakwood	0900-0930	331	1
Oakwood	0930-1000	273	1
Oakwood	1000-1030	208	1
Oakwood	1030-1100	185	1
Oakwood	1100-1130	167	1
Oakwood	1130-1200	153	1
Oakwood	1200-1230	151	1
Oakwood	1230-1300	157	1
Oakwood	1300-1330	158	1
Oakwood	1330-1400	162	1
Oakwood	1400-1430	160	1
Oakwood	1430-1500	190	1
Oakwood	1500-1530	247	1
Oakwood	1530-1600	260	1
Oakwood	1600-1630	290	1
Oakwood	1630-1700	303	1
Oakwood	1700-1730	340	1
Oakwood	1730-1800	354	1
Oakwood	1800-1830	393	1
Oakwood	1830-1900	373	1
Oakwood	1900-1930	301	1
Oakwood	1930-2000	234	1
Oakwood	2000-2030	176	1
Oakwood	2030-2100	145	1
Oakwood	2100-2130	133	1
Oakwood	2130-2200	118	1
Oakwood	2200-2230	135	1
Oakwood	2230-2300	136	1
Oakwood	2300-2330	118	1
Oakwood	2330-2400	100	1
Oakwood	0000-0030	70	1
Oakwood	0030-0100	43	1
Oakwood	0100-0130	20	1
Oakwood	0130-0200	6	1
Oakwood	0200-0230	0	0
Oakwood	0230-0300	0	0
Oakwood	0300-0330	0	0
Oakwood	0330-0400	0	0
Oakwood	0400-0430	0	0
Old Street	0430-0500	0	0
Old Street	0500-0530	0	1
Old Street	0530-0600	92	1
Old Street	0600-0630	287	1
Old Street	0630-0700	863	1
Old Street	0700-0730	1670	1
Old Street	0730-0800	2442	1
Old Street	0800-0830	3336	1
Old Street	0830-0900	4765	1
Old Street	0900-0930	4799	1
Old Street	0930-1000	3638	1
Old Street	1000-1030	2314	1
Old Street	1030-1100	1820	1
Old Street	1100-1130	1527	1
Old Street	1130-1200	1542	1
Old Street	1200-1230	1633	1
Old Street	1230-1300	1712	1
Old Street	1300-1330	1758	1
Old Street	1330-1400	1744	1
Old Street	1400-1430	1645	1
Old Street	1430-1500	1675	1
Old Street	1500-1530	1798	1
Old Street	1530-1600	2056	1
Old Street	1600-1630	2545	1
Old Street	1630-1700	3047	1
Old Street	1700-1730	4061	1
Old Street	1730-1800	4959	1
Old Street	1800-1830	5000	1
Old Street	1830-1900	4256	1
Old Street	1900-1930	3034	1
Old Street	1930-2000	2220	1
Old Street	2000-2030	1802	1
Old Street	2030-2100	1555	1
Old Street	2100-2130	1456	1
Old Street	2130-2200	1394	1
Old Street	2200-2230	1351	1
Old Street	2230-2300	1325	1
Old Street	2300-2330	1242	1
Old Street	2330-2400	984	1
Old Street	0000-0030	599	1
Old Street	0030-0100	132	1
Old Street	0100-0130	0	1
Old Street	0130-0200	0	1
Old Street	0200-0230	0	0
Old Street	0230-0300	0	0
Old Street	0300-0330	0	0
Old Street	0330-0400	0	0
Old Street	0400-0430	0	0
Osterley	0430-0500	0	0
Osterley	0500-0530	26	1
Osterley	0530-0600	66	1
Osterley	0600-0630	123	1
Osterley	0630-0700	186	1
Osterley	0700-0730	274	1
Osterley	0730-0800	430	1
Osterley	0800-0830	479	1
Osterley	0830-0900	393	1
Osterley	0900-0930	264	1
Osterley	0930-1000	168	1
Osterley	1000-1030	123	1
Osterley	1030-1100	107	1
Osterley	1100-1130	99	1
Osterley	1130-1200	91	1
Osterley	1200-1230	90	1
Osterley	1230-1300	99	1
Osterley	1300-1330	104	1
Osterley	1330-1400	103	1
Osterley	1400-1430	104	1
Osterley	1430-1500	110	1
Osterley	1500-1530	125	1
Osterley	1530-1600	148	1
Osterley	1600-1630	190	1
Osterley	1630-1700	239	1
Osterley	1700-1730	297	1
Osterley	1730-1800	358	1
Osterley	1800-1830	385	1
Osterley	1830-1900	341	1
Osterley	1900-1930	274	1
Osterley	1930-2000	194	1
Osterley	2000-2030	145	1
Osterley	2030-2100	121	1
Osterley	2100-2130	108	1
Osterley	2130-2200	96	1
Osterley	2200-2230	87	1
Osterley	2230-2300	94	1
Osterley	2300-2330	82	1
Osterley	2330-2400	55	1
Osterley	0000-0030	39	1
Osterley	0030-0100	26	1
Osterley	0100-0130	14	1
Osterley	0130-0200	3	1
Osterley	0200-0230	0	0
Osterley	0230-0300	0	0
Osterley	0300-0330	0	0
Osterley	0330-0400	0	0
Osterley	0400-0430	0	0
Oval	0430-0500	0	0
Oval	0500-0530	20	1
Oval	0530-0600	83	1
Oval	0600-0630	210	1
Oval	0630-0700	375	1
Oval	0700-0730	589	1
Oval	0730-0800	897	1
Oval	0800-0830	1184	1
Oval	0830-0900	1428	1
Oval	0900-0930	1277	1
Oval	0930-1000	807	1
Oval	1000-1030	518	1
Oval	1030-1100	413	1
Oval	1100-1130	374	1
Oval	1130-1200	362	1
Oval	1200-1230	383	1
Oval	1230-1300	414	1
Oval	1300-1330	458	1
Oval	1330-1400	443	1
Oval	1400-1430	417	1
Oval	1430-1500	428	1
Oval	1500-1530	476	1
Oval	1530-1600	538	1
Oval	1600-1630	647	1
Oval	1630-1700	739	1
Oval	1700-1730	992	1
Oval	1730-1800	1288	1
Oval	1800-1830	1277	1
Oval	1830-1900	1095	1
Oval	1900-1930	867	1
Oval	1930-2000	658	1
Oval	2000-2030	506	1
Oval	2030-2100	459	1
Oval	2100-2130	429	1
Oval	2130-2200	406	1
Oval	2200-2230	398	1
Oval	2230-2300	389	1
Oval	2300-2330	344	1
Oval	2330-2400	279	1
Oval	0000-0030	182	1
Oval	0030-0100	87	1
Oval	0100-0130	25	1
Oval	0130-0200	20	1
Oval	0200-0230	0	0
Oval	0230-0300	0	0
Oval	0300-0330	0	0
Oval	0330-0400	0	0
Oval	0400-0430	0	0
Oxford Circus	0430-0500	0	0
Oxford Circus	0500-0530	35	1
Oxford Circus	0530-0600	462	1
Oxford Circus	0600-0630	860	1
Oxford Circus	0630-0700	1976	1
Oxford Circus	0700-0730	2840	1
Oxford Circus	0730-0800	5073	1
Oxford Circus	0800-0830	7884	1
Oxford Circus	0830-0900	12459	1
Oxford Circus	0900-0930	13336	1
Oxford Circus	0930-1000	9845	1
Oxford Circus	1000-1030	6828	1
Oxford Circus	1030-1100	6335	1
Oxford Circus	1100-1130	5806	1
Oxford Circus	1130-1200	6142	1
Oxford Circus	1200-1230	6574	1
Oxford Circus	1230-1300	7107	1
Oxford Circus	1300-1330	7277	1
Oxford Circus	1330-1400	7262	1
Oxford Circus	1400-1430	7042	1
Oxford Circus	1430-1500	7233	1
Oxford Circus	1500-1530	7559	1
Oxford Circus	1530-1600	8333	1
Oxford Circus	1600-1630	9238	1
Oxford Circus	1630-1700	9804	1
Oxford Circus	1700-1730	11652	1
Oxford Circus	1730-1800	13102	1
Oxford Circus	1800-1830	13704	1
Oxford Circus	1830-1900	12058	1
Oxford Circus	1900-1930	9625	1
Oxford Circus	1930-2000	7172	1
Oxford Circus	2000-2030	6281	1
Oxford Circus	2030-2100	5259	1
Oxford Circus	2100-2130	4694	1
Oxford Circus	2130-2200	3846	1
Oxford Circus	2200-2230	3804	1
Oxford Circus	2230-2300	3152	1
Oxford Circus	2300-2330	2597	1
Oxford Circus	2330-2400	1801	1
Oxford Circus	0000-0030	1081	1
Oxford Circus	0030-0100	362	1
Oxford Circus	0100-0130	175	1
Oxford Circus	0130-0200	94	1
Oxford Circus	0200-0230	0	0
Oxford Circus	0230-0300	0	0
Oxford Circus	0300-0330	0	0
Oxford Circus	0330-0400	0	0
Oxford Circus	0400-0430	0	0
Paddington	0430-0500	0	0
Paddington	0500-0530	40	1
Paddington	0530-0600	250	1
Paddington	0600-0630	975	1
Paddington	0630-0700	2383	1
Paddington	0700-0730	4254	1
Paddington	0730-0800	6419	1
Paddington	0800-0830	8310	1
Paddington	0830-0900	9042	1
Paddington	0900-0930	7658	1
Paddington	0930-1000	5409	1
Paddington	1000-1030	4306	1
Paddington	1030-1100	3889	1
Paddington	1100-1130	3441	1
Paddington	1130-1200	3320	1
Paddington	1200-1230	3329	1
Paddington	1230-1300	3520	1
Paddington	1300-1330	3268	1
Paddington	1330-1400	3430	1
Paddington	1400-1430	3420	1
Paddington	1430-1500	3616	1
Paddington	1500-1530	3934	1
Paddington	1530-1600	4526	1
Paddington	1600-1630	5183	1
Paddington	1630-1700	6078	1
Paddington	1700-1730	7541	1
Paddington	1730-1800	8728	1
Paddington	1800-1830	8311	1
Paddington	1830-1900	6924	1
Paddington	1900-1930	4815	1
Paddington	1930-2000	3604	1
Paddington	2000-2030	2764	1
Paddington	2030-2100	2259	1
Paddington	2100-2130	2002	1
Paddington	2130-2200	1781	1
Paddington	2200-2230	1730	1
Paddington	2230-2300	1693	1
Paddington	2300-2330	1362	1
Paddington	2330-2400	977	1
Paddington	0000-0030	466	1
Paddington	0030-0100	115	1
Paddington	0100-0130	4	1
Paddington	0130-0200	3	1
Paddington	0200-0230	0	0
Paddington	0230-0300	0	0
Paddington	0300-0330	0	0
Paddington	0330-0400	0	0
Paddington	0400-0430	0	0
Park Royal	0430-0500	0	0
Park Royal	0500-0530	12	1
Park Royal	0530-0600	31	1
Park Royal	0600-0630	86	1
Park Royal	0630-0700	146	1
Park Royal	0700-0730	228	1
Park Royal	0730-0800	331	1
Park Royal	0800-0830	424	1
Park Royal	0830-0900	437	1
Park Royal	0900-0930	277	1
Park Royal	0930-1000	177	1
Park Royal	1000-1030	131	1
Park Royal	1030-1100	110	1
Park Royal	1100-1130	97	1
Park Royal	1130-1200	103	1
Park Royal	1200-1230	98	1
Park Royal	1230-1300	92	1
Park Royal	1300-1330	108	1
Park Royal	1330-1400	105	1
Park Royal	1400-1430	116	1
Park Royal	1430-1500	116	1
Park Royal	1500-1530	138	1
Park Royal	1530-1600	178	1
Park Royal	1600-1630	219	1
Park Royal	1630-1700	272	1
Park Royal	1700-1730	401	1
Park Royal	1730-1800	410	1
Park Royal	1800-1830	356	1
Park Royal	1830-1900	261	1
Park Royal	1900-1930	203	1
Park Royal	1930-2000	139	1
Park Royal	2000-2030	103	1
Park Royal	2030-2100	102	1
Park Royal	2100-2130	84	1
Park Royal	2130-2200	73	1
Park Royal	2200-2230	75	1
Park Royal	2230-2300	65	1
Park Royal	2300-2330	63	1
Park Royal	2330-2400	47	1
Park Royal	0000-0030	29	1
Park Royal	0030-0100	14	1
Park Royal	0100-0130	5	1
Park Royal	0130-0200	0	1
Park Royal	0200-0230	0	0
Park Royal	0230-0300	0	0
Park Royal	0300-0330	0	0
Park Royal	0330-0400	0	0
Park Royal	0400-0430	0	0
Parsons Green	0430-0500	0	0
Parsons Green	0500-0530	12	1
Parsons Green	0530-0600	42	1
Parsons Green	0600-0630	135	1
Parsons Green	0630-0700	322	1
Parsons Green	0700-0730	808	1
Parsons Green	0730-0800	1584	1
Parsons Green	0800-0830	1911	1
Parsons Green	0830-0900	1579	1
Parsons Green	0900-0930	992	1
Parsons Green	0930-1000	622	1
Parsons Green	1000-1030	440	1
Parsons Green	1030-1100	353	1
Parsons Green	1100-1130	338	1
Parsons Green	1130-1200	336	1
Parsons Green	1200-1230	365	1
Parsons Green	1230-1300	379	1
Parsons Green	1300-1330	373	1
Parsons Green	1330-1400	372	1
Parsons Green	1400-1430	354	1
Parsons Green	1430-1500	372	1
Parsons Green	1500-1530	473	1
Parsons Green	1530-1600	613	1
Parsons Green	1600-1630	610	1
Parsons Green	1630-1700	784	1
Parsons Green	1700-1730	965	1
Parsons Green	1730-1800	1083	1
Parsons Green	1800-1830	1226	1
Parsons Green	1830-1900	1127	1
Parsons Green	1900-1930	880	1
Parsons Green	1930-2000	614	1
Parsons Green	2000-2030	426	1
Parsons Green	2030-2100	331	1
Parsons Green	2100-2130	277	1
Parsons Green	2130-2200	276	1
Parsons Green	2200-2230	274	1
Parsons Green	2230-2300	248	1
Parsons Green	2300-2330	200	1
Parsons Green	2330-2400	140	1
Parsons Green	0000-0030	83	1
Parsons Green	0030-0100	34	1
Parsons Green	0100-0130	6	1
Parsons Green	0130-0200	0	1
Parsons Green	0200-0230	0	0
Parsons Green	0230-0300	0	0
Parsons Green	0300-0330	0	0
Parsons Green	0330-0400	0	0
Parsons Green	0400-0430	0	0
Perivale	0430-0500	0	0
Perivale	0500-0530	16	1
Perivale	0530-0600	69	1
Perivale	0600-0630	183	1
Perivale	0630-0700	314	1
Perivale	0700-0730	394	1
Perivale	0730-0800	497	1
Perivale	0800-0830	509	1
Perivale	0830-0900	426	1
Perivale	0900-0930	322	1
Perivale	0930-1000	230	1
Perivale	1000-1030	152	1
Perivale	1030-1100	122	1
Perivale	1100-1130	116	1
Perivale	1130-1200	108	1
Perivale	1200-1230	108	1
Perivale	1230-1300	116	1
Perivale	1300-1330	126	1
Perivale	1330-1400	137	1
Perivale	1400-1430	144	1
Perivale	1430-1500	153	1
Perivale	1500-1530	161	1
Perivale	1530-1600	203	1
Perivale	1600-1630	250	1
Perivale	1630-1700	303	1
Perivale	1700-1730	445	1
Perivale	1730-1800	474	1
Perivale	1800-1830	463	1
Perivale	1830-1900	356	1
Perivale	1900-1930	259	1
Perivale	1930-2000	183	1
Perivale	2000-2030	141	1
Perivale	2030-2100	125	1
Perivale	2100-2130	107	1
Perivale	2130-2200	101	1
Perivale	2200-2230	84	1
Perivale	2230-2300	71	1
Perivale	2300-2330	66	1
Perivale	2330-2400	51	1
Perivale	0000-0030	38	1
Perivale	0030-0100	22	1
Perivale	0100-0130	4	1
Perivale	0130-0200	0	1
Perivale	0200-0230	0	0
Perivale	0230-0300	0	0
Perivale	0300-0330	0	0
Perivale	0330-0400	0	0
Perivale	0400-0430	0	0
Piccadilly Circus	0430-0500	0	0
Piccadilly Circus	0500-0530	9	1
Piccadilly Circus	0530-0600	111	1
Piccadilly Circus	0600-0630	272	1
Piccadilly Circus	0630-0700	629	1
Piccadilly Circus	0700-0730	988	1
Piccadilly Circus	0730-0800	1638	1
Piccadilly Circus	0800-0830	2318	1
Piccadilly Circus	0830-0900	3888	1
Piccadilly Circus	0900-0930	4165	1
Piccadilly Circus	0930-1000	3033	1
Piccadilly Circus	1000-1030	2171	1
Piccadilly Circus	1030-1100	2178	1
Piccadilly Circus	1100-1130	2106	1
Piccadilly Circus	1130-1200	2361	1
Piccadilly Circus	1200-1230	2578	1
Piccadilly Circus	1230-1300	2802	1
Piccadilly Circus	1300-1330	2804	1
Piccadilly Circus	1330-1400	2814	1
Piccadilly Circus	1400-1430	2891	1
Piccadilly Circus	1430-1500	3067	1
Piccadilly Circus	1500-1530	3165	1
Piccadilly Circus	1530-1600	3492	1
Piccadilly Circus	1600-1630	3763	1
Piccadilly Circus	1630-1700	4302	1
Piccadilly Circus	1700-1730	5336	1
Piccadilly Circus	1730-1800	6731	1
Piccadilly Circus	1800-1830	7196	1
Piccadilly Circus	1830-1900	6382	1
Piccadilly Circus	1900-1930	4886	1
Piccadilly Circus	1930-2000	3550	1
Piccadilly Circus	2000-2030	3128	1
Piccadilly Circus	2030-2100	2868	1
Piccadilly Circus	2100-2130	2819	1
Piccadilly Circus	2130-2200	2990	1
Piccadilly Circus	2200-2230	3820	1
Piccadilly Circus	2230-2300	3285	1
Piccadilly Circus	2300-2330	2334	1
Piccadilly Circus	2330-2400	1839	1
Piccadilly Circus	0000-0030	1027	1
Piccadilly Circus	0030-0100	267	1
Piccadilly Circus	0100-0130	146	1
Piccadilly Circus	0130-0200	76	1
Piccadilly Circus	0200-0230	0	0
Piccadilly Circus	0230-0300	0	0
Piccadilly Circus	0300-0330	0	0
Piccadilly Circus	0330-0400	0	0
Piccadilly Circus	0400-0430	0	0
Pimlico	0430-0500	0	0
Pimlico	0500-0530	17	1
Pimlico	0530-0600	72	1
Pimlico	0600-0630	171	1
Pimlico	0630-0700	354	1
Pimlico	0700-0730	687	1
Pimlico	0730-0800	1395	1
Pimlico	0800-0830	2117	1
Pimlico	0830-0900	2329	1
Pimlico	0900-0930	1956	1
Pimlico	0930-1000	1443	1
Pimlico	1000-1030	972	1
Pimlico	1030-1100	806	1
Pimlico	1100-1130	695	1
Pimlico	1130-1200	681	1
Pimlico	1200-1230	706	1
Pimlico	1230-1300	749	1
Pimlico	1300-1330	752	1
Pimlico	1330-1400	772	1
Pimlico	1400-1430	757	1
Pimlico	1430-1500	780	1
Pimlico	1500-1530	903	1
Pimlico	1530-1600	1082	1
Pimlico	1600-1630	1318	1
Pimlico	1630-1700	1459	1
Pimlico	1700-1730	1693	1
Pimlico	1730-1800	1873	1
Pimlico	1800-1830	1729	1
Pimlico	1830-1900	1335	1
Pimlico	1900-1930	1037	1
Pimlico	1930-2000	798	1
Pimlico	2000-2030	655	1
Pimlico	2030-2100	558	1
Pimlico	2100-2130	509	1
Pimlico	2130-2200	460	1
Pimlico	2200-2230	433	1
Pimlico	2230-2300	417	1
Pimlico	2300-2330	326	1
Pimlico	2330-2400	243	1
Pimlico	0000-0030	137	1
Pimlico	0030-0100	52	1
Pimlico	0100-0130	20	1
Pimlico	0130-0200	14	1
Pimlico	0200-0230	0	0
Pimlico	0230-0300	0	0
Pimlico	0300-0330	0	0
Pimlico	0330-0400	0	0
Pimlico	0400-0430	0	0
Pinner	0430-0500	0	0
Pinner	0500-0530	8	1
Pinner	0530-0600	58	1
Pinner	0600-0630	129	1
Pinner	0630-0700	277	1
Pinner	0700-0730	633	1
Pinner	0730-0800	1117	1
Pinner	0800-0830	945	1
Pinner	0830-0900	586	1
Pinner	0900-0930	317	1
Pinner	0930-1000	207	1
Pinner	1000-1030	158	1
Pinner	1030-1100	141	1
Pinner	1100-1130	145	1
Pinner	1130-1200	142	1
Pinner	1200-1230	146	1
Pinner	1230-1300	143	1
Pinner	1300-1330	141	1
Pinner	1330-1400	145	1
Pinner	1400-1430	157	1
Pinner	1430-1500	164	1
Pinner	1500-1530	182	1
Pinner	1530-1600	311	1
Pinner	1600-1630	417	1
Pinner	1630-1700	408	1
Pinner	1700-1730	442	1
Pinner	1730-1800	596	1
Pinner	1800-1830	671	1
Pinner	1830-1900	648	1
Pinner	1900-1930	554	1
Pinner	1930-2000	336	1
Pinner	2000-2030	232	1
Pinner	2030-2100	144	1
Pinner	2100-2130	116	1
Pinner	2130-2200	122	1
Pinner	2200-2230	117	1
Pinner	2230-2300	124	1
Pinner	2300-2330	149	1
Pinner	2330-2400	106	1
Pinner	0000-0030	51	1
Pinner	0030-0100	23	1
Pinner	0100-0130	3	1
Pinner	0130-0200	0	1
Pinner	0200-0230	0	0
Pinner	0230-0300	0	0
Pinner	0300-0330	0	0
Pinner	0330-0400	0	0
Pinner	0400-0430	0	0
Plaistow	0430-0500	0	0
Plaistow	0500-0530	126	1
Plaistow	0530-0600	246	1
Plaistow	0600-0630	506	1
Plaistow	0630-0700	716	1
Plaistow	0700-0730	806	1
Plaistow	0730-0800	871	1
Plaistow	0800-0830	1043	1
Plaistow	0830-0900	942	1
Plaistow	0900-0930	707	1
Plaistow	0930-1000	508	1
Plaistow	1000-1030	390	1
Plaistow	1030-1100	325	1
Plaistow	1100-1130	330	1
Plaistow	1130-1200	308	1
Plaistow	1200-1230	312	1
Plaistow	1230-1300	319	1
Plaistow	1300-1330	326	1
Plaistow	1330-1400	325	1
Plaistow	1400-1430	342	1
Plaistow	1430-1500	402	1
Plaistow	1500-1530	469	1
Plaistow	1530-1600	550	1
Plaistow	1600-1630	633	1
Plaistow	1630-1700	777	1
Plaistow	1700-1730	877	1
Plaistow	1730-1800	954	1
Plaistow	1800-1830	918	1
Plaistow	1830-1900	817	1
Plaistow	1900-1930	615	1
Plaistow	1930-2000	482	1
Plaistow	2000-2030	400	1
Plaistow	2030-2100	342	1
Plaistow	2100-2130	302	1
Plaistow	2130-2200	262	1
Plaistow	2200-2230	233	1
Plaistow	2230-2300	236	1
Plaistow	2300-2330	215	1
Plaistow	2330-2400	189	1
Plaistow	0000-0030	138	1
Plaistow	0030-0100	79	1
Plaistow	0100-0130	21	1
Plaistow	0130-0200	0	1
Plaistow	0200-0230	0	0
Plaistow	0230-0300	0	0
Plaistow	0300-0330	0	0
Plaistow	0330-0400	0	0
Plaistow	0400-0430	0	0
Preston Road	0430-0500	0	0
Preston Road	0500-0530	26	1
Preston Road	0530-0600	112	1
Preston Road	0600-0630	312	1
Preston Road	0630-0700	412	1
Preston Road	0700-0730	473	1
Preston Road	0730-0800	702	1
Preston Road	0800-0830	894	1
Preston Road	0830-0900	694	1
Preston Road	0900-0930	429	1
Preston Road	0930-1000	305	1
Preston Road	1000-1030	239	1
Preston Road	1030-1100	201	1
Preston Road	1100-1130	186	1
Preston Road	1130-1200	176	1
Preston Road	1200-1230	179	1
Preston Road	1230-1300	182	1
Preston Road	1300-1330	187	1
Preston Road	1330-1400	191	1
Preston Road	1400-1430	187	1
Preston Road	1430-1500	224	1
Preston Road	1500-1530	248	1
Preston Road	1530-1600	302	1
Preston Road	1600-1630	340	1
Preston Road	1630-1700	425	1
Preston Road	1700-1730	470	1
Preston Road	1730-1800	562	1
Preston Road	1800-1830	601	1
Preston Road	1830-1900	575	1
Preston Road	1900-1930	392	1
Preston Road	1930-2000	295	1
Preston Road	2000-2030	214	1
Preston Road	2030-2100	173	1
Preston Road	2100-2130	142	1
Preston Road	2130-2200	125	1
Preston Road	2200-2230	125	1
Preston Road	2230-2300	118	1
Preston Road	2300-2330	94	1
Preston Road	2330-2400	90	1
Preston Road	0000-0030	72	1
Preston Road	0030-0100	36	1
Preston Road	0100-0130	4	1
Preston Road	0130-0200	0	1
Preston Road	0200-0230	0	0
Preston Road	0230-0300	0	0
Preston Road	0300-0330	0	0
Preston Road	0330-0400	0	0
Preston Road	0400-0430	0	0
Putney Bridge	0430-0500	0	0
Putney Bridge	0500-0530	14	1
Putney Bridge	0530-0600	32	1
Putney Bridge	0600-0630	101	1
Putney Bridge	0630-0700	257	1
Putney Bridge	0700-0730	562	1
Putney Bridge	0730-0800	916	1
Putney Bridge	0800-0830	998	1
Putney Bridge	0830-0900	1010	1
Putney Bridge	0900-0930	751	1
Putney Bridge	0930-1000	451	1
Putney Bridge	1000-1030	332	1
Putney Bridge	1030-1100	293	1
Putney Bridge	1100-1130	291	1
Putney Bridge	1130-1200	302	1
Putney Bridge	1200-1230	318	1
Putney Bridge	1230-1300	314	1
Putney Bridge	1300-1330	304	1
Putney Bridge	1330-1400	313	1
Putney Bridge	1400-1430	317	1
Putney Bridge	1430-1500	329	1
Putney Bridge	1500-1530	372	1
Putney Bridge	1530-1600	419	1
Putney Bridge	1600-1630	509	1
Putney Bridge	1630-1700	632	1
Putney Bridge	1700-1730	818	1
Putney Bridge	1730-1800	1000	1
Putney Bridge	1800-1830	970	1
Putney Bridge	1830-1900	824	1
Putney Bridge	1900-1930	622	1
Putney Bridge	1930-2000	435	1
Putney Bridge	2000-2030	330	1
Putney Bridge	2030-2100	270	1
Putney Bridge	2100-2130	238	1
Putney Bridge	2130-2200	250	1
Putney Bridge	2200-2230	242	1
Putney Bridge	2230-2300	233	1
Putney Bridge	2300-2330	216	1
Putney Bridge	2330-2400	153	1
Putney Bridge	0000-0030	88	1
Putney Bridge	0030-0100	35	1
Putney Bridge	0100-0130	7	1
Putney Bridge	0130-0200	0	1
Putney Bridge	0200-0230	0	0
Putney Bridge	0230-0300	0	0
Putney Bridge	0300-0330	0	0
Putney Bridge	0330-0400	0	0
Putney Bridge	0400-0430	0	0
Queen's Park	0430-0500	0	0
Queen's Park	0500-0530	25	1
Queen's Park	0530-0600	80	1
Queen's Park	0600-0630	149	1
Queen's Park	0630-0700	281	1
Queen's Park	0700-0730	514	1
Queen's Park	0730-0800	901	1
Queen's Park	0800-0830	1223	1
Queen's Park	0830-0900	1154	1
Queen's Park	0900-0930	835	1
Queen's Park	0930-1000	552	1
Queen's Park	1000-1030	394	1
Queen's Park	1030-1100	326	1
Queen's Park	1100-1130	313	1
Queen's Park	1130-1200	314	1
Queen's Park	1200-1230	313	1
Queen's Park	1230-1300	308	1
Queen's Park	1300-1330	323	1
Queen's Park	1330-1400	321	1
Queen's Park	1400-1430	336	1
Queen's Park	1430-1500	347	1
Queen's Park	1500-1530	380	1
Queen's Park	1530-1600	404	1
Queen's Park	1600-1630	490	1
Queen's Park	1630-1700	571	1
Queen's Park	1700-1730	680	1
Queen's Park	1730-1800	820	1
Queen's Park	1800-1830	942	1
Queen's Park	1830-1900	836	1
Queen's Park	1900-1930	673	1
Queen's Park	1930-2000	500	1
Queen's Park	2000-2030	418	1
Queen's Park	2030-2100	343	1
Queen's Park	2100-2130	320	1
Queen's Park	2130-2200	287	1
Queen's Park	2200-2230	277	1
Queen's Park	2230-2300	275	1
Queen's Park	2300-2330	227	1
Queen's Park	2330-2400	188	1
Queen's Park	0000-0030	126	1
Queen's Park	0030-0100	66	1
Queen's Park	0100-0130	0	1
Queen's Park	0130-0200	0	1
Queen's Park	0200-0230	0	0
Queen's Park	0230-0300	0	0
Queen's Park	0300-0330	0	0
Queen's Park	0330-0400	0	0
Queen's Park	0400-0430	0	0
Queensbury	0430-0500	0	0
Queensbury	0500-0530	70	1
Queensbury	0530-0600	276	1
Queensbury	0600-0630	851	1
Queensbury	0630-0700	1014	1
Queensbury	0700-0730	737	1
Queensbury	0730-0800	769	1
Queensbury	0800-0830	829	1
Queensbury	0830-0900	578	1
Queensbury	0900-0930	357	1
Queensbury	0930-1000	243	1
Queensbury	1000-1030	183	1
Queensbury	1030-1100	168	1
Queensbury	1100-1130	161	1
Queensbury	1130-1200	166	1
Queensbury	1200-1230	167	1
Queensbury	1230-1300	170	1
Queensbury	1300-1330	170	1
Queensbury	1330-1400	173	1
Queensbury	1400-1430	193	1
Queensbury	1430-1500	215	1
Queensbury	1500-1530	245	1
Queensbury	1530-1600	296	1
Queensbury	1600-1630	396	1
Queensbury	1630-1700	530	1
Queensbury	1700-1730	719	1
Queensbury	1730-1800	867	1
Queensbury	1800-1830	988	1
Queensbury	1830-1900	948	1
Queensbury	1900-1930	627	1
Queensbury	1930-2000	379	1
Queensbury	2000-2030	270	1
Queensbury	2030-2100	212	1
Queensbury	2100-2130	181	1
Queensbury	2130-2200	164	1
Queensbury	2200-2230	151	1
Queensbury	2230-2300	141	1
Queensbury	2300-2330	109	1
Queensbury	2330-2400	83	1
Queensbury	0000-0030	55	1
Queensbury	0030-0100	35	1
Queensbury	0100-0130	13	1
Queensbury	0130-0200	7	1
Queensbury	0200-0230	0	0
Queensbury	0230-0300	0	0
Queensbury	0300-0330	0	0
Queensbury	0330-0400	0	0
Queensbury	0400-0430	0	0
Queensway	0430-0500	0	0
Queensway	0500-0530	6	1
Queensway	0530-0600	37	1
Queensway	0600-0630	140	1
Queensway	0630-0700	267	1
Queensway	0700-0730	450	1
Queensway	0730-0800	633	1
Queensway	0800-0830	849	1
Queensway	0830-0900	1059	1
Queensway	0900-0930	917	1
Queensway	0930-1000	841	1
Queensway	1000-1030	719	1
Queensway	1030-1100	664	1
Queensway	1100-1130	559	1
Queensway	1130-1200	545	1
Queensway	1200-1230	535	1
Queensway	1230-1300	525	1
Queensway	1300-1330	556	1
Queensway	1330-1400	583	1
Queensway	1400-1430	599	1
Queensway	1430-1500	633	1
Queensway	1500-1530	670	1
Queensway	1530-1600	720	1
Queensway	1600-1630	800	1
Queensway	1630-1700	861	1
Queensway	1700-1730	944	1
Queensway	1730-1800	1016	1
Queensway	1800-1830	1073	1
Queensway	1830-1900	1022	1
Queensway	1900-1930	847	1
Queensway	1930-2000	707	1
Queensway	2000-2030	601	1
Queensway	2030-2100	537	1
Queensway	2100-2130	508	1
Queensway	2130-2200	476	1
Queensway	2200-2230	487	1
Queensway	2230-2300	545	1
Queensway	2300-2330	496	1
Queensway	2330-2400	368	1
Queensway	0000-0030	208	1
Queensway	0030-0100	80	1
Queensway	0100-0130	29	1
Queensway	0130-0200	14	1
Queensway	0200-0230	0	0
Queensway	0230-0300	0	0
Queensway	0300-0330	0	0
Queensway	0330-0400	0	0
Queensway	0400-0430	0	0
Ravenscourt Park	0430-0500	0	0
Ravenscourt Park	0500-0530	6	1
Ravenscourt Park	0530-0600	20	1
Ravenscourt Park	0600-0630	52	1
Ravenscourt Park	0630-0700	102	1
Ravenscourt Park	0700-0730	220	1
Ravenscourt Park	0730-0800	547	1
Ravenscourt Park	0800-0830	900	1
Ravenscourt Park	0830-0900	666	1
Ravenscourt Park	0900-0930	490	1
Ravenscourt Park	0930-1000	350	1
Ravenscourt Park	1000-1030	245	1
Ravenscourt Park	1030-1100	172	1
Ravenscourt Park	1100-1130	178	1
Ravenscourt Park	1130-1200	161	1
Ravenscourt Park	1200-1230	154	1
Ravenscourt Park	1230-1300	166	1
Ravenscourt Park	1300-1330	171	1
Ravenscourt Park	1330-1400	169	1
Ravenscourt Park	1400-1430	171	1
Ravenscourt Park	1430-1500	188	1
Ravenscourt Park	1500-1530	229	1
Ravenscourt Park	1530-1600	393	1
Ravenscourt Park	1600-1630	626	1
Ravenscourt Park	1630-1700	443	1
Ravenscourt Park	1700-1730	494	1
Ravenscourt Park	1730-1800	537	1
Ravenscourt Park	1800-1830	532	1
Ravenscourt Park	1830-1900	417	1
Ravenscourt Park	1900-1930	323	1
Ravenscourt Park	1930-2000	221	1
Ravenscourt Park	2000-2030	173	1
Ravenscourt Park	2030-2100	156	1
Ravenscourt Park	2100-2130	148	1
Ravenscourt Park	2130-2200	143	1
Ravenscourt Park	2200-2230	131	1
Ravenscourt Park	2230-2300	125	1
Ravenscourt Park	2300-2330	107	1
Ravenscourt Park	2330-2400	77	1
Ravenscourt Park	0000-0030	42	1
Ravenscourt Park	0030-0100	20	1
Ravenscourt Park	0100-0130	3	1
Ravenscourt Park	0130-0200	0	1
Ravenscourt Park	0200-0230	0	0
Ravenscourt Park	0230-0300	0	0
Ravenscourt Park	0300-0330	0	0
Ravenscourt Park	0330-0400	0	0
Ravenscourt Park	0400-0430	0	0
Rayners Lane	0430-0500	0	0
Rayners Lane	0500-0530	45	1
Rayners Lane	0530-0600	124	1
Rayners Lane	0600-0630	300	1
Rayners Lane	0630-0700	410	1
Rayners Lane	0700-0730	622	1
Rayners Lane	0730-0800	877	1
Rayners Lane	0800-0830	931	1
Rayners Lane	0830-0900	733	1
Rayners Lane	0900-0930	472	1
Rayners Lane	0930-1000	312	1
Rayners Lane	1000-1030	244	1
Rayners Lane	1030-1100	218	1
Rayners Lane	1100-1130	216	1
Rayners Lane	1130-1200	213	1
Rayners Lane	1200-1230	223	1
Rayners Lane	1230-1300	215	1
Rayners Lane	1300-1330	222	1
Rayners Lane	1330-1400	228	1
Rayners Lane	1400-1430	232	1
Rayners Lane	1430-1500	279	1
Rayners Lane	1500-1530	271	1
Rayners Lane	1530-1600	358	1
Rayners Lane	1600-1630	417	1
Rayners Lane	1630-1700	535	1
Rayners Lane	1700-1730	599	1
Rayners Lane	1730-1800	707	1
Rayners Lane	1800-1830	792	1
Rayners Lane	1830-1900	728	1
Rayners Lane	1900-1930	523	1
Rayners Lane	1930-2000	366	1
Rayners Lane	2000-2030	271	1
Rayners Lane	2030-2100	196	1
Rayners Lane	2100-2130	173	1
Rayners Lane	2130-2200	153	1
Rayners Lane	2200-2230	144	1
Rayners Lane	2230-2300	130	1
Rayners Lane	2300-2330	123	1
Rayners Lane	2330-2400	130	1
Rayners Lane	0000-0030	121	1
Rayners Lane	0030-0100	96	1
Rayners Lane	0100-0130	28	1
Rayners Lane	0130-0200	0	1
Rayners Lane	0200-0230	0	0
Rayners Lane	0230-0300	0	0
Rayners Lane	0300-0330	0	0
Rayners Lane	0330-0400	0	0
Rayners Lane	0400-0430	0	0
Redbridge	0430-0500	0	0
Redbridge	0500-0530	34	1
Redbridge	0530-0600	123	1
Redbridge	0600-0630	256	1
Redbridge	0630-0700	327	1
Redbridge	0700-0730	371	1
Redbridge	0730-0800	476	1
Redbridge	0800-0830	587	1
Redbridge	0830-0900	448	1
Redbridge	0900-0930	304	1
Redbridge	0930-1000	203	1
Redbridge	1000-1030	164	1
Redbridge	1030-1100	143	1
Redbridge	1100-1130	139	1
Redbridge	1130-1200	131	1
Redbridge	1200-1230	134	1
Redbridge	1230-1300	136	1
Redbridge	1300-1330	139	1
Redbridge	1330-1400	136	1
Redbridge	1400-1430	147	1
Redbridge	1430-1500	163	1
Redbridge	1500-1530	181	1
Redbridge	1530-1600	231	1
Redbridge	1600-1630	274	1
Redbridge	1630-1700	338	1
Redbridge	1700-1730	398	1
Redbridge	1730-1800	474	1
Redbridge	1800-1830	488	1
Redbridge	1830-1900	429	1
Redbridge	1900-1930	334	1
Redbridge	1930-2000	254	1
Redbridge	2000-2030	192	1
Redbridge	2030-2100	172	1
Redbridge	2100-2130	132	1
Redbridge	2130-2200	129	1
Redbridge	2200-2230	118	1
Redbridge	2230-2300	112	1
Redbridge	2300-2330	109	1
Redbridge	2330-2400	93	1
Redbridge	0000-0030	57	1
Redbridge	0030-0100	28	1
Redbridge	0100-0130	8	1
Redbridge	0130-0200	3	1
Redbridge	0200-0230	0	0
Redbridge	0230-0300	0	0
Redbridge	0300-0330	0	0
Redbridge	0330-0400	0	0
Redbridge	0400-0430	0	0
Regent's Park	0430-0500	0	0
Regent's Park	0500-0530	0	1
Regent's Park	0530-0600	10	1
Regent's Park	0600-0630	29	1
Regent's Park	0630-0700	94	1
Regent's Park	0700-0730	266	1
Regent's Park	0730-0800	442	1
Regent's Park	0800-0830	574	1
Regent's Park	0830-0900	799	1
Regent's Park	0900-0930	694	1
Regent's Park	0930-1000	504	1
Regent's Park	1000-1030	357	1
Regent's Park	1030-1100	321	1
Regent's Park	1100-1130	282	1
Regent's Park	1130-1200	298	1
Regent's Park	1200-1230	302	1
Regent's Park	1230-1300	306	1
Regent's Park	1300-1330	297	1
Regent's Park	1330-1400	296	1
Regent's Park	1400-1430	290	1
Regent's Park	1430-1500	305	1
Regent's Park	1500-1530	341	1
Regent's Park	1530-1600	400	1
Regent's Park	1600-1630	492	1
Regent's Park	1630-1700	542	1
Regent's Park	1700-1730	668	1
Regent's Park	1730-1800	656	1
Regent's Park	1800-1830	624	1
Regent's Park	1830-1900	410	1
Regent's Park	1900-1930	284	1
Regent's Park	1930-2000	201	1
Regent's Park	2000-2030	168	1
Regent's Park	2030-2100	136	1
Regent's Park	2100-2130	108	1
Regent's Park	2130-2200	98	1
Regent's Park	2200-2230	81	1
Regent's Park	2230-2300	75	1
Regent's Park	2300-2330	62	1
Regent's Park	2330-2400	38	1
Regent's Park	0000-0030	22	1
Regent's Park	0030-0100	5	1
Regent's Park	0100-0130	0	1
Regent's Park	0130-0200	0	1
Regent's Park	0200-0230	0	0
Regent's Park	0230-0300	0	0
Regent's Park	0300-0330	0	0
Regent's Park	0330-0400	0	0
Regent's Park	0400-0430	0	0
Richmond	0430-0500	0	0
Richmond	0500-0530	6	1
Richmond	0530-0600	25	1
Richmond	0600-0630	139	1
Richmond	0630-0700	416	1
Richmond	0700-0730	1246	1
Richmond	0730-0800	1039	1
Richmond	0800-0830	1951	1
Richmond	0830-0900	1225	1
Richmond	0900-0930	745	1
Richmond	0930-1000	737	1
Richmond	1000-1030	523	1
Richmond	1030-1100	423	1
Richmond	1100-1130	555	1
Richmond	1130-1200	672	1
Richmond	1200-1230	470	1
Richmond	1230-1300	322	1
Richmond	1300-1330	476	1
Richmond	1330-1400	488	1
Richmond	1400-1430	390	1
Richmond	1430-1500	512	1
Richmond	1500-1530	560	1
Richmond	1530-1600	659	1
Richmond	1600-1630	875	1
Richmond	1630-1700	780	1
Richmond	1700-1730	1350	1
Richmond	1730-1800	1344	1
Richmond	1800-1830	1101	1
Richmond	1830-1900	960	1
Richmond	1900-1930	629	1
Richmond	1930-2000	722	1
Richmond	2000-2030	325	1
Richmond	2030-2100	304	1
Richmond	2100-2130	314	1
Richmond	2130-2200	336	1
Richmond	2200-2230	281	1
Richmond	2230-2300	364	1
Richmond	2300-2330	269	1
Richmond	2330-2400	187	1
Richmond	0000-0030	167	1
Richmond	0030-0100	141	1
Richmond	0100-0130	43	1
Richmond	0130-0200	0	1
Richmond	0200-0230	0	0
Richmond	0230-0300	0	0
Richmond	0300-0330	0	0
Richmond	0330-0400	0	0
Richmond	0400-0430	0	0
Rickmansworth	0430-0500	0	0
Rickmansworth	0500-0530	9	1
Rickmansworth	0530-0600	40	1
Rickmansworth	0600-0630	152	1
Rickmansworth	0630-0700	256	1
Rickmansworth	0700-0730	436	1
Rickmansworth	0730-0800	840	1
Rickmansworth	0800-0830	977	1
Rickmansworth	0830-0900	453	1
Rickmansworth	0900-0930	266	1
Rickmansworth	0930-1000	201	1
Rickmansworth	1000-1030	131	1
Rickmansworth	1030-1100	117	1
Rickmansworth	1100-1130	106	1
Rickmansworth	1130-1200	103	1
Rickmansworth	1200-1230	101	1
Rickmansworth	1230-1300	112	1
Rickmansworth	1300-1330	114	1
Rickmansworth	1330-1400	118	1
Rickmansworth	1400-1430	121	1
Rickmansworth	1430-1500	127	1
Rickmansworth	1500-1530	383	1
Rickmansworth	1530-1600	490	1
Rickmansworth	1600-1630	318	1
Rickmansworth	1630-1700	349	1
Rickmansworth	1700-1730	384	1
Rickmansworth	1730-1800	425	1
Rickmansworth	1800-1830	441	1
Rickmansworth	1830-1900	414	1
Rickmansworth	1900-1930	325	1
Rickmansworth	1930-2000	217	1
Rickmansworth	2000-2030	157	1
Rickmansworth	2030-2100	108	1
Rickmansworth	2100-2130	93	1
Rickmansworth	2130-2200	85	1
Rickmansworth	2200-2230	82	1
Rickmansworth	2230-2300	72	1
Rickmansworth	2300-2330	80	1
Rickmansworth	2330-2400	63	1
Rickmansworth	0000-0030	46	1
Rickmansworth	0030-0100	24	1
Rickmansworth	0100-0130	11	1
Rickmansworth	0130-0200	0	1
Rickmansworth	0200-0230	0	0
Rickmansworth	0230-0300	0	0
Rickmansworth	0300-0330	0	0
Rickmansworth	0330-0400	0	0
Rickmansworth	0400-0430	0	0
Roding Valley	0430-0500	0	0
Roding Valley	0500-0530	0	1
Roding Valley	0530-0600	4	1
Roding Valley	0600-0630	17	1
Roding Valley	0630-0700	63	1
Roding Valley	0700-0730	96	1
Roding Valley	0730-0800	147	1
Roding Valley	0800-0830	69	1
Roding Valley	0830-0900	39	1
Roding Valley	0900-0930	25	1
Roding Valley	0930-1000	20	1
Roding Valley	1000-1030	23	1
Roding Valley	1030-1100	15	1
Roding Valley	1100-1130	9	1
Roding Valley	1130-1200	19	1
Roding Valley	1200-1230	16	1
Roding Valley	1230-1300	25	1
Roding Valley	1300-1330	11	1
Roding Valley	1330-1400	17	1
Roding Valley	1400-1430	7	1
Roding Valley	1430-1500	12	1
Roding Valley	1500-1530	103	1
Roding Valley	1530-1600	68	1
Roding Valley	1600-1630	46	1
Roding Valley	1630-1700	41	1
Roding Valley	1700-1730	62	1
Roding Valley	1730-1800	88	1
Roding Valley	1800-1830	81	1
Roding Valley	1830-1900	30	1
Roding Valley	1900-1930	39	1
Roding Valley	1930-2000	8	1
Roding Valley	2000-2030	6	1
Roding Valley	2030-2100	25	1
Roding Valley	2100-2130	15	1
Roding Valley	2130-2200	16	1
Roding Valley	2200-2230	17	1
Roding Valley	2230-2300	15	1
Roding Valley	2300-2330	10	1
Roding Valley	2330-2400	13	1
Roding Valley	0000-0030	5	1
Roding Valley	0030-0100	0	1
Roding Valley	0100-0130	0	1
Roding Valley	0130-0200	0	1
Roding Valley	0200-0230	0	0
Roding Valley	0230-0300	0	0
Roding Valley	0300-0330	0	0
Roding Valley	0330-0400	0	0
Roding Valley	0400-0430	0	0
Royal Oak	0430-0500	0	0
Royal Oak	0500-0530	11	1
Royal Oak	0530-0600	29	1
Royal Oak	0600-0630	61	1
Royal Oak	0630-0700	126	1
Royal Oak	0700-0730	237	1
Royal Oak	0730-0800	429	1
Royal Oak	0800-0830	557	1
Royal Oak	0830-0900	505	1
Royal Oak	0900-0930	382	1
Royal Oak	0930-1000	255	1
Royal Oak	1000-1030	183	1
Royal Oak	1030-1100	155	1
Royal Oak	1100-1130	145	1
Royal Oak	1130-1200	139	1
Royal Oak	1200-1230	147	1
Royal Oak	1230-1300	156	1
Royal Oak	1300-1330	161	1
Royal Oak	1330-1400	153	1
Royal Oak	1400-1430	163	1
Royal Oak	1430-1500	166	1
Royal Oak	1500-1530	188	1
Royal Oak	1530-1600	236	1
Royal Oak	1600-1630	266	1
Royal Oak	1630-1700	321	1
Royal Oak	1700-1730	349	1
Royal Oak	1730-1800	394	1
Royal Oak	1800-1830	448	1
Royal Oak	1830-1900	393	1
Royal Oak	1900-1930	319	1
Royal Oak	1930-2000	236	1
Royal Oak	2000-2030	186	1
Royal Oak	2030-2100	159	1
Royal Oak	2100-2130	141	1
Royal Oak	2130-2200	127	1
Royal Oak	2200-2230	122	1
Royal Oak	2230-2300	101	1
Royal Oak	2300-2330	89	1
Royal Oak	2330-2400	65	1
Royal Oak	0000-0030	39	1
Royal Oak	0030-0100	18	1
Royal Oak	0100-0130	0	1
Royal Oak	0130-0200	0	1
Royal Oak	0200-0230	0	0
Royal Oak	0230-0300	0	0
Royal Oak	0300-0330	0	0
Royal Oak	0330-0400	0	0
Royal Oak	0400-0430	0	0
Ruislip	0430-0500	0	0
Ruislip	0500-0530	17	1
Ruislip	0530-0600	35	1
Ruislip	0600-0630	84	1
Ruislip	0630-0700	159	1
Ruislip	0700-0730	263	1
Ruislip	0730-0800	368	1
Ruislip	0800-0830	387	1
Ruislip	0830-0900	286	1
Ruislip	0900-0930	196	1
Ruislip	0930-1000	172	1
Ruislip	1000-1030	141	1
Ruislip	1030-1100	141	1
Ruislip	1100-1130	142	1
Ruislip	1130-1200	145	1
Ruislip	1200-1230	146	1
Ruislip	1230-1300	150	1
Ruislip	1300-1330	150	1
Ruislip	1330-1400	147	1
Ruislip	1400-1430	154	1
Ruislip	1430-1500	160	1
Ruislip	1500-1530	183	1
Ruislip	1530-1600	195	1
Ruislip	1600-1630	232	1
Ruislip	1630-1700	267	1
Ruislip	1700-1730	288	1
Ruislip	1730-1800	319	1
Ruislip	1800-1830	309	1
Ruislip	1830-1900	252	1
Ruislip	1900-1930	196	1
Ruislip	1930-2000	138	1
Ruislip	2000-2030	100	1
Ruislip	2030-2100	80	1
Ruislip	2100-2130	64	1
Ruislip	2130-2200	60	1
Ruislip	2200-2230	67	1
Ruislip	2230-2300	61	1
Ruislip	2300-2330	49	1
Ruislip	2330-2400	33	1
Ruislip	0000-0030	21	1
Ruislip	0030-0100	12	1
Ruislip	0100-0130	3	1
Ruislip	0130-0200	1	1
Ruislip	0200-0230	0	0
Ruislip	0230-0300	0	0
Ruislip	0300-0330	0	0
Ruislip	0330-0400	0	0
Ruislip	0400-0430	0	0
Ruislip Gardens	0430-0500	0	0
Ruislip Gardens	0500-0530	20	1
Ruislip Gardens	0530-0600	50	1
Ruislip Gardens	0600-0630	78	1
Ruislip Gardens	0630-0700	148	1
Ruislip Gardens	0700-0730	223	1
Ruislip Gardens	0730-0800	334	1
Ruislip Gardens	0800-0830	327	1
Ruislip Gardens	0830-0900	221	1
Ruislip Gardens	0900-0930	119	1
Ruislip Gardens	0930-1000	85	1
Ruislip Gardens	1000-1030	55	1
Ruislip Gardens	1030-1100	45	1
Ruislip Gardens	1100-1130	45	1
Ruislip Gardens	1130-1200	45	1
Ruislip Gardens	1200-1230	45	1
Ruislip Gardens	1230-1300	48	1
Ruislip Gardens	1300-1330	46	1
Ruislip Gardens	1330-1400	46	1
Ruislip Gardens	1400-1430	56	1
Ruislip Gardens	1430-1500	68	1
Ruislip Gardens	1500-1530	82	1
Ruislip Gardens	1530-1600	88	1
Ruislip Gardens	1600-1630	114	1
Ruislip Gardens	1630-1700	142	1
Ruislip Gardens	1700-1730	158	1
Ruislip Gardens	1730-1800	180	1
Ruislip Gardens	1800-1830	194	1
Ruislip Gardens	1830-1900	169	1
Ruislip Gardens	1900-1930	130	1
Ruislip Gardens	1930-2000	84	1
Ruislip Gardens	2000-2030	63	1
Ruislip Gardens	2030-2100	51	1
Ruislip Gardens	2100-2130	44	1
Ruislip Gardens	2130-2200	48	1
Ruislip Gardens	2200-2230	57	1
Ruislip Gardens	2230-2300	44	1
Ruislip Gardens	2300-2330	41	1
Ruislip Gardens	2330-2400	29	1
Ruislip Gardens	0000-0030	20	1
Ruislip Gardens	0030-0100	11	1
Ruislip Gardens	0100-0130	3	1
Ruislip Gardens	0130-0200	0	1
Ruislip Gardens	0200-0230	0	0
Ruislip Gardens	0230-0300	0	0
Ruislip Gardens	0300-0330	0	0
Ruislip Gardens	0330-0400	0	0
Ruislip Gardens	0400-0430	0	0
Ruislip Manor	0430-0500	0	0
Ruislip Manor	0500-0530	15	1
Ruislip Manor	0530-0600	40	1
Ruislip Manor	0600-0630	116	1
Ruislip Manor	0630-0700	192	1
Ruislip Manor	0700-0730	282	1
Ruislip Manor	0730-0800	441	1
Ruislip Manor	0800-0830	585	1
Ruislip Manor	0830-0900	365	1
Ruislip Manor	0900-0930	189	1
Ruislip Manor	0930-1000	146	1
Ruislip Manor	1000-1030	117	1
Ruislip Manor	1030-1100	108	1
Ruislip Manor	1100-1130	108	1
Ruislip Manor	1130-1200	115	1
Ruislip Manor	1200-1230	114	1
Ruislip Manor	1230-1300	110	1
Ruislip Manor	1300-1330	114	1
Ruislip Manor	1330-1400	123	1
Ruislip Manor	1400-1430	125	1
Ruislip Manor	1430-1500	138	1
Ruislip Manor	1500-1530	190	1
Ruislip Manor	1530-1600	308	1
Ruislip Manor	1600-1630	260	1
Ruislip Manor	1630-1700	258	1
Ruislip Manor	1700-1730	286	1
Ruislip Manor	1730-1800	325	1
Ruislip Manor	1800-1830	331	1
Ruislip Manor	1830-1900	296	1
Ruislip Manor	1900-1930	213	1
Ruislip Manor	1930-2000	139	1
Ruislip Manor	2000-2030	107	1
Ruislip Manor	2030-2100	76	1
Ruislip Manor	2100-2130	65	1
Ruislip Manor	2130-2200	61	1
Ruislip Manor	2200-2230	64	1
Ruislip Manor	2230-2300	62	1
Ruislip Manor	2300-2330	59	1
Ruislip Manor	2330-2400	45	1
Ruislip Manor	0000-0030	28	1
Ruislip Manor	0030-0100	17	1
Ruislip Manor	0100-0130	7	1
Ruislip Manor	0130-0200	0	1
Ruislip Manor	0200-0230	0	0
Ruislip Manor	0230-0300	0	0
Ruislip Manor	0300-0330	0	0
Ruislip Manor	0330-0400	0	0
Ruislip Manor	0400-0430	0	0
Russell Square	0430-0500	0	0
Russell Square	0500-0530	7	1
Russell Square	0530-0600	55	1
Russell Square	0600-0630	106	1
Russell Square	0630-0700	227	1
Russell Square	0700-0730	488	1
Russell Square	0730-0800	833	1
Russell Square	0800-0830	1005	1
Russell Square	0830-0900	1475	1
Russell Square	0900-0930	1654	1
Russell Square	0930-1000	1509	1
Russell Square	1000-1030	1127	1
Russell Square	1030-1100	1033	1
Russell Square	1100-1130	840	1
Russell Square	1130-1200	763	1
Russell Square	1200-1230	811	1
Russell Square	1230-1300	924	1
Russell Square	1300-1330	984	1
Russell Square	1330-1400	939	1
Russell Square	1400-1430	912	1
Russell Square	1430-1500	944	1
Russell Square	1500-1530	1069	1
Russell Square	1530-1600	1150	1
Russell Square	1600-1630	1349	1
Russell Square	1630-1700	1563	1
Russell Square	1700-1730	1887	1
Russell Square	1730-1800	1870	1
Russell Square	1800-1830	1693	1
Russell Square	1830-1900	1365	1
Russell Square	1900-1930	1108	1
Russell Square	1930-2000	878	1
Russell Square	2000-2030	853	1
Russell Square	2030-2100	816	1
Russell Square	2100-2130	757	1
Russell Square	2130-2200	533	1
Russell Square	2200-2230	535	1
Russell Square	2230-2300	530	1
Russell Square	2300-2330	445	1
Russell Square	2330-2400	330	1
Russell Square	0000-0030	170	1
Russell Square	0030-0100	50	1
Russell Square	0100-0130	17	1
Russell Square	0130-0200	12	1
Russell Square	0200-0230	0	0
Russell Square	0230-0300	0	0
Russell Square	0300-0330	0	0
Russell Square	0330-0400	0	0
Russell Square	0400-0430	0	0
Seven Sisters	0430-0500	0	0
Seven Sisters	0500-0530	302	1
Seven Sisters	0530-0600	589	1
Seven Sisters	0600-0630	1276	1
Seven Sisters	0630-0700	2074	1
Seven Sisters	0700-0730	2411	1
Seven Sisters	0730-0800	2271	1
Seven Sisters	0800-0830	2763	1
Seven Sisters	0830-0900	2681	1
Seven Sisters	0900-0930	2071	1
Seven Sisters	0930-1000	1419	1
Seven Sisters	1000-1030	1047	1
Seven Sisters	1030-1100	947	1
Seven Sisters	1100-1130	908	1
Seven Sisters	1130-1200	865	1
Seven Sisters	1200-1230	880	1
Seven Sisters	1230-1300	913	1
Seven Sisters	1300-1330	941	1
Seven Sisters	1330-1400	948	1
Seven Sisters	1400-1430	997	1
Seven Sisters	1430-1500	1082	1
Seven Sisters	1500-1530	1213	1
Seven Sisters	1530-1600	1368	1
Seven Sisters	1600-1630	1641	1
Seven Sisters	1630-1700	1992	1
Seven Sisters	1700-1730	2395	1
Seven Sisters	1730-1800	2686	1
Seven Sisters	1800-1830	2605	1
Seven Sisters	1830-1900	2337	1
Seven Sisters	1900-1930	1821	1
Seven Sisters	1930-2000	1373	1
Seven Sisters	2000-2030	1155	1
Seven Sisters	2030-2100	1044	1
Seven Sisters	2100-2130	946	1
Seven Sisters	2130-2200	888	1
Seven Sisters	2200-2230	841	1
Seven Sisters	2230-2300	835	1
Seven Sisters	2300-2330	777	1
Seven Sisters	2330-2400	711	1
Seven Sisters	0000-0030	550	1
Seven Sisters	0030-0100	312	1
Seven Sisters	0100-0130	80	1
Seven Sisters	0130-0200	46	1
Seven Sisters	0200-0230	0	0
Seven Sisters	0230-0300	0	0
Seven Sisters	0300-0330	0	0
Seven Sisters	0330-0400	0	0
Seven Sisters	0400-0430	0	0
Shepherd's Bush (Cen)	0430-0500	0	0
Shepherd's Bush (Cen)	0500-0530	32	1
Shepherd's Bush (Cen)	0530-0600	161	1
Shepherd's Bush (Cen)	0600-0630	562	1
Shepherd's Bush (Cen)	0630-0700	1278	1
Shepherd's Bush (Cen)	0700-0730	1962	1
Shepherd's Bush (Cen)	0730-0800	2632	1
Shepherd's Bush (Cen)	0800-0830	3394	1
Shepherd's Bush (Cen)	0830-0900	3679	1
Shepherd's Bush (Cen)	0900-0930	2821	1
Shepherd's Bush (Cen)	0930-1000	2011	1
Shepherd's Bush (Cen)	1000-1030	1323	1
Shepherd's Bush (Cen)	1030-1100	1270	1
Shepherd's Bush (Cen)	1100-1130	1187	1
Shepherd's Bush (Cen)	1130-1200	1223	1
Shepherd's Bush (Cen)	1200-1230	1226	1
Shepherd's Bush (Cen)	1230-1300	1282	1
Shepherd's Bush (Cen)	1300-1330	1371	1
Shepherd's Bush (Cen)	1330-1400	1382	1
Shepherd's Bush (Cen)	1400-1430	1419	1
Shepherd's Bush (Cen)	1430-1500	1438	1
Shepherd's Bush (Cen)	1500-1530	1537	1
Shepherd's Bush (Cen)	1530-1600	1842	1
Shepherd's Bush (Cen)	1600-1630	2111	1
Shepherd's Bush (Cen)	1630-1700	2417	1
Shepherd's Bush (Cen)	1700-1730	2934	1
Shepherd's Bush (Cen)	1730-1800	3491	1
Shepherd's Bush (Cen)	1800-1830	3895	1
Shepherd's Bush (Cen)	1830-1900	3374	1
Shepherd's Bush (Cen)	1900-1930	2559	1
Shepherd's Bush (Cen)	1930-2000	1907	1
Shepherd's Bush (Cen)	2000-2030	1547	1
Shepherd's Bush (Cen)	2030-2100	1278	1
Shepherd's Bush (Cen)	2100-2130	1161	1
Shepherd's Bush (Cen)	2130-2200	1092	1
Shepherd's Bush (Cen)	2200-2230	1134	1
Shepherd's Bush (Cen)	2230-2300	1233	1
Shepherd's Bush (Cen)	2300-2330	1071	1
Shepherd's Bush (Cen)	2330-2400	704	1
Shepherd's Bush (Cen)	0000-0030	427	1
Shepherd's Bush (Cen)	0030-0100	187	1
Shepherd's Bush (Cen)	0100-0130	64	1
Shepherd's Bush (Cen)	0130-0200	30	1
Shepherd's Bush (Cen)	0200-0230	0	0
Shepherd's Bush (Cen)	0230-0300	0	0
Shepherd's Bush (Cen)	0300-0330	0	0
Shepherd's Bush (Cen)	0330-0400	0	0
Shepherd's Bush (Cen)	0400-0430	0	0
Shepherd's Bush (H&C)	0430-0500	0	0
Shepherd's Bush (H&C)	0500-0530	20	1
Shepherd's Bush (H&C)	0530-0600	39	1
Shepherd's Bush (H&C)	0600-0630	77	1
Shepherd's Bush (H&C)	0630-0700	158	1
Shepherd's Bush (H&C)	0700-0730	261	1
Shepherd's Bush (H&C)	0730-0800	434	1
Shepherd's Bush (H&C)	0800-0830	594	1
Shepherd's Bush (H&C)	0830-0900	582	1
Shepherd's Bush (H&C)	0900-0930	452	1
Shepherd's Bush (H&C)	0930-1000	324	1
Shepherd's Bush (H&C)	1000-1030	237	1
Shepherd's Bush (H&C)	1030-1100	213	1
Shepherd's Bush (H&C)	1100-1130	209	1
Shepherd's Bush (H&C)	1130-1200	211	1
Shepherd's Bush (H&C)	1200-1230	241	1
Shepherd's Bush (H&C)	1230-1300	252	1
Shepherd's Bush (H&C)	1300-1330	270	1
Shepherd's Bush (H&C)	1330-1400	275	1
Shepherd's Bush (H&C)	1400-1430	271	1
Shepherd's Bush (H&C)	1430-1500	266	1
Shepherd's Bush (H&C)	1500-1530	275	1
Shepherd's Bush (H&C)	1530-1600	318	1
Shepherd's Bush (H&C)	1600-1630	365	1
Shepherd's Bush (H&C)	1630-1700	399	1
Shepherd's Bush (H&C)	1700-1730	466	1
Shepherd's Bush (H&C)	1730-1800	542	1
Shepherd's Bush (H&C)	1800-1830	577	1
Shepherd's Bush (H&C)	1830-1900	562	1
Shepherd's Bush (H&C)	1900-1930	430	1
Shepherd's Bush (H&C)	1930-2000	307	1
Shepherd's Bush (H&C)	2000-2030	244	1
Shepherd's Bush (H&C)	2030-2100	202	1
Shepherd's Bush (H&C)	2100-2130	184	1
Shepherd's Bush (H&C)	2130-2200	235	1
Shepherd's Bush (H&C)	2200-2230	202	1
Shepherd's Bush (H&C)	2230-2300	203	1
Shepherd's Bush (H&C)	2300-2330	173	1
Shepherd's Bush (H&C)	2330-2400	101	1
Shepherd's Bush (H&C)	0000-0030	62	1
Shepherd's Bush (H&C)	0030-0100	30	1
Shepherd's Bush (H&C)	0100-0130	7	1
Shepherd's Bush (H&C)	0130-0200	0	1
Shepherd's Bush (H&C)	0200-0230	0	0
Shepherd's Bush (H&C)	0230-0300	0	0
Shepherd's Bush (H&C)	0300-0330	0	0
Shepherd's Bush (H&C)	0330-0400	0	0
Shepherd's Bush (H&C)	0400-0430	0	0
Sloane Square	0430-0500	0	0
Sloane Square	0500-0530	15	1
Sloane Square	0530-0600	104	1
Sloane Square	0600-0630	295	1
Sloane Square	0630-0700	774	1
Sloane Square	0700-0730	1680	1
Sloane Square	0730-0800	2519	1
Sloane Square	0800-0830	2635	1
Sloane Square	0830-0900	2704	1
Sloane Square	0900-0930	2169	1
Sloane Square	0930-1000	1793	1
Sloane Square	1000-1030	1416	1
Sloane Square	1030-1100	1325	1
Sloane Square	1100-1130	1237	1
Sloane Square	1130-1200	1311	1
Sloane Square	1200-1230	1351	1
Sloane Square	1230-1300	1368	1
Sloane Square	1300-1330	1330	1
Sloane Square	1330-1400	1348	1
Sloane Square	1400-1430	1352	1
Sloane Square	1430-1500	1438	1
Sloane Square	1500-1530	1624	1
Sloane Square	1530-1600	1815	1
Sloane Square	1600-1630	2117	1
Sloane Square	1630-1700	2265	1
Sloane Square	1700-1730	2542	1
Sloane Square	1730-1800	2744	1
Sloane Square	1800-1830	2952	1
Sloane Square	1830-1900	2483	1
Sloane Square	1900-1930	1971	1
Sloane Square	1930-2000	1212	1
Sloane Square	2000-2030	951	1
Sloane Square	2030-2100	720	1
Sloane Square	2100-2130	680	1
Sloane Square	2130-2200	666	1
Sloane Square	2200-2230	619	1
Sloane Square	2230-2300	496	1
Sloane Square	2300-2330	422	1
Sloane Square	2330-2400	309	1
Sloane Square	0000-0030	163	1
Sloane Square	0030-0100	36	1
Sloane Square	0100-0130	0	1
Sloane Square	0130-0200	0	1
Sloane Square	0200-0230	0	0
Sloane Square	0230-0300	0	0
Sloane Square	0300-0330	0	0
Sloane Square	0330-0400	0	0
Sloane Square	0400-0430	0	0
Snaresbrook	0430-0500	0	0
Snaresbrook	0500-0530	34	1
Snaresbrook	0530-0600	48	1
Snaresbrook	0600-0630	111	1
Snaresbrook	0630-0700	225	1
Snaresbrook	0700-0730	452	1
Snaresbrook	0730-0800	732	1
Snaresbrook	0800-0830	1015	1
Snaresbrook	0830-0900	804	1
Snaresbrook	0900-0930	538	1
Snaresbrook	0930-1000	321	1
Snaresbrook	1000-1030	169	1
Snaresbrook	1030-1100	144	1
Snaresbrook	1100-1130	127	1
Snaresbrook	1130-1200	129	1
Snaresbrook	1200-1230	126	1
Snaresbrook	1230-1300	134	1
Snaresbrook	1300-1330	141	1
Snaresbrook	1330-1400	132	1
Snaresbrook	1400-1430	138	1
Snaresbrook	1430-1500	144	1
Snaresbrook	1500-1530	172	1
Snaresbrook	1530-1600	200	1
Snaresbrook	1600-1630	340	1
Snaresbrook	1630-1700	320	1
Snaresbrook	1700-1730	321	1
Snaresbrook	1730-1800	374	1
Snaresbrook	1800-1830	402	1
Snaresbrook	1830-1900	383	1
Snaresbrook	1900-1930	306	1
Snaresbrook	1930-2000	215	1
Snaresbrook	2000-2030	161	1
Snaresbrook	2030-2100	133	1
Snaresbrook	2100-2130	115	1
Snaresbrook	2130-2200	109	1
Snaresbrook	2200-2230	101	1
Snaresbrook	2230-2300	100	1
Snaresbrook	2300-2330	79	1
Snaresbrook	2330-2400	69	1
Snaresbrook	0000-0030	44	1
Snaresbrook	0030-0100	28	1
Snaresbrook	0100-0130	10	1
Snaresbrook	0130-0200	5	1
Snaresbrook	0200-0230	0	0
Snaresbrook	0230-0300	0	0
Snaresbrook	0300-0330	0	0
Snaresbrook	0330-0400	0	0
Snaresbrook	0400-0430	0	0
South Ealing	0430-0500	0	0
South Ealing	0500-0530	31	1
South Ealing	0530-0600	59	1
South Ealing	0600-0630	112	1
South Ealing	0630-0700	225	1
South Ealing	0700-0730	377	1
South Ealing	0730-0800	583	1
South Ealing	0800-0830	707	1
South Ealing	0830-0900	665	1
South Ealing	0900-0930	474	1
South Ealing	0930-1000	298	1
South Ealing	1000-1030	229	1
South Ealing	1030-1100	206	1
South Ealing	1100-1130	203	1
South Ealing	1130-1200	190	1
South Ealing	1200-1230	194	1
South Ealing	1230-1300	212	1
South Ealing	1300-1330	215	1
South Ealing	1330-1400	205	1
South Ealing	1400-1430	215	1
South Ealing	1430-1500	228	1
South Ealing	1500-1530	271	1
South Ealing	1530-1600	288	1
South Ealing	1600-1630	339	1
South Ealing	1630-1700	397	1
South Ealing	1700-1730	511	1
South Ealing	1730-1800	576	1
South Ealing	1800-1830	593	1
South Ealing	1830-1900	526	1
South Ealing	1900-1930	419	1
South Ealing	1930-2000	315	1
South Ealing	2000-2030	225	1
South Ealing	2030-2100	187	1
South Ealing	2100-2130	181	1
South Ealing	2130-2200	177	1
South Ealing	2200-2230	177	1
South Ealing	2230-2300	170	1
South Ealing	2300-2330	152	1
South Ealing	2330-2400	131	1
South Ealing	0000-0030	93	1
South Ealing	0030-0100	52	1
South Ealing	0100-0130	18	1
South Ealing	0130-0200	13	1
South Ealing	0200-0230	0	0
South Ealing	0230-0300	0	0
South Ealing	0300-0330	0	0
South Ealing	0330-0400	0	0
South Ealing	0400-0430	0	0
South Harrow	0430-0500	0	0
South Harrow	0500-0530	42	1
South Harrow	0530-0600	83	1
South Harrow	0600-0630	162	1
South Harrow	0630-0700	241	1
South Harrow	0700-0730	297	1
South Harrow	0730-0800	398	1
South Harrow	0800-0830	446	1
South Harrow	0830-0900	338	1
South Harrow	0900-0930	215	1
South Harrow	0930-1000	148	1
South Harrow	1000-1030	121	1
South Harrow	1030-1100	112	1
South Harrow	1100-1130	115	1
South Harrow	1130-1200	117	1
South Harrow	1200-1230	116	1
South Harrow	1230-1300	121	1
South Harrow	1300-1330	130	1
South Harrow	1330-1400	129	1
South Harrow	1400-1430	146	1
South Harrow	1430-1500	146	1
South Harrow	1500-1530	161	1
South Harrow	1530-1600	200	1
South Harrow	1600-1630	243	1
South Harrow	1630-1700	268	1
South Harrow	1700-1730	331	1
South Harrow	1730-1800	368	1
South Harrow	1800-1830	374	1
South Harrow	1830-1900	326	1
South Harrow	1900-1930	239	1
South Harrow	1930-2000	183	1
South Harrow	2000-2030	140	1
South Harrow	2030-2100	106	1
South Harrow	2100-2130	87	1
South Harrow	2130-2200	78	1
South Harrow	2200-2230	70	1
South Harrow	2230-2300	69	1
South Harrow	2300-2330	70	1
South Harrow	2330-2400	58	1
South Harrow	0000-0030	39	1
South Harrow	0030-0100	22	1
South Harrow	0100-0130	8	1
South Harrow	0130-0200	0	1
South Harrow	0200-0230	0	0
South Harrow	0230-0300	0	0
South Harrow	0300-0330	0	0
South Harrow	0330-0400	0	0
South Harrow	0400-0430	0	0
South Kensington	0430-0500	0	0
South Kensington	0500-0530	21	1
South Kensington	0530-0600	147	1
South Kensington	0600-0630	379	1
South Kensington	0630-0700	857	1
South Kensington	0700-0730	1679	1
South Kensington	0730-0800	2650	1
South Kensington	0800-0830	3817	1
South Kensington	0830-0900	5002	1
South Kensington	0900-0930	4212	1
South Kensington	0930-1000	3581	1
South Kensington	1000-1030	2858	1
South Kensington	1030-1100	2818	1
South Kensington	1100-1130	2522	1
South Kensington	1130-1200	2530	1
South Kensington	1200-1230	2637	1
South Kensington	1230-1300	2741	1
South Kensington	1300-1330	2740	1
South Kensington	1330-1400	2770	1
South Kensington	1400-1430	2699	1
South Kensington	1430-1500	2834	1
South Kensington	1500-1530	3109	1
South Kensington	1530-1600	3467	1
South Kensington	1600-1630	4062	1
South Kensington	1630-1700	4052	1
South Kensington	1700-1730	4873	1
South Kensington	1730-1800	5066	1
South Kensington	1800-1830	5203	1
South Kensington	1830-1900	4022	1
South Kensington	1900-1930	3048	1
South Kensington	1930-2000	2144	1
South Kensington	2000-2030	1864	1
South Kensington	2030-2100	1625	1
South Kensington	2100-2130	1471	1
South Kensington	2130-2200	1396	1
South Kensington	2200-2230	1393	1
South Kensington	2230-2300	1445	1
South Kensington	2300-2330	1090	1
South Kensington	2330-2400	733	1
South Kensington	0000-0030	412	1
South Kensington	0030-0100	114	1
South Kensington	0100-0130	35	1
South Kensington	0130-0200	17	1
South Kensington	0200-0230	0	0
South Kensington	0230-0300	0	0
South Kensington	0300-0330	0	0
South Kensington	0330-0400	0	0
South Kensington	0400-0430	0	0
South Kenton	0430-0500	0	0
South Kenton	0500-0530	1	1
South Kenton	0530-0600	11	1
South Kenton	0600-0630	31	1
South Kenton	0630-0700	91	1
South Kenton	0700-0730	200	1
South Kenton	0730-0800	258	1
South Kenton	0800-0830	321	1
South Kenton	0830-0900	214	1
South Kenton	0900-0930	105	1
South Kenton	0930-1000	75	1
South Kenton	1000-1030	76	1
South Kenton	1030-1100	65	1
South Kenton	1100-1130	62	1
South Kenton	1130-1200	58	1
South Kenton	1200-1230	53	1
South Kenton	1230-1300	60	1
South Kenton	1300-1330	73	1
South Kenton	1330-1400	49	1
South Kenton	1400-1430	79	1
South Kenton	1430-1500	121	1
South Kenton	1500-1530	191	1
South Kenton	1530-1600	144	1
South Kenton	1600-1630	147	1
South Kenton	1630-1700	118	1
South Kenton	1700-1730	184	1
South Kenton	1730-1800	216	1
South Kenton	1800-1830	196	1
South Kenton	1830-1900	143	1
South Kenton	1900-1930	112	1
South Kenton	1930-2000	88	1
South Kenton	2000-2030	57	1
South Kenton	2030-2100	45	1
South Kenton	2100-2130	29	1
South Kenton	2130-2200	0	1
South Kenton	2200-2230	77	1
South Kenton	2230-2300	79	1
South Kenton	2300-2330	58	1
South Kenton	2330-2400	40	1
South Kenton	0000-0030	23	1
South Kenton	0030-0100	7	1
South Kenton	0100-0130	0	1
South Kenton	0130-0200	0	1
South Kenton	0200-0230	0	0
South Kenton	0230-0300	0	0
South Kenton	0300-0330	0	0
South Kenton	0330-0400	0	0
South Kenton	0400-0430	0	0
South Ruislip	0430-0500	0	0
South Ruislip	0500-0530	21	1
South Ruislip	0530-0600	62	1
South Ruislip	0600-0630	153	1
South Ruislip	0630-0700	240	1
South Ruislip	0700-0730	347	1
South Ruislip	0730-0800	500	1
South Ruislip	0800-0830	507	1
South Ruislip	0830-0900	372	1
South Ruislip	0900-0930	222	1
South Ruislip	0930-1000	142	1
South Ruislip	1000-1030	103	1
South Ruislip	1030-1100	90	1
South Ruislip	1100-1130	83	1
South Ruislip	1130-1200	75	1
South Ruislip	1200-1230	73	1
South Ruislip	1230-1300	78	1
South Ruislip	1300-1330	78	1
South Ruislip	1330-1400	92	1
South Ruislip	1400-1430	91	1
South Ruislip	1430-1500	110	1
South Ruislip	1500-1530	107	1
South Ruislip	1530-1600	134	1
South Ruislip	1600-1630	182	1
South Ruislip	1630-1700	237	1
South Ruislip	1700-1730	308	1
South Ruislip	1730-1800	364	1
South Ruislip	1800-1830	373	1
South Ruislip	1830-1900	334	1
South Ruislip	1900-1930	233	1
South Ruislip	1930-2000	154	1
South Ruislip	2000-2030	111	1
South Ruislip	2030-2100	87	1
South Ruislip	2100-2130	75	1
South Ruislip	2130-2200	81	1
South Ruislip	2200-2230	96	1
South Ruislip	2230-2300	73	1
South Ruislip	2300-2330	61	1
South Ruislip	2330-2400	51	1
South Ruislip	0000-0030	31	1
South Ruislip	0030-0100	18	1
South Ruislip	0100-0130	5	1
South Ruislip	0130-0200	0	1
South Ruislip	0200-0230	0	0
South Ruislip	0230-0300	0	0
South Ruislip	0300-0330	0	0
South Ruislip	0330-0400	0	0
South Ruislip	0400-0430	0	0
South Wimbledon	0430-0500	0	0
South Wimbledon	0500-0530	36	1
South Wimbledon	0530-0600	73	1
South Wimbledon	0600-0630	187	1
South Wimbledon	0630-0700	388	1
South Wimbledon	0700-0730	702	1
South Wimbledon	0730-0800	1174	1
South Wimbledon	0800-0830	1366	1
South Wimbledon	0830-0900	1025	1
South Wimbledon	0900-0930	611	1
South Wimbledon	0930-1000	358	1
South Wimbledon	1000-1030	241	1
South Wimbledon	1030-1100	208	1
South Wimbledon	1100-1130	203	1
South Wimbledon	1130-1200	208	1
South Wimbledon	1200-1230	216	1
South Wimbledon	1230-1300	224	1
South Wimbledon	1300-1330	231	1
South Wimbledon	1330-1400	230	1
South Wimbledon	1400-1430	233	1
South Wimbledon	1430-1500	244	1
South Wimbledon	1500-1530	258	1
South Wimbledon	1530-1600	315	1
South Wimbledon	1600-1630	365	1
South Wimbledon	1630-1700	473	1
South Wimbledon	1700-1730	640	1
South Wimbledon	1730-1800	772	1
South Wimbledon	1800-1830	822	1
South Wimbledon	1830-1900	703	1
South Wimbledon	1900-1930	547	1
South Wimbledon	1930-2000	394	1
South Wimbledon	2000-2030	296	1
South Wimbledon	2030-2100	247	1
South Wimbledon	2100-2130	215	1
South Wimbledon	2130-2200	203	1
South Wimbledon	2200-2230	196	1
South Wimbledon	2230-2300	203	1
South Wimbledon	2300-2330	195	1
South Wimbledon	2330-2400	167	1
South Wimbledon	0000-0030	111	1
South Wimbledon	0030-0100	68	1
South Wimbledon	0100-0130	34	1
South Wimbledon	0130-0200	17	1
South Wimbledon	0200-0230	0	0
South Wimbledon	0230-0300	0	0
South Wimbledon	0300-0330	0	0
South Wimbledon	0330-0400	0	0
South Wimbledon	0400-0430	0	0
South Woodford	0430-0500	0	0
South Woodford	0500-0530	28	1
South Woodford	0530-0600	95	1
South Woodford	0600-0630	179	1
South Woodford	0630-0700	312	1
South Woodford	0700-0730	583	1
South Woodford	0730-0800	958	1
South Woodford	0800-0830	1279	1
South Woodford	0830-0900	1036	1
South Woodford	0900-0930	672	1
South Woodford	0930-1000	408	1
South Woodford	1000-1030	297	1
South Woodford	1030-1100	253	1
South Woodford	1100-1130	245	1
South Woodford	1130-1200	244	1
South Woodford	1200-1230	245	1
South Woodford	1230-1300	239	1
South Woodford	1300-1330	256	1
South Woodford	1330-1400	255	1
South Woodford	1400-1430	256	1
South Woodford	1430-1500	298	1
South Woodford	1500-1530	341	1
South Woodford	1530-1600	380	1
South Woodford	1600-1630	478	1
South Woodford	1630-1700	620	1
South Woodford	1700-1730	775	1
South Woodford	1730-1800	969	1
South Woodford	1800-1830	1011	1
South Woodford	1830-1900	937	1
South Woodford	1900-1930	694	1
South Woodford	1930-2000	491	1
South Woodford	2000-2030	361	1
South Woodford	2030-2100	325	1
South Woodford	2100-2130	265	1
South Woodford	2130-2200	232	1
South Woodford	2200-2230	229	1
South Woodford	2230-2300	235	1
South Woodford	2300-2330	202	1
South Woodford	2330-2400	159	1
South Woodford	0000-0030	113	1
South Woodford	0030-0100	61	1
South Woodford	0100-0130	29	1
South Woodford	0130-0200	14	1
South Woodford	0200-0230	0	0
South Woodford	0230-0300	0	0
South Woodford	0300-0330	0	0
South Woodford	0330-0400	0	0
South Woodford	0400-0430	0	0
Southfields	0430-0500	0	0
Southfields	0500-0530	20	1
Southfields	0530-0600	71	1
Southfields	0600-0630	193	1
Southfields	0630-0700	454	1
Southfields	0700-0730	882	1
Southfields	0730-0800	1414	1
Southfields	0800-0830	1560	1
Southfields	0830-0900	1082	1
Southfields	0900-0930	634	1
Southfields	0930-1000	398	1
Southfields	1000-1030	328	1
Southfields	1030-1100	293	1
Southfields	1100-1130	286	1
Southfields	1130-1200	277	1
Southfields	1200-1230	284	1
Southfields	1230-1300	287	1
Southfields	1300-1330	297	1
Southfields	1330-1400	307	1
Southfields	1400-1430	301	1
Southfields	1430-1500	317	1
Southfields	1500-1530	455	1
Southfields	1530-1600	497	1
Southfields	1600-1630	572	1
Southfields	1630-1700	662	1
Southfields	1700-1730	752	1
Southfields	1730-1800	919	1
Southfields	1800-1830	1029	1
Southfields	1830-1900	967	1
Southfields	1900-1930	749	1
Southfields	1930-2000	529	1
Southfields	2000-2030	376	1
Southfields	2030-2100	320	1
Southfields	2100-2130	294	1
Southfields	2130-2200	295	1
Southfields	2200-2230	254	1
Southfields	2230-2300	251	1
Southfields	2300-2330	214	1
Southfields	2330-2400	159	1
Southfields	0000-0030	113	1
Southfields	0030-0100	66	1
Southfields	0100-0130	14	1
Southfields	0130-0200	0	1
Southfields	0200-0230	0	0
Southfields	0230-0300	0	0
Southfields	0300-0330	0	0
Southfields	0330-0400	0	0
Southfields	0400-0430	0	0
Southgate	0430-0500	0	0
Southgate	0500-0530	56	1
Southgate	0530-0600	93	1
Southgate	0600-0630	245	1
Southgate	0630-0700	428	1
Southgate	0700-0730	655	1
Southgate	0730-0800	967	1
Southgate	0800-0830	1125	1
Southgate	0830-0900	923	1
Southgate	0900-0930	691	1
Southgate	0930-1000	438	1
Southgate	1000-1030	361	1
Southgate	1030-1100	328	1
Southgate	1100-1130	315	1
Southgate	1130-1200	300	1
Southgate	1200-1230	319	1
Southgate	1230-1300	317	1
Southgate	1300-1330	329	1
Southgate	1330-1400	322	1
Southgate	1400-1430	334	1
Southgate	1430-1500	359	1
Southgate	1500-1530	443	1
Southgate	1530-1600	479	1
Southgate	1600-1630	517	1
Southgate	1630-1700	629	1
Southgate	1700-1730	760	1
Southgate	1730-1800	860	1
Southgate	1800-1830	875	1
Southgate	1830-1900	798	1
Southgate	1900-1930	636	1
Southgate	1930-2000	494	1
Southgate	2000-2030	350	1
Southgate	2030-2100	295	1
Southgate	2100-2130	267	1
Southgate	2130-2200	236	1
Southgate	2200-2230	245	1
Southgate	2230-2300	232	1
Southgate	2300-2330	199	1
Southgate	2330-2400	165	1
Southgate	0000-0030	116	1
Southgate	0030-0100	73	1
Southgate	0100-0130	25	1
Southgate	0130-0200	9	1
Southgate	0200-0230	0	0
Southgate	0230-0300	0	0
Southgate	0300-0330	0	0
Southgate	0330-0400	0	0
Southgate	0400-0430	0	0
Southwark	0430-0500	0	0
Southwark	0500-0530	41	1
Southwark	0530-0600	184	1
Southwark	0600-0630	382	1
Southwark	0630-0700	796	1
Southwark	0700-0730	1457	1
Southwark	0730-0800	2375	1
Southwark	0800-0830	3151	1
Southwark	0830-0900	4439	1
Southwark	0900-0930	4064	1
Southwark	0930-1000	2445	1
Southwark	1000-1030	1375	1
Southwark	1030-1100	1042	1
Southwark	1100-1130	889	1
Southwark	1130-1200	948	1
Southwark	1200-1230	996	1
Southwark	1230-1300	1056	1
Southwark	1300-1330	1075	1
Southwark	1330-1400	1101	1
Southwark	1400-1430	1045	1
Southwark	1430-1500	1080	1
Southwark	1500-1530	1161	1
Southwark	1530-1600	1499	1
Southwark	1600-1630	2035	1
Southwark	1630-1700	2462	1
Southwark	1700-1730	3335	1
Southwark	1730-1800	3749	1
Southwark	1800-1830	3097	1
Southwark	1830-1900	2131	1
Southwark	1900-1930	1477	1
Southwark	1930-2000	1044	1
Southwark	2000-2030	824	1
Southwark	2030-2100	691	1
Southwark	2100-2130	689	1
Southwark	2130-2200	618	1
Southwark	2200-2230	568	1
Southwark	2230-2300	518	1
Southwark	2300-2330	489	1
Southwark	2330-2400	351	1
Southwark	0000-0030	183	1
Southwark	0030-0100	81	1
Southwark	0100-0130	32	1
Southwark	0130-0200	12	1
Southwark	0200-0230	0	0
Southwark	0230-0300	0	0
Southwark	0300-0330	0	0
Southwark	0330-0400	0	0
Southwark	0400-0430	0	0
St. James's Park	0430-0500	0	0
St. James's Park	0500-0530	9	1
St. James's Park	0530-0600	82	1
St. James's Park	0600-0630	196	1
St. James's Park	0630-0700	510	1
St. James's Park	0700-0730	969	1
St. James's Park	0730-0800	1906	1
St. James's Park	0800-0830	2687	1
St. James's Park	0830-0900	3604	1
St. James's Park	0900-0930	3659	1
St. James's Park	0930-1000	2638	1
St. James's Park	1000-1030	1636	1
St. James's Park	1030-1100	1212	1
St. James's Park	1100-1130	975	1
St. James's Park	1130-1200	1083	1
St. James's Park	1200-1230	1182	1
St. James's Park	1230-1300	1157	1
St. James's Park	1300-1330	1137	1
St. James's Park	1330-1400	1140	1
St. James's Park	1400-1430	1124	1
St. James's Park	1430-1500	1167	1
St. James's Park	1500-1530	1296	1
St. James's Park	1530-1600	1658	1
St. James's Park	1600-1630	2183	1
St. James's Park	1630-1700	2521	1
St. James's Park	1700-1730	3133	1
St. James's Park	1730-1800	3122	1
St. James's Park	1800-1830	2606	1
St. James's Park	1830-1900	1717	1
St. James's Park	1900-1930	1123	1
St. James's Park	1930-2000	522	1
St. James's Park	2000-2030	515	1
St. James's Park	2030-2100	424	1
St. James's Park	2100-2130	352	1
St. James's Park	2130-2200	321	1
St. James's Park	2200-2230	289	1
St. James's Park	2230-2300	252	1
St. James's Park	2300-2330	215	1
St. James's Park	2330-2400	134	1
St. James's Park	0000-0030	62	1
St. James's Park	0030-0100	14	1
St. James's Park	0100-0130	0	1
St. James's Park	0130-0200	0	1
St. James's Park	0200-0230	0	0
St. James's Park	0230-0300	0	0
St. James's Park	0300-0330	0	0
St. James's Park	0330-0400	0	0
St. James's Park	0400-0430	0	0
St. John's Wood	0430-0500	0	0
St. John's Wood	0500-0530	16	1
St. John's Wood	0530-0600	69	1
St. John's Wood	0600-0630	212	1
St. John's Wood	0630-0700	471	1
St. John's Wood	0700-0730	916	1
St. John's Wood	0730-0800	1449	1
St. John's Wood	0800-0830	1451	1
St. John's Wood	0830-0900	1406	1
St. John's Wood	0900-0930	1029	1
St. John's Wood	0930-1000	762	1
St. John's Wood	1000-1030	546	1
St. John's Wood	1030-1100	497	1
St. John's Wood	1100-1130	460	1
St. John's Wood	1130-1200	500	1
St. John's Wood	1200-1230	508	1
St. John's Wood	1230-1300	523	1
St. John's Wood	1300-1330	518	1
St. John's Wood	1330-1400	516	1
St. John's Wood	1400-1430	525	1
St. John's Wood	1430-1500	577	1
St. John's Wood	1500-1530	677	1
St. John's Wood	1530-1600	726	1
St. John's Wood	1600-1630	866	1
St. John's Wood	1630-1700	981	1
St. John's Wood	1700-1730	1126	1
St. John's Wood	1730-1800	1123	1
St. John's Wood	1800-1830	1128	1
St. John's Wood	1830-1900	994	1
St. John's Wood	1900-1930	789	1
St. John's Wood	1930-2000	625	1
St. John's Wood	2000-2030	521	1
St. John's Wood	2030-2100	427	1
St. John's Wood	2100-2130	356	1
St. John's Wood	2130-2200	296	1
St. John's Wood	2200-2230	283	1
St. John's Wood	2230-2300	280	1
St. John's Wood	2300-2330	253	1
St. John's Wood	2330-2400	179	1
St. John's Wood	0000-0030	100	1
St. John's Wood	0030-0100	37	1
St. John's Wood	0100-0130	10	1
St. John's Wood	0130-0200	9	1
St. John's Wood	0200-0230	0	0
St. John's Wood	0230-0300	0	0
St. John's Wood	0300-0330	0	0
St. John's Wood	0330-0400	0	0
St. John's Wood	0400-0430	0	0
St. Paul's	0430-0500	0	0
St. Paul's	0500-0530	0	1
St. Paul's	0530-0600	101	1
St. Paul's	0600-0630	365	1
St. Paul's	0630-0700	808	1
St. Paul's	0700-0730	1286	1
St. Paul's	0730-0800	2187	1
St. Paul's	0800-0830	3034	1
St. Paul's	0830-0900	3848	1
St. Paul's	0900-0930	3492	1
St. Paul's	0930-1000	2216	1
St. Paul's	1000-1030	1472	1
St. Paul's	1030-1100	1329	1
St. Paul's	1100-1130	1180	1
St. Paul's	1130-1200	1308	1
St. Paul's	1200-1230	1493	1
St. Paul's	1230-1300	1502	1
St. Paul's	1300-1330	1460	1
St. Paul's	1330-1400	1488	1
St. Paul's	1400-1430	1464	1
St. Paul's	1430-1500	1492	1
St. Paul's	1500-1530	1561	1
St. Paul's	1530-1600	1725	1
St. Paul's	1600-1630	2100	1
St. Paul's	1630-1700	2327	1
St. Paul's	1700-1730	3066	1
St. Paul's	1730-1800	3276	1
St. Paul's	1800-1830	2981	1
St. Paul's	1830-1900	2342	1
St. Paul's	1900-1930	1717	1
St. Paul's	1930-2000	1172	1
St. Paul's	2000-2030	883	1
St. Paul's	2030-2100	727	1
St. Paul's	2100-2130	631	1
St. Paul's	2130-2200	533	1
St. Paul's	2200-2230	504	1
St. Paul's	2230-2300	448	1
St. Paul's	2300-2330	392	1
St. Paul's	2330-2400	256	1
St. Paul's	0000-0030	162	1
St. Paul's	0030-0100	51	1
St. Paul's	0100-0130	35	1
St. Paul's	0130-0200	17	1
St. Paul's	0200-0230	0	0
St. Paul's	0230-0300	0	0
St. Paul's	0300-0330	0	0
St. Paul's	0330-0400	0	0
St. Paul's	0400-0430	0	0
Stamford Brook	0430-0500	0	0
Stamford Brook	0500-0530	10	1
Stamford Brook	0530-0600	27	1
Stamford Brook	0600-0630	60	1
Stamford Brook	0630-0700	113	1
Stamford Brook	0700-0730	265	1
Stamford Brook	0730-0800	516	1
Stamford Brook	0800-0830	610	1
Stamford Brook	0830-0900	548	1
Stamford Brook	0900-0930	392	1
Stamford Brook	0930-1000	234	1
Stamford Brook	1000-1030	169	1
Stamford Brook	1030-1100	146	1
Stamford Brook	1100-1130	135	1
Stamford Brook	1130-1200	137	1
Stamford Brook	1200-1230	152	1
Stamford Brook	1230-1300	149	1
Stamford Brook	1300-1330	150	1
Stamford Brook	1330-1400	142	1
Stamford Brook	1400-1430	139	1
Stamford Brook	1430-1500	143	1
Stamford Brook	1500-1530	163	1
Stamford Brook	1530-1600	198	1
Stamford Brook	1600-1630	253	1
Stamford Brook	1630-1700	312	1
Stamford Brook	1700-1730	385	1
Stamford Brook	1730-1800	463	1
Stamford Brook	1800-1830	495	1
Stamford Brook	1830-1900	432	1
Stamford Brook	1900-1930	335	1
Stamford Brook	1930-2000	241	1
Stamford Brook	2000-2030	199	1
Stamford Brook	2030-2100	146	1
Stamford Brook	2100-2130	136	1
Stamford Brook	2130-2200	133	1
Stamford Brook	2200-2230	132	1
Stamford Brook	2230-2300	119	1
Stamford Brook	2300-2330	104	1
Stamford Brook	2330-2400	76	1
Stamford Brook	0000-0030	43	1
Stamford Brook	0030-0100	20	1
Stamford Brook	0100-0130	4	1
Stamford Brook	0130-0200	0	1
Stamford Brook	0200-0230	0	0
Stamford Brook	0230-0300	0	0
Stamford Brook	0300-0330	0	0
Stamford Brook	0330-0400	0	0
Stamford Brook	0400-0430	0	0
Stanmore	0430-0500	0	0
Stanmore	0500-0530	43	1
Stanmore	0530-0600	107	1
Stanmore	0600-0630	267	1
Stanmore	0630-0700	396	1
Stanmore	0700-0730	578	1
Stanmore	0730-0800	847	1
Stanmore	0800-0830	861	1
Stanmore	0830-0900	576	1
Stanmore	0900-0930	360	1
Stanmore	0930-1000	259	1
Stanmore	1000-1030	210	1
Stanmore	1030-1100	195	1
Stanmore	1100-1130	178	1
Stanmore	1130-1200	169	1
Stanmore	1200-1230	171	1
Stanmore	1230-1300	179	1
Stanmore	1300-1330	188	1
Stanmore	1330-1400	203	1
Stanmore	1400-1430	192	1
Stanmore	1430-1500	219	1
Stanmore	1500-1530	244	1
Stanmore	1530-1600	341	1
Stanmore	1600-1630	425	1
Stanmore	1630-1700	458	1
Stanmore	1700-1730	548	1
Stanmore	1730-1800	604	1
Stanmore	1800-1830	668	1
Stanmore	1830-1900	592	1
Stanmore	1900-1930	467	1
Stanmore	1930-2000	316	1
Stanmore	2000-2030	242	1
Stanmore	2030-2100	178	1
Stanmore	2100-2130	152	1
Stanmore	2130-2200	143	1
Stanmore	2200-2230	143	1
Stanmore	2230-2300	148	1
Stanmore	2300-2330	150	1
Stanmore	2330-2400	124	1
Stanmore	0000-0030	75	1
Stanmore	0030-0100	41	1
Stanmore	0100-0130	21	1
Stanmore	0130-0200	11	1
Stanmore	0200-0230	0	0
Stanmore	0230-0300	0	0
Stanmore	0300-0330	0	0
Stanmore	0330-0400	0	0
Stanmore	0400-0430	0	0
Stepney Green	0430-0500	0	0
Stepney Green	0500-0530	32	1
Stepney Green	0530-0600	97	1
Stepney Green	0600-0630	168	1
Stepney Green	0630-0700	295	1
Stepney Green	0700-0730	449	1
Stepney Green	0730-0800	731	1
Stepney Green	0800-0830	1056	1
Stepney Green	0830-0900	1130	1
Stepney Green	0900-0930	887	1
Stepney Green	0930-1000	653	1
Stepney Green	1000-1030	504	1
Stepney Green	1030-1100	473	1
Stepney Green	1100-1130	433	1
Stepney Green	1130-1200	409	1
Stepney Green	1200-1230	417	1
Stepney Green	1230-1300	432	1
Stepney Green	1300-1330	442	1
Stepney Green	1330-1400	448	1
Stepney Green	1400-1430	455	1
Stepney Green	1430-1500	473	1
Stepney Green	1500-1530	540	1
Stepney Green	1530-1600	602	1
Stepney Green	1600-1630	689	1
Stepney Green	1630-1700	751	1
Stepney Green	1700-1730	911	1
Stepney Green	1730-1800	924	1
Stepney Green	1800-1830	924	1
Stepney Green	1830-1900	807	1
Stepney Green	1900-1930	673	1
Stepney Green	1930-2000	544	1
Stepney Green	2000-2030	492	1
Stepney Green	2030-2100	438	1
Stepney Green	2100-2130	354	1
Stepney Green	2130-2200	319	1
Stepney Green	2200-2230	301	1
Stepney Green	2230-2300	288	1
Stepney Green	2300-2330	278	1
Stepney Green	2330-2400	240	1
Stepney Green	0000-0030	146	1
Stepney Green	0030-0100	68	1
Stepney Green	0100-0130	13	1
Stepney Green	0130-0200	0	1
Stepney Green	0200-0230	0	0
Stepney Green	0230-0300	0	0
Stepney Green	0300-0330	0	0
Stepney Green	0330-0400	0	0
Stepney Green	0400-0430	0	0
Stockwell	0430-0500	0	0
Stockwell	0500-0530	93	1
Stockwell	0530-0600	177	1
Stockwell	0600-0630	366	1
Stockwell	0630-0700	626	1
Stockwell	0700-0730	1132	1
Stockwell	0730-0800	1914	1
Stockwell	0800-0830	3241	1
Stockwell	0830-0900	3137	1
Stockwell	0900-0930	1761	1
Stockwell	0930-1000	1033	1
Stockwell	1000-1030	636	1
Stockwell	1030-1100	532	1
Stockwell	1100-1130	491	1
Stockwell	1130-1200	500	1
Stockwell	1200-1230	502	1
Stockwell	1230-1300	515	1
Stockwell	1300-1330	518	1
Stockwell	1330-1400	523	1
Stockwell	1400-1430	538	1
Stockwell	1430-1500	570	1
Stockwell	1500-1530	636	1
Stockwell	1530-1600	712	1
Stockwell	1600-1630	841	1
Stockwell	1630-1700	1002	1
Stockwell	1700-1730	1274	1
Stockwell	1730-1800	1588	1
Stockwell	1800-1830	1702	1
Stockwell	1830-1900	1582	1
Stockwell	1900-1930	1254	1
Stockwell	1930-2000	971	1
Stockwell	2000-2030	784	1
Stockwell	2030-2100	686	1
Stockwell	2100-2130	647	1
Stockwell	2130-2200	586	1
Stockwell	2200-2230	592	1
Stockwell	2230-2300	618	1
Stockwell	2300-2330	523	1
Stockwell	2330-2400	420	1
Stockwell	0000-0030	292	1
Stockwell	0030-0100	173	1
Stockwell	0100-0130	59	1
Stockwell	0130-0200	32	1
Stockwell	0200-0230	0	0
Stockwell	0230-0300	0	0
Stockwell	0300-0330	0	0
Stockwell	0330-0400	0	0
Stockwell	0400-0430	0	0
Stonebridge Park	0430-0500	0	0
Stonebridge Park	0500-0530	31	1
Stonebridge Park	0530-0600	115	1
Stonebridge Park	0600-0630	208	1
Stonebridge Park	0630-0700	334	1
Stonebridge Park	0700-0730	401	1
Stonebridge Park	0730-0800	453	1
Stonebridge Park	0800-0830	513	1
Stonebridge Park	0830-0900	420	1
Stonebridge Park	0900-0930	269	1
Stonebridge Park	0930-1000	174	1
Stonebridge Park	1000-1030	147	1
Stonebridge Park	1030-1100	129	1
Stonebridge Park	1100-1130	120	1
Stonebridge Park	1130-1200	112	1
Stonebridge Park	1200-1230	113	1
Stonebridge Park	1230-1300	120	1
Stonebridge Park	1300-1330	135	1
Stonebridge Park	1330-1400	143	1
Stonebridge Park	1400-1430	151	1
Stonebridge Park	1430-1500	156	1
Stonebridge Park	1500-1530	172	1
Stonebridge Park	1530-1600	238	1
Stonebridge Park	1600-1630	284	1
Stonebridge Park	1630-1700	329	1
Stonebridge Park	1700-1730	401	1
Stonebridge Park	1730-1800	460	1
Stonebridge Park	1800-1830	428	1
Stonebridge Park	1830-1900	356	1
Stonebridge Park	1900-1930	261	1
Stonebridge Park	1930-2000	181	1
Stonebridge Park	2000-2030	146	1
Stonebridge Park	2030-2100	116	1
Stonebridge Park	2100-2130	105	1
Stonebridge Park	2130-2200	108	1
Stonebridge Park	2200-2230	107	1
Stonebridge Park	2230-2300	82	1
Stonebridge Park	2300-2330	69	1
Stonebridge Park	2330-2400	61	1
Stonebridge Park	0000-0030	41	1
Stonebridge Park	0030-0100	28	1
Stonebridge Park	0100-0130	0	1
Stonebridge Park	0130-0200	0	1
Stonebridge Park	0200-0230	0	0
Stonebridge Park	0230-0300	0	0
Stonebridge Park	0300-0330	0	0
Stonebridge Park	0330-0400	0	0
Stonebridge Park	0400-0430	0	0
Stratford	0430-0500	0	0
Stratford	0500-0530	556	1
Stratford	0530-0600	1218	1
Stratford	0600-0630	2644	1
Stratford	0630-0700	4549	1
Stratford	0700-0730	5484	1
Stratford	0730-0800	5414	1
Stratford	0800-0830	6790	1
Stratford	0830-0900	7115	1
Stratford	0900-0930	5524	1
Stratford	0930-1000	4484	1
Stratford	1000-1030	3721	1
Stratford	1030-1100	3619	1
Stratford	1100-1130	3642	1
Stratford	1130-1200	3780	1
Stratford	1200-1230	4049	1
Stratford	1230-1300	4332	1
Stratford	1300-1330	4502	1
Stratford	1330-1400	4587	1
Stratford	1400-1430	4729	1
Stratford	1430-1500	4865	1
Stratford	1500-1530	5106	1
Stratford	1530-1600	5771	1
Stratford	1600-1630	6759	1
Stratford	1630-1700	7719	1
Stratford	1700-1730	8767	1
Stratford	1730-1800	9373	1
Stratford	1800-1830	8978	1
Stratford	1830-1900	7868	1
Stratford	1900-1930	6163	1
Stratford	1930-2000	4807	1
Stratford	2000-2030	4094	1
Stratford	2030-2100	3650	1
Stratford	2100-2130	3290	1
Stratford	2130-2200	2667	1
Stratford	2200-2230	2459	1
Stratford	2230-2300	1989	1
Stratford	2300-2330	1761	1
Stratford	2330-2400	1370	1
Stratford	0000-0030	939	1
Stratford	0030-0100	586	1
Stratford	0100-0130	228	1
Stratford	0130-0200	79	1
Stratford	0200-0230	0	0
Stratford	0230-0300	0	0
Stratford	0300-0330	0	0
Stratford	0330-0400	0	0
Stratford	0400-0430	0	0
Sudbury Hill	0430-0500	0	0
Sudbury Hill	0500-0530	34	1
Sudbury Hill	0530-0600	78	1
Sudbury Hill	0600-0630	179	1
Sudbury Hill	0630-0700	266	1
Sudbury Hill	0700-0730	304	1
Sudbury Hill	0730-0800	356	1
Sudbury Hill	0800-0830	381	1
Sudbury Hill	0830-0900	267	1
Sudbury Hill	0900-0930	176	1
Sudbury Hill	0930-1000	118	1
Sudbury Hill	1000-1030	95	1
Sudbury Hill	1030-1100	82	1
Sudbury Hill	1100-1130	84	1
Sudbury Hill	1130-1200	81	1
Sudbury Hill	1200-1230	86	1
Sudbury Hill	1230-1300	90	1
Sudbury Hill	1300-1330	101	1
Sudbury Hill	1330-1400	100	1
Sudbury Hill	1400-1430	107	1
Sudbury Hill	1430-1500	124	1
Sudbury Hill	1500-1530	126	1
Sudbury Hill	1530-1600	181	1
Sudbury Hill	1600-1630	227	1
Sudbury Hill	1630-1700	227	1
Sudbury Hill	1700-1730	272	1
Sudbury Hill	1730-1800	356	1
Sudbury Hill	1800-1830	341	1
Sudbury Hill	1830-1900	281	1
Sudbury Hill	1900-1930	205	1
Sudbury Hill	1930-2000	143	1
Sudbury Hill	2000-2030	108	1
Sudbury Hill	2030-2100	89	1
Sudbury Hill	2100-2130	74	1
Sudbury Hill	2130-2200	67	1
Sudbury Hill	2200-2230	62	1
Sudbury Hill	2230-2300	49	1
Sudbury Hill	2300-2330	44	1
Sudbury Hill	2330-2400	38	1
Sudbury Hill	0000-0030	25	1
Sudbury Hill	0030-0100	13	1
Sudbury Hill	0100-0130	6	1
Sudbury Hill	0130-0200	0	1
Sudbury Hill	0200-0230	0	0
Sudbury Hill	0230-0300	0	0
Sudbury Hill	0300-0330	0	0
Sudbury Hill	0330-0400	0	0
Sudbury Hill	0400-0430	0	0
Sudbury Town	0430-0500	0	0
Sudbury Town	0500-0530	34	1
Sudbury Town	0530-0600	60	1
Sudbury Town	0600-0630	156	1
Sudbury Town	0630-0700	205	1
Sudbury Town	0700-0730	289	1
Sudbury Town	0730-0800	352	1
Sudbury Town	0800-0830	419	1
Sudbury Town	0830-0900	271	1
Sudbury Town	0900-0930	169	1
Sudbury Town	0930-1000	137	1
Sudbury Town	1000-1030	108	1
Sudbury Town	1030-1100	90	1
Sudbury Town	1100-1130	84	1
Sudbury Town	1130-1200	80	1
Sudbury Town	1200-1230	87	1
Sudbury Town	1230-1300	84	1
Sudbury Town	1300-1330	90	1
Sudbury Town	1330-1400	95	1
Sudbury Town	1400-1430	104	1
Sudbury Town	1430-1500	105	1
Sudbury Town	1500-1530	111	1
Sudbury Town	1530-1600	158	1
Sudbury Town	1600-1630	199	1
Sudbury Town	1630-1700	213	1
Sudbury Town	1700-1730	259	1
Sudbury Town	1730-1800	307	1
Sudbury Town	1800-1830	336	1
Sudbury Town	1830-1900	287	1
Sudbury Town	1900-1930	191	1
Sudbury Town	1930-2000	142	1
Sudbury Town	2000-2030	110	1
Sudbury Town	2030-2100	88	1
Sudbury Town	2100-2130	74	1
Sudbury Town	2130-2200	66	1
Sudbury Town	2200-2230	61	1
Sudbury Town	2230-2300	62	1
Sudbury Town	2300-2330	58	1
Sudbury Town	2330-2400	39	1
Sudbury Town	0000-0030	28	1
Sudbury Town	0030-0100	16	1
Sudbury Town	0100-0130	4	1
Sudbury Town	0130-0200	0	1
Sudbury Town	0200-0230	0	0
Sudbury Town	0230-0300	0	0
Sudbury Town	0300-0330	0	0
Sudbury Town	0330-0400	0	0
Sudbury Town	0400-0430	0	0
Swiss Cottage	0430-0500	0	0
Swiss Cottage	0500-0530	26	1
Swiss Cottage	0530-0600	66	1
Swiss Cottage	0600-0630	154	1
Swiss Cottage	0630-0700	387	1
Swiss Cottage	0700-0730	727	1
Swiss Cottage	0730-0800	1189	1
Swiss Cottage	0800-0830	1521	1
Swiss Cottage	0830-0900	1421	1
Swiss Cottage	0900-0930	1048	1
Swiss Cottage	0930-1000	819	1
Swiss Cottage	1000-1030	575	1
Swiss Cottage	1030-1100	490	1
Swiss Cottage	1100-1130	435	1
Swiss Cottage	1130-1200	430	1
Swiss Cottage	1200-1230	441	1
Swiss Cottage	1230-1300	475	1
Swiss Cottage	1300-1330	498	1
Swiss Cottage	1330-1400	510	1
Swiss Cottage	1400-1430	483	1
Swiss Cottage	1430-1500	511	1
Swiss Cottage	1500-1530	575	1
Swiss Cottage	1530-1600	694	1
Swiss Cottage	1600-1630	848	1
Swiss Cottage	1630-1700	984	1
Swiss Cottage	1700-1730	1068	1
Swiss Cottage	1730-1800	1117	1
Swiss Cottage	1800-1830	1185	1
Swiss Cottage	1830-1900	1115	1
Swiss Cottage	1900-1930	905	1
Swiss Cottage	1930-2000	660	1
Swiss Cottage	2000-2030	528	1
Swiss Cottage	2030-2100	437	1
Swiss Cottage	2100-2130	398	1
Swiss Cottage	2130-2200	430	1
Swiss Cottage	2200-2230	364	1
Swiss Cottage	2230-2300	344	1
Swiss Cottage	2300-2330	302	1
Swiss Cottage	2330-2400	227	1
Swiss Cottage	0000-0030	129	1
Swiss Cottage	0030-0100	59	1
Swiss Cottage	0100-0130	15	1
Swiss Cottage	0130-0200	12	1
Swiss Cottage	0200-0230	0	0
Swiss Cottage	0230-0300	0	0
Swiss Cottage	0300-0330	0	0
Swiss Cottage	0330-0400	0	0
Swiss Cottage	0400-0430	0	0
Temple	0430-0500	0	0
Temple	0500-0530	5	1
Temple	0530-0600	35	1
Temple	0600-0630	91	1
Temple	0630-0700	246	1
Temple	0700-0730	480	1
Temple	0730-0800	794	1
Temple	0800-0830	1196	1
Temple	0830-0900	1948	1
Temple	0900-0930	2008	1
Temple	0930-1000	1438	1
Temple	1000-1030	923	1
Temple	1030-1100	802	1
Temple	1100-1130	690	1
Temple	1130-1200	707	1
Temple	1200-1230	761	1
Temple	1230-1300	789	1
Temple	1300-1330	769	1
Temple	1330-1400	776	1
Temple	1400-1430	749	1
Temple	1430-1500	744	1
Temple	1500-1530	782	1
Temple	1530-1600	895	1
Temple	1600-1630	1098	1
Temple	1630-1700	1210	1
Temple	1700-1730	1749	1
Temple	1730-1800	2111	1
Temple	1800-1830	1991	1
Temple	1830-1900	1375	1
Temple	1900-1930	959	1
Temple	1930-2000	662	1
Temple	2000-2030	527	1
Temple	2030-2100	407	1
Temple	2100-2130	365	1
Temple	2130-2200	323	1
Temple	2200-2230	384	1
Temple	2230-2300	317	1
Temple	2300-2330	237	1
Temple	2330-2400	177	1
Temple	0000-0030	87	1
Temple	0030-0100	17	1
Temple	0100-0130	0	1
Temple	0130-0200	0	1
Temple	0200-0230	0	0
Temple	0230-0300	0	0
Temple	0300-0330	0	0
Temple	0330-0400	0	0
Temple	0400-0430	0	0
Theydon Bois	0430-0500	0	0
Theydon Bois	0500-0530	20	1
Theydon Bois	0530-0600	58	1
Theydon Bois	0600-0630	103	1
Theydon Bois	0630-0700	122	1
Theydon Bois	0700-0730	156	1
Theydon Bois	0730-0800	241	1
Theydon Bois	0800-0830	201	1
Theydon Bois	0830-0900	109	1
Theydon Bois	0900-0930	63	1
Theydon Bois	0930-1000	52	1
Theydon Bois	1000-1030	40	1
Theydon Bois	1030-1100	36	1
Theydon Bois	1100-1130	37	1
Theydon Bois	1130-1200	32	1
Theydon Bois	1200-1230	37	1
Theydon Bois	1230-1300	39	1
Theydon Bois	1300-1330	45	1
Theydon Bois	1330-1400	37	1
Theydon Bois	1400-1430	44	1
Theydon Bois	1430-1500	51	1
Theydon Bois	1500-1530	65	1
Theydon Bois	1530-1600	99	1
Theydon Bois	1600-1630	109	1
Theydon Bois	1630-1700	110	1
Theydon Bois	1700-1730	131	1
Theydon Bois	1730-1800	154	1
Theydon Bois	1800-1830	168	1
Theydon Bois	1830-1900	138	1
Theydon Bois	1900-1930	97	1
Theydon Bois	1930-2000	73	1
Theydon Bois	2000-2030	55	1
Theydon Bois	2030-2100	39	1
Theydon Bois	2100-2130	34	1
Theydon Bois	2130-2200	30	1
Theydon Bois	2200-2230	35	1
Theydon Bois	2230-2300	30	1
Theydon Bois	2300-2330	28	1
Theydon Bois	2330-2400	28	1
Theydon Bois	0000-0030	19	1
Theydon Bois	0030-0100	10	1
Theydon Bois	0100-0130	4	1
Theydon Bois	0130-0200	1	1
Theydon Bois	0200-0230	0	0
Theydon Bois	0230-0300	0	0
Theydon Bois	0300-0330	0	0
Theydon Bois	0330-0400	0	0
Theydon Bois	0400-0430	0	0
Tooting Bec	0430-0500	0	0
Tooting Bec	0500-0530	34	1
Tooting Bec	0530-0600	85	1
Tooting Bec	0600-0630	261	1
Tooting Bec	0630-0700	538	1
Tooting Bec	0700-0730	1033	1
Tooting Bec	0730-0800	1692	1
Tooting Bec	0800-0830	2113	1
Tooting Bec	0830-0900	1694	1
Tooting Bec	0900-0930	1024	1
Tooting Bec	0930-1000	584	1
Tooting Bec	1000-1030	407	1
Tooting Bec	1030-1100	350	1
Tooting Bec	1100-1130	354	1
Tooting Bec	1130-1200	342	1
Tooting Bec	1200-1230	347	1
Tooting Bec	1230-1300	356	1
Tooting Bec	1300-1330	351	1
Tooting Bec	1330-1400	350	1
Tooting Bec	1400-1430	341	1
Tooting Bec	1430-1500	361	1
Tooting Bec	1500-1530	412	1
Tooting Bec	1530-1600	483	1
Tooting Bec	1600-1630	554	1
Tooting Bec	1630-1700	713	1
Tooting Bec	1700-1730	888	1
Tooting Bec	1730-1800	1126	1
Tooting Bec	1800-1830	1340	1
Tooting Bec	1830-1900	1278	1
Tooting Bec	1900-1930	1088	1
Tooting Bec	1930-2000	810	1
Tooting Bec	2000-2030	618	1
Tooting Bec	2030-2100	526	1
Tooting Bec	2100-2130	458	1
Tooting Bec	2130-2200	434	1
Tooting Bec	2200-2230	422	1
Tooting Bec	2230-2300	409	1
Tooting Bec	2300-2330	384	1
Tooting Bec	2330-2400	309	1
Tooting Bec	0000-0030	223	1
Tooting Bec	0030-0100	116	1
Tooting Bec	0100-0130	44	1
Tooting Bec	0130-0200	22	1
Tooting Bec	0200-0230	0	0
Tooting Bec	0230-0300	0	0
Tooting Bec	0300-0330	0	0
Tooting Bec	0330-0400	0	0
Tooting Bec	0400-0430	0	0
Tooting Broadway	0430-0500	0	0
Tooting Broadway	0500-0530	117	1
Tooting Broadway	0530-0600	241	1
Tooting Broadway	0600-0630	620	1
Tooting Broadway	0630-0700	1155	1
Tooting Broadway	0700-0730	1797	1
Tooting Broadway	0730-0800	2631	1
Tooting Broadway	0800-0830	3343	1
Tooting Broadway	0830-0900	2903	1
Tooting Broadway	0900-0930	1962	1
Tooting Broadway	0930-1000	1265	1
Tooting Broadway	1000-1030	918	1
Tooting Broadway	1030-1100	827	1
Tooting Broadway	1100-1130	819	1
Tooting Broadway	1130-1200	800	1
Tooting Broadway	1200-1230	844	1
Tooting Broadway	1230-1300	887	1
Tooting Broadway	1300-1330	891	1
Tooting Broadway	1330-1400	910	1
Tooting Broadway	1400-1430	913	1
Tooting Broadway	1430-1500	982	1
Tooting Broadway	1500-1530	1102	1
Tooting Broadway	1530-1600	1246	1
Tooting Broadway	1600-1630	1461	1
Tooting Broadway	1630-1700	1822	1
Tooting Broadway	1700-1730	2181	1
Tooting Broadway	1730-1800	2485	1
Tooting Broadway	1800-1830	2592	1
Tooting Broadway	1830-1900	2310	1
Tooting Broadway	1900-1930	1883	1
Tooting Broadway	1930-2000	1414	1
Tooting Broadway	2000-2030	1127	1
Tooting Broadway	2030-2100	917	1
Tooting Broadway	2100-2130	834	1
Tooting Broadway	2130-2200	768	1
Tooting Broadway	2200-2230	708	1
Tooting Broadway	2230-2300	700	1
Tooting Broadway	2300-2330	642	1
Tooting Broadway	2330-2400	533	1
Tooting Broadway	0000-0030	363	1
Tooting Broadway	0030-0100	223	1
Tooting Broadway	0100-0130	80	1
Tooting Broadway	0130-0200	31	1
Tooting Broadway	0200-0230	0	0
Tooting Broadway	0230-0300	0	0
Tooting Broadway	0300-0330	0	0
Tooting Broadway	0330-0400	0	0
Tooting Broadway	0400-0430	0	0
Tottenham Court Road	0430-0500	0	0
Tottenham Court Road	0500-0530	5	1
Tottenham Court Road	0530-0600	165	1
Tottenham Court Road	0600-0630	406	1
Tottenham Court Road	0630-0700	902	1
Tottenham Court Road	0700-0730	1374	1
Tottenham Court Road	0730-0800	2183	1
Tottenham Court Road	0800-0830	3191	1
Tottenham Court Road	0830-0900	5247	1
Tottenham Court Road	0900-0930	5888	1
Tottenham Court Road	0930-1000	4502	1
Tottenham Court Road	1000-1030	2842	1
Tottenham Court Road	1030-1100	2457	1
Tottenham Court Road	1100-1130	2297	1
Tottenham Court Road	1130-1200	2463	1
Tottenham Court Road	1200-1230	2733	1
Tottenham Court Road	1230-1300	3036	1
Tottenham Court Road	1300-1330	3032	1
Tottenham Court Road	1330-1400	3104	1
Tottenham Court Road	1400-1430	3070	1
Tottenham Court Road	1430-1500	3200	1
Tottenham Court Road	1500-1530	3393	1
Tottenham Court Road	1530-1600	3689	1
Tottenham Court Road	1600-1630	4081	1
Tottenham Court Road	1630-1700	4749	1
Tottenham Court Road	1700-1730	5981	1
Tottenham Court Road	1730-1800	7517	1
Tottenham Court Road	1800-1830	8040	1
Tottenham Court Road	1830-1900	6619	1
Tottenham Court Road	1900-1930	4872	1
Tottenham Court Road	1930-2000	3467	1
Tottenham Court Road	2000-2030	2958	1
Tottenham Court Road	2030-2100	2654	1
Tottenham Court Road	2100-2130	2446	1
Tottenham Court Road	2130-2200	2230	1
Tottenham Court Road	2200-2230	3299	1
Tottenham Court Road	2230-2300	2604	1
Tottenham Court Road	2300-2330	2083	1
Tottenham Court Road	2330-2400	1622	1
Tottenham Court Road	0000-0030	979	1
Tottenham Court Road	0030-0100	336	1
Tottenham Court Road	0100-0130	196	1
Tottenham Court Road	0130-0200	103	1
Tottenham Court Road	0200-0230	0	0
Tottenham Court Road	0230-0300	0	0
Tottenham Court Road	0300-0330	0	0
Tottenham Court Road	0330-0400	0	0
Tottenham Court Road	0400-0430	0	0
Tottenham Hale	0430-0500	0	0
Tottenham Hale	0500-0530	48	1
Tottenham Hale	0530-0600	241	1
Tottenham Hale	0600-0630	606	1
Tottenham Hale	0630-0700	1113	1
Tottenham Hale	0700-0730	1560	1
Tottenham Hale	0730-0800	1981	1
Tottenham Hale	0800-0830	2375	1
Tottenham Hale	0830-0900	2151	1
Tottenham Hale	0900-0930	1684	1
Tottenham Hale	0930-1000	1212	1
Tottenham Hale	1000-1030	1000	1
Tottenham Hale	1030-1100	849	1
Tottenham Hale	1100-1130	750	1
Tottenham Hale	1130-1200	702	1
Tottenham Hale	1200-1230	726	1
Tottenham Hale	1230-1300	764	1
Tottenham Hale	1300-1330	802	1
Tottenham Hale	1330-1400	828	1
Tottenham Hale	1400-1430	835	1
Tottenham Hale	1430-1500	846	1
Tottenham Hale	1500-1530	953	1
Tottenham Hale	1530-1600	1119	1
Tottenham Hale	1600-1630	1439	1
Tottenham Hale	1630-1700	1677	1
Tottenham Hale	1700-1730	2025	1
Tottenham Hale	1730-1800	2259	1
Tottenham Hale	1800-1830	2135	1
Tottenham Hale	1830-1900	1758	1
Tottenham Hale	1900-1930	1363	1
Tottenham Hale	1930-2000	1019	1
Tottenham Hale	2000-2030	863	1
Tottenham Hale	2030-2100	779	1
Tottenham Hale	2100-2130	721	1
Tottenham Hale	2130-2200	638	1
Tottenham Hale	2200-2230	592	1
Tottenham Hale	2230-2300	602	1
Tottenham Hale	2300-2330	501	1
Tottenham Hale	2330-2400	372	1
Tottenham Hale	0000-0030	177	1
Tottenham Hale	0030-0100	83	1
Tottenham Hale	0100-0130	29	1
Tottenham Hale	0130-0200	14	1
Tottenham Hale	0200-0230	0	0
Tottenham Hale	0230-0300	0	0
Tottenham Hale	0300-0330	0	0
Tottenham Hale	0330-0400	0	0
Tottenham Hale	0400-0430	0	0
Totteridge & Whetstone	0430-0500	0	0
Totteridge & Whetstone	0500-0530	19	1
Totteridge & Whetstone	0530-0600	50	1
Totteridge & Whetstone	0600-0630	112	1
Totteridge & Whetstone	0630-0700	212	1
Totteridge & Whetstone	0700-0730	389	1
Totteridge & Whetstone	0730-0800	602	1
Totteridge & Whetstone	0800-0830	693	1
Totteridge & Whetstone	0830-0900	475	1
Totteridge & Whetstone	0900-0930	314	1
Totteridge & Whetstone	0930-1000	199	1
Totteridge & Whetstone	1000-1030	141	1
Totteridge & Whetstone	1030-1100	118	1
Totteridge & Whetstone	1100-1130	115	1
Totteridge & Whetstone	1130-1200	114	1
Totteridge & Whetstone	1200-1230	115	1
Totteridge & Whetstone	1230-1300	115	1
Totteridge & Whetstone	1300-1330	125	1
Totteridge & Whetstone	1330-1400	127	1
Totteridge & Whetstone	1400-1430	132	1
Totteridge & Whetstone	1430-1500	133	1
Totteridge & Whetstone	1500-1530	150	1
Totteridge & Whetstone	1530-1600	183	1
Totteridge & Whetstone	1600-1630	239	1
Totteridge & Whetstone	1630-1700	291	1
Totteridge & Whetstone	1700-1730	362	1
Totteridge & Whetstone	1730-1800	412	1
Totteridge & Whetstone	1800-1830	458	1
Totteridge & Whetstone	1830-1900	400	1
Totteridge & Whetstone	1900-1930	303	1
Totteridge & Whetstone	1930-2000	222	1
Totteridge & Whetstone	2000-2030	167	1
Totteridge & Whetstone	2030-2100	129	1
Totteridge & Whetstone	2100-2130	119	1
Totteridge & Whetstone	2130-2200	109	1
Totteridge & Whetstone	2200-2230	106	1
Totteridge & Whetstone	2230-2300	110	1
Totteridge & Whetstone	2300-2330	92	1
Totteridge & Whetstone	2330-2400	70	1
Totteridge & Whetstone	0000-0030	55	1
Totteridge & Whetstone	0030-0100	33	1
Totteridge & Whetstone	0100-0130	10	1
Totteridge & Whetstone	0130-0200	4	1
Totteridge & Whetstone	0200-0230	0	0
Totteridge & Whetstone	0230-0300	0	0
Totteridge & Whetstone	0300-0330	0	0
Totteridge & Whetstone	0330-0400	0	0
Totteridge & Whetstone	0400-0430	0	0
Tower Hill	0430-0500	0	0
Tower Hill	0500-0530	47	1
Tower Hill	0530-0600	131	1
Tower Hill	0600-0630	454	1
Tower Hill	0630-0700	1064	1
Tower Hill	0700-0730	1594	1
Tower Hill	0730-0800	2218	1
Tower Hill	0800-0830	3262	1
Tower Hill	0830-0900	4084	1
Tower Hill	0900-0930	3408	1
Tower Hill	0930-1000	2254	1
Tower Hill	1000-1030	1631	1
Tower Hill	1030-1100	1547	1
Tower Hill	1100-1130	1385	1
Tower Hill	1130-1200	1425	1
Tower Hill	1200-1230	1491	1
Tower Hill	1230-1300	1465	1
Tower Hill	1300-1330	1433	1
Tower Hill	1330-1400	1489	1
Tower Hill	1400-1430	1512	1
Tower Hill	1430-1500	1629	1
Tower Hill	1500-1530	1752	1
Tower Hill	1530-1600	2015	1
Tower Hill	1600-1630	2498	1
Tower Hill	1630-1700	2975	1
Tower Hill	1700-1730	3678	1
Tower Hill	1730-1800	4029	1
Tower Hill	1800-1830	3469	1
Tower Hill	1830-1900	2528	1
Tower Hill	1900-1930	1671	1
Tower Hill	1930-2000	1214	1
Tower Hill	2000-2030	993	1
Tower Hill	2030-2100	803	1
Tower Hill	2100-2130	384	1
Tower Hill	2130-2200	341	1
Tower Hill	2200-2230	360	1
Tower Hill	2230-2300	400	1
Tower Hill	2300-2330	309	1
Tower Hill	2330-2400	192	1
Tower Hill	0000-0030	90	1
Tower Hill	0030-0100	29	1
Tower Hill	0100-0130	3	1
Tower Hill	0130-0200	0	1
Tower Hill	0200-0230	0	0
Tower Hill	0230-0300	0	0
Tower Hill	0300-0330	0	0
Tower Hill	0330-0400	0	0
Tower Hill	0400-0430	0	0
Tufnell Park	0430-0500	0	0
Tufnell Park	0500-0530	6	1
Tufnell Park	0530-0600	34	1
Tufnell Park	0600-0630	76	1
Tufnell Park	0630-0700	148	1
Tufnell Park	0700-0730	295	1
Tufnell Park	0730-0800	542	1
Tufnell Park	0800-0830	819	1
Tufnell Park	0830-0900	768	1
Tufnell Park	0900-0930	582	1
Tufnell Park	0930-1000	388	1
Tufnell Park	1000-1030	279	1
Tufnell Park	1030-1100	233	1
Tufnell Park	1100-1130	218	1
Tufnell Park	1130-1200	206	1
Tufnell Park	1200-1230	202	1
Tufnell Park	1230-1300	214	1
Tufnell Park	1300-1330	237	1
Tufnell Park	1330-1400	230	1
Tufnell Park	1400-1430	214	1
Tufnell Park	1430-1500	222	1
Tufnell Park	1500-1530	264	1
Tufnell Park	1530-1600	292	1
Tufnell Park	1600-1630	335	1
Tufnell Park	1630-1700	384	1
Tufnell Park	1700-1730	434	1
Tufnell Park	1730-1800	551	1
Tufnell Park	1800-1830	625	1
Tufnell Park	1830-1900	623	1
Tufnell Park	1900-1930	516	1
Tufnell Park	1930-2000	414	1
Tufnell Park	2000-2030	321	1
Tufnell Park	2030-2100	273	1
Tufnell Park	2100-2130	252	1
Tufnell Park	2130-2200	243	1
Tufnell Park	2200-2230	251	1
Tufnell Park	2230-2300	293	1
Tufnell Park	2300-2330	256	1
Tufnell Park	2330-2400	177	1
Tufnell Park	0000-0030	105	1
Tufnell Park	0030-0100	52	1
Tufnell Park	0100-0130	17	1
Tufnell Park	0130-0200	10	1
Tufnell Park	0200-0230	0	0
Tufnell Park	0230-0300	0	0
Tufnell Park	0300-0330	0	0
Tufnell Park	0330-0400	0	0
Tufnell Park	0400-0430	0	0
Turnham Green	0430-0500	0	0
Turnham Green	0500-0530	19	1
Turnham Green	0530-0600	60	1
Turnham Green	0600-0630	160	1
Turnham Green	0630-0700	309	1
Turnham Green	0700-0730	615	1
Turnham Green	0730-0800	1122	1
Turnham Green	0800-0830	1301	1
Turnham Green	0830-0900	1023	1
Turnham Green	0900-0930	756	1
Turnham Green	0930-1000	513	1
Turnham Green	1000-1030	394	1
Turnham Green	1030-1100	316	1
Turnham Green	1100-1130	320	1
Turnham Green	1130-1200	340	1
Turnham Green	1200-1230	345	1
Turnham Green	1230-1300	338	1
Turnham Green	1300-1330	349	1
Turnham Green	1330-1400	339	1
Turnham Green	1400-1430	342	1
Turnham Green	1430-1500	364	1
Turnham Green	1500-1530	407	1
Turnham Green	1530-1600	477	1
Turnham Green	1600-1630	657	1
Turnham Green	1630-1700	711	1
Turnham Green	1700-1730	831	1
Turnham Green	1730-1800	987	1
Turnham Green	1800-1830	1111	1
Turnham Green	1830-1900	951	1
Turnham Green	1900-1930	811	1
Turnham Green	1930-2000	535	1
Turnham Green	2000-2030	397	1
Turnham Green	2030-2100	331	1
Turnham Green	2100-2130	315	1
Turnham Green	2130-2200	303	1
Turnham Green	2200-2230	314	1
Turnham Green	2230-2300	334	1
Turnham Green	2300-2330	292	1
Turnham Green	2330-2400	204	1
Turnham Green	0000-0030	126	1
Turnham Green	0030-0100	58	1
Turnham Green	0100-0130	20	1
Turnham Green	0130-0200	11	1
Turnham Green	0200-0230	0	0
Turnham Green	0230-0300	0	0
Turnham Green	0300-0330	0	0
Turnham Green	0330-0400	0	0
Turnham Green	0400-0430	0	0
Turnpike Lane	0430-0500	0	0
Turnpike Lane	0500-0530	119	1
Turnpike Lane	0530-0600	292	1
Turnpike Lane	0600-0630	571	1
Turnpike Lane	0630-0700	927	1
Turnpike Lane	0700-0730	1122	1
Turnpike Lane	0730-0800	1291	1
Turnpike Lane	0800-0830	1658	1
Turnpike Lane	0830-0900	1446	1
Turnpike Lane	0900-0930	1177	1
Turnpike Lane	0930-1000	819	1
Turnpike Lane	1000-1030	660	1
Turnpike Lane	1030-1100	602	1
Turnpike Lane	1100-1130	594	1
Turnpike Lane	1130-1200	550	1
Turnpike Lane	1200-1230	555	1
Turnpike Lane	1230-1300	569	1
Turnpike Lane	1300-1330	594	1
Turnpike Lane	1330-1400	607	1
Turnpike Lane	1400-1430	622	1
Turnpike Lane	1430-1500	672	1
Turnpike Lane	1500-1530	745	1
Turnpike Lane	1530-1600	817	1
Turnpike Lane	1600-1630	973	1
Turnpike Lane	1630-1700	1174	1
Turnpike Lane	1700-1730	1375	1
Turnpike Lane	1730-1800	1572	1
Turnpike Lane	1800-1830	1588	1
Turnpike Lane	1830-1900	1484	1
Turnpike Lane	1900-1930	1201	1
Turnpike Lane	1930-2000	895	1
Turnpike Lane	2000-2030	709	1
Turnpike Lane	2030-2100	644	1
Turnpike Lane	2100-2130	578	1
Turnpike Lane	2130-2200	556	1
Turnpike Lane	2200-2230	538	1
Turnpike Lane	2230-2300	540	1
Turnpike Lane	2300-2330	491	1
Turnpike Lane	2330-2400	469	1
Turnpike Lane	0000-0030	343	1
Turnpike Lane	0030-0100	204	1
Turnpike Lane	0100-0130	48	1
Turnpike Lane	0130-0200	24	1
Turnpike Lane	0200-0230	0	0
Turnpike Lane	0230-0300	0	0
Turnpike Lane	0300-0330	0	0
Turnpike Lane	0330-0400	0	0
Turnpike Lane	0400-0430	0	0
Upminster	0430-0500	6	1
Upminster	0500-0530	37	1
Upminster	0530-0600	204	1
Upminster	0600-0630	418	1
Upminster	0630-0700	668	1
Upminster	0700-0730	1060	1
Upminster	0730-0800	1363	1
Upminster	0800-0830	1564	1
Upminster	0830-0900	787	1
Upminster	0900-0930	406	1
Upminster	0930-1000	332	1
Upminster	1000-1030	255	1
Upminster	1030-1100	219	1
Upminster	1100-1130	268	1
Upminster	1130-1200	213	1
Upminster	1200-1230	222	1
Upminster	1230-1300	222	1
Upminster	1300-1330	224	1
Upminster	1330-1400	292	1
Upminster	1400-1430	220	1
Upminster	1430-1500	319	1
Upminster	1500-1530	365	1
Upminster	1530-1600	486	1
Upminster	1600-1630	492	1
Upminster	1630-1700	685	1
Upminster	1700-1730	847	1
Upminster	1730-1800	1265	1
Upminster	1800-1830	1215	1
Upminster	1830-1900	908	1
Upminster	1900-1930	578	1
Upminster	1930-2000	462	1
Upminster	2000-2030	263	1
Upminster	2030-2100	234	1
Upminster	2100-2130	207	1
Upminster	2130-2200	175	1
Upminster	2200-2230	235	1
Upminster	2230-2300	181	1
Upminster	2300-2330	186	1
Upminster	2330-2400	178	1
Upminster	0000-0030	92	1
Upminster	0030-0100	28	1
Upminster	0100-0130	12	1
Upminster	0130-0200	0	1
Upminster	0200-0230	0	0
Upminster	0230-0300	0	0
Upminster	0300-0330	0	0
Upminster	0330-0400	0	0
Upminster	0400-0430	0	0
Upminster Bridge	0430-0500	0	0
Upminster Bridge	0500-0530	17	1
Upminster Bridge	0530-0600	49	1
Upminster Bridge	0600-0630	105	1
Upminster Bridge	0630-0700	122	1
Upminster Bridge	0700-0730	192	1
Upminster Bridge	0730-0800	279	1
Upminster Bridge	0800-0830	450	1
Upminster Bridge	0830-0900	240	1
Upminster Bridge	0900-0930	146	1
Upminster Bridge	0930-1000	106	1
Upminster Bridge	1000-1030	93	1
Upminster Bridge	1030-1100	89	1
Upminster Bridge	1100-1130	55	1
Upminster Bridge	1130-1200	74	1
Upminster Bridge	1200-1230	39	1
Upminster Bridge	1230-1300	86	1
Upminster Bridge	1300-1330	73	1
Upminster Bridge	1330-1400	66	1
Upminster Bridge	1400-1430	74	1
Upminster Bridge	1430-1500	108	1
Upminster Bridge	1500-1530	76	1
Upminster Bridge	1530-1600	186	1
Upminster Bridge	1600-1630	148	1
Upminster Bridge	1630-1700	220	1
Upminster Bridge	1700-1730	130	1
Upminster Bridge	1730-1800	160	1
Upminster Bridge	1800-1830	172	1
Upminster Bridge	1830-1900	135	1
Upminster Bridge	1900-1930	80	1
Upminster Bridge	1930-2000	56	1
Upminster Bridge	2000-2030	39	1
Upminster Bridge	2030-2100	32	1
Upminster Bridge	2100-2130	28	1
Upminster Bridge	2130-2200	27	1
Upminster Bridge	2200-2230	24	1
Upminster Bridge	2230-2300	24	1
Upminster Bridge	2300-2330	27	1
Upminster Bridge	2330-2400	22	1
Upminster Bridge	0000-0030	13	1
Upminster Bridge	0030-0100	7	1
Upminster Bridge	0100-0130	2	1
Upminster Bridge	0130-0200	1	1
Upminster Bridge	0200-0230	0	0
Upminster Bridge	0230-0300	0	0
Upminster Bridge	0300-0330	0	0
Upminster Bridge	0330-0400	0	0
Upminster Bridge	0400-0430	0	0
Upney	0430-0500	0	0
Upney	0500-0530	78	1
Upney	0530-0600	150	1
Upney	0600-0630	322	1
Upney	0630-0700	378	1
Upney	0700-0730	373	1
Upney	0730-0800	476	1
Upney	0800-0830	551	1
Upney	0830-0900	434	1
Upney	0900-0930	316	1
Upney	0930-1000	210	1
Upney	1000-1030	172	1
Upney	1030-1100	149	1
Upney	1100-1130	140	1
Upney	1130-1200	136	1
Upney	1200-1230	128	1
Upney	1230-1300	134	1
Upney	1300-1330	143	1
Upney	1330-1400	145	1
Upney	1400-1430	155	1
Upney	1430-1500	183	1
Upney	1500-1530	213	1
Upney	1530-1600	245	1
Upney	1600-1630	282	1
Upney	1630-1700	338	1
Upney	1700-1730	414	1
Upney	1730-1800	442	1
Upney	1800-1830	465	1
Upney	1830-1900	365	1
Upney	1900-1930	271	1
Upney	1930-2000	195	1
Upney	2000-2030	142	1
Upney	2030-2100	122	1
Upney	2100-2130	107	1
Upney	2130-2200	94	1
Upney	2200-2230	77	1
Upney	2230-2300	69	1
Upney	2300-2330	66	1
Upney	2330-2400	57	1
Upney	0000-0030	36	1
Upney	0030-0100	23	1
Upney	0100-0130	8	1
Upney	0130-0200	0	1
Upney	0200-0230	0	0
Upney	0230-0300	0	0
Upney	0300-0330	0	0
Upney	0330-0400	0	0
Upney	0400-0430	0	0
Upton Park	0430-0500	0	0
Upton Park	0500-0530	187	1
Upton Park	0530-0600	391	1
Upton Park	0600-0630	867	1
Upton Park	0630-0700	1201	1
Upton Park	0700-0730	1199	1
Upton Park	0730-0800	1274	1
Upton Park	0800-0830	1486	1
Upton Park	0830-0900	1259	1
Upton Park	0900-0930	985	1
Upton Park	0930-1000	725	1
Upton Park	1000-1030	603	1
Upton Park	1030-1100	552	1
Upton Park	1100-1130	557	1
Upton Park	1130-1200	537	1
Upton Park	1200-1230	540	1
Upton Park	1230-1300	555	1
Upton Park	1300-1330	573	1
Upton Park	1330-1400	595	1
Upton Park	1400-1430	616	1
Upton Park	1430-1500	700	1
Upton Park	1500-1530	768	1
Upton Park	1530-1600	901	1
Upton Park	1600-1630	974	1
Upton Park	1630-1700	1145	1
Upton Park	1700-1730	1310	1
Upton Park	1730-1800	1468	1
Upton Park	1800-1830	1462	1
Upton Park	1830-1900	1279	1
Upton Park	1900-1930	968	1
Upton Park	1930-2000	760	1
Upton Park	2000-2030	590	1
Upton Park	2030-2100	488	1
Upton Park	2100-2130	414	1
Upton Park	2130-2200	370	1
Upton Park	2200-2230	323	1
Upton Park	2230-2300	294	1
Upton Park	2300-2330	276	1
Upton Park	2330-2400	252	1
Upton Park	0000-0030	165	1
Upton Park	0030-0100	107	1
Upton Park	0100-0130	38	1
Upton Park	0130-0200	0	1
Upton Park	0200-0230	0	0
Upton Park	0230-0300	0	0
Upton Park	0300-0330	0	0
Upton Park	0330-0400	0	0
Upton Park	0400-0430	0	0
Uxbridge	0430-0500	0	0
Uxbridge	0500-0530	47	1
Uxbridge	0530-0600	91	1
Uxbridge	0600-0630	299	1
Uxbridge	0630-0700	535	1
Uxbridge	0700-0730	825	1
Uxbridge	0730-0800	1217	1
Uxbridge	0800-0830	1447	1
Uxbridge	0830-0900	1570	1
Uxbridge	0900-0930	1072	1
Uxbridge	0930-1000	850	1
Uxbridge	1000-1030	670	1
Uxbridge	1030-1100	655	1
Uxbridge	1100-1130	601	1
Uxbridge	1130-1200	647	1
Uxbridge	1200-1230	638	1
Uxbridge	1230-1300	673	1
Uxbridge	1300-1330	675	1
Uxbridge	1330-1400	646	1
Uxbridge	1400-1430	642	1
Uxbridge	1430-1500	678	1
Uxbridge	1500-1530	732	1
Uxbridge	1530-1600	946	1
Uxbridge	1600-1630	1113	1
Uxbridge	1630-1700	1249	1
Uxbridge	1700-1730	1580	1
Uxbridge	1730-1800	1525	1
Uxbridge	1800-1830	1239	1
Uxbridge	1830-1900	1001	1
Uxbridge	1900-1930	763	1
Uxbridge	1930-2000	506	1
Uxbridge	2000-2030	411	1
Uxbridge	2030-2100	321	1
Uxbridge	2100-2130	270	1
Uxbridge	2130-2200	241	1
Uxbridge	2200-2230	226	1
Uxbridge	2230-2300	212	1
Uxbridge	2300-2330	188	1
Uxbridge	2330-2400	142	1
Uxbridge	0000-0030	106	1
Uxbridge	0030-0100	59	1
Uxbridge	0100-0130	34	1
Uxbridge	0130-0200	3	1
Uxbridge	0200-0230	0	0
Uxbridge	0230-0300	0	0
Uxbridge	0300-0330	0	0
Uxbridge	0330-0400	0	0
Uxbridge	0400-0430	0	0
Vauxhall	0430-0500	0	0
Vauxhall	0500-0530	71	1
Vauxhall	0530-0600	321	1
Vauxhall	0600-0630	1155	1
Vauxhall	0630-0700	2604	1
Vauxhall	0700-0730	3976	1
Vauxhall	0730-0800	4819	1
Vauxhall	0800-0830	5688	1
Vauxhall	0830-0900	6204	1
Vauxhall	0900-0930	4939	1
Vauxhall	0930-1000	3204	1
Vauxhall	1000-1030	2122	1
Vauxhall	1030-1100	1699	1
Vauxhall	1100-1130	1501	1
Vauxhall	1130-1200	1500	1
Vauxhall	1200-1230	1560	1
Vauxhall	1230-1300	1594	1
Vauxhall	1300-1330	1635	1
Vauxhall	1330-1400	1655	1
Vauxhall	1400-1430	1619	1
Vauxhall	1430-1500	1730	1
Vauxhall	1500-1530	1909	1
Vauxhall	1530-1600	2254	1
Vauxhall	1600-1630	2959	1
Vauxhall	1630-1700	3584	1
Vauxhall	1700-1730	4750	1
Vauxhall	1730-1800	5797	1
Vauxhall	1800-1830	5454	1
Vauxhall	1830-1900	4377	1
Vauxhall	1900-1930	3198	1
Vauxhall	1930-2000	2291	1
Vauxhall	2000-2030	1795	1
Vauxhall	2030-2100	1565	1
Vauxhall	2100-2130	1416	1
Vauxhall	2130-2200	1308	1
Vauxhall	2200-2230	1266	1
Vauxhall	2230-2300	1299	1
Vauxhall	2300-2330	1106	1
Vauxhall	2330-2400	821	1
Vauxhall	0000-0030	476	1
Vauxhall	0030-0100	165	1
Vauxhall	0100-0130	66	1
Vauxhall	0130-0200	34	1
Vauxhall	0200-0230	0	0
Vauxhall	0230-0300	0	0
Vauxhall	0300-0330	0	0
Vauxhall	0330-0400	0	0
Vauxhall	0400-0430	0	0
Victoria	0430-0500	0	0
Victoria	0500-0530	116	1
Victoria	0530-0600	626	1
Victoria	0600-0630	1667	1
Victoria	0630-0700	4249	1
Victoria	0700-0730	6408	1
Victoria	0730-0800	9399	1
Victoria	0800-0830	10840	1
Victoria	0830-0900	12321	1
Victoria	0900-0930	10822	1
Victoria	0930-1000	8152	1
Victoria	1000-1030	6342	1
Victoria	1030-1100	5750	1
Victoria	1100-1130	5181	1
Victoria	1130-1200	5231	1
Victoria	1200-1230	5460	1
Victoria	1230-1300	5527	1
Victoria	1300-1330	5574	1
Victoria	1330-1400	5557	1
Victoria	1400-1430	5563	1
Victoria	1430-1500	5763	1
Victoria	1500-1530	6315	1
Victoria	1530-1600	7165	1
Victoria	1600-1630	8780	1
Victoria	1630-1700	10022	1
Victoria	1700-1730	11741	1
Victoria	1730-1800	13248	1
Victoria	1800-1830	12503	1
Victoria	1830-1900	10284	1
Victoria	1900-1930	7627	1
Victoria	1930-2000	5550	1
Victoria	2000-2030	4667	1
Victoria	2030-2100	4112	1
Victoria	2100-2130	3867	1
Victoria	2130-2200	3514	1
Victoria	2200-2230	4039	1
Victoria	2230-2300	3667	1
Victoria	2300-2330	2848	1
Victoria	2330-2400	1898	1
Victoria	0000-0030	1002	1
Victoria	0030-0100	266	1
Victoria	0100-0130	90	1
Victoria	0130-0200	48	1
Victoria	0200-0230	0	0
Victoria	0230-0300	0	0
Victoria	0300-0330	0	0
Victoria	0330-0400	0	0
Victoria	0400-0430	0	0
Walthamstow Central	0430-0500	0	0
Walthamstow Central	0500-0530	92	1
Walthamstow Central	0530-0600	198	1
Walthamstow Central	0600-0630	451	1
Walthamstow Central	0630-0700	694	1
Walthamstow Central	0700-0730	979	1
Walthamstow Central	0730-0800	1209	1
Walthamstow Central	0800-0830	1647	1
Walthamstow Central	0830-0900	1459	1
Walthamstow Central	0900-0930	1063	1
Walthamstow Central	0930-1000	723	1
Walthamstow Central	1000-1030	495	1
Walthamstow Central	1030-1100	433	1
Walthamstow Central	1100-1130	446	1
Walthamstow Central	1130-1200	431	1
Walthamstow Central	1200-1230	444	1
Walthamstow Central	1230-1300	475	1
Walthamstow Central	1300-1330	497	1
Walthamstow Central	1330-1400	522	1
Walthamstow Central	1400-1430	539	1
Walthamstow Central	1430-1500	602	1
Walthamstow Central	1500-1530	649	1
Walthamstow Central	1530-1600	764	1
Walthamstow Central	1600-1630	952	1
Walthamstow Central	1630-1700	1204	1
Walthamstow Central	1700-1730	1430	1
Walthamstow Central	1730-1800	1702	1
Walthamstow Central	1800-1830	1643	1
Walthamstow Central	1830-1900	1500	1
Walthamstow Central	1900-1930	1147	1
Walthamstow Central	1930-2000	815	1
Walthamstow Central	2000-2030	625	1
Walthamstow Central	2030-2100	546	1
Walthamstow Central	2100-2130	459	1
Walthamstow Central	2130-2200	457	1
Walthamstow Central	2200-2230	420	1
Walthamstow Central	2230-2300	420	1
Walthamstow Central	2300-2330	383	1
Walthamstow Central	2330-2400	350	1
Walthamstow Central	0000-0030	239	1
Walthamstow Central	0030-0100	151	1
Walthamstow Central	0100-0130	63	1
Walthamstow Central	0130-0200	33	1
Walthamstow Central	0200-0230	0	0
Walthamstow Central	0230-0300	0	0
Walthamstow Central	0300-0330	0	0
Walthamstow Central	0330-0400	0	0
Walthamstow Central	0400-0430	0	0
Wanstead	0430-0500	0	0
Wanstead	0500-0530	17	1
Wanstead	0530-0600	68	1
Wanstead	0600-0630	103	1
Wanstead	0630-0700	179	1
Wanstead	0700-0730	318	1
Wanstead	0730-0800	554	1
Wanstead	0800-0830	739	1
Wanstead	0830-0900	561	1
Wanstead	0900-0930	347	1
Wanstead	0930-1000	229	1
Wanstead	1000-1030	178	1
Wanstead	1030-1100	167	1
Wanstead	1100-1130	164	1
Wanstead	1130-1200	158	1
Wanstead	1200-1230	163	1
Wanstead	1230-1300	159	1
Wanstead	1300-1330	165	1
Wanstead	1330-1400	167	1
Wanstead	1400-1430	158	1
Wanstead	1430-1500	178	1
Wanstead	1500-1530	200	1
Wanstead	1530-1600	260	1
Wanstead	1600-1630	264	1
Wanstead	1630-1700	322	1
Wanstead	1700-1730	387	1
Wanstead	1730-1800	469	1
Wanstead	1800-1830	480	1
Wanstead	1830-1900	429	1
Wanstead	1900-1930	332	1
Wanstead	1930-2000	242	1
Wanstead	2000-2030	187	1
Wanstead	2030-2100	158	1
Wanstead	2100-2130	133	1
Wanstead	2130-2200	127	1
Wanstead	2200-2230	125	1
Wanstead	2230-2300	120	1
Wanstead	2300-2330	116	1
Wanstead	2330-2400	89	1
Wanstead	0000-0030	53	1
Wanstead	0030-0100	28	1
Wanstead	0100-0130	11	1
Wanstead	0130-0200	2	1
Wanstead	0200-0230	0	0
Wanstead	0230-0300	0	0
Wanstead	0300-0330	0	0
Wanstead	0330-0400	0	0
Wanstead	0400-0430	0	0
Warren Street	0430-0500	0	0
Warren Street	0500-0530	20	1
Warren Street	0530-0600	126	1
Warren Street	0600-0630	272	1
Warren Street	0630-0700	698	1
Warren Street	0700-0730	1342	1
Warren Street	0730-0800	2514	1
Warren Street	0800-0830	3576	1
Warren Street	0830-0900	4604	1
Warren Street	0900-0930	4403	1
Warren Street	0930-1000	3159	1
Warren Street	1000-1030	1900	1
Warren Street	1030-1100	1596	1
Warren Street	1100-1130	1296	1
Warren Street	1130-1200	1236	1
Warren Street	1200-1230	1347	1
Warren Street	1230-1300	1452	1
Warren Street	1300-1330	1471	1
Warren Street	1330-1400	1465	1
Warren Street	1400-1430	1379	1
Warren Street	1430-1500	1367	1
Warren Street	1500-1530	1485	1
Warren Street	1530-1600	1768	1
Warren Street	1600-1630	2359	1
Warren Street	1630-1700	2815	1
Warren Street	1700-1730	4009	1
Warren Street	1730-1800	4451	1
Warren Street	1800-1830	4011	1
Warren Street	1830-1900	2962	1
Warren Street	1900-1930	2187	1
Warren Street	1930-2000	1613	1
Warren Street	2000-2030	1320	1
Warren Street	2030-2100	1126	1
Warren Street	2100-2130	1004	1
Warren Street	2130-2200	793	1
Warren Street	2200-2230	714	1
Warren Street	2230-2300	588	1
Warren Street	2300-2330	540	1
Warren Street	2330-2400	406	1
Warren Street	0000-0030	229	1
Warren Street	0030-0100	84	1
Warren Street	0100-0130	43	1
Warren Street	0130-0200	24	1
Warren Street	0200-0230	0	0
Warren Street	0230-0300	0	0
Warren Street	0300-0330	0	0
Warren Street	0330-0400	0	0
Warren Street	0400-0430	0	0
Warwick Avenue	0430-0500	0	0
Warwick Avenue	0500-0530	0	1
Warwick Avenue	0530-0600	28	1
Warwick Avenue	0600-0630	87	1
Warwick Avenue	0630-0700	206	1
Warwick Avenue	0700-0730	417	1
Warwick Avenue	0730-0800	692	1
Warwick Avenue	0800-0830	881	1
Warwick Avenue	0830-0900	871	1
Warwick Avenue	0900-0930	595	1
Warwick Avenue	0930-1000	397	1
Warwick Avenue	1000-1030	293	1
Warwick Avenue	1030-1100	254	1
Warwick Avenue	1100-1130	227	1
Warwick Avenue	1130-1200	236	1
Warwick Avenue	1200-1230	237	1
Warwick Avenue	1230-1300	240	1
Warwick Avenue	1300-1330	246	1
Warwick Avenue	1330-1400	239	1
Warwick Avenue	1400-1430	244	1
Warwick Avenue	1430-1500	255	1
Warwick Avenue	1500-1530	289	1
Warwick Avenue	1530-1600	315	1
Warwick Avenue	1600-1630	378	1
Warwick Avenue	1630-1700	448	1
Warwick Avenue	1700-1730	539	1
Warwick Avenue	1730-1800	614	1
Warwick Avenue	1800-1830	669	1
Warwick Avenue	1830-1900	619	1
Warwick Avenue	1900-1930	516	1
Warwick Avenue	1930-2000	392	1
Warwick Avenue	2000-2030	305	1
Warwick Avenue	2030-2100	252	1
Warwick Avenue	2100-2130	238	1
Warwick Avenue	2130-2200	211	1
Warwick Avenue	2200-2230	215	1
Warwick Avenue	2230-2300	213	1
Warwick Avenue	2300-2330	182	1
Warwick Avenue	2330-2400	132	1
Warwick Avenue	0000-0030	73	1
Warwick Avenue	0030-0100	29	1
Warwick Avenue	0100-0130	0	1
Warwick Avenue	0130-0200	0	1
Warwick Avenue	0200-0230	0	0
Warwick Avenue	0230-0300	0	0
Warwick Avenue	0300-0330	0	0
Warwick Avenue	0330-0400	0	0
Warwick Avenue	0400-0430	0	0
Waterloo	0430-0500	0	0
Waterloo	0500-0530	99	1
Waterloo	0530-0600	424	1
Waterloo	0600-0630	1707	1
Waterloo	0630-0700	5035	1
Waterloo	0700-0730	9902	1
Waterloo	0730-0800	14973	1
Waterloo	0800-0830	18562	1
Waterloo	0830-0900	18848	1
Waterloo	0900-0930	13311	1
Waterloo	0930-1000	8756	1
Waterloo	1000-1030	6337	1
Waterloo	1030-1100	5406	1
Waterloo	1100-1130	4629	1
Waterloo	1130-1200	4678	1
Waterloo	1200-1230	4887	1
Waterloo	1230-1300	4954	1
Waterloo	1300-1330	4945	1
Waterloo	1330-1400	4910	1
Waterloo	1400-1430	4870	1
Waterloo	1430-1500	5038	1
Waterloo	1500-1530	5521	1
Waterloo	1530-1600	6825	1
Waterloo	1600-1630	9153	1
Waterloo	1630-1700	11821	1
Waterloo	1700-1730	16361	1
Waterloo	1730-1800	19476	1
Waterloo	1800-1830	19009	1
Waterloo	1830-1900	15137	1
Waterloo	1900-1930	10742	1
Waterloo	1930-2000	7186	1
Waterloo	2000-2030	5451	1
Waterloo	2030-2100	4512	1
Waterloo	2100-2130	4074	1
Waterloo	2130-2200	3955	1
Waterloo	2200-2230	4195	1
Waterloo	2230-2300	3987	1
Waterloo	2300-2330	3374	1
Waterloo	2330-2400	2416	1
Waterloo	0000-0030	1146	1
Waterloo	0030-0100	369	1
Waterloo	0100-0130	114	1
Waterloo	0130-0200	56	1
Waterloo	0200-0230	0	0
Waterloo	0230-0300	0	0
Waterloo	0300-0330	0	0
Waterloo	0330-0400	0	0
Waterloo	0400-0430	0	0
Watford	0430-0500	0	0
Watford	0500-0530	31	1
Watford	0530-0600	56	1
Watford	0600-0630	141	1
Watford	0630-0700	207	1
Watford	0700-0730	327	1
Watford	0730-0800	545	1
Watford	0800-0830	560	1
Watford	0830-0900	283	1
Watford	0900-0930	145	1
Watford	0930-1000	107	1
Watford	1000-1030	78	1
Watford	1030-1100	75	1
Watford	1100-1130	80	1
Watford	1130-1200	69	1
Watford	1200-1230	69	1
Watford	1230-1300	74	1
Watford	1300-1330	97	1
Watford	1330-1400	89	1
Watford	1400-1430	90	1
Watford	1430-1500	82	1
Watford	1500-1530	259	1
Watford	1530-1600	242	1
Watford	1600-1630	209	1
Watford	1630-1700	241	1
Watford	1700-1730	245	1
Watford	1730-1800	267	1
Watford	1800-1830	294	1
Watford	1830-1900	283	1
Watford	1900-1930	219	1
Watford	1930-2000	153	1
Watford	2000-2030	112	1
Watford	2030-2100	84	1
Watford	2100-2130	70	1
Watford	2130-2200	59	1
Watford	2200-2230	57	1
Watford	2230-2300	52	1
Watford	2300-2330	49	1
Watford	2330-2400	37	1
Watford	0000-0030	27	1
Watford	0030-0100	14	1
Watford	0100-0130	2	1
Watford	0130-0200	0	1
Watford	0200-0230	0	0
Watford	0230-0300	0	0
Watford	0300-0330	0	0
Watford	0330-0400	0	0
Watford	0400-0430	0	0
Wembley Central	0430-0500	0	0
Wembley Central	0500-0530	58	1
Wembley Central	0530-0600	167	1
Wembley Central	0600-0630	335	1
Wembley Central	0630-0700	573	1
Wembley Central	0700-0730	700	1
Wembley Central	0730-0800	813	1
Wembley Central	0800-0830	907	1
Wembley Central	0830-0900	714	1
Wembley Central	0900-0930	562	1
Wembley Central	0930-1000	411	1
Wembley Central	1000-1030	410	1
Wembley Central	1030-1100	345	1
Wembley Central	1100-1130	362	1
Wembley Central	1130-1200	342	1
Wembley Central	1200-1230	363	1
Wembley Central	1230-1300	369	1
Wembley Central	1300-1330	418	1
Wembley Central	1330-1400	415	1
Wembley Central	1400-1430	441	1
Wembley Central	1430-1500	474	1
Wembley Central	1500-1530	499	1
Wembley Central	1530-1600	618	1
Wembley Central	1600-1630	670	1
Wembley Central	1630-1700	725	1
Wembley Central	1700-1730	869	1
Wembley Central	1730-1800	934	1
Wembley Central	1800-1830	980	1
Wembley Central	1830-1900	764	1
Wembley Central	1900-1930	647	1
Wembley Central	1930-2000	445	1
Wembley Central	2000-2030	379	1
Wembley Central	2030-2100	275	1
Wembley Central	2100-2130	230	1
Wembley Central	2130-2200	179	1
Wembley Central	2200-2230	176	1
Wembley Central	2230-2300	176	1
Wembley Central	2300-2330	163	1
Wembley Central	2330-2400	120	1
Wembley Central	0000-0030	76	1
Wembley Central	0030-0100	20	1
Wembley Central	0100-0130	0	1
Wembley Central	0130-0200	2	1
Wembley Central	0200-0230	0	0
Wembley Central	0230-0300	0	0
Wembley Central	0300-0330	0	0
Wembley Central	0330-0400	0	0
Wembley Central	0400-0430	0	0
Wembley Park	0430-0500	0	0
Wembley Park	0500-0530	108	1
Wembley Park	0530-0600	293	1
Wembley Park	0600-0630	701	1
Wembley Park	0630-0700	1261	1
Wembley Park	0700-0730	1772	1
Wembley Park	0730-0800	2127	1
Wembley Park	0800-0830	2781	1
Wembley Park	0830-0900	2304	1
Wembley Park	0900-0930	1635	1
Wembley Park	0930-1000	1255	1
Wembley Park	1000-1030	1022	1
Wembley Park	1030-1100	891	1
Wembley Park	1100-1130	850	1
Wembley Park	1130-1200	849	1
Wembley Park	1200-1230	874	1
Wembley Park	1230-1300	966	1
Wembley Park	1300-1330	997	1
Wembley Park	1330-1400	978	1
Wembley Park	1400-1430	998	1
Wembley Park	1430-1500	1066	1
Wembley Park	1500-1530	1195	1
Wembley Park	1530-1600	1398	1
Wembley Park	1600-1630	1775	1
Wembley Park	1630-1700	1976	1
Wembley Park	1700-1730	2481	1
Wembley Park	1730-1800	2703	1
Wembley Park	1800-1830	2613	1
Wembley Park	1830-1900	2302	1
Wembley Park	1900-1930	2058	1
Wembley Park	1930-2000	1541	1
Wembley Park	2000-2030	1032	1
Wembley Park	2030-2100	809	1
Wembley Park	2100-2130	756	1
Wembley Park	2130-2200	626	1
Wembley Park	2200-2230	699	1
Wembley Park	2230-2300	876	1
Wembley Park	2300-2330	615	1
Wembley Park	2330-2400	391	1
Wembley Park	0000-0030	276	1
Wembley Park	0030-0100	151	1
Wembley Park	0100-0130	56	1
Wembley Park	0130-0200	17	1
Wembley Park	0200-0230	0	0
Wembley Park	0230-0300	0	0
Wembley Park	0300-0330	0	0
Wembley Park	0330-0400	0	0
Wembley Park	0400-0430	0	0
West Acton	0430-0500	0	0
West Acton	0500-0530	11	1
West Acton	0530-0600	31	1
West Acton	0600-0630	53	1
West Acton	0630-0700	116	1
West Acton	0700-0730	200	1
West Acton	0730-0800	304	1
West Acton	0800-0830	429	1
West Acton	0830-0900	362	1
West Acton	0900-0930	213	1
West Acton	0930-1000	121	1
West Acton	1000-1030	93	1
West Acton	1030-1100	81	1
West Acton	1100-1130	86	1
West Acton	1130-1200	79	1
West Acton	1200-1230	83	1
West Acton	1230-1300	92	1
West Acton	1300-1330	98	1
West Acton	1330-1400	96	1
West Acton	1400-1430	101	1
West Acton	1430-1500	112	1
West Acton	1500-1530	166	1
West Acton	1530-1600	196	1
West Acton	1600-1630	163	1
West Acton	1630-1700	169	1
West Acton	1700-1730	227	1
West Acton	1730-1800	222	1
West Acton	1800-1830	255	1
West Acton	1830-1900	215	1
West Acton	1900-1930	174	1
West Acton	1930-2000	133	1
West Acton	2000-2030	103	1
West Acton	2030-2100	88	1
West Acton	2100-2130	86	1
West Acton	2130-2200	74	1
West Acton	2200-2230	60	1
West Acton	2230-2300	64	1
West Acton	2300-2330	56	1
West Acton	2330-2400	48	1
West Acton	0000-0030	34	1
West Acton	0030-0100	24	1
West Acton	0100-0130	10	1
West Acton	0130-0200	2	1
West Acton	0200-0230	0	0
West Acton	0230-0300	0	0
West Acton	0300-0330	0	0
West Acton	0330-0400	0	0
West Acton	0400-0430	0	0
West Brompton	0430-0500	0	0
West Brompton	0500-0530	4	1
West Brompton	0530-0600	34	1
West Brompton	0600-0630	143	1
West Brompton	0630-0700	518	1
West Brompton	0700-0730	1009	1
West Brompton	0730-0800	1270	1
West Brompton	0800-0830	1400	1
West Brompton	0830-0900	1072	1
West Brompton	0900-0930	864	1
West Brompton	0930-1000	625	1
West Brompton	1000-1030	372	1
West Brompton	1030-1100	300	1
West Brompton	1100-1130	279	1
West Brompton	1130-1200	279	1
West Brompton	1200-1230	289	1
West Brompton	1230-1300	299	1
West Brompton	1300-1330	317	1
West Brompton	1330-1400	326	1
West Brompton	1400-1430	330	1
West Brompton	1430-1500	404	1
West Brompton	1500-1530	761	1
West Brompton	1530-1600	860	1
West Brompton	1600-1630	899	1
West Brompton	1630-1700	951	1
West Brompton	1700-1730	1097	1
West Brompton	1730-1800	1082	1
West Brompton	1800-1830	918	1
West Brompton	1830-1900	803	1
West Brompton	1900-1930	542	1
West Brompton	1930-2000	326	1
West Brompton	2000-2030	248	1
West Brompton	2030-2100	245	1
West Brompton	2100-2130	217	1
West Brompton	2130-2200	225	1
West Brompton	2200-2230	235	1
West Brompton	2230-2300	204	1
West Brompton	2300-2330	138	1
West Brompton	2330-2400	85	1
West Brompton	0000-0030	43	1
West Brompton	0030-0100	16	1
West Brompton	0100-0130	1	1
West Brompton	0130-0200	0	1
West Brompton	0200-0230	0	0
West Brompton	0230-0300	0	0
West Brompton	0300-0330	0	0
West Brompton	0330-0400	0	0
West Brompton	0400-0430	0	0
West Finchley	0430-0500	0	0
West Finchley	0500-0530	9	1
West Finchley	0530-0600	23	1
West Finchley	0600-0630	61	1
West Finchley	0630-0700	112	1
West Finchley	0700-0730	237	1
West Finchley	0730-0800	406	1
West Finchley	0800-0830	484	1
West Finchley	0830-0900	410	1
West Finchley	0900-0930	224	1
West Finchley	0930-1000	132	1
West Finchley	1000-1030	95	1
West Finchley	1030-1100	80	1
West Finchley	1100-1130	72	1
West Finchley	1130-1200	70	1
West Finchley	1200-1230	67	1
West Finchley	1230-1300	64	1
West Finchley	1300-1330	75	1
West Finchley	1330-1400	130	1
West Finchley	1400-1430	77	1
West Finchley	1430-1500	94	1
West Finchley	1500-1530	116	1
West Finchley	1530-1600	124	1
West Finchley	1600-1630	149	1
West Finchley	1630-1700	171	1
West Finchley	1700-1730	209	1
West Finchley	1730-1800	259	1
West Finchley	1800-1830	292	1
West Finchley	1830-1900	274	1
West Finchley	1900-1930	227	1
West Finchley	1930-2000	161	1
West Finchley	2000-2030	112	1
West Finchley	2030-2100	94	1
West Finchley	2100-2130	84	1
West Finchley	2130-2200	75	1
West Finchley	2200-2230	72	1
West Finchley	2230-2300	68	1
West Finchley	2300-2330	62	1
West Finchley	2330-2400	54	1
West Finchley	0000-0030	36	1
West Finchley	0030-0100	21	1
West Finchley	0100-0130	7	1
West Finchley	0130-0200	2	1
West Finchley	0200-0230	0	0
West Finchley	0230-0300	0	0
West Finchley	0300-0330	0	0
West Finchley	0330-0400	0	0
West Finchley	0400-0430	0	0
West Ham	0430-0500	0	0
West Ham	0500-0530	116	1
West Ham	0530-0600	159	1
West Ham	0600-0630	309	1
West Ham	0630-0700	458	1
West Ham	0700-0730	556	1
West Ham	0730-0800	606	1
West Ham	0800-0830	771	1
West Ham	0830-0900	659	1
West Ham	0900-0930	422	1
West Ham	0930-1000	297	1
West Ham	1000-1030	238	1
West Ham	1030-1100	206	1
West Ham	1100-1130	211	1
West Ham	1130-1200	207	1
West Ham	1200-1230	215	1
West Ham	1230-1300	229	1
West Ham	1300-1330	235	1
West Ham	1330-1400	234	1
West Ham	1400-1430	245	1
West Ham	1430-1500	276	1
West Ham	1500-1530	323	1
West Ham	1530-1600	361	1
West Ham	1600-1630	443	1
West Ham	1630-1700	497	1
West Ham	1700-1730	579	1
West Ham	1730-1800	637	1
West Ham	1800-1830	636	1
West Ham	1830-1900	578	1
West Ham	1900-1930	457	1
West Ham	1930-2000	356	1
West Ham	2000-2030	280	1
West Ham	2030-2100	259	1
West Ham	2100-2130	240	1
West Ham	2130-2200	199	1
West Ham	2200-2230	204	1
West Ham	2230-2300	199	1
West Ham	2300-2330	171	1
West Ham	2330-2400	149	1
West Ham	0000-0030	98	1
West Ham	0030-0100	60	1
West Ham	0100-0130	26	1
West Ham	0130-0200	11	1
West Ham	0200-0230	0	0
West Ham	0230-0300	0	0
West Ham	0300-0330	0	0
West Ham	0330-0400	0	0
West Ham	0400-0430	0	0
West Hampstead	0430-0500	0	0
West Hampstead	0500-0530	35	1
West Hampstead	0530-0600	116	1
West Hampstead	0600-0630	462	1
West Hampstead	0630-0700	1031	1
West Hampstead	0700-0730	1501	1
West Hampstead	0730-0800	2080	1
West Hampstead	0800-0830	3054	1
West Hampstead	0830-0900	2788	1
West Hampstead	0900-0930	1716	1
West Hampstead	0930-1000	1101	1
West Hampstead	1000-1030	746	1
West Hampstead	1030-1100	612	1
West Hampstead	1100-1130	529	1
West Hampstead	1130-1200	521	1
West Hampstead	1200-1230	522	1
West Hampstead	1230-1300	528	1
West Hampstead	1300-1330	536	1
West Hampstead	1330-1400	539	1
West Hampstead	1400-1430	561	1
West Hampstead	1430-1500	566	1
West Hampstead	1500-1530	649	1
West Hampstead	1530-1600	762	1
West Hampstead	1600-1630	983	1
West Hampstead	1630-1700	1209	1
West Hampstead	1700-1730	1568	1
West Hampstead	1730-1800	1961	1
West Hampstead	1800-1830	2143	1
West Hampstead	1830-1900	1851	1
West Hampstead	1900-1930	1353	1
West Hampstead	1930-2000	990	1
West Hampstead	2000-2030	745	1
West Hampstead	2030-2100	622	1
West Hampstead	2100-2130	538	1
West Hampstead	2130-2200	513	1
West Hampstead	2200-2230	532	1
West Hampstead	2230-2300	526	1
West Hampstead	2300-2330	453	1
West Hampstead	2330-2400	358	1
West Hampstead	0000-0030	228	1
West Hampstead	0030-0100	89	1
West Hampstead	0100-0130	24	1
West Hampstead	0130-0200	15	1
West Hampstead	0200-0230	0	0
West Hampstead	0230-0300	0	0
West Hampstead	0300-0330	0	0
West Hampstead	0330-0400	0	0
West Hampstead	0400-0430	0	0
West Harrow	0430-0500	0	0
West Harrow	0500-0530	17	1
West Harrow	0530-0600	50	1
West Harrow	0600-0630	107	1
West Harrow	0630-0700	159	1
West Harrow	0700-0730	226	1
West Harrow	0730-0800	324	1
West Harrow	0800-0830	346	1
West Harrow	0830-0900	240	1
West Harrow	0900-0930	130	1
West Harrow	0930-1000	89	1
West Harrow	1000-1030	77	1
West Harrow	1030-1100	68	1
West Harrow	1100-1130	56	1
West Harrow	1130-1200	61	1
West Harrow	1200-1230	70	1
West Harrow	1230-1300	66	1
West Harrow	1300-1330	65	1
West Harrow	1330-1400	66	1
West Harrow	1400-1430	63	1
West Harrow	1430-1500	72	1
West Harrow	1500-1530	88	1
West Harrow	1530-1600	115	1
West Harrow	1600-1630	129	1
West Harrow	1630-1700	196	1
West Harrow	1700-1730	255	1
West Harrow	1730-1800	294	1
West Harrow	1800-1830	284	1
West Harrow	1830-1900	251	1
West Harrow	1900-1930	204	1
West Harrow	1930-2000	126	1
West Harrow	2000-2030	122	1
West Harrow	2030-2100	89	1
West Harrow	2100-2130	82	1
West Harrow	2130-2200	38	1
West Harrow	2200-2230	46	1
West Harrow	2230-2300	62	1
West Harrow	2300-2330	58	1
West Harrow	2330-2400	44	1
West Harrow	0000-0030	31	1
West Harrow	0030-0100	15	1
West Harrow	0100-0130	0	1
West Harrow	0130-0200	0	1
West Harrow	0200-0230	0	0
West Harrow	0230-0300	0	0
West Harrow	0300-0330	0	0
West Harrow	0330-0400	0	0
West Harrow	0400-0430	0	0
West Kensington	0430-0500	0	0
West Kensington	0500-0530	33	1
West Kensington	0530-0600	46	1
West Kensington	0600-0630	112	1
West Kensington	0630-0700	194	1
West Kensington	0700-0730	395	1
West Kensington	0730-0800	721	1
West Kensington	0800-0830	974	1
West Kensington	0830-0900	939	1
West Kensington	0900-0930	813	1
West Kensington	0930-1000	620	1
West Kensington	1000-1030	412	1
West Kensington	1030-1100	367	1
West Kensington	1100-1130	337	1
West Kensington	1130-1200	310	1
West Kensington	1200-1230	326	1
West Kensington	1230-1300	311	1
West Kensington	1300-1330	341	1
West Kensington	1330-1400	338	1
West Kensington	1400-1430	343	1
West Kensington	1430-1500	318	1
West Kensington	1500-1530	369	1
West Kensington	1530-1600	427	1
West Kensington	1600-1630	471	1
West Kensington	1630-1700	550	1
West Kensington	1700-1730	685	1
West Kensington	1730-1800	836	1
West Kensington	1800-1830	820	1
West Kensington	1830-1900	736	1
West Kensington	1900-1930	598	1
West Kensington	1930-2000	451	1
West Kensington	2000-2030	344	1
West Kensington	2030-2100	297	1
West Kensington	2100-2130	285	1
West Kensington	2130-2200	276	1
West Kensington	2200-2230	265	1
West Kensington	2230-2300	268	1
West Kensington	2300-2330	220	1
West Kensington	2330-2400	163	1
West Kensington	0000-0030	89	1
West Kensington	0030-0100	40	1
West Kensington	0100-0130	4	1
West Kensington	0130-0200	0	1
West Kensington	0200-0230	0	0
West Kensington	0230-0300	0	0
West Kensington	0300-0330	0	0
West Kensington	0330-0400	0	0
West Kensington	0400-0430	0	0
West Ruislip	0430-0500	0	0
West Ruislip	0500-0530	14	1
West Ruislip	0530-0600	37	1
West Ruislip	0600-0630	91	1
West Ruislip	0630-0700	150	1
West Ruislip	0700-0730	248	1
West Ruislip	0730-0800	379	1
West Ruislip	0800-0830	384	1
West Ruislip	0830-0900	273	1
West Ruislip	0900-0930	184	1
West Ruislip	0930-1000	154	1
West Ruislip	1000-1030	111	1
West Ruislip	1030-1100	75	1
West Ruislip	1100-1130	87	1
West Ruislip	1130-1200	83	1
West Ruislip	1200-1230	73	1
West Ruislip	1230-1300	73	1
West Ruislip	1300-1330	83	1
West Ruislip	1330-1400	76	1
West Ruislip	1400-1430	83	1
West Ruislip	1430-1500	81	1
West Ruislip	1500-1530	92	1
West Ruislip	1530-1600	126	1
West Ruislip	1600-1630	161	1
West Ruislip	1630-1700	206	1
West Ruislip	1700-1730	237	1
West Ruislip	1730-1800	278	1
West Ruislip	1800-1830	306	1
West Ruislip	1830-1900	279	1
West Ruislip	1900-1930	221	1
West Ruislip	1930-2000	141	1
West Ruislip	2000-2030	116	1
West Ruislip	2030-2100	94	1
West Ruislip	2100-2130	78	1
West Ruislip	2130-2200	65	1
West Ruislip	2200-2230	77	1
West Ruislip	2230-2300	66	1
West Ruislip	2300-2330	61	1
West Ruislip	2330-2400	51	1
West Ruislip	0000-0030	34	1
West Ruislip	0030-0100	24	1
West Ruislip	0100-0130	7	1
West Ruislip	0130-0200	0	1
West Ruislip	0200-0230	0	0
West Ruislip	0230-0300	0	0
West Ruislip	0300-0330	0	0
West Ruislip	0330-0400	0	0
West Ruislip	0400-0430	0	0
Westbourne Park	0430-0500	0	0
Westbourne Park	0500-0530	20	1
Westbourne Park	0530-0600	49	1
Westbourne Park	0600-0630	104	1
Westbourne Park	0630-0700	177	1
Westbourne Park	0700-0730	345	1
Westbourne Park	0730-0800	625	1
Westbourne Park	0800-0830	796	1
Westbourne Park	0830-0900	856	1
Westbourne Park	0900-0930	702	1
Westbourne Park	0930-1000	487	1
Westbourne Park	1000-1030	326	1
Westbourne Park	1030-1100	265	1
Westbourne Park	1100-1130	254	1
Westbourne Park	1130-1200	243	1
Westbourne Park	1200-1230	247	1
Westbourne Park	1230-1300	259	1
Westbourne Park	1300-1330	276	1
Westbourne Park	1330-1400	270	1
Westbourne Park	1400-1430	270	1
Westbourne Park	1430-1500	270	1
Westbourne Park	1500-1530	295	1
Westbourne Park	1530-1600	355	1
Westbourne Park	1600-1630	428	1
Westbourne Park	1630-1700	477	1
Westbourne Park	1700-1730	582	1
Westbourne Park	1730-1800	604	1
Westbourne Park	1800-1830	718	1
Westbourne Park	1830-1900	584	1
Westbourne Park	1900-1930	436	1
Westbourne Park	1930-2000	319	1
Westbourne Park	2000-2030	274	1
Westbourne Park	2030-2100	224	1
Westbourne Park	2100-2130	202	1
Westbourne Park	2130-2200	189	1
Westbourne Park	2200-2230	171	1
Westbourne Park	2230-2300	150	1
Westbourne Park	2300-2330	138	1
Westbourne Park	2330-2400	108	1
Westbourne Park	0000-0030	66	1
Westbourne Park	0030-0100	31	1
Westbourne Park	0100-0130	3	1
Westbourne Park	0130-0200	0	1
Westbourne Park	0200-0230	0	0
Westbourne Park	0230-0300	0	0
Westbourne Park	0300-0330	0	0
Westbourne Park	0330-0400	0	0
Westbourne Park	0400-0430	0	0
Westminster	0430-0500	0	0
Westminster	0500-0530	32	1
Westminster	0530-0600	182	1
Westminster	0600-0630	356	1
Westminster	0630-0700	701	1
Westminster	0700-0730	1156	1
Westminster	0730-0800	2069	1
Westminster	0800-0830	3016	1
Westminster	0830-0900	4299	1
Westminster	0900-0930	4258	1
Westminster	0930-1000	3421	1
Westminster	1000-1030	2502	1
Westminster	1030-1100	2112	1
Westminster	1100-1130	1881	1
Westminster	1130-1200	1990	1
Westminster	1200-1230	2148	1
Westminster	1230-1300	2203	1
Westminster	1300-1330	2225	1
Westminster	1330-1400	2229	1
Westminster	1400-1430	2225	1
Westminster	1430-1500	2285	1
Westminster	1500-1530	2473	1
Westminster	1530-1600	2711	1
Westminster	1600-1630	3283	1
Westminster	1630-1700	3575	1
Westminster	1700-1730	4145	1
Westminster	1730-1800	4226	1
Westminster	1800-1830	3709	1
Westminster	1830-1900	2701	1
Westminster	1900-1930	1882	1
Westminster	1930-2000	1301	1
Westminster	2000-2030	1108	1
Westminster	2030-2100	954	1
Westminster	2100-2130	833	1
Westminster	2130-2200	782	1
Westminster	2200-2230	680	1
Westminster	2230-2300	592	1
Westminster	2300-2330	451	1
Westminster	2330-2400	303	1
Westminster	0000-0030	153	1
Westminster	0030-0100	62	1
Westminster	0100-0130	19	1
Westminster	0130-0200	9	1
Westminster	0200-0230	0	0
Westminster	0230-0300	0	0
Westminster	0300-0330	0	0
Westminster	0330-0400	0	0
Westminster	0400-0430	0	0
White City	0430-0500	0	0
White City	0500-0530	28	1
White City	0530-0600	93	1
White City	0600-0630	201	1
White City	0630-0700	634	1
White City	0700-0730	1157	1
White City	0730-0800	1390	1
White City	0800-0830	1405	1
White City	0830-0900	1673	1
White City	0900-0930	2012	1
White City	0930-1000	1853	1
White City	1000-1030	1144	1
White City	1030-1100	601	1
White City	1100-1130	457	1
White City	1130-1200	405	1
White City	1200-1230	411	1
White City	1230-1300	433	1
White City	1300-1330	457	1
White City	1330-1400	452	1
White City	1400-1430	452	1
White City	1430-1500	471	1
White City	1500-1530	541	1
White City	1530-1600	740	1
White City	1600-1630	985	1
White City	1630-1700	1210	1
White City	1700-1730	1590	1
White City	1730-1800	1931	1
White City	1800-1830	1797	1
White City	1830-1900	1259	1
White City	1900-1930	913	1
White City	1930-2000	614	1
White City	2000-2030	462	1
White City	2030-2100	370	1
White City	2100-2130	327	1
White City	2130-2200	411	1
White City	2200-2230	336	1
White City	2230-2300	241	1
White City	2300-2330	188	1
White City	2330-2400	140	1
White City	0000-0030	98	1
White City	0030-0100	55	1
White City	0100-0130	22	1
White City	0130-0200	14	1
White City	0200-0230	0	0
White City	0230-0300	0	0
White City	0300-0330	0	0
White City	0330-0400	0	0
White City	0400-0430	0	0
Whitechapel	0430-0500	0	0
Whitechapel	0500-0530	46	1
Whitechapel	0530-0600	156	1
Whitechapel	0600-0630	343	1
Whitechapel	0630-0700	720	1
Whitechapel	0700-0730	1266	1
Whitechapel	0730-0800	1661	1
Whitechapel	0800-0830	2000	1
Whitechapel	0830-0900	2556	1
Whitechapel	0900-0930	2044	1
Whitechapel	0930-1000	1528	1
Whitechapel	1000-1030	1208	1
Whitechapel	1030-1100	1085	1
Whitechapel	1100-1130	1004	1
Whitechapel	1130-1200	982	1
Whitechapel	1200-1230	998	1
Whitechapel	1230-1300	1036	1
Whitechapel	1300-1330	1108	1
Whitechapel	1330-1400	1110	1
Whitechapel	1400-1430	1114	1
Whitechapel	1430-1500	1183	1
Whitechapel	1500-1530	1309	1
Whitechapel	1530-1600	1419	1
Whitechapel	1600-1630	1606	1
Whitechapel	1630-1700	1874	1
Whitechapel	1700-1730	2307	1
Whitechapel	1730-1800	2308	1
Whitechapel	1800-1830	2125	1
Whitechapel	1830-1900	1641	1
Whitechapel	1900-1930	1362	1
Whitechapel	1930-2000	1100	1
Whitechapel	2000-2030	969	1
Whitechapel	2030-2100	839	1
Whitechapel	2100-2130	669	1
Whitechapel	2130-2200	553	1
Whitechapel	2200-2230	492	1
Whitechapel	2230-2300	435	1
Whitechapel	2300-2330	411	1
Whitechapel	2330-2400	345	1
Whitechapel	0000-0030	209	1
Whitechapel	0030-0100	90	1
Whitechapel	0100-0130	12	1
Whitechapel	0130-0200	0	1
Whitechapel	0200-0230	0	0
Whitechapel	0230-0300	0	0
Whitechapel	0300-0330	0	0
Whitechapel	0330-0400	0	0
Whitechapel	0400-0430	0	0
Willesden Green	0430-0500	0	0
Willesden Green	0500-0530	87	1
Willesden Green	0530-0600	149	1
Willesden Green	0600-0630	325	1
Willesden Green	0630-0700	534	1
Willesden Green	0700-0730	868	1
Willesden Green	0730-0800	1248	1
Willesden Green	0800-0830	1666	1
Willesden Green	0830-0900	1441	1
Willesden Green	0900-0930	1042	1
Willesden Green	0930-1000	732	1
Willesden Green	1000-1030	567	1
Willesden Green	1030-1100	505	1
Willesden Green	1100-1130	500	1
Willesden Green	1130-1200	462	1
Willesden Green	1200-1230	466	1
Willesden Green	1230-1300	475	1
Willesden Green	1300-1330	484	1
Willesden Green	1330-1400	495	1
Willesden Green	1400-1430	520	1
Willesden Green	1430-1500	531	1
Willesden Green	1500-1530	597	1
Willesden Green	1530-1600	645	1
Willesden Green	1600-1630	787	1
Willesden Green	1630-1700	896	1
Willesden Green	1700-1730	1042	1
Willesden Green	1730-1800	1236	1
Willesden Green	1800-1830	1314	1
Willesden Green	1830-1900	1230	1
Willesden Green	1900-1930	969	1
Willesden Green	1930-2000	784	1
Willesden Green	2000-2030	663	1
Willesden Green	2030-2100	565	1
Willesden Green	2100-2130	507	1
Willesden Green	2130-2200	481	1
Willesden Green	2200-2230	449	1
Willesden Green	2230-2300	450	1
Willesden Green	2300-2330	379	1
Willesden Green	2330-2400	339	1
Willesden Green	0000-0030	262	1
Willesden Green	0030-0100	142	1
Willesden Green	0100-0130	35	1
Willesden Green	0130-0200	24	1
Willesden Green	0200-0230	0	0
Willesden Green	0230-0300	0	0
Willesden Green	0300-0330	0	0
Willesden Green	0330-0400	0	0
Willesden Green	0400-0430	0	0
Willesden Junction	0430-0500	0	0
Willesden Junction	0500-0530	15	1
Willesden Junction	0530-0600	103	1
Willesden Junction	0600-0630	203	1
Willesden Junction	0630-0700	421	1
Willesden Junction	0700-0730	597	1
Willesden Junction	0730-0800	765	1
Willesden Junction	0800-0830	999	1
Willesden Junction	0830-0900	846	1
Willesden Junction	0900-0930	588	1
Willesden Junction	0930-1000	406	1
Willesden Junction	1000-1030	276	1
Willesden Junction	1030-1100	234	1
Willesden Junction	1100-1130	277	1
Willesden Junction	1130-1200	273	1
Willesden Junction	1200-1230	290	1
Willesden Junction	1230-1300	294	1
Willesden Junction	1300-1330	313	1
Willesden Junction	1330-1400	342	1
Willesden Junction	1400-1430	331	1
Willesden Junction	1430-1500	308	1
Willesden Junction	1500-1530	294	1
Willesden Junction	1530-1600	355	1
Willesden Junction	1600-1630	513	1
Willesden Junction	1630-1700	565	1
Willesden Junction	1700-1730	712	1
Willesden Junction	1730-1800	762	1
Willesden Junction	1800-1830	753	1
Willesden Junction	1830-1900	654	1
Willesden Junction	1900-1930	452	1
Willesden Junction	1930-2000	395	1
Willesden Junction	2000-2030	236	1
Willesden Junction	2030-2100	274	1
Willesden Junction	2100-2130	203	1
Willesden Junction	2130-2200	210	1
Willesden Junction	2200-2230	232	1
Willesden Junction	2230-2300	194	1
Willesden Junction	2300-2330	144	1
Willesden Junction	2330-2400	129	1
Willesden Junction	0000-0030	82	1
Willesden Junction	0030-0100	33	1
Willesden Junction	0100-0130	7	1
Willesden Junction	0130-0200	0	1
Willesden Junction	0200-0230	0	0
Willesden Junction	0230-0300	0	0
Willesden Junction	0300-0330	0	0
Willesden Junction	0330-0400	0	0
Willesden Junction	0400-0430	0	0
Wimbledon	0430-0500	0	0
Wimbledon	0500-0530	37	1
Wimbledon	0530-0600	180	1
Wimbledon	0600-0630	617	1
Wimbledon	0630-0700	1357	1
Wimbledon	0700-0730	1919	1
Wimbledon	0730-0800	2336	1
Wimbledon	0800-0830	1841	1
Wimbledon	0830-0900	1414	1
Wimbledon	0900-0930	1076	1
Wimbledon	0930-1000	755	1
Wimbledon	1000-1030	646	1
Wimbledon	1030-1100	477	1
Wimbledon	1100-1130	411	1
Wimbledon	1130-1200	460	1
Wimbledon	1200-1230	508	1
Wimbledon	1230-1300	625	1
Wimbledon	1300-1330	812	1
Wimbledon	1330-1400	749	1
Wimbledon	1400-1430	874	1
Wimbledon	1430-1500	636	1
Wimbledon	1500-1530	846	1
Wimbledon	1530-1600	1085	1
Wimbledon	1600-1630	1411	1
Wimbledon	1630-1700	1901	1
Wimbledon	1700-1730	2478	1
Wimbledon	1730-1800	2698	1
Wimbledon	1800-1830	2433	1
Wimbledon	1830-1900	1962	1
Wimbledon	1900-1930	1499	1
Wimbledon	1930-2000	979	1
Wimbledon	2000-2030	796	1
Wimbledon	2030-2100	416	1
Wimbledon	2100-2130	360	1
Wimbledon	2130-2200	411	1
Wimbledon	2200-2230	384	1
Wimbledon	2230-2300	241	1
Wimbledon	2300-2330	240	1
Wimbledon	2330-2400	200	1
Wimbledon	0000-0030	168	1
Wimbledon	0030-0100	72	1
Wimbledon	0100-0130	27	1
Wimbledon	0130-0200	0	1
Wimbledon	0200-0230	0	0
Wimbledon	0230-0300	0	0
Wimbledon	0300-0330	0	0
Wimbledon	0330-0400	0	0
Wimbledon	0400-0430	0	0
Wimbledon Park	0430-0500	0	0
Wimbledon Park	0500-0530	9	1
Wimbledon Park	0530-0600	26	1
Wimbledon Park	0600-0630	69	1
Wimbledon Park	0630-0700	147	1
Wimbledon Park	0700-0730	328	1
Wimbledon Park	0730-0800	530	1
Wimbledon Park	0800-0830	478	1
Wimbledon Park	0830-0900	360	1
Wimbledon Park	0900-0930	246	1
Wimbledon Park	0930-1000	157	1
Wimbledon Park	1000-1030	132	1
Wimbledon Park	1030-1100	116	1
Wimbledon Park	1100-1130	108	1
Wimbledon Park	1130-1200	116	1
Wimbledon Park	1200-1230	117	1
Wimbledon Park	1230-1300	129	1
Wimbledon Park	1300-1330	141	1
Wimbledon Park	1330-1400	135	1
Wimbledon Park	1400-1430	130	1
Wimbledon Park	1430-1500	124	1
Wimbledon Park	1500-1530	138	1
Wimbledon Park	1530-1600	172	1
Wimbledon Park	1600-1630	226	1
Wimbledon Park	1630-1700	292	1
Wimbledon Park	1700-1730	316	1
Wimbledon Park	1730-1800	319	1
Wimbledon Park	1800-1830	345	1
Wimbledon Park	1830-1900	324	1
Wimbledon Park	1900-1930	254	1
Wimbledon Park	1930-2000	165	1
Wimbledon Park	2000-2030	122	1
Wimbledon Park	2030-2100	100	1
Wimbledon Park	2100-2130	86	1
Wimbledon Park	2130-2200	91	1
Wimbledon Park	2200-2230	85	1
Wimbledon Park	2230-2300	74	1
Wimbledon Park	2300-2330	70	1
Wimbledon Park	2330-2400	49	1
Wimbledon Park	0000-0030	33	1
Wimbledon Park	0030-0100	20	1
Wimbledon Park	0100-0130	5	1
Wimbledon Park	0130-0200	0	1
Wimbledon Park	0200-0230	0	0
Wimbledon Park	0230-0300	0	0
Wimbledon Park	0300-0330	0	0
Wimbledon Park	0330-0400	0	0
Wimbledon Park	0400-0430	0	0
Wood Green	0430-0500	0	0
Wood Green	0500-0530	145	1
Wood Green	0530-0600	326	1
Wood Green	0600-0630	785	1
Wood Green	0630-0700	1314	1
Wood Green	0700-0730	1536	1
Wood Green	0730-0800	1456	1
Wood Green	0800-0830	1843	1
Wood Green	0830-0900	1726	1
Wood Green	0900-0930	1422	1
Wood Green	0930-1000	1063	1
Wood Green	1000-1030	806	1
Wood Green	1030-1100	705	1
Wood Green	1100-1130	713	1
Wood Green	1130-1200	655	1
Wood Green	1200-1230	677	1
Wood Green	1230-1300	729	1
Wood Green	1300-1330	747	1
Wood Green	1330-1400	751	1
Wood Green	1400-1430	787	1
Wood Green	1430-1500	845	1
Wood Green	1500-1530	917	1
Wood Green	1530-1600	1023	1
Wood Green	1600-1630	1256	1
Wood Green	1630-1700	1481	1
Wood Green	1700-1730	1754	1
Wood Green	1730-1800	1930	1
Wood Green	1800-1830	1915	1
Wood Green	1830-1900	1656	1
Wood Green	1900-1930	1330	1
Wood Green	1930-2000	1015	1
Wood Green	2000-2030	798	1
Wood Green	2030-2100	700	1
Wood Green	2100-2130	604	1
Wood Green	2130-2200	568	1
Wood Green	2200-2230	555	1
Wood Green	2230-2300	626	1
Wood Green	2300-2330	673	1
Wood Green	2330-2400	571	1
Wood Green	0000-0030	330	1
Wood Green	0030-0100	191	1
Wood Green	0100-0130	52	1
Wood Green	0130-0200	15	1
Wood Green	0200-0230	0	0
Wood Green	0230-0300	0	0
Wood Green	0300-0330	0	0
Wood Green	0330-0400	0	0
Wood Green	0400-0430	0	0
Wood Lane	0430-0500	0	0
Wood Lane	0500-0530	13	1
Wood Lane	0530-0600	35	1
Wood Lane	0600-0630	66	1
Wood Lane	0630-0700	185	1
Wood Lane	0700-0730	340	1
Wood Lane	0730-0800	459	1
Wood Lane	0800-0830	526	1
Wood Lane	0830-0900	634	1
Wood Lane	0900-0930	622	1
Wood Lane	0930-1000	501	1
Wood Lane	1000-1030	301	1
Wood Lane	1030-1100	258	1
Wood Lane	1100-1130	255	1
Wood Lane	1130-1200	259	1
Wood Lane	1200-1230	274	1
Wood Lane	1230-1300	306	1
Wood Lane	1300-1330	318	1
Wood Lane	1330-1400	315	1
Wood Lane	1400-1430	303	1
Wood Lane	1430-1500	306	1
Wood Lane	1500-1530	327	1
Wood Lane	1530-1600	382	1
Wood Lane	1600-1630	468	1
Wood Lane	1630-1700	551	1
Wood Lane	1700-1730	721	1
Wood Lane	1730-1800	823	1
Wood Lane	1800-1830	759	1
Wood Lane	1830-1900	614	1
Wood Lane	1900-1930	435	1
Wood Lane	1930-2000	319	1
Wood Lane	2000-2030	247	1
Wood Lane	2030-2100	205	1
Wood Lane	2100-2130	179	1
Wood Lane	2130-2200	163	1
Wood Lane	2200-2230	151	1
Wood Lane	2230-2300	95	1
Wood Lane	2300-2330	73	1
Wood Lane	2330-2400	46	1
Wood Lane	0000-0030	26	1
Wood Lane	0030-0100	11	1
Wood Lane	0100-0130	2	1
Wood Lane	0130-0200	0	1
Wood Lane	0200-0230	0	0
Wood Lane	0230-0300	0	0
Wood Lane	0300-0330	0	0
Wood Lane	0330-0400	0	0
Wood Lane	0400-0430	0	0
Woodford	0430-0500	0	0
Woodford	0500-0530	69	1
Woodford	0530-0600	170	1
Woodford	0600-0630	336	1
Woodford	0630-0700	600	1
Woodford	0700-0730	869	1
Woodford	0730-0800	1237	1
Woodford	0800-0830	1406	1
Woodford	0830-0900	965	1
Woodford	0900-0930	642	1
Woodford	0930-1000	456	1
Woodford	1000-1030	341	1
Woodford	1030-1100	309	1
Woodford	1100-1130	310	1
Woodford	1130-1200	287	1
Woodford	1200-1230	289	1
Woodford	1230-1300	299	1
Woodford	1300-1330	309	1
Woodford	1330-1400	302	1
Woodford	1400-1430	315	1
Woodford	1430-1500	333	1
Woodford	1500-1530	399	1
Woodford	1530-1600	485	1
Woodford	1600-1630	549	1
Woodford	1630-1700	679	1
Woodford	1700-1730	805	1
Woodford	1730-1800	975	1
Woodford	1800-1830	998	1
Woodford	1830-1900	884	1
Woodford	1900-1930	696	1
Woodford	1930-2000	494	1
Woodford	2000-2030	370	1
Woodford	2030-2100	315	1
Woodford	2100-2130	227	1
Woodford	2130-2200	219	1
Woodford	2200-2230	217	1
Woodford	2230-2300	220	1
Woodford	2300-2330	212	1
Woodford	2330-2400	165	1
Woodford	0000-0030	120	1
Woodford	0030-0100	68	1
Woodford	0100-0130	31	1
Woodford	0130-0200	7	1
Woodford	0200-0230	0	0
Woodford	0230-0300	0	0
Woodford	0300-0330	0	0
Woodford	0330-0400	0	0
Woodford	0400-0430	0	0
Woodside Park	0430-0500	1	1
Woodside Park	0500-0530	21	1
Woodside Park	0530-0600	53	1
Woodside Park	0600-0630	116	1
Woodside Park	0630-0700	223	1
Woodside Park	0700-0730	421	1
Woodside Park	0730-0800	675	1
Woodside Park	0800-0830	874	1
Woodside Park	0830-0900	645	1
Woodside Park	0900-0930	406	1
Woodside Park	0930-1000	263	1
Woodside Park	1000-1030	187	1
Woodside Park	1030-1100	150	1
Woodside Park	1100-1130	147	1
Woodside Park	1130-1200	152	1
Woodside Park	1200-1230	153	1
Woodside Park	1230-1300	160	1
Woodside Park	1300-1330	186	1
Woodside Park	1330-1400	173	1
Woodside Park	1400-1430	173	1
Woodside Park	1430-1500	186	1
Woodside Park	1500-1530	240	1
Woodside Park	1530-1600	275	1
Woodside Park	1600-1630	345	1
Woodside Park	1630-1700	419	1
Woodside Park	1700-1730	516	1
Woodside Park	1730-1800	695	1
Woodside Park	1800-1830	764	1
Woodside Park	1830-1900	626	1
Woodside Park	1900-1930	450	1
Woodside Park	1930-2000	279	1
Woodside Park	2000-2030	232	1
Woodside Park	2030-2100	210	1
Woodside Park	2100-2130	212	1
Woodside Park	2130-2200	181	1
Woodside Park	2200-2230	163	1
Woodside Park	2230-2300	162	1
Woodside Park	2300-2330	123	1
Woodside Park	2330-2400	83	1
Woodside Park	0000-0030	44	1
Woodside Park	0030-0100	11	1
Woodside Park	0100-0130	3	1
Woodside Park	0130-0200	2	1
Woodside Park	0200-0230	0	0
Woodside Park	0230-0300	0	0
Woodside Park	0300-0330	0	0
Woodside Park	0330-0400	0	0
Woodside Park	0400-0430	0	0"""
        |> fromDelimited '\t'

londonMapSchema : Table
londonMapSchema =
          """object	Coordinate	Row	Col	RowReverse	ColReverse	rowSketch	colSketch	gridOrientation	Type	localAuthority	showTubeZone
        Acton Town	L29	29	12	21	34	12.03	21.04	Station	Station	Ealing	No
        Aldgate	AF22	22	32	28	14	32.05	28.05	Station	Station	City of London	No
        Aldgate East	AG21	21	33	29	13	33.04	29.02	Station	Station	Tower Hamlets	No
        Alperton	K17	17	11	33	35	11.02	33.04	Station	Station	Brent	No
        Amersham	D2	2	4	48	42	4.01	48.02	Station	Station	Chiltern	No
        Angel	AB17	17	28	33	18	28.04	33.05	Station	Station	Islington	No
        Archway	AA11	11	27	39	19	27.05	39.02	Station	Station	Islington	No
        Arnos Grove	AD4	4	30	46	16	30.05	46.02	Station	Station	Enfield	No
        Arsenal	AD10	10	30	40	16	30.01	40.04	Station	Station	Islington	No
        Baker Street	V17	17	22	33	24	22.01	33.02	Station	Station	City of Westminster	No
        Balham	X45	45	24	5	22	24.02	5.01	Station	Station	Wandsworth	No
        Bank & Monument	AD25	25	30	25	16	30.05	25.02	Station	Station	City of London	No
        Barbican	AB19	19	28	31	18	28.02	31.04	Station	Station	City of London	No
        Barking	AP14	14	42	36	4	42.03	36.01	Station	Station	Barking and Dagenham	No
        Barkingside	AO10	10	41	40	5	41.02	40.02	Station	Station	Redbridge	No
        Barons Court	R30	30	18	20	28	18.02	20.03	Station	Station	Hammersmith and Fulham	No
        Bayswater	S20	20	19	30	27	19.01	30.04	Station	Station	City of Westminster	No
        Becontree	AQ12	12	43	38	3	43.01	38.04	Station	Station	Barking and Dagenham	No
        Belsize Park	Y12	12	25	38	21	25.01	38.03	Station	Station	Camden	No
        Bermondsey	AG30	30	33	20	13	33.02	20.01	Station	Station	Southwark	No
        Bethnal Green	AI17	17	35	33	11	35.01	33.05	Station	Station	Tower Hamlets	No
        Blackfriars	AC29	29	29	21	17	29.03	21.05	Station	Station	City of London	No
        Blackhorse Road	AH8	8	34	42	12	34.03	42.03	Station	Station	Waltham Forest	No
        Bond Street	W22	22	23	28	23	23.03	28.01	Station	Station	City of Westminster	No
        Borough	AE36	36	31	14	15	31.02	14.01	Station	Station	Southwark	No
        Boston Manor	H31	31	8	19	38	8.05	19.04	Station	Station	Ealing	No
        Bounds Green	AD5	5	30	45	16	30.01	45.05	Station	Station	Haringey	No
        Bow Road	AK19	19	37	31	9	37.05	31.04	Station	Station	Tower Hamlets	No
        Brent Cross	W9	9	23	41	23	23.03	41.05	Station	Station	Barnet	No
        Brixton	AB43	43	28	7	18	28.05	7.04	Station	Station	Lambeth	No
        Bromley-by-Bow	AL19	19	38	31	8	38.02	31.02	Station	Station	Tower Hamlets	No
        Buckhurst Hill	AL7	7	38	43	8	38.01	43.02	Station	Station	Epping Forest	No
        Burnt Oak	U6	6	21	44	25	21.02	44.03	Station	Station	Barnet	No
        Caledonian Road	AC13	13	29	37	17	29.03	37.02	Station	Station	Islington	No
        Camden Town	Z14	14	26	36	20	26.03	36.04	Station	Station	Camden	No
        Canada Water	AH30	30	34	20	12	34.05	20.03	Station	Station	Southwark	No
        Canary Wharf	AJ30	30	36	20	10	36.01	20.04	Station	Station	Tower Hamlets	No
        Canning Town	AL22	22	38	28	8	38.05	28.03	Station	Station	Newham	No
        Cannon Street	AD27	27	30	23	16	30.04	23.05	Station	Station	City of London	No
        Canons Park	S7	7	19	43	27	19.02	43.04	Station	Station	Harrow	No
        Chalfont & Latimer	F2	2	6	48	40	6.01	48.04	Station	Station	Chiltern	No
        Chalk Farm	Y13	13	25	37	21	25.03	37.03	Station	Station	Camden	No
        Chancery Lane	AB23	23	28	27	18	28.02	27.04	Station	Station	City of London	No
        Charing Cross	Z28	28	26	22	20	26.05	22.03	Station	Station	City of Westminster	No
        Chesham	E1	1	5	49	41	5.04	49.04	Station	Station	Chiltern	No
        Chigwell	AN7	7	40	43	6	40.02	43.04	Station	Station	Epping Forest	No
        Chiswick Park	M30	30	13	20	33	13.01	20.01	Station	Station	Ealing	No
        Chorleywood	G3	3	7	47	39	7.01	47.04	Station	Station	Three Rivers	No
        Clapham Common	Y43	43	25	7	21	25.04	7.02	Station	Station	Lambeth	No
        Clapham North	Y42	42	25	8	21	25.03	8.05	Station	Station	Lambeth	No
        Clapham South	Y44	44	25	6	21	25.03	6.05	Station	Station	Wandsworth	No
        Cockfosters	AD1	1	30	49	16	30.03	49.05	Station	Station	Enfield	No
        Colindale	V7	7	22	43	24	22.03	43.02	Station	Station	Barnet	No
        Colliers Wood	W48	48	23	2	23	23.01	2.02	Station	Station	Merton	No
        Covent Garden	Z24	24	26	26	20	26.05	26.02	Station	Station	City of Westminster	No
        Croxley	I3	3	9	47	37	9.02	47.03	Station	Station	Three Rivers	No
        Dagenham East	AR10	10	44	40	2	44.03	40.04	Station	Station	Barking and Dagenham	No
        Dagenham Heathway	AR11	11	44	39	2	44.05	39.05	Station	Station	Barking and Dagenham	No
        Debden	AL5	5	38	45	8	38.02	45.04	Station	Station	Epping Forest	No
        Dollis Hill	T11	11	20	39	26	20.01	39.01	Station	Station	Brent	No
        Ealing Broadway	J26	26	10	24	36	10.03	24.04	Station	Station	Ealing	No
        Ealing Common	K28	28	11	22	35	11.03	22.03	Station	Station	Ealing	No
        Earl's Court	T30	30	20	20	26	20.05	20.01	Station	Station	Kensington and Chelsea	No
        East Acton	N26	26	14	24	32	14.01	24.01	Station	Station	Hammersmith and Fulham	No
        East Finchley	AA9	9	27	41	19	27.05	41.02	Station	Station	Barnet	No
        East Ham	AO15	15	41	35	5	41.03	35.02	Station	Station	Newham	No
        East Putney	T39	39	20	11	26	20.05	11.01	Station	Station	Wandsworth	No
        Eastcote	J12	12	10	38	36	10.01	38.01	Station	Station	Hillingdon	No
        Edgware	U5	5	21	45	25	21.05	45.03	Station	Station	Barnet	No
        Edgware Road (Bak)	T16	16	20	34	26	20.02	34.04	Station	Station	City of Westminster	No
        Edgware Road (Cir)	T17	17	20	33	26	20.02	33.05	Station	Station	City of Westminster	No
        Elephant & Castle	AD38	38	30	12	16	30.04	12.03	Station	Station	Southwark	No
        Elm Park	AS9	9	45	41	1	45.02	41.03	Station	Station	Havering	No
        Embankment	AA30	30	27	20	19	27.01	20.02	Station	Station	City of Westminster	No
        Epping	AL3	3	38	47	8	38.05	47.03	Station	Station	Epping Forest	No
        Euston	Y16	16	25	34	21	25.01	34.03	Station	Station	Camden	No
        Euston Square	X17	17	24	33	22	24.01	33.01	Station	Station	Camden	No
        Fairlop	AO9	9	41	41	5	41.02	41.04	Station	Station	Redbridge	No
        Farringdon	AA18	18	27	32	19	27.04	32.01	Station	Station	Islington	No
        Finchley Central	AA8	8	27	42	19	27.01	42.04	Station	Station	Barnet	No
        Finchley Road	U14	14	21	36	25	21.03	36.05	Station	Station	Camden	No
        Finsbury Park	AE9	9	31	41	15	31.02	41.02	Station	Station	Islington	No
        Fulham Broadway	T33	33	20	17	26	20.02	17.05	Station	Station	Hammersmith and Fulham	No
        Gants Hill	AO12	12	41	38	5	41.01	38.02	Station	Station	Redbridge	No
        Gloucester Road	U30	30	21	20	25	21.05	20.02	Station	Station	Kensington and Chelsea	No
        Golders Green	W10	10	23	40	23	23.02	40.02	Station	Station	Barnet	No
        Goldhawk Road	P28	28	16	22	30	16.01	22.01	Station	Station	Hammersmith and Fulham	No
        Goodge Street	Y20	20	25	30	21	25.03	30.02	Station	Station	Camden	No
        Grange Hill	AO7	7	41	43	5	41.03	43.01	Station	Station	Redbridge	No
        Great Portland Street	W17	17	23	33	23	23.05	33.02	Station	Station	City of Westminster	No
        Green Park	X26	26	24	24	22	24.03	24.01	Station	Station	City of Westminster	No
        Greenford	H20	20	8	30	38	8.03	30.05	Station	Station	Ealing	No
        Gunnersbury	N32	32	14	18	32	14.03	18.02	Station	Station	Hounslow	No
        Hainault	AO8	8	41	42	5	41.05	42.04	Station	Station	Redbridge	No
        Hammersmith (Dis)	Q30	30	17	20	29	17.04	20.02	Station	Station	Hammersmith and Fulham	No
        Hammersmith (H&C)	P29	29	16	21	30	16.05	21.05	Station	Station	Hammersmith and Fulham	No
        Hampstead	X11	11	24	39	22	24.03	39.02	Station	Station	Camden	No
        Hanger Lane	J22	22	10	28	36	10.05	28.01	Station	Station	Ealing	No
        Harlesden	O12	12	15	38	31	15.03	38.04	Station	Station	Brent	No
        Harrow & Wealdstone	O6	6	15	44	31	15.03	44.02	Station	Station	Harrow	No
        Harrow-on-the-Hill	L10	10	12	40	34	12.05	40.04	Station	Station	Harrow	No
        Hatton Cross	C36	36	3	14	43	3.01	14.03	Station	Station	Hillingdon	No
        Heathrow Terminals 123	B37	37	2	13	44	2.02	13.04	Station	Station	Hillingdon	No
        Heathrow Terminal 4	B38	38	2	12	44	2.03	12.05	Station	Station	Hillingdon	No
        Heathrow Terminal 5	A38	38	1	12	45	1.03	12.04	Station	Station	Hillingdon	No
        Hendon Central	V8	8	22	42	24	22.05	42.05	Station	Station	Barnet	No
        High Barnet	AA4	4	27	46	19	27.01	46.01	Station	Station	Barnet	No
        High Street Kensington	S27	27	19	23	27	19.02	23.05	Station	Station	Kensington and Chelsea	No
        Highbury & Islington	AD13	13	30	37	16	30.05	37.05	Station	Station	Islington	No
        Highgate	AA10	10	27	40	19	27.01	40.01	Station	Station	Haringey	No
        Hillingdon	F12	12	6	38	40	6.01	38.02	Station	Station	Hillingdon	No
        Holborn	AA22	22	27	28	19	27.03	28.05	Station	Station	Camden	No
        Holland Park	R26	26	18	24	28	18.03	24.03	Station	Station	Kensington and Chelsea	No
        Holloway Road	AC11	11	29	39	17	29.01	39.01	Station	Station	Islington	No
        Hornchurch	AS8	8	45	42	1	45.01	42.04	Station	Station	Havering	No
        Hounslow Central	E34	34	5	16	41	5.05	16.03	Station	Station	Hounslow	No
        Hounslow East	F33	33	6	17	40	6.03	17.05	Station	Station	Hounslow	No
        Hounslow West	D35	35	4	15	42	4.03	15.05	Station	Station	Hounslow	No
        Hyde Park Corner	W27	27	23	23	23	23.03	23.05	Station	Station	City of Westminster	No
        Ickenham	G12	12	7	38	39	7.01	38.04	Station	Station	Hillingdon	No
        Kennington	AB39	39	28	11	18	28.04	11.04	Station	Station	Southwark	No
        Kensal Green	O14	14	15	36	31	15.03	36.05	Station	Station	Brent	No
        Kensington (Olympia)	R27	27	18	23	28	18.04	23.04	Station	Station	Kensington and Chelsea	No
        Kentish Town	AA13	13	27	37	19	27.02	37.05	Station	Station	Camden	No
        Kenton	O7	7	15	43	31	15.03	43.04	Station	Station	Brent	No
        Kew Gardens	N34	34	14	16	32	14.04	16.04	Station	Station	Richmond	No
        Kilburn	U12	12	21	38	25	21.01	38.02	Station	Station	Brent	No
        Kilburn Park	O16	16	15	34	31	15.01	34.01	Station	Station	Brent	No
        King's Cross St. Pancras	Z17	17	26	33	20	26.01	33.05	Station	Station	Camden	No
        Kingsbury	S9	9	19	41	27	19.04	41.01	Station	Station	Brent	No
        Knightsbridge	V28	28	22	22	24	22.03	22.05	Station	Station	Kensington and Chelsea	No
        Ladbroke Grove	P20	20	16	30	30	16.02	30.05	Station	Station	Kensington and Chelsea	No
        Lambeth North	AB36	36	28	14	18	28.01	14.02	Station	Station	Lambeth	No
        Lancaster Gate	U24	24	21	26	25	21.02	26.04	Station	Station	City of Westminster	No
        Latimer Road	P22	22	16	28	30	16.04	28.02	Station	Station	Kensington and Chelsea	No
        Leicester Square	Z25	25	26	25	20	26.03	25.03	Station	Station	City of Westminster	No
        Leyton	AL15	15	38	35	8	38.02	35.02	Station	Station	Waltham Forest	No
        Leytonstone	AL14	14	38	36	8	38.01	36.05	Station	Station	Waltham Forest	No
        Liverpool Street	AE20	20	31	30	15	31.01	30.01	Station	Station	City of London	No
        London Bridge	AF30	30	32	20	14	32.02	20.03	Station	Station	Southwark	No
        Loughton	AL6	6	38	44	8	38.03	44.02	Station	Station	Epping Forest	No
        Maida Vale	P16	16	16	34	30	16.01	34.04	Station	Station	City of Westminster	No
        Manor House	AD8	8	30	42	16	30.03	42.04	Station	Station	Hackney	No
        Mansion House	AC28	28	29	22	17	29.03	22.05	Station	Station	City of London	No
        Marble Arch	V23	23	22	27	24	22.02	27.05	Station	Station	City of Westminster	No
        Marylebone	U17	17	21	33	25	21.03	33.01	Station	Station	City of Westminster	No
        Mile End	AJ19	19	36	31	10	36.02	31.02	Station	Station	Tower Hamlets	No
        Mill Hill East	Z7	7	26	43	20	26.03	43.03	Station	Station	Barnet	No
        Moor Park	I5	5	9	45	37	9.02	45.02	Station	Station	Three Rivers	No
        Moorgate	AC20	20	29	30	17	29.01	30.01	Station	Station	City of London	No
        Morden	U50	50	21	0	25	21.04	0.05	Station	Station	Merton	No
        Mornington Crescent	Y15	15	25	35	21	25.03	35.02	Station	Station	Camden	No
        Neasden	T10	10	20	40	26	20.04	40.04	Station	Station	Brent	No
        Newbury Park	AO11	11	41	39	5	41.03	39.02	Station	Station	Redbridge	No
        North Acton	M26	26	13	24	33	13.01	24.04	Station	Station	Ealing	No
        North Ealing	K24	24	11	26	35	11.02	26.05	Station	Station	Ealing	No
        North Greenwich	AL27	27	38	23	8	38.02	23.01	Station	Station	Greenwich	No
        North Harrow	K8	8	11	42	35	11.01	42.05	Station	Station	Harrow	No
        North Wembley	O9	9	15	41	31	15.01	41.03	Station	Station	Brent	No
        Northfields	I30	30	9	20	37	9.04	20.05	Station	Station	Ealing	No
        Northolt	G18	18	7	32	39	7.04	32.03	Station	Station	Ealing	No
        Northwick Park	M10	10	13	40	33	13.03	40.04	Station	Station	Brent	No
        Northwood	J6	6	10	44	36	10.03	44.02	Station	Station	Hillingdon	No
        Northwood Hills	J7	7	10	43	36	10.01	43.02	Station	Station	Hillingdon	No
        Notting Hill Gate	S26	26	19	24	27	19.01	24.02	Station	Station	Kensington and Chelsea	No
        Oakwood	AD2	2	30	48	16	30.05	48.02	Station	Station	Enfield	No
        Old Street	AC18	18	29	32	17	29.02	32.04	Station	Station	Islington	No
        Osterley	G32	32	7	18	39	7.02	18.05	Station	Station	Hounslow	No
        Oval	AA40	40	27	10	19	27.05	10.04	Station	Station	Lambeth	No
        Oxford Circus	X22	22	24	28	22	24.02	28.05	Station	Station	City of Westminster	No
        Paddington	S17	17	19	33	27	19.02	33.03	Station	Station	City of Westminster	No
        Park Royal	K23	23	11	27	35	11.03	27.01	Station	Station	Ealing	No
        Parsons Green	T34	34	20	16	26	20.05	16.01	Station	Station	Hammersmith and Fulham	No
        Perivale	I21	21	9	29	37	9.01	29.05	Station	Station	Ealing	No
        Piccadilly Circus	Y26	26	25	24	21	25.04	24.04	Station	Station	City of Westminster	No
        Pimlico	X35	35	24	15	22	24.04	15.04	Station	Station	City of Westminster	No
        Pinner	K7	7	11	43	35	11.03	43.05	Station	Station	Harrow	No
        Plaistow	AN17	17	40	33	6	40.04	33.03	Station	Station	Newham	No
        Preston Road	Q10	10	17	40	29	17.04	40.04	Station	Station	Brent	No
        Putney Bridge	T35	35	20	15	26	20.04	15.01	Station	Station	Hammersmith and Fulham	No
        Queen's Park	O15	15	15	35	31	15.01	35.03	Station	Station	Brent	No
        Queensbury	S8	8	19	42	27	19.03	42.03	Station	Station	Brent	No
        Queensway	T26	26	20	24	26	20.03	24.02	Station	Station	City of Westminster	No
        Ravenscourt Park	P30	30	16	20	30	16.02	20.03	Station	Station	Hammersmith and Fulham	No
        Rayners Lane	K13	13	11	37	35	11.03	37.02	Station	Station	Harrow	No
        Redbridge	AN12	12	40	38	6	40.02	38.01	Station	Station	Redbridge	No
        Regent's Park	W20	20	23	30	23	23.01	30.02	Station	Station	City of Westminster	No
        Richmond	N35	35	14	15	32	14.04	15.01	Station	Station	Richmond	No
        Rickmansworth	H4	4	8	46	38	8.04	46.04	Station	Station	Three Rivers	No
        Roding Valley	AM7	7	39	43	7	39.03	43.02	Station	Station	Epping Forest	No
        Royal Oak	R18	18	18	32	28	18.05	32.05	Station	Station	City of Westminster	No
        Ruislip	H12	12	8	38	38	8.04	38.01	Station	Station	Hillingdon	No
        Ruislip Gardens	G14	14	7	36	39	7.04	36.05	Station	Station	Hillingdon	No
        Ruislip Manor	I12	12	9	38	37	9.03	38.01	Station	Station	Hillingdon	No
        Russell Square	Z20	20	26	30	20	26.01	30.02	Station	Station	Camden	No
        Seven Sisters	AF8	8	32	42	14	32.03	42.03	Station	Station	Haringey	No
        Shepherd's Bush (Cen)	Q26	26	17	24	29	17.02	24.01	Station	Station	Hammersmith and Fulham	No
        Shepherd's Bush (H&C)	P27	27	16	23	30	16.04	23.01	Station	Station	Hammersmith and Fulham	No
        Sloane Square	W30	30	23	20	23	23.03	20.01	Station	Station	Kensington and Chelsea	No
        Snaresbrook	AL12	12	38	38	8	38.05	38.02	Station	Station	Redbridge	No
        South Ealing	J29	29	10	21	36	10.04	21.01	Station	Station	Ealing	No
        South Harrow	K14	14	11	36	35	11.01	36.01	Station	Station	Harrow	No
        South Kensington	V30	30	22	20	24	22.03	20.01	Station	Station	Kensington and Chelsea	No
        South Kenton	O8	8	15	42	31	15.01	42.03	Station	Station	Brent	No
        South Ruislip	G16	16	7	34	39	7.03	34.01	Station	Station	Hillingdon	No
        South Wimbledon	V49	49	22	1	24	22.02	1.03	Station	Station	Merton	No
        South Woodford	AL11	11	38	39	8	38.05	39.04	Station	Station	Redbridge	No
        Southfields	T40	40	20	10	26	20.01	10.05	Station	Station	Wandsworth	No
        Southgate	AD3	3	30	47	16	30.01	47.04	Station	Station	Enfield	No
        Southwark	AD34	34	30	16	16	30.05	16.01	Station	Station	Southwark	No
        St. James's Park	Y30	30	25	20	21	25.03	20.05	Station	Station	City of Westminster	No
        St. John's Wood	V16	16	22	34	24	22.04	34.02	Station	Station	City of Westminster	No
        St. Paul's	AC24	24	29	26	17	29.01	26.04	Station	Station	City of London	No
        Stamford Brook	O30	30	15	20	31	15.03	20.03	Station	Station	Hammersmith and Fulham	No
        Stanmore	S6	6	19	44	27	19.05	44.02	Station	Station	Harrow	No
        Stepney Green	AI19	19	35	31	11	35.05	31.02	Station	Station	Tower Hamlets	No
        Stockwell	Z41	41	26	9	20	26.03	9.05	Station	Station	Lambeth	No
        Stonebridge Park	O11	11	15	39	31	15.02	39.04	Station	Station	Brent	No
        Stratford	AL16	16	38	34	8	38.03	34.05	Station	Station	Newham	No
        Sudbury Hill	K15	15	11	35	35	11.03	35.01	Station	Station	Ealing	No
        Sudbury Town	K16	16	11	34	35	11.01	34.04	Station	Station	Brent	No
        Swiss Cottage	V15	15	22	35	24	22.03	35.01	Station	Station	Camden	No
        Temple	AB30	30	28	20	18	28.02	20.03	Station	Station	City of Westminster	No
        Theydon Bois	AL4	4	38	46	8	38.04	46.02	Station	Station	Epping Forest	No
        Tooting Bec	X46	46	24	4	22	24.05	4.01	Station	Station	Wandsworth	No
        Tooting Broadway	X47	47	24	3	22	24.01	3.04	Station	Station	Wandsworth	No
        Tottenham Court Road	Y22	22	25	28	21	25.04	28.02	Station	Station	City of Westminster	No
        Tottenham Hale	AG8	8	33	42	13	33.05	42.04	Station	Station	Haringey	No
        Totteridge & Whetstone	AA5	5	27	45	19	27.03	45.05	Station	Station	Barnet	No
        Tower Hill	AF24	24	32	26	14	32.01	26.04	Station	Station	Tower Hamlets	No
        Tufnell Park	AA12	12	27	38	19	27.03	38.04	Station	Station	Islington	No
        Turnham Green	N30	30	14	20	32	14.03	20.01	Station	Station	Hounslow	No
        Turnpike Lane	AD7	7	30	43	16	30.01	43.02	Station	Station	Haringey	No
        Upminster	AT6	6	46	44	0	46.05	44.05	Station	Station	Havering	No
        Upminster Bridge	AT7	7	46	43	0	46.04	43.02	Station	Station	Havering	No
        Upney	AQ13	13	43	37	3	43.04	37.04	Station	Station	Barking and Dagenham	No
        Upton Park	AN16	16	40	34	6	40.04	34.02	Station	Station	Newham	No
        Uxbridge	E12	12	5	38	41	5.03	38.05	Station	Station	Hillingdon	No
        Vauxhall	X38	38	24	12	22	24.05	12.03	Station	Station	Lambeth	No
        Victoria	X30	30	24	20	22	24.05	20.01	Station	Station	City of Westminster	No
        Walthamstow Central	AI8	8	35	42	11	35.04	42.03	Station	Station	Waltham Forest	No
        Wanstead	AM12	12	39	38	7	39.01	38.03	Station	Station	Redbridge	No
        Warren Street	Y18	18	25	32	21	25.02	32.04	Station	Station	Camden	No
        Warwick Avenue	Q16	16	17	34	29	17.01	34.01	Station	Station	City of Westminster	No
        Waterloo	AA33	33	27	17	19	27.04	17.03	Station	Station	Lambeth	No
        Watford	I1	1	9	49	37	9.02	49.03	Station	Station	Watford	No
        Wembley Central	O10	10	15	40	31	15.04	40.05	Station	Station	Brent	No
        Wembley Park	R11	11	18	39	28	18.04	39.01	Station	Station	Brent	No
        West Acton	L26	26	12	24	34	12.02	24.02	Station	Station	Ealing	No
        West Brompton	T32	32	20	18	26	20.03	18.03	Station	Station	Kensington and Chelsea	No
        West Finchley	AA7	7	27	43	19	27.02	43.03	Station	Station	Barnet	No
        West Ham	AM18	18	39	32	7	39.01	32.02	Station	Station	Newham	No
        West Hampstead	U13	13	21	37	25	21.01	37.05	Station	Station	Camden	No
        West Harrow	K10	10	11	40	35	11.04	40.02	Station	Station	Harrow	No
        West Kensington	S30	30	19	20	27	19.03	20.05	Station	Station	Hammersmith and Fulham	No
        West Ruislip	G8	8	7	42	39	7.05	42.03	Station	Station	Hillingdon	No
        Westbourne Park	Q19	19	17	31	29	17.01	31.05	Station	Station	City of Westminster	No
        Westminster	Z30	30	26	20	20	26.05	20.05	Station	Station	City of Westminster	No
        White City	O26	26	15	24	31	15.03	24.04	Station	Station	Hammersmith and Fulham	No
        Whitechapel	AH20	20	34	30	12	34.02	30.03	Station	Station	Tower Hamlets	No
        Willesden Green	T12	12	20	38	26	20.02	38.02	Station	Station	Brent	No
        Willesden Junction	O13	13	15	37	31	15.02	37.05	Station	Station	Brent	No
        Wimbledon	T42	42	20	8	26	20.01	8.02	Station	Station	Merton	No
        Wimbledon Park	T41	41	20	9	26	20.01	9.03	Station	Station	Merton	No
        Wood Green	AD6	6	30	44	16	30.04	44.03	Station	Station	Haringey	No
        Wood Lane	P25	25	16	25	30	16.02	25.05	Station	Station	Hammersmith and Fulham	No
        Woodford	AL10	10	38	40	8	38.03	40.03	Station	Station	Redbridge	No
        Woodside Park	AA6	6	27	44	19	27.05	44.02	Station	Station	Barnet	No
        river1	A40	40	1	10	45	1.01	10.03	RiverHorizontal	River		No
        river2	B40	40	2	10	44	2.04	10.02	RiverHorizontal	River		No
        river3	C40	40	3	10	43	3.05	10.01	RiverHorizontal	River		No
        river4	D40	40	4	10	42	4.01	10.01	RiverHorizontal	River		No
        river5	E40	40	5	10	41	5.02	10.01	RiverHorizontal	River		No
        river6	F40	40	6	10	40	6.04	10.02	RiverHorizontal	River		No
        river7	G40	40	7	10	39	7.05	10.02	RiverHorizontal	River		No
        river8	H40	40	8	10	38	8.01	10.05	RiverHorizontal	River		No
        river9	I40	40	9	10	37	9.04	10.02	RiverHorizontal	River		No
        river10	J40	40	10	10	36	10.01	10.02	RiverHorizontal	River		No
        river11	K40	40	11	10	35	11.03	10.05	RiverHorizontal	River		No
        river12	L40	40	12	10	34	12.03	10.01	RiverHorizontal	River		No
        river13	M40	40	12.99999	10	33.00001	13.01	10.04	RiverCurveHVLeft	River		No
        river20	M33	33	13	17	33	13.01	17.03	RiverCurveVHRight	River		No
        river21	N33	33	14	17	32	14.01	17.04	RiverHorizontal	River		No
        river22	O33	33	15	17	31	15.04	17.02	RiverCurve45HV	River		No
        river23	P34	34	16	16	30	16.03	16.03	River45D	River		No
        river24	Q35	35	17	15	29	17.02	15.02	River45D	River		No
        river25	R36	36	18	14	28	18.02	14.03	River45D	River		No
        river26	S37	37	19	13	27	19.04	13.01	RiverCurve45H	River		No
        river27	T37	37	20	13	26	20.03	13.02	RiverHorizontal	River		No
        river28	U37	37	21	13	25	21.05	13.02	RiverHorizontal	River		No
        river29	V37	37	22	13	24	22.02	13.05	RiverHorizontal	River		No
        river30	W37	37	23	13	23	23.01	13.03	RiverHorizontal	River		No
        river31	X37	37	24	13	22	24.03	13.02	RiverHorizontal	River		No
        river32	Y37	37	24.9999	13	21.0001	25.04	13.03	RiverCurveHVLeft	River		No
        river37	Y32	32	25	18	21	25.03	18.03	RiverCurveVHRight	River		No
        river38	Z32	32	26	18	20	26.03	18.02	RiverHorizontal	River		No
        river39	AA32	32	27	18	19	27.01	18.03	RiverHorizontal	River		No
        river40	AB32	32	28	18	18	28.03	18.05	RiverCurveV45	River		No
        river41	AC31	31	29	19	17	29.05	19.04	River45U	River		No
        river42	AD30	30	30	20	16	30.01	20.04	River45U	River		No
        river43	AE29	29	31	21	15	31.02	21.01	River45U	River		No
        river44	AF28	28	32	22	14	32.03	22.05	River45U	River		No
        river45	AG27	27	33	23	13	33.03	23.03	RiverCurve45HLeft	River		No
        river46	AH27	27	34	23	12	34.01	23.01	RiverHorizontal	River		No
        river47	AI27	27	34.9999	23	11.0001	35.03	23.03	RiverCurveHVRight	River		No
        river54	AI34	34	35	16	11	35.02	16.05	RiverCurveVHLeft	River		No
        river55	AJ34	34	36	16	10	36.05	16.04	RiverHorizontal	River		No
        river56	AK34	34	36.9999	16	9.0001	37.01	16.03	RiverCurveHVLeft	River		No
        river65	AK25	25	37	25	9	37.05	25.04	RiverCurveVHRight	River		No
        river66	AL25	25	38	25	8	38.01	25.01	RiverHorizontal	River		No
        river67	AM25	25	39	25	7	39.04	25.04	RiverHorizontal	River		No
        river68	AN25	25	39.9999	25	6.0001	40.01	25.02	RiverCurveHVRight	River		No
        river75	AN32	32	40	18	6	40.02	18.04	RiverCurveVHLeft	River		No
        river76	AO32	32	41	18	5	41.03	18.04	RiverHorizontal	River		No
        river77	AP32	32	42	18	4	42.04	18.02	RiverHorizontal	River		No
        river78	AQ32	32	43	18	3	43.05	18.01	RiverHorizontal	River		No
        river79	AR32	32	44	18	2	44.02	18.03	RiverHorizontal	River		No
        river80	AS32	32	45	18	1	45.02	18.01	RiverHorizontal	River		No
        river81	AT32	32	46	18	0	46.05	18.03	RiverHorizontal	River		No
        zone1	R16	16	17.9999	34	28.0001	18.01	34.05	Zone1NWAngle	Zone1		Yes
        zone2	R28	28	18	22	28	18.02	22.04	Zone1Horizontal	Zone1		Yes
        zone3	S28	28	18.9999	22	27.0001	19.04	22.03	Zone1Horizontal	Zone1		Yes
        zone4	S32	32	19	18	27	19.05	18.02	Zone1Horizontal	Zone1		Yes
        zone5	V32	32	21.9999	18	24.0001	22.02	18.02	Zone1Horizontal	Zone1		Yes
        zone6	V39	39	22	11	24	22.05	11.02	Zone1Horizontal	Zone1		Yes
        zone7	AG39	39	32.9999	11	13.0001	33.01	11.02	Zone1Horizontal	Zone1		Yes
        zone8	AG29	29	33	21	13	33.01	21.02	Zone1Horizontal	Zone1		Yes
        zone9	AH29	29	33.9999	21	12.0001	34.02	21.03	Zone1Horizontal	Zone1		Yes
        zone10	AH16	16	34	34	12	34.02	34.01	Zone1Horizontal	Zone1		Yes """
          |> fromDelimited '\t'
```
