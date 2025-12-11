# Mid-Term-Project-GIS-Analysis-2
Reproduce Paper:  A GIS-based analysis of the urban green space
 accessibility in Craiova city, Romania (Vilcea C. & Sosea C. 2020)

Git Hub:
- git pull (always do git pull before continuing with the code)
- git stash (stashing own changes)
- git pull
- git stash pop (combine changes with own changes and check conflicts - then continue with new code)
- git add .
- git commit -m "Message"
- git push 
- always push new changes after finishing working

# Reproduction of Green Space Accessibility Analysis (Graz)

This project reproduces and adapts the methodology of a published GIS-based study on accessibility to public green spaces in Graz.

## Description 
While the original paper investigates green-space accessibility in Craiova, Romania, we apply the same core workflow to the city of **Graz, Austria**, adapting the datasets and implementation using open geospatial data and Python-based GIS tools. The workflow can therefore be adapted to any city. The main objective is to identify **residential areas with insufficient access to public green spaces** and to relate these areas to **population density at district level**.

---

## Dependencies
- Developed in Python 3.11+ (tested with Python 3.11 and 3.12)

- install osmnx keplergl geopandas shapely matplotlib pandas seaborn numpy


## Installation
- Clone the repository:

```bash
git clone https://github.com/tobiashochreiter/Mid-Term-Project-GIS-Analysis-2.git
cd Mid-Term-Project-GIS-Analysis-2


## Executing program
- if needed, adapt data integration; otherwise no user input needed
- run cell by cell or whole notebook for all results

---

## Original Study
Vîlcea, C., & Șoșea, C. (2020). A GIS-based analysis of the urban green space accessibility in Craiova city, Romania. Geografisk Tidsskrift-Danish Journal of Geography, 120(1), 19-34.
**Main idea:**  
- Measure accessibility to green spaces using distance-based criteria  
- Combine accessibility results with population data  
- Identify spatial inequalities in urban green-space provision  

---

## Study Area
- **City:** Graz, Austria  
- **Spatial units:** Administrative districts (“Bezirke”)  
- **Coordinate Reference System:** EPSG:31256 (MGI / Austria GK East)  

---

## Data Sources

### Spatial Data
- **Administrative boundaries:**  
  Source: City of Graz / Open Data Portal  
- **Street network:**  
  Source: OpenStreetMap via OSMnx  
- **Green spaces:**  
  Source: OpenStreetMap (OSM tags: `leisure`, `landuse`, `natural`, `amenity`)  

### Population Data
- **Population per district:**  
  Source: City of Graz statistics (`graz_bev.csv`)  
  Attributes:
  - District name  
  - Population (EW)  
  - Area (km²)  
  - Population density (persons/km²)  

---

## Workflow

The analysis follows these main steps:

1. **Data acquisition**
   - Download street network and green spaces using OSMnx
   - Load administrative boundaries and population data

2. **Data preprocessing**
   - Harmonize CRS across all layers  
   - Clean OSM green-space data (remove private or unsuitable areas)  
   - Buffer major roads to exclude unsuitable green spaces  

3. **Green-space selection**
   - Extract public, accessible green spaces  
   - Classify green spaces into thematic categories  
   - Exclude small green areas (< 1 ha)

4. **Accessibility analysis**
   - Generate access points at intersections between green-space boundaries and the street network  
   - Calculate accessibility using:
     - Euclidean distance buffers
     - Network-based walking distance (OSMnx graph)
   - Identify residential areas beyond predefined accessibility thresholds

5. **Population analysis**
   - Join population data to districts  
   - Visualize population density  
   - Overlay districts with deficient accessibility zones  

---

## Results

### Areal statistics

- Percentage of residential areas within certain distances to green spaces
- Deficient area percentages for each district (Euclidean and walking distance)
- Percentage of population within certain distances to green spaces
- "Greenness" of each district (percentage of green areas / public green spaces per district)
- Area percentage within certain walking distances to public green spaces

### Maps

- Map of all green spaces
- Map of public green spaces by category (urban forest, park, cemetery, other)
- Comparison: all public green spaces vs. public green spaces >1ha
- Comparison: public vs. non-public green spaces
- Kernel density (green spaces)
- Population density per district
- Map of residential areas
- Map of accessibility to public green spaces (Euclidean)
- Population density and deficient areas (poor access to green spaces)
- Map of accessibility to public green spaces (walking distance)
- Choropleth map of population density by district  
- Map of residential areas with poor access to green spaces  
- Combined visualization highlighting high-density districts with accessibility deficits  

---

## Differences to the Original Study

Compared to the original paper by Vîlcea & Șoșea (2020), we made the following adaptations:

- **Study area and population data**  
  - Different study area: Graz instead of Craiova  
  - Population data only available at district level, whereas the original study uses higher-resolution census data

- **Data sources and green-space definition**  
  - Public green spaces derived mainly from OpenStreetMap tags, instead of CORINE Land Cover / Urban Atlas combined with local authority datasets  
  - Our definition of “public green spaces” and the inclusion/exclusion rules (e.g. cemeteries, private gardens) therefore differ from the original study

- **Minimum size threshold**  
  - Several analyses focus on public green spaces larger than 1 ha  
  - The original study distinguishes different park size classes, but does not apply the same strict >1 ha cut-off for accessibility

- **Accessibility modeling and implementation**  
  - We implement the entire workflow in a fully scripted Python/Jupyter environment (osmnx, GeoPandas, etc.), whereas the original study uses ArcGIS 10.5 and Network Analyst  
  - While both studies compare Euclidean and network-based distances, details such as the derivation of park entrances, network processing and the construction of accessibility zones differ

- **Transport modes and access points**  
  - Our analysis focuses on walking distance only  
  - The original study additionally considers car access and integrates bus stops as further access points to green spaces

These deviations were necessary due to **data availability and scale differences**.

---

## Limitations

- OpenStreetMap data quality and completeness vary spatially and temporally.
- OSM tagging choices directly influence which green spaces are included or excluded.
- Euclidean distance does not reflect real walking paths or physical barriers.
- Network-based walking distances remain a simplified representation of pedestrian behavior.
- Automated derivation of green-space access points may miss informal or restricted entrances.
- Accessibility is assessed using distance only, not travel time or perceived effort.
- Green-space quality, amenities, size, and maintenance are not considered.
- User preferences and socio-demographic differences are not analyzed.
- Population data is aggregated at district level.
- Protected areas (e.g. Natura 2000 sites) are excluded from the accessibility analysis, even though public access may be possible in some cases.
- The >1 ha minimum size criterion excludes many small parks and pocket green spaces and can therefore change which districts appear well-served or deficient.


---

## Reproducibility

All data used in this project is open-source, and all steps of the analysis are fully 
documented and implemented in the provided Jupyter Notebook (.ipynb).  
The workflow can be re-run for the same study area or adapted to other cities using the 
same code base.


---

## Authors

V. Duit, M. Erdler, Y. Fleischhacker, T. Hochreiter
Date: 24.11.2025
