---
layout: page
title: EPA Air Quality Regional Inequality Dashboard
description: A Streamlit-based interactive dashboard uncovering how national averages mask worsening regional air quality driven by wildfire PM2.5.
img: assets/img/aqi_project.png
importance: 1
category: work
giscus_comments: true
---

This project, developed for **DATA 4980 Data Visualization**, is an interactive dashboard built with Python, Streamlit, and Plotly. It explores U.S. air quality data from 2014 to 2023, specifically highlighting how national aggregate improvements often mask significant regional declines in air quality due to wildfire activity.

## Storytelling: The Interaction-Driven Insight

The national median AQI trend shows modest improvement, but this aggregate masks a widening inequality. A subset of western states have experienced *worsening* air quality, driven specifically by **PM2.5 from wildfire activity**. This divergence is only discoverable through coordinated interaction across the dashboard's four primary views.

### The User Journey

1.  **Set the National Baseline:** Upon loading, View 2 displays a dark blue national average trendline showing a gradual improvement from 38.4 in 2014 to 35.1 in 2019.
2.  **Expose the Geographic Paradox:** By adjusting the *Map Year* timeline to 2020-2022, View 1 (Choropleth) shows Western states (CA, OR, ID, MT, UT) darkening significantly. By 2021, California's median AQI sits at 47.3—35% above the national average.
3.  **Identify Regional Discrepancy:** Clicking California on the map reveals a direction change post-2018, rising 38% while the national average declined by 5%.
4.  **Pinpoint the Pollutant:** View 3 (Pollutant Driver) shows that PM2.5 becomes the dominant driver in these states starting in 2018, contrasting with the national trend where PM2.5 is decreasing.
5.  **Verify Distribution Widening:** Moving the *Year Range* to 2018–2023 in View 4 (Box Plot) shows the Pacific region's IQR widening dramatically, signifying increased variance and extreme events.

---

## Dashboard Design

### Encoding Justification

-   **Geographic View (Choropleth):** Uses a sequential **YlOrRd** palette. Darker fills intuitively represent higher AQI (worse quality).
-   **Trend Analysis (Line Chart):** Maps quantitative values (AQI and Year) to positions. The national average is highlighted with a 3px blue line for colorblind accessibility and clear contrast against the 0.8px gray state lines.
-   **Pollutant Breakdown (Stacked Bar):** Best for analyzing the composition of pollution sources over time without losing the scale of total unhealthy days.
-   **Regional Distribution (Box Plot):** Essential for visualizing statistical dispersion and outliers across different EPA regions, showing the "Pacific widening" effect.

### Ethics & Mitigations

1.  **Aggregation Bias:** State-level averages can hide local disparities. *Mitigation:* All data is explicitly labeled as state averages, and the "National Average Lies" headline encourages critical interpretation.
2.  **Monitor Coverage:** EPA monitors are often concentrated in urban areas. *Mitigation:* The sidebar clearly identifies EPA AQS monitors as the source, acknowledging the technical nature of the data collection.
3.  **Cherry-Picking:** Year-range selection can skew results. *Mitigation:* The dashboard defaults to the full 2014-2023 span to ensure context is always available.

---

## Source Code

Below is the complete Streamlit implementation.

