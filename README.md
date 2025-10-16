# Ride Sharing Analytics Using Spark Streaming and Spark SQL.
---
## **Prerequisites**
Before starting the assignment, ensure you have the following software installed and properly configured on your machine:
1. **Python 3.x**:
   - [Download and Install Python](https://www.python.org/downloads/)
   - Verify installation:
     ```bash
     python3 --version
     ```

2. **PySpark**:
   - Install using `pip`:
     ```bash
     pip install pyspark
     ```

3. **Faker**:
   - Install using `pip`:
     ```bash
     pip install faker
     ```

---

## **Setup Instructions**

### **1. Project Structure**

Ensure your project directory follows the structure below:

```
ride-sharing-analytics/
├── outputs/
│   ├── task_1
│   |    └── CSV files of task 1.
|   ├── task_2
│   |    └── CSV files of task 2.
|   └── task_3
│       └── CSV files of task 3.
├── task1.py
├── task2.py
├── task3.py
├── data_generator.py
└── README.md
```

- **data_generator.py/**: generates a constant stream of input data of the schema (trip_id, driver_id, distance_km, fare_amount, timestamp)  
- **outputs/**: CSV files of processed data of each task stored in respective folders.
- **README.md**: Assignment instructions and guidelines.
  
---

### **2. Running the Analysis Tasks**

You can run the analysis tasks either locally.

1. **Execute Each Task **: The data_generator.py should be continuosly running on a terminal. open a new terminal to execute each of the tasks.
   ```bash
     python data_generator.py
     python task1.py
     python task2.py
     python task3.py
   ```

2. **Verify the Outputs**:
   Check the `outputs/` directory for the resulting files:
   ```bash
   ls outputs/
   ```

---

## **Overview**

In this assignment, we will build a real-time analytics pipeline for a ride-sharing platform using Apache Spark Structured Streaming. we will process streaming data, perform real-time aggregations, and analyze trends over time.

## **Objectives**

By the end of this assignment, you should be able to:

1. Task 1: Ingest and parse real-time ride data.
2. Task 2: Perform real-time aggregations on driver earnings and trip distances.
3. Task 3: Analyze trends over time using a sliding time window.

---

## **Task 1: Basic Streaming Ingestion and Parsing**

1. Ingest streaming data from the provided socket (e.g., localhost:9999) using Spark Structured Streaming.
2. Parse the incoming JSON messages into a Spark DataFrame with proper columns (trip_id, driver_id, distance_km, fare_amount, timestamp).

## **Instructions:**
1. Create a Spark session.
2. Use spark.readStream.format("socket") to read from localhost:9999.
3. Parse the JSON payload into columns.
4. Print the parsed data to the console (using .writeStream.format("console")).

## **Output:**
```bash
078be2a9-58ce-48a0-9ef7-cd181b7f6260,26,21.02,102.38,2025-10-15 17:48:53

89b94137-1445-4c82-a34f-68a556f8961a,79,6.07,113.0,2025-10-15 17:48:48

933aba8d-8036-4b84-adca-c8b235e76663,48,44.32,76.27,2025-10-15 17:48:34

cd98ba47-2318-42de-8ea6-f0d21006f7e0,19,28.24,73.18,2025-10-15 17:48:45
```

---

## **Task 2: Real-Time Aggregations (Driver-Level)**

1. Aggregate the data in real time to answer the following questions:
  • Total fare amount grouped by driver_id.
  • Average distance (distance_km) grouped by driver_id.
2. Output these aggregations to the console in real time.

## **Instructions:**
1. Reuse the parsed DataFrame from Task 1.
2. Group by driver_id and compute:
3. SUM(fare_amount) as total_fare
4. AVG(distance_km) as avg_distance
5. Store the result in csv

## **Output:**
```bash
driver_id,total_fare,avg_distance
51,112.9,24.455
15,185.55,27.655
54,76.91,30.755000000000003
69,93.28,32.84
87,123.88,2.56
64,84.87,41.52
30,80.76,40.74
34,143.36,35.205
59,29.67,47.92
28,101.78,8.21
85,168.14,12.93
35,76.22,20.0
16,10.85,2.53
71,120.49,43.28
31,61.56,46.18
18,265.18,9.120000000000001
75,138.95,46.46
17,26.88,46.85
26,50.71,43.72
46,47.58,35.14
78,24.72,28.97
68,102.64,45.41
19,88.04,2.04
41,106.92,36.08
93,43.22,17.11
25,15.26,30.28
86,89.56,6.1
81,226.69,30.625
97,120.06,24.8
67,160.5,28.625
79,95.59,10.54
24,113.73,22.42
9,169.07,9.225000000000001
1,113.04,22.03
56,209.79000000000002,40.435
10,126.99,40.48
37,93.16,28.32
63,140.93,12.64
12,6.84,14.71
94,139.53,37.42
76,96.18,16.695
80,252.57999999999998,22.115000000000002
45,45.62,11.27
57,119.09,8.45

driver_id,total_fare,avg_distance
15,185.55,27.655
54,57.91,40.06
69,93.28,32.84
30,80.76,40.74
34,78.08,43.65
18,119.06,14.55
17,26.88,46.85
78,24.72,28.97
93,43.22,17.11
86,89.56,6.1
81,103.91,41.11
56,139.09,47.3
80,252.57999999999998,22.115000000000002
```
---

## **Task 3: Windowed Time-Based Analytics**

1. Convert the timestamp column to a proper TimestampType.
2. Perform a 5-minute windowed aggregation on fare_amount (sliding by 1 minute and watermarking by 1 minute).

## **Instructions:**

1. Convert the string-based timestamp column to a TimestampType column (e.g., event_time).
2. Use Spark’s window function to aggregate over a 5-minute window, sliding by 1 minute, for the sum of fare_amount.
3. Output the windowed results to csv.

## **Output:**
```bash
window_start,window_end,sum_fare
2025-10-15T17:38:00.000Z,2025-10-15T17:43:00.000Z,3235.67
---

---

## 📬 Submission Checklist

- [ ] Python scripts 
- [ ] Output files in the `outputs/` directory  
- [ ] Completed `README.md`  
- [ ] Commit everything to GitHub Classroom  
- [ ] Submit your GitHub repo link on canvas

---

