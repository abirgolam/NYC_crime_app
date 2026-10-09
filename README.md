# NYC Crime Analysis App

An interactive R Shiny dashboard for exploring NYPD arrest records by year, age group, offense severity, and demographics, with a filterable data table, a seasonal trend chart, summary statistics, and a Leaflet map.

**Live demo:** https://abir-golam.shinyapps.io/final_app/

Built during my M.S. in Computer Science at Marquette University. I explored the data in Tableau first, then built this interactive app in R Shiny.

## Features
- **Filters** in the sidebar: year, age group, offense category, and race. Every view updates reactively.
- **Dashboard tab**
  - a filterable, searchable data table (`DT`)
  - arrests by season (Winter → Fall), stacked by race (`ggplot2`)
  - summary counts of total, high, medium, and low severity arrests
- **Map tab**: every arrest plotted on a Leaflet map, colored by severity, with a popup showing date, charge, category, age group, and race.

## How offenses are categorized
Offense descriptions (`OFNS_DESC`) are bucketed with keyword rules:

| Category | Examples |
|---|---|
| High | homicide, rape, felony assault, kidnapping, robbery, arson |
| Medium | burglary, grand larceny, drug, fraud, weapons |
| Low | misdemeanors, harassment, trespass, disorderly conduct, traffic |
| Other | anything unmatched |

Rows are limited to the age groups 18–24, 25–44, 45–64 and 65+.

## Run it locally
1. Download **NYPD Arrests Data (Historic)** from [NYC Open Data](https://data.cityofnewyork.us/), clean it, and save it as `final_app/data/NYPD_Arrests_Data_Historic_fully_cleaned.csv`. The dataset is too large to keep in the repo.
2. Install the packages and run the app:
   ```r
   install.packages(c("shiny", "shinydashboard", "dplyr", "ggplot2", "DT",
                      "data.table", "leaflet", "RColorBrewer"))
   shiny::runApp("final_app")
   ```

## Stack
R · Shiny · shinydashboard · dplyr · data.table · ggplot2 · DT · Leaflet

## Known limitations
- Map marker size is meant to vary by age group, but `age_size()` receives a formula rather than each row's value, so every marker draws at the same size. The fix is to compute the radius with a vectorized lookup, for example `radius = ~ifelse(AGE_GROUP == "18-24", 8, ifelse(AGE_GROUP == "25-44", 6, 5))`.
- Severity buckets come from keyword matching, so some offenses fall into "Other". A lookup table keyed on offense code would be more precise.
