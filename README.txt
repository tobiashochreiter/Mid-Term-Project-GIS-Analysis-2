# Reproduction of Green Space Accessibility Analysis (Graz)

This project reproduces and adapts the methodology of a published GIS-based study on accessibility to public green spaces in Graz.

## Description 
While the original paper investigates green-space accessibility in Craiova, Romania, we apply the same core workflow to the city of **Graz, Austria**, adapting the datasets and implementation using open geospatial data and Python-based GIS tools. The workflow can therefore be adapted to any city. The main objective is to identify **residential areas with insufficient access to public green spaces** and to relate these areas to **population density at district level**.

---

## Dependencies
- Developed in Python 3.11
- install osmnx keplergl geopandas shapely matplotlib pandas seaborn numpy

## Installing
- pull from https://github.com/tobiashochreiter/Mid-Term-Project-GIS-Analysis-2 
- for a different study area, adapt data integration section

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
   - Generate access points for green spaces  
   - Calculate Euclidean distance from residential areas  
   - Identify residential areas beyond the defined accessibility threshold  

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

Compared to the original paper, we made the following adaptations:
- Different study area (Graz instead of [Original Area])  
- Open data instead of proprietary datasets  
- Simplified distance measure (Euclidean instead of network-based distance)  
- Modified green-space classification to match OSM data availability  

These deviations were necessary due to **data availability and scale differences**.

---

## Limitations

- OpenStreetMap data completeness varies by location  
- Euclidean distance does not represent actual walking paths  
- Green-space accessibility does not account for quality or capacity  
- Population data is aggregated at district level  

---

## Reproducibility

All data is open-source and all steps of the analysis are documented in the .ipynb. 

---

## Authors
V. Duit, M. Erdler, Y. Fleischhacker, T. Hochreiter


Git Hub:

git pull (always do git pull before continuing with the code)
git stash (stashing own changes)
git pull
git stash pop (combine changes with own changes and check conflicts - then continue with new code)
git add .
git commit -m "Message"
git push
always push new changes after finishing working
