---
layout: project
title: 'Invasive Species Scanner'
caption: Tool for rapidly scanning a list of species for potential invasives
description: >
  Tool for rapidly scanning a list of species for potential invasives using webscraping and API calls
date: 1 March 2022
image: 
  path: /assets/img/projects/species_graphic.png
#   srcset: 
#     1920w: /assets/img/projects/VIRA.jpg
#     960w:  /assets/img/projects/qwtel@0,5x.jpg
#     480w:  /assets/img/projects/qwtel@0,25x.jpg
links:
  - title: Link
    url: https://re8gg2-johannes-nelson.shinyapps.io/invasive_species_scanner/
accent_color: '#4fb1ba'
accent_image: 
  background: '#193747'
theme_color: '#193747'
sitemap: false
---
### Invasive Species Scanner

## Overview
I developed this tool as a part of a much larger data analysis/processing pipeline when
I was working as a consultant for Conservation International (CI). This pipeline processes
and analyzes data from a massive tree restoration effort initiated by MasterCard called
the [Priceless Planet Coalition (PPC)](https://www.priceless.com/pricelessplanetcoalition),
which aims to restore 100 million trees by 2025. 

In order to ensure that these efforts go beyond simple 'tree planting' projects--which do not
always result in a genuinely restored ecosystem--a robust monitoring protocol was developed 
where project partner's would send people into the field periodically to collect data about 
the restoration sites--including things like counts of species and size classes of trees. 
Restoration requires ongoing work and attention. By including this monitoring protocol--which 
will go on for five years after initial planitng--CI and MasterCard can ensure that projects 
are indeed sustainably restoring trees and the myriad ecosystem services they provide. 

With so many project partners planting thousands of different species in dozens of different
countries, it is very important to ensure that invasive species are not being planted. Scanning
the list of planted species manually would have taken a long time, so I developed scripts to do
this rapidly. 

## How it works
The script relies primarily on web-scraping the [Global Invasive Species Database (GISD)](https://www.iucngisd.org/gisd/). 
This database had easy-to-parse html source code that allowed me to use the 'rvest' package to 
locate and extract essential elements of invasive species results such as a summary of invasiveness,
the native range of the plant, and the alien range of the plant. 

Since I knew most plants would certainly not be invasive--and since I didn't want to spam requests
to the GISD website needlessly--I used API calls to the [Global Biodiversity Information Facility](https://www.gbif.org/), 
which houses a record of what plants are included in the GISD database and which allows for a higher rate of API requests.
This way, I could first check if the species actually existed in the database before performing webscraping on the GISD
website itself.

The output of the tool is a CSV with columns storing relevant information from the GISD wesbite. To test it
yourself, you can load your own CSV with a column called 'species', you can type in a comma-separated list of 
species, or you can simply run the demo which uses a preloaded species list. 



<style>
.responsive-iframe-container {
  position: relative;
  padding-bottom: 56.25%; /* 16:9 Aspect Ratio */
  padding-top: 25px;
  height: 0;
}
.responsive-iframe-container iframe {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
</style>

<div class="responsive-iframe-container">
  <iframe src="https://johannes-nelson.shinyapps.io/invasive_species_scanner/" frameborder="0"></iframe>
</div>

## Links
* [Invasive species scanner Shiny app](https://johannes-nelson.shinyapps.io/invasive_species_scanner/)
* [Source code for the app](https://github.com/johannesnelson/PPC_Data_Analysis_Pipeline/blob/main/Scripts/inv_app/app.R)
* [GitHub Repo for the Full Data Analysis Pipeline](https://github.com/johannesnelson/PPC_Data_Analysis_Pipeline/) (which I also 
talk about as a [separate project](placeholder/))

## Credit
As I was searching for ways to automate this scanning process, I came across an old R package
called 'originr' which sought to perform a similar function, I leaned heavily on the strategies
employed by the package authors and am grateful to have found their code!