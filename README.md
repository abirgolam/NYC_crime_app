# NYC Crime Analysis Dashboard

An interactive **R Shiny** dashboard for exploring NYPD historic arrest data, with filterable tables, seasonal trend charts, and an interactive Leaflet map color-coded by offense severity.

**Live app:** https://abir-golam.shinyapps.io/final_app/ (deployed to shinyapps.io)

## Features

- **Filters:** year, age group, offense severity category, and perpetrator race, all applied reactively across every view
- **Dashboard tab:** a searchable data table (DT), a seasonal arrest-count bar chart (ggplot2), and summary statistics by severity
- **Map tab:** a Leaflet map of arrest locations, with markers colored by severity (High / Medium / Low / Other) and popups for date, charge, and category
- **Derived fields:** a season computed from the arrest date, plus a rule-based severity classifier that maps NYPD `OFNS_DESC` offense descriptions to High, Medium or Low

## Tech stack

R · Shiny · shinydashboard · dplyr · data.table · ggplot2 · DT · Leaflet · RColorBrewer

## Running locally

```r
install.packages(c("shiny", "shinydashboard", "dplyr", "ggplot2", "DT",
                   "data.table", "leaflet", "RColorBrewer"))
shiny::runApp("final_app")
```

The app expects the cleaned dataset at `final_app/data/NYPD_Arrests_Data_Historic_fully_cleaned.csv`. It is not checked in because of its size. The source is the public [NYPD Arrests Data (Historic)](https://data.cityofnewyork.us/Public-Safety/NYPD-Arrests-Data-Historic-/8h9b-rp9u) dataset on NYC Open Data. Cleaning involved removing invalid age groups and records without coordinates, and normalizing dates to `MM/DD/YYYY`.

## Project structure

```
final_app/
├── final_app.R        # UI + server in one file
└── data/              # (not committed) cleaned NYPD CSV
```

## Notes

Built as a graduate course project at Marquette University (MS Computer Science).
