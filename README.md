# Data Modeling with Postgres & ETL Pipeline Automation (Work in Progress)

## **Overview**

In this project, we apply **Data Modeling with Postgres** and build an **ETL pipeline using Python**. The goal is to process and store music streaming data collected in JSON format, allowing the **analytics team** to query and analyze user activity and song preferences.

### **Current Progress:**

✅ **Built and tested the ETL pipeline manually** using Python scripts.  
✅ **Created the necessary tables** in PostgreSQL to store processed data.  
✅ **Verified data consistency** after executing the ETL pipeline.  
✅ **Attempted to automate the ETL process using Apache Airflow**.  
⚠ **Faced issues with Airflow DAG visibility and provider dependencies**.  
🔜 **Plan to learn Apache Airflow in-depth before resuming automation**.

---

## **Datasets Used**

### **Song Dataset**

- A subset of the **Million Song Dataset**.
- Contains metadata about songs and artists.

**Sample Record:**

```json
{
  "num_songs": 1,
  "artist_id": "ARJIE2Y1187B994AB7",
  "artist_latitude": null,
  "artist_longitude": null,
  "artist_location": "",
  "artist_name": "Line Renaud",
  "song_id": "SOUPIRU12A6D4FA1E1",
  "title": "Der Kleine Dompfaff",
  "duration": 152.92036,
  "year": 0
}
```

### **Log Dataset**

- Generated using an **Event Simulator**.
- Captures user interactions with the music streaming app.

**Sample Record:**

```json
{
  "artist": null,
  "auth": "Logged In",
  "firstName": "Walter",
  "gender": "M",
  "itemInSession": 0,
  "lastName": "Frye",
  "length": null,
  "level": "free",
  "location": "San Francisco-Oakland-Hayward, CA",
  "method": "GET",
  "page": "Home",
  "registration": 1540919166796.0,
  "sessionId": 38,
  "song": null,
  "status": 200,
  "ts": 1541105830796,
  "userAgent": "Mozilla/5.0 (Macintosh; Intel Mac OS X 10_9_4)...",
  "userId": "39"
}
```

---

## **Database Schema**

The database follows a **star schema**, with **one fact table** and **four dimension tables**.

### **Fact Table**

✅ **songplays** - records log data associated with song plays.

| Column      | Type               | Description                           |
| ----------- | ------------------ | ------------------------------------- |
| songplay_id | SERIAL PRIMARY KEY | Unique identifier for each song play. |
| start_time  | TIMESTAMP NOT NULL | Timestamp of song play.               |
| user_id     | INT NOT NULL       | ID of the user.                       |
| level       | VARCHAR            | User level (free/paid).               |
| song_id     | VARCHAR            | ID of the played song.                |
| artist_id   | VARCHAR            | ID of the artist.                     |
| session_id  | INT                | ID of the user session.               |
| location    | VARCHAR            | User's location.                      |
| user_agent  | VARCHAR            | Browser used.                         |

### **Dimension Tables**

✅ **users** - Users in the app  
✅ **songs** - Songs in the database  
✅ **artists** - Artist information  
✅ **time** - Timestamps broken down into specific units

---

## **Project Files & Description**

| **File**           | **Description**                                                      |
| ------------------ | -------------------------------------------------------------------- |
| `sql_queries.py`   | SQL queries for table creation, insertion, and dropping.             |
| `create_tables.py` | Creates the `sparkifydb` database and tables.                        |
| `etl.ipynb`        | Jupyter notebook for analyzing the dataset before loading.           |
| `etl.py`           | Python script to process `song_data` and `log_data` into PostgreSQL. |
| `test.ipynb`       | Notebook to validate data in PostgreSQL.                             |
| `sparkify_dag.py`  | Airflow DAG (Work in Progress) for ETL automation.                   |
| `sparkify_etl.py`  | Airflow ETL script (Pending fixes).                                  |

---

## **How to Run the ETL Process Manually**

Since **Apache Airflow automation is not fully implemented**, the ETL process can be run manually using the following steps:

### **1. Set Up PostgreSQL**

Ensure that PostgreSQL is running and accessible.

### **2. Create Tables**

Run the following command to create the required tables:

```bash
python create_tables.py
```

### **3. Execute the ETL Script**

To extract and load data from JSON files into the database, run:

```bash
python etl.py
```

### **4. Validate Data in PostgreSQL**

After running the ETL script, verify data using SQL queries:

```sql
SELECT * FROM songplays LIMIT 10;
```

---

## **Future Plan: Automating with Apache Airflow**

Once Airflow is fully configured, the ETL pipeline will be automated as follows:

1. **Schedule the DAG** to run the ETL at regular intervals.
2. **Task dependencies** will ensure data integrity.
3. **Monitor execution** via the Airflow UI.
4. **Enable error handling** and retry mechanisms.

### **Current Issues:**

- DAG visibility issues in Airflow.
- `airflow.providers.postgres` module error.
- Airflow scheduler setup needs debugging.

---

## **Environment & Dependencies**

- **Python** (3.9+)
- **PostgreSQL** (14+)
- **Psycopg2** (PostgreSQL adapter for Python)
- **Pandas** (Data processing)
- **Apache Airflow** (Pending full setup)

### **How to Install Dependencies**

Run the following command inside the virtual environment:

```bash
pip install -r requirements.txt
```

---

## **Resources & References**

- [PostgreSQL Documentation](https://www.postgresql.org/docs/)
- [Pandas Documentation](https://pandas.pydata.org/pandas-docs/stable/)
- [Airflow Documentation](https://airflow.apache.org/docs/apache-airflow/stable/index.html)
- [Psycopg2 Docs](http://initd.org/psycopg/docs/)

---

## **Summary**

- ✅ **ETL manually implemented and verified** in PostgreSQL.
- ✅ **Database schema successfully created**.
- ✅ **Airflow partially configured** but not fully functional.
- 🔜 **Plan to learn Airflow deeply before re-attempting automation**.

🚀 **Next Steps:**

- Debug Airflow DAG execution issues.
- Complete the automation workflow.
- Deploy and test the pipeline end-to-end.
