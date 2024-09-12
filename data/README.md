# Overview
The raw data was collected from the test systems at Westermo Network Technologies AB. See the README.md in the top level directory for more information. The labelled data was created by Gustav Kånåhols as part of his bachelor thesis (Time Series Anomaly Detection for DevOps Test Systems, 2024) at Mälardalen University in collaboration with Westermo Network Technologies AB. 


```

└── data 			# Data directory
      ├── raw       # Raw data obtained from the test systems
      │   ├── system-1.csv
	  ...
      │   ├── system-19.csv
      ├── labelled 	# Labelled data
      |   | # Data with anomalies:
      │   ├── system-6_sys-thermal_anomalies_m-15m.csv      # A period of unusually high temperature fluctuations
      │   ├── system-14_cpu-user_anomalies.csv              # Several periods of CPU usage peaking at 100%
      │   ├── system-1_sys-mem-buffered_m-30m_anomalies.csv # The buffered memory suddenly drops
      |   |
      │   | # Data without the anomalies, other anomalies might be present but are not labelled,
      |   | # can be used to train semi-supervised models:
      │   ├── system-10_sys-thermal_normal_m-15m.csv      # Normal, system-10, sys-thermal
      │   ├── system-14_cpu-user_normal.csv               # Normal, system-14, cpu-user
      │   └── system-17_sys-mem-buffered_normal_m-30m.csv # Normal, system-17, sys-mem-buffered
```

# Data format
The data is stored in CSV files with the following columns: timestamp, value, is_anomaly. The timestamp is the number of seconds since first data was collected, value is the value of the metric at that time, and is_anomaly is a binary value indicating whether the data point is an anomaly or not.

Example:

| timestamp | value | is_anomaly |
|-----------|-------|------------|
| 0 | 0.1 | 0 |
| 30 | 200 | 1 |
| 60 | 0.1 | 0 |

Some data is downsampled to reduce processing time. The downsampled data is labelled with the suffix "_m-\<window\>m" where \<window\> is the window size in minutes. The data is downsampled by taking the mean of every \<window\> minute window.

