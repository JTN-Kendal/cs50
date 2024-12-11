## ReadMe: AirWare - CS50 Final Project 
### By Nathan Wiles
###
#### Running the site / Setup
- Open app.py
- In terminal type: 'flask run' 
- Launch browser if needed
- Navigation / key features
  - Select a location to look at - choose Oxford
  - Use drop-downs on the left to filter the data - note change in table data
  - Choose to visualise the data pressing...

#### Project Structure
```
├── DECISIONS.md
├── DESIGN.md
├── LEARNING_OUTCOMES.md
├── NOTES.md
├── README.md
├── app.py
├── data
│   ├── air.db
│   ├── data_raw
│   │   ├── 2024-12-05-Data-Selector-Export-01.csv
│   │   ├── Oxford_air_cleaning.ipynb
│   │   ├── data_sample
│   │   └── data_sample.csv
│   ├── db_schema.sql
│   ├── db_setup.py
│   ├── dummy_data_generation.py
│   └── querey.sql
├── helpers.py
├── requirements.txt
├── static
│   ├── air-icon.png
│   ├── designs
│   │   └── webpage-wireframe.svg
│   └── styles.css
└── templates
    ├── explore_data.html
    └── layout.html
```
#### Features

#### Tech Stack
- Python / Flask (Backend)
- HTML / CSS / Bootstrap / JS (Frontend)
- SQLite3 (database)
- Python / Pandas (Data cleaning, reshaping, analysis)

#### Data Sources
- https://www.oxonair.uk (download of data)
- Dummy data based on the above data download - Generated by Claude (LLM)
- https://www.londonair.org.uk/Londonair/API/ (Planning to connect to API, not implemented)

#### Database Schema
```
CREATE TABLE locations (
    location_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL UNIQUE
);
CREATE TABLE sqlite_sequence(name,seq);
CREATE TABLE sub_locations (
    sub_location_id INTEGER PRIMARY KEY AUTOINCREMENT,
    location_id INTEGER NOT NULL,
    name TEXT NOT NULL,
    UNIQUE(location_id, name),
    FOREIGN KEY (location_id) REFERENCES locations(location_id)
);
CREATE TABLE pollutants (
    pollutant_id INTEGER PRIMARY KEY AUTOINCREMENT,
    name TEXT NOT NULL UNIQUE
);
CREATE TABLE measurements (
    measurement_id INTEGER PRIMARY KEY AUTOINCREMENT,
    sub_location_id INTEGER NOT NULL,
    pollutant_id INTEGER NOT NULL,
    value REAL NOT NULL,
    status TEXT NOT NULL,
    measured_at DATE NOT NULL,
    FOREIGN KEY (sub_location_id) REFERENCES sub_locations(sub_location_id),
    FOREIGN KEY (pollutant_id) REFERENCES pollutants(pollutant_id)
);
CREATE INDEX idx_measurements_date ON measurements(measured_at);
CREATE INDEX idx_measurements_location ON measurements(sub_location_id);
CREATE INDEX idx_measurements_pollutant ON measurements(pollutant_id);
```

#### Development Status

#### Future Development

####Primary Learning Outcomes / Observations  
- Everything takes longer than you think
- Setting up the database schema, and making sure it is correct is critical
- LLMs are an incredible learning tool and development partner - I used for debugging, explaining topics or code I didn't understand
- There are compromises from the very start - trade-offs on what is possible vs time available
- Using other peoples data isn't always easy - need to shape into usable format before importing into db or using
- Starting without a plan creates extra work
- There is so much to read when learning a new library

