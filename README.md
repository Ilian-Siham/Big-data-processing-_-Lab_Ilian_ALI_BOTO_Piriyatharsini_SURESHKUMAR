# Big-data-processing-_-Laboratory
## authors : 
 - Ilian ALI BOTO
 - Piriyatharsini SURESHKUMAR

## Laboratory 5 ##
We tried to do the Lab 5 but do to some technical problem that we tried to solve in class and even after the dedicated hours of lecture, we weren't able to do the lab 5.

## Project Part II: Streaming Processing ##

1. Data Ingestion (Prerequisite)

Before running this analysis, you must execute the separate ingestion notebook: wikimedia_get_raw_stream_data.

**Purpose**: This notebook establishes a connection to the Wikimedia EventStreams API.

**Function**: It captures live JSON events for all English Wikipedia edits and persists them into a Unity Catalog Volume as raw files.

**Action**: Ensure that the ingestion notebook has been running for at least 10–15 minutes to provide a sufficient data sample for the filters.

2. Stream Processing & Filtering

Once the raw data is available, this notebook performs the following processing steps:

**Schema Definition**: We apply a strict StructType schema to the raw JSON to ensure data integrity during the readStream process.

**Entity Selection**: We define five specific entities chosen randomly (e.g., Drama, Star Wars, Johnny Depp, Game of Thrones, and Thriller) and some entities extracted from the IMDb dataset (e.g., Comedy movie, Drama tv series title, actor and actress names) to track within the global edit stream.

**Filtering Logic**: We use Regex (rlike) and namespace filtering to isolate edits belonging to our entities while excluding "noise" (such as internal Wikipedia talk pages or category maintenance).

3. Metrics and Alerting

The structured stream is split into two distinct outputs (Sinks):

**Simple Metrics**: A windowed aggregation that counts the number of edits per entity  over a 10-minute period, stored in a Delta Table.

**Alerting System**: A secondary stream that filters for specific event types (e.g., automated Bot edits). These "alerts" are routed to a separate destination to mimic a real-world notification or auditing system.
