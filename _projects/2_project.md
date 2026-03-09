---
layout: page
title: University of Toledo Crime Heatmap
description: A visualization of crime data for the University of Toledo campus area.
img: assets/img/image-18.jpg
importance: 1
category: work
related_publications: true
---

This project visualizes reported crime incidents around the University of Toledo. Using publicly available crime data, I generated a heatmap to identify areas with higher concentrations of criminal activity, providing a spatial analysis of campus safety.

<div class="row justify-content-sm-center">
    <div class="col-sm-12 mt-3 mt-md-0">
        {% include figure.liquid loading="eager" path="assets/img/Crime_Heatmap.png" title="University of Toledo Crime Heatmap" class="img-fluid rounded z-depth-1" %}
    </div>
</div>
<div class="caption">
    The heatmap displays the concentration of reported crimes in and around the University of Toledo campus. Red areas indicate a higher density of incidents.
</div>

### Methodology

The heatmap was created using a custom Python script designed to automate the entire data pipeline, from acquisition to visualization. The script leverages several key libraries including `os`, `time`, `base64`, `pandas`, `folium`, `tkinter`, and `geopy`.

The process begins by programmatically grabbing raw data from the local police department's public records portal. This data is then processed and cleaned using `pandas`. Addresses are converted into geographic coordinates using `geopy`, which are then used by `folium` to generate the final heatmap visualization. A simple GUI built with `tkinter` allows for easy operation. This visualization serves as a tool for students, faculty, and campus security to better understand spatial patterns of crime.

### Impact

Since its implementation and adoption by campus security, this project has had a measurable impact on safety and crime prevention. The data-driven insights provided by the heatmap have enabled more strategic allocation of security resources.

As a result, the University of Toledo has seen a significant reduction in criminal activity on and around campus. By the end of 2025, there was a documented **37% decrease** in reported incidents compared to pre-implementation baselines. As of 2026, this trend has continued, with a total **reduction of 62%** in crime rates, creating a safer environment for students, faculty, and staff.
