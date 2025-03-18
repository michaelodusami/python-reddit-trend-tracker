## **🔥 Reddit Trend Tracker – ETL, Data Warehouse, & Sentiment Analysis**  
🚀 **Extract, Transform, and Load (ETL) real-time Reddit data, analyze sentiment, and store it in a star-schema data warehouse.**  

---
  
## 📌 **Project Overview**  
This project **extracts trending Reddit posts** from a subreddit, **performs sentiment analysis**, and **stores structured data** in a PostgreSQL data warehouse using a **star schema**.  

### **💡 Key Features**  
✅ **ETL Pipeline:** Extracts, cleans, and loads real-time Reddit data.  
✅ **Sentiment Analysis:** Uses AI (`TextBlob`) to categorize sentiment (Positive, Neutral, Negative).  
✅ **Data Warehouse:** Stores posts in **a structured star schema** for optimized querying.  
✅ **SQL Optimization:** Enables **fast queries** for insights into top trends and discussions.  

---

## 🏗 **Tech Stack**  
🔹 **Python** – For data extraction, transformation, and loading  
🔹 **Reddit API (`PRAW`)** – Fetches live Reddit data  
🔹 **PostgreSQL** – Stores structured data  
🔹 **SQLAlchemy** – Connects Python to PostgreSQL  
🔹 **TextBlob** – Performs sentiment analysis  
🔹 **Pandas** – Data transformation  
🔹 **Git** – Version control  

---

## 📂 **Project Architecture**  
```plaintext
┌──────────────────────────┐
│  Reddit API (PRAW)       │
└──────────┬──────────────┘
           ▼  
┌──────────────────────────┐
│  Python ETL Script       │
│  - Extract: Fetch posts  │
│  - Transform: Clean data │
│  - Sentiment Analysis    │
└──────────┬──────────────┘
           ▼  
┌──────────────────────────┐
│  PostgreSQL (Star Schema)│
│  - fact_posts           │
│  - dim_authors
│  - dim_subreddit        │
│  - dim_date             │
└──────────┬──────────────┘
           ▼  
┌──────────────────────────┐
│  SQL Queries & Insights  │
│  - Top trending posts    │
│  - Sentiment breakdown   │
│  - Most active users     │
└──────────────────────────┘
```

---

## ⚙ **Setup Instructions**  

### **🔹 1. Clone the Repository**  
```bash
git clone https://github.com/yourusername/reddit-trend-tracker.git
cd reddit-trend-tracker
```

### **🔹 2. Install Dependencies**  
Ensure you have **Python 3.8+** installed. Then, install the required libraries:  
```bash
pip install praw pandas textblob sqlalchemy psycopg2
```
Make sure to setup the praw configuration from praw's docs.

### **🔹 3. Set Up PostgreSQL Database**  
1. Open **PostgreSQL** and create a new database:  
```sql
CREATE DATABASE reddit_dw;
```
2. Run the SQL schema script to set up tables:  
```bash
psql -U your_user -d reddit_dw -f setup_schema.sql
```

---

## 🛠 **Star Schema Database Design**  
### **Fact Table (`fact_posts`)**  
| Column         | Type        | Description                        |
|---------------|------------|------------------------------------|
| post_id       | VARCHAR(20) | Reddit post ID                    |
| author_id     | INT         | Foreign key to `dim_authors`      |
| subreddit_id  | INT         | Foreign key to `dim_subreddit`    |
| score         | INT         | Upvotes for the post              |
| num_comments  | INT         | Number of comments on the post    |
| sentiment     | VARCHAR(20) | Positive, Negative, or Neutral    |
| date_id       | INT         | Foreign key to `dim_date`         |

### **Dimension Tables**  
#### **1. `dim_authors`** (Stores unique Reddit users)  
| Column      | Type         | Description          |
|------------|-------------|----------------------|
| id  | SERIAL (PK) | Unique author ID    |
| author_name     | VARCHAR(255) | Reddit username    |

#### **2. `dim_subreddit`** (Stores subreddit info)  
| Column        | Type        | Description          |
|--------------|------------|----------------------|
| id | SERIAL (PK) | Unique subreddit ID |
| subreddit_name    | VARCHAR(255) | Subreddit name     |

#### **3. `dim_date`** (Stores post dates)  
| Column       | Type         | Description          |
|-------------|-------------|----------------------|
| date_id     | SERIAL (PK) | Unique date ID      |
| date_value  | DATE        | Actual date        |
| year        | INT         | Year of post       |
| month       | INT         | Month of post      |
| day_of_week | INT         | Day of the week    |

---

## 🚀 **Running the ETL Pipeline**  
### **1️⃣ Extract & Transform Reddit Data**  
Run the Python script to **fetch and process Reddit posts**:  
```bash
python extract_transform.py
```

### **2️⃣ Load Data into PostgreSQL**  
After extracting data, load it into your database:  
```bash
python load_to_postgres.py
```

---

## 🔍 **SQL Query Examples (Insights & Analysis)**  

### **1️⃣ Top 5 Highest Scoring Posts**  
```sql
SELECT p.post_id, a.author_name, p.score
FROM fact_posts p
JOIN dim_authors a ON p.author_id = a.author_id
ORDER BY p.score DESC
LIMIT 5;
```

### **2️⃣ Sentiment Breakdown (Positive vs. Negative Posts)**  
```sql
SELECT sentiment, COUNT(*) as post_count
FROM fact_posts
GROUP BY sentiment
ORDER BY post_count DESC;
```

### **3️⃣ Most Active Users (Authors Posting the Most)**  
```sql
SELECT a.author_name, COUNT(*) as post_count
FROM fact_posts p
JOIN dim_authors a ON p.author_id = a.author_id
GROUP BY a.author_name
ORDER BY post_count DESC
LIMIT 10;
```

---



## 📝 **Later Improvements**  
- **Enhance Sentiment Analysis**: Use **NLTK** or a **machine learning model** instead of `TextBlob`.  
- **Streamline with Apache Airflow**: Automate ETL pipeline scheduling.  
- **Deploy on AWS**: Store processed data in **Amazon S3**, run queries using **AWS Athena**.  
- **Create a Web Dashboard**: Use **Tableau or Power BI** to visualize Reddit trends.  


**🌟 Ready to dive into the data? Clone, run, and explore the trends!**  

📌 **GitHub Repository**: [🔗 Link to Repo](https://github.com/michaelodusami/reddit-trend-tracker)  

