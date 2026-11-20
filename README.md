# Western Australia Road Crash & School Speed Zone Analysis

A Python data analysis project that matches 5 years of Western Australian road crash records to recorded school speed zone segments, then explores crash severity, timing, location and road user involvement.

Final project for Data Science & AI (Data Wrangling with Python), North Metropolitan TAFE.

## Research question

How can historical crash patterns and school speed zone data inform road safety investigations in Western Australia?

## Key findings

- **5,007 unique crashes** (3.77% of 132,862 records) were geographically matched to recorded school speed zone segments.
- Weekday crashes on matched segments peak sharply at **8 am and 3 pm**, in line with school drop-off and pick-up. Weekends show no such peaks.
- In approximate school travel windows there were **777 morning** and **907 afternoon** matched crashes.
- Matched segments have a higher share of **right-angle crashes (37.63% vs 23.91%)** and **pedestrian crashes (3.33% vs 1.11%)** than other roads.
- **Rear-end crashes make up 40.34%** of crashes in the afternoon school travel window.
- Crashes involving pedestrians or cyclists are more severe: **75.54%** of the pedestrian-dominated NMF pattern and **64.80%** of the bicycle-dominated pattern were Medical or Hospital, compared with **25.96%** for other vehicles.
- Read Street and Stirling Highway had the most matched crashes (94 each). A location check on Beechboro Road North found 60 crashes sharing one SLK position and one set of coordinates, which suggests a common road reference point, not a true hotspot.

## Data sources

Both datasets are published by **Main Roads Western Australia** on the WA Government Open Data Catalogue.

| Dataset | Records | Fields | Source |
| --- | --- | --- | --- |
| Crash Information (Last 5 Years), 2021–2025 | 132,862 | 25 | [data.wa.gov.au](https://catalogue.data.wa.gov.au/dataset/mrwa-crash-information-last-5-years-) |
| Legal Speed Zones (school zone segments) | 6,510 | 19 | [data.wa.gov.au](https://catalogue.data.wa.gov.au/dataset/mrwa-legal-speed-zones) |

Data was downloaded in October 2026. Copies of both files are in the [`datasets`](datasets) folder.

## Repository structure

```
├── datasets/
│   ├── Crash_Information.csv          # WA crash records, 2021–2025
│   └── Legal_Speed_Zones.csv          # School speed zone segments
├── WA_Road_Analysis.ipynb             # Python analysis notebook
├── WA Road Safety Report.pdf          # Written report
├── WA Road Safety Presentation.pdf    # Presentation slides
└── README.md
```

## Project files

- [Analysis notebook](WA_Road_Analysis.ipynb): all data cleaning, matching, analysis and charts.
- [Report](WA%20Road%20Safety%20Report.pdf): written summary of the findings, recommendations and limitations.
- [Presentation](WA%20Road%20Safety%20Presentation.pdf): slides from the final project presentation.

## How to run

The notebook was built in **Google Colab** with the data stored in Google Drive.

1. Download this repository (**Code → Download ZIP**) and unzip it.
2. Upload the `datasets` folder to Google Drive inside a folder called `WA_Road_Safety_Project`, so the files sit at `MyDrive/WA_Road_Safety_Project/datasets/`.
3. Open `WA_Road_Analysis.ipynb` in Google Colab.
4. Choose **Runtime → Run all** and allow access to Google Drive when asked.

To run it locally instead, remove the `drive.mount` cell and set `PROJECT_DIR` to the folder that holds the `datasets` folder.

### Requirements

- Python 3
- pandas
- numpy
- matplotlib
- seaborn
- scikit-learn

```
pip install pandas numpy matplotlib seaborn scikit-learn
```

## Methodology

1. **Data exploration and cleaning:** dataset shapes, column summaries, missing values (investigated by accident type, not dropped automatically) and duplicate checks.
2. **Segment validation:** road identifiers, carriageway codes, segment start and end positions, segment length outliers (IQR) and overlapping segments.
3. **Geographic matching:** carriageway codes standardised, crashes joined to speed zone segments by road and carriageway, then filtered to crashes whose SLK falls inside a segment. Each crash is counted once.
4. **Descriptive analysis:** severity, hour of day, weekday vs weekend, approximate school travel periods, month, roads and segments, and crash type compared with other roads.
5. **PCA and K-Means:** six road user involvement features standardised and reduced with PCA. The first two components explain 40.86% of variance and five components retain 90.86%. K-Means clustering on the components grouped crashes for severity comparison.
6. **NMF:** non-negative matrix factorisation on the same features found three road user patterns: other vehicles, pedestrians and bicycles.
7. **Location validation:** high-count segments checked for repeated SLK positions, coordinates and crash dates.

## Limitations

- A recorded school zone segment does not confirm that a school zone restriction was active when a crash happened.
- The speed zone data is a current snapshot. Historical speed zone changes, school calendars and holidays were not verified.
- Traffic volumes, actual speeds and pedestrian exposure were not available, so counts are not risk rates.
- Repeated SLK positions and coordinates can create apparent hotspots.

Findings point to priorities for further investigation. They do not establish crash causes or the effectiveness of school speed limits.