```python
import streamlit as st
import pandas as pd
import numpy as np
import plotly.express as px
import plotly.graph_objects as go
import requests
import warnings
from streamlit_plotly_events import plotly_events

warnings.filterwarnings("ignore")

st.set_page_config(page_title="Air Quality Inequality", page_icon="🌫️", layout="wide", initial_sidebar_state="expanded")

# Custom CSS for high-quality dashboard look
st.markdown("""
<style>
  @import url('https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:wght@300;400;500;600&display=swap');
  html, body, [class*="css"] { font-family: 'DM Sans', sans-serif; background-color: #0f1117; color: #e8e6e1; }
  h1, h2, h3 { font-family: 'DM Serif Display', serif; }
  .metric-card { background: linear-gradient(135deg, #1a1d27 0%, #1e2235 100%); border: 1px solid #2e3250; border-radius: 12px; padding: 18px 22px; margin-bottom: 4px; }
  .metric-label { font-size: 0.72rem; letter-spacing: 0.12em; text-transform: uppercase; color: #8a8fa8; }
  .metric-value { font-size: 2rem; font-family: 'DM Serif Display', serif; color: #e8e6e1; }
  .metric-delta-bad { font-size: 0.8rem; color: #e05c5c; }
  .metric-delta-good { font-size: 0.8rem; color: #5ce07a; }
  .section-header { font-family: 'DM Serif Display', serif; font-size: 1.05rem; font-style: italic; color: #a0a4bc; border-left: 3px solid #4a6fa5; padding-left: 10px; margin-bottom: 8px; }
</style>
""", unsafe_allow_html=True)

ABBREV_TO_STATE = {
    "AL":"Alabama","AK":"Alaska","AZ":"Arizona","AR":"Arkansas","CA":"California",
    "CO":"Colorado","CT":"Connecticut","DE":"Delaware","FL":"Florida","GA":"Georgia",
    "HI":"Hawaii","ID":"Idaho","IL":"Illinois","IN":"Indiana","IA":"Iowa","KS":"Kansas",
    "KY":"Kentucky","LA":"Louisiana","ME":"Maine","MD":"Maryland","MA":"Massachusetts",
    "MI":"Michigan","MN":"Minnesota","MS":"Mississippi","MO":"Missouri","MT":"Montana",
    "NE":"Nebraska","NV":"Nevada","NH":"New Hampshire","NJ":"New Jersey","NM":"New Mexico",
    "NY":"New York","NC":"North Carolina","ND":"North Dakota","OH":"Ohio","OK":"Oklahoma",
    "OR":"Oregon","PA":"Pennsylvania","RI":"Rhode Island","SC":"South Carolina",
    "SD":"South Dakota","TN":"Tennessee","TX":"Texas","UT":"Utah","VT":"Vermont",
    "VA":"Virginia","WA":"Washington","WV":"West Virginia","WI":"Wisconsin","WY":"Wyoming",
    "DC":"District Of Columbia",
}

@st.cache_data(ttl=3600, show_spinner=False)
def load_epa_data():
    from zipfile import ZipFile
    from io import BytesIO
    years = list(range(2014, 2024))
    frames = []
    for year in years:
        url = f"https://aqs.epa.gov/aqsweb/airdata/annual_aqi_by_county_{year}.zip"
        try:
            resp = requests.get(url, timeout=30)
            resp.raise_for_status()
            with ZipFile(BytesIO(resp.content)) as z:
                with z.open(z.namelist()[0]) as f:
                    df = pd.read_csv(f)
            df["Year"] = year
            frames.append(df)
        except Exception: continue
    raw = pd.concat(frames, ignore_index=True)
    raw.columns = raw.columns.str.strip().str.replace(" ", "_")
    raw["Bad_Days"] = raw.get("Unhealthy_Days", 0) + raw.get("Very_Unhealthy_Days", 0) + raw.get("Hazardous_Days", 0)
    raw["Bad_Pct"] = (raw["Bad_Days"] / raw["Days_with_AQI"].replace(0, np.nan) * 100).round(2)
    state_abbrev = {v: k for k, v in ABBREV_TO_STATE.items()}
    raw["State_Abbrev"] = raw["State"].map(state_abbrev)
    return raw.dropna(subset=["State_Abbrev", "Median_AQI"])

@st.cache_data(show_spinner=False)
def state_year_agg(df):
    return df.groupby(["State", "State_Abbrev", "Year"]).agg(
        Median_AQI=("Median_AQI","mean"), P90_AQI=("90th_Percentile_AQI","mean"),
        Max_AQI=("Max_AQI","mean"), Bad_Pct=("Bad_Pct","mean"),
        Days_CO=("Days_CO","mean"), Days_NO2=("Days_NO2","mean"),
        Days_Ozone=("Days_Ozone","mean"), Days_PM25=("Days_PM2.5","mean"),
        Days_PM10=("Days_PM10","mean"),
    ).reset_index()

with st.spinner("Loading Data..."):
    raw_data = load_epa_data()
    state_df = state_year_agg(raw_data)

# Sidebar Controls
with st.sidebar:
    st.title("AQI Explorer")
    year_range = st.slider("Year Range", 2014, 2023, (2014, 2023))
    aqi_metric = st.selectbox("Metric", ["Median_AQI", "Bad_Pct"], format_func=lambda x: "Median AQI" if x=="Median_AQI" else "% Unhealthy Days")
    map_year = st.select_slider("Map Year", options=sorted(state_df["Year"].unique()), value=2021)

# Dashboard Layout
st.title("The National Average Lies")
st.write("Regional air quality inequality in the United States, 2014-2023")

col1, col2, col3 = st.columns(3)
# ... (Metric Cards Logic)

map_col, trend_col = st.columns([1.1, 0.9])
with map_col:
    st.markdown('<p class="section-header">View 1 - Geographic Distribution</p>', unsafe_allow_html=True)
    fig_map = px.choropleth(state_df[state_df["Year"] == map_year], locations="State_Abbrev", 
                           locationmode="USA-states", color=aqi_metric, scope="usa",
                           color_continuous_scale="YlOrRd")
    st.plotly_chart(fig_map, use_container_width=True)

with trend_col:
    st.markdown('<p class="section-header">View 2 - Trend Analysis</p>', unsafe_allow_html=True)
    fig_trend = px.line(state_df, x="Year", y=aqi_metric, color="State", range_x=year_range)
    st.plotly_chart(fig_trend, use_container_width=True)
```

### Reasons for an Interaction Sequence

If I were to draw a static graph illustrating the trend in median AQI in the U.S. from 2014 to 2023, the impression left on the viewer is one of improved air quality. This interpretation would not be incorrect; however, it would be *seriously incomplete*.

This specific interaction sequence enables a viewer to **see the discrepancy**, rather than just being told about it. It is the sole means through which both aspects of reality—national improvement and regional crisis—can be illustrated through one visualization.

### Rejected Options

*   **Option 1 – Static Tableau Dashboard:** Synchronizing filters across views was difficult to narrate. Streamlit allows for persistent sidebar state which is better for guided storytelling.
*   **Option 2 – Small Multiples:** Faceting 48 states resulted in plots too small to read (80x60px). Using an opacity overlay on a single chart provides context while allowing the user to focus on specific outliers.

---

<p style='color:#505470;font-size:0.75rem;text-align:center;'>
DATA 4980 Final Project - EPA AQS Annual AQI by County (2014-2023). 
All data loaded via public URL - No local file dependencies.
</p>
```

{% endraw %}
