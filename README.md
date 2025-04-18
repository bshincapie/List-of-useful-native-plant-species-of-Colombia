# Useful Plants of Colombia – Data Analysis

This repository contains scripts and functions developed to analyze a dataset of **useful native plant species of Colombia**, as part of a larger project led by the Royal Botanic Gardens, Kew, in collaboration with the Alexander von Humboldt Biological Resources Research Institute.
# Reference
Instituto de investigación de Recursos Biológicos Alexander von Humboldt y Royal Botanic Gardens, Kew.. 2023. Lista de las plantas nativas útiles de Colombia. Aportados por: Torres-Morales, G (Autor, editor, contacto del recurso), Aguilar, A (Autor), Jiménez, D (Autor), Guevara, L (Autor) & Alzate, B (Autor, proveedor de los metadatos). http://i2d.humboldt.org.co/ceiba/resource.do?r=plantas-utiles_2023

The dataset was compiled through a **systematic review of scientific articles, theses, books, and technical reports**, resulting in a database of 4,172 species from 234 plant families and 1,282 genera.

## 🔬 Objective

To explore patterns of plant uses in Colombia—such as medicinal, food, cosmetic, and environmental applications—and their distribution across departments, using data visualization, spatial mapping, and statistical summaries.

## 📁 Repository structure

```
├── scripts/                  # R scripts for data analysis and visualization
├── data/                    # (Not included) Original dataset [confidential]
│   └── data_example.xlsx    # Dummy file illustrating expected structure
├── mapas_generados/         # Output: maps by department (created by script)
├── carpeta_de_graficas/     # Output: barplots per use category
├── depto2/                  # Shapefile folder for Colombian departments
├── README.md                # Project documentation
└── .gitignore               # Excludes sensitive files and large data
```

## 📊 Main analyses

- Summary statistics of use categories
- Interactive pie charts, histograms, and funnel plots with `plotly`
- Frequency analysis of uses per department
- Generation of maps with `ggplot2` and `sf` (per-use and total)

## ⚙️ Technologies used

- **R** and RStudio
- **MySQL** for data storage and query filtering
- Libraries: `plotly`, `ggplot2`, `sf`, `dplyr`, `DataExplorer`, `readxl`, `openxlsx`
- Spatial data: Colombian department shapefile (`.shp`)

## 🔐 Data policy

The original dataset contains unpublished and sensitive information and is therefore **not publicly available**.

## ✍️ Author

**Brian Steven Alzate Hincapié**  
Biologist | Pollen and Plant Use Research | Universidad EAFIT  
Contact: bsalzateh@eafit.edu.co

---

```r
# Project: Data analysis on useful plants of Colombia
# Author: Brian Steven Alzate Hincapié
# Description: This script analyzes information on useful plants based on a confidential database (not included).

# Libraries
library(readxl)
library(plotly)
library(openxlsx)
library(ggthemes)
library(ggplot2)
library(DataExplorer)
library(sf)
library(dplyr)

# Load data (replace with real path or use a properly structured example file)
# para_analisis_de_datos_plantas <- read_excel("data/para_analisis_de_datos_plantas.xlsx", col_types = c("text", rep("text", 12), "numeric"))

# Exploratory analysis
# attach(para_analisis_de_datos_plantas)
# plot_missing(para_analisis_de_datos_plantas)
# summary(para_analisis_de_datos_plantas)
# apply(para_analisis_de_datos_plantas, MARGIN = 2, FUN = table)
# ftable(para_analisis_de_datos_plantas)
# rowSums(para_analisis_de_datos_plantas)

# Pie chart of uses (requires defining labels and values from the data)
# fig <- plot_ly(type='pie', labels=labels, values=values, textinfo='label+percent', insidetextorientation='radial')

# Histogram of total uses
# fig <- plot_ly(x = TotalUsos, type = "histogram")
# fig <- fig %>% layout(title = 'Plant Uses in Colombia', xaxis = list(title = "Total Uses"), yaxis = list(title = "Frequency"))

# Funnel Plot
# fig <- plot_ly() %>%
#   add_trace(type = "funnel", y = c(...), x = c(...)) %>%
#   layout(title = "Plant Uses")

# Departmental analysis
# Create departmental data frame (df)

# Function for data visualization
plot_barras <- function(df, variable, titulo, folder){
  conteo <- df[[variable]]
  names(conteo) <- df$Departmentos1
  conteo <- sort(conteo, decreasing = TRUE)[1:10]
  p <- plot_ly(x = conteo, y = names(conteo), type = "bar", orientation = 'h') %>%
    layout(title = titulo, xaxis = list(title = "Frequency"), yaxis = list(title = "Departments"))
  export(p, file = paste(folder, "/", titulo, ".png", sep = ""))
  return(p)
}

# Generate maps by variable
# deptos <- read_sf("./depto2/archivo_shapefile.shp")
# Merge data and plot maps for each variable in df

# Calculate and add total per department
# df$total <- rowSums(df[, -1])
# deptos_df <- left_join(deptos, df, by = c("name_1" = "Departmentos1"))
# plot <- ggplot(deptos_df) +
#   geom_sf(aes(fill = total)) +
#   scale_fill_gradient(low = "white", high = "darkgreen", na.value = "gray80") +
#   labs(title = "Total by Department", fill = "Total") +
#   theme_void()

# plot
