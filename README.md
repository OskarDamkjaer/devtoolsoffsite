# Graph Summit 2023 EMEA - Workshop Digital Twin (work in progress!)

This repository contains the workshop material used during the **Graph Summit 2023 Workshops**. All code, data, dashboards, Bloom perspectives and slides are available for dowload.

The aim of the workshop was, to provide a structure way of build a small mini digital twin knowledge graph. It is supposed to answer some basic questions coming from the business and discusses futher, how such digital twin graph could be extended for more insights and business values.

#### About the data that is been used

The datasets used here, describes a network of railroad tracks and places (so called operational units) 
connected to those tracks. Operational units can be a variaty of places like a Station, a Switch, etc., see the list below.

The dataset is essentailly a digital twin of the existing rail network.

The dataset is available in German on the OpenDB website of Deutsche Bahn (DB). We have renamed most headers, places, some city names, etc. into english names to make if more accessible for a broader audience. For the the workshop use the data from the directory above, **NOT** the orginal data from:

- [Original Track/Operational Unit Data](https://data.deutschebahn.com/dataset/)

---

#### Tracks

Tracks have a Track Number (and a Name, too) and they can cover longer distances, many places
(Operational Units) are on their way.

Think of it like an Highway, which has a name, and covers a long distance, passing many freeway
ramps, parking place, food areas, etc. belonging to different cities.

Tracks have the following interesting **Properties**:

- TRACK_NUM: the internal number
- KMSTR_E: an internal starting point (in km) on the one imagined abstract railroad.
- KMEND_E: the internal ending point on said imagined abstract railroad
- SHORTCUT: a short name
- TRACKNAME: is the name of the track correcponding to the shortcut

#### Operational Units

Following our image of an Highway, Operational Units (OUs) are like freeway ramps. They are connected to
a specific track. Because the tracks in cities are quite close together, we can group OUs
with the same shortname together, thinking of the group as a train station, or a place (City).

Operational units have the following **Properties:**

- TRACK_NUM: the internal number of the Track the OU is on
- DIRECTION: the direction it is on (maybe right side or left side of the track), not important so
  far
- DESCRIPTION: the longer name of a OU
- UNIT_KIND: the type of the OU. See belows list for more information of the meaning of the abbreviations
- SHORTCUT: the short, non-unique name of the OU, can be used for grouping
- LAT: latitude
- LONG: longitude
- KM_I: Internal reference point for the OU

Other data is imported, but not used in this demo.

#### Point of Interests

POIs are distributed through the country and refer to either a main station (and so to a city), or to a station that is closest by the POI. Reason is, that some POIs are in the country side and there is no station close by. POIs have the following interesting **Properties**:

- SHORTCUT: Shortcut of the station at the POI or close by
- CITY: City name at or close to the POI
- POI_DESCRIPTION: A short description of the POI
- LINK_FOTO: A URL to a POI Foto
- LINK_WEBSITE: A URL to a Website discussing POIs
- LAT: Latidude of the POI
- LONG: Longditude of the POI
- SECRET: Is the a well know POI (False) or more a secret place (True)


#### List describing the kind of Operational Units (OUs)

The data set contains different operational Units, whereas an OU can be from different types. The following is an incomplete list of all OUs covering most of them:

**Shortcut explanation:**

- Station = "St"
- Switch = "Swch"
- StopPoint = "Sp"
- BorderPoint = "Bp"
- StationSwitch = "St Swch"
- Reroute = "Rerout"
- StationPart = "Stp"
- StationPartSwitch = "Stp Swch"
- Bridge = "Cro"
- StopPointBridge = "Sp Cro"
- StationOutofService = "St o.S." --> Switches out of Service, etc. also available
- ConnectionPoint = "CoPt"
- StopPointBlockPoint = "Hp Bk"
- BlockPoint = "Bk"
- Track Change = "Trch"

---

---

## Building the demo environment

The following high level steps are required, to build the demo environment:

1. Download and install [Neo4j Desktop](https://neo4j.com/download-center/). Since we use some Graph Data Science Algorithms during the demo, we require the **GDS Library** to be installed. **Installation instruction** can be found [here](https://neo4j.com/docs/desktop-manual/current/).
- As an alternative, you can run an [Neo4j Sandbox for Data Scientists](https://sandbox.neo4j.com/?ref=neo4j-home-hero&persona=data-scientist) from (https://sandbox.neo4j.com/ and use an "Blank Sandbox"

2. Open Neo4j Browser and run the load-all-data.cypher script from the code directory above. You can cut & paste the code into the Neo4j Browser command line.

3. 