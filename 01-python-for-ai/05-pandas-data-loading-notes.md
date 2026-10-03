

---

# **Pandas for Efficient Data Loading & Processing**

This module focuses on efficiently loading large datasets from disk into RAM, especially suitable when dealing with CSV files. For optimal performance, we recommend using `pd.read_parquet()`, which is a highly efficient columnar format.

## **Key Techniques Covered**

### **Module 1: Efficient Data Loading**

- **Streaming Large CSV Files (`chunksize=N`)**:
  - When reading extremely large CSV files that won’t fit into memory all at once, you must process the file in "chunks."
  
    ```python
    for chunk in pd.read_csv('large_file.csv', chunksize=5000):
        # Process each chunk here (e.g., cleaning data)
    ```

- **Switching to Parquet for Faster Loading**:
  - [Parquet](https://parquet.apache.org/) is a columnar storage file format optimized for analytical queries and supports compression. Converting your CSV files to Parquet can significantly speed up loading times.
  
    ```python
    df = pd.read_parquet('data.parquet')
    ```

- **Reducing Memory Footprint**:
  - For categorical columns with repeating text, convert them into the `category` data type to save a lot of memory.
  
    ```python
    df['gender'] = df['gender'].astype('category')
    ```

---

## **Module 2: Data Inspection & Indexing**

Understanding your dataset before diving into cleaning is crucial. Here are the tools you need:

- **df.info()**:
  - Provides a summary of the DataFrame, including data types and how many non-null values are in each column.
  
- **df.describe()**:
  - Offers statistical summaries (mean, minimum, maximum) for numerical columns.

- **df.value_counts()**:
  - Shows you the frequency distribution of distinct values.

### **Selection Tools**

- **`df.loc[]`: Selection by Label**
  - Use this to select data based on index labels or conditions.
  
    ```python
    filtered_df = df.loc[df['age'] > 30]
    ```

- **`df.iloc[]`: Selection by Position**
  - `iloc` allows you to retrieve rows and columns using integer positions, regardless of their labels.
  
    ```python
    first_five_rows = df.iloc[0:5]
    ```

---

## **Module 3: Data Cleaning**

Real-world data is often messy, which can disrupt machine learning pipelines. Here’s how to handle common issues:

### **Handling Missing Values**

- **dropping rows with missing values**:
  - This method removes any row where a specified column contains NaN (missing) values.
  
    ```python
    df_cleaned = df.dropna(subset=['target_column'])
    ```

- **forward-filling NaN values**:
  - `ffill` is particularly useful in time-series data, replacing missing entries with the last observed value.

    ```python
    df_filled = df.fillna(method='ffill')
    ```

### **Cleaning Text Data**

- **String Methods in Pandas**:
  
    ```python
    df['cleaned_text'] = df['text_col'].str.lower().str.strip()
    ```

---

## **Module 4: Feature Engineering for AI**

Machine learning models understand only numerical inputs. Hence, converting categorical data to numerical values is essential.

### **Handling Dates & Times**

- **Convert String Dates to `datetime` Objects**:
  
    ```python
    df['date'] = pd.to_datetime(df['date_col'])
    ```

  - Once converted, you can derive insights like the month or day of the week.
  
    ```python
    df['month'] = df['date'].dt.month
    ```

### **One-Hot Encoding Categorical Features**

- **Convert Categories to Binary Columns**:
  - This method converts each category into a separate binary column.

    ```python
    encoded_df = pd.get_dummies(df['category'])
    ```

---

## **Module 5: Aggregation & Grouping**

After cleaning the data, understanding patterns through groupings can give deeper insights:

### **Group by One or More Columns and Aggregate Data**

- **Simple Aggregations**:
  
    ```python
    average_sales = df.groupby('category_col')['numeric_col'].mean()
    ```

- **Simultaneous Multiple Aggregations**:
  
    ```python
    aggregated_data = df.groupby('user_id').agg({'purchase': 'sum', 'login': 'count'})
    ```

---

## **Module 6: Merging & Joining Related Data**

Real-life scenarios frequently require combining data from multiple sources. Pandas provides the tools for this effortlessly.

### **Merging & Joining Techniques**

- **`pd.merge()`**: Similar to SQL JOINs, it links two or more DataFrames based on a common key.
  
    ```python
    merged_df = pd.merge(df1, df2, on='id', how='left')
    ```

- **`pd.concat()`**: Stacks multiple Datasets vertically, ideal for combining chunks into one frame.

    ```python
    combined_df = pd.concat([df1, df2], axis=0)
    ```

## **Downloadable Kaggle Dataset for Practical Hands-On**

To maximize the learning experience from this module, here are a few datasets you should download and include in your `'data/'` directory:

### Data Cleaning &amp; String Manipulation (Modules 3 &amp; 4)

- **Zomato Bangalore Restaurants Dataset** - Perfect for handling messy string data, missing values, and categorical text.
  
  *Download it from Kaggle* [here](https://www.kaggle.com/datasets/yogendra pratap singh/zomato-bangalore-restaurants-data).

### Relational Merging (Module 6)

- **Olist Brazilian E-Commerce Dataset** - Composed of several CSV files, perfect for