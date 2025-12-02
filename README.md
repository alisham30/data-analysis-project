file: https://github.com/alisham30/data-analysis-project/blob/main/musicanalysis%20project.pbix

✅ 📁 1. Project Overview

This project analyzes music streaming session data using a properly designed star schema consisting of:

FACT_LISTEN_EVENTS → Streaming events (song clicks/plays)

DIM_SONGS → Song metadata

DIM_USERS → Listener/user information

A complete Power BI dashboard was built to answer key business questions such as:

Who are the top artists?

Which songs are most played?

How many unique users are active?

What does the daily listening trend look like?

When do users listen the most (heatmap)?

Which albums get the highest share of streams?

🧊 2. Data Source — Snowflake

All datasets were loaded into Snowflake:

DIM_USERS

DIM_SONGS

FACT_LISTEN_EVENTS

Using Power BI’s Snowflake connector, the tables were imported into Power BI via:

Server: <your_snowflake_server>
Warehouse: COMPUTE_WH
Database: MUSIC_ANALYTICS
Schema: STREAMING


Power BI was connected in Import mode for better performance.

⭐ 3. Data Model (Star Schema)
Final Schema:
          DIM_USERS
              │
              │ 1 → *
              │
      FACT_LISTEN_EVENTS
              │
              │ * → 1
              │
          DIM_SONGS

Relationships:

FACT_LISTEN_EVENTS[USER_ID] → DIM_USERS[USER_ID]

FACT_LISTEN_EVENTS[SONG_ID] → DIM_SONGS[SONG_ID]

Cardinality:

Many-to-One (*:1) from FACT → DIM
Cross filter:

Single direction

This ensures correct aggregation for measures and visuals.

📈 4. Visuals Created in the Dashboard

You built six major visuals:

🔹 1. KPI Cards (Top Metrics)
a) Total Streams

Count of SONG_ID (from FACT_LISTEN_EVENTS)
Displayed as a big number card.

b) Total Unique Users

Using Distinct Count of USER_ID
Displayed as a second KPI card.

🔹 2. Top Artists by Total Streams (Bar Chart)

Visual: Clustered Bar Chart
Fields:

Axis → ARTIST

Values → Count of SONG_ID
Sorted by descending number of plays.

Shows which artists generate the most engagement.

🔹 3. Top 10 Most Played Songs (Bar Chart with Top N Filter)

Visual: Clustered Bar Chart
Fields:

Axis → TRACK_NAME

Values → Count of SONG_ID

Filters → Top N → 10 → by Count of SONG_ID

Displays the ten songs with the highest streaming count.

🔹 4. Daily Listening Trend (Line Chart)

Visual: Line Chart
Fields:

X-axis → TIMESTAMP → Day hierarchy

Y-axis → Count of SONG_ID

This visual reveals the activity pattern across the days of the month.

🔹 5. Listening Heatmap (Day vs Hour Matrix)

Visual: Matrix Table

Rows: Day of Week
Columns: Hour of Day
Values: Count of SONG_ID

A conditional formatting color scale was applied to turn the table into a heatmap.

Shows when users stream the most (peak hours & days).

🔹 6. Streams by Album (Donut Chart)

Visual: Donut Chart

Fields:

Legend → ALBUM

Values → Count of SONG_ID

Shows each album’s share of total streams.

Formatted with:

Inner radius

Data labels

Title: “Streams by Album”
