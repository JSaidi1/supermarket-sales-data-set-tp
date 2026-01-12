
### Kaggle Dataset

**Superstore Sales Dataset**
https://www.kaggle.com/datasets/vivek468/superstore-dataset-final

### Part 1: Loading and Exploration

1. Load the CSV into a DataFrame with the header option
2. Display the DataFrame schema
3. Display the first 20 rows
4. Count the total number of rows
5. Display the unique regions (column `Region`)

### Part 2: Simple Transformations

1. Create a column `Profit Margin` = `Profit` / `Sales`
2. Create a column `Year` by extracting the year from `Order Date`
3. Create a column `Total Value` = `Sales` - `Discount`
4. Display the first 10 rows with these new columns
5. **Cache this DataFrame** (you will reuse it several times)

### Part 3: UDF – Sales Categorization

1. Create a UDF `categorizeSale` that takes the `Sales` amount and returns:

   - "Small sale" if < $100
   - "Medium sale" if between $100 and $500
   - "Large sale" if > $500

2. Apply this UDF to create a column `Sale Category`
3. Display a few rows with this new column
4. Count the number of sales per category (Small/Medium/Large)

### Part 4: UDF – Discount Level

1. Create a UDF `discountLevel` that takes `Discount` and returns:

   - "No discount" if = 0
   - "Low discount" if between 0 and 0.2
   - "High discount" if > 0.2

2. Apply this UDF to create a column `Discount Level`
3. Calculate total revenue by discount level

### Part 5: Basic Aggregations

1. Calculate total revenue (`Sales`) by region
2. Calculate total profit by product category (`Category`)
3. Calculate the number of orders by customer segment (`Segment`)
4. Identify the top 10 products (`Product Name`) by quantity sold
5. Identify the top 5 states (`State`) with the highest revenue

### Part 6: Broadcast Variable – Region Codes

1. Create a Map that associates each region with a code:

```scala
val regionCodes = Map(
  "East" -> "EST",
  "West" -> "WST",
  "Central" -> "CTR",
  "South" -> "STH"
)
```

2. Broadcast this Map using `spark.sparkContext.broadcast()`

3. Create a UDF that uses this broadcast variable to create a `Region Code` column

4. Display a few rows with the region code

### Part 7: Broadcast Variable – Priority Coefficients

1. Create a Map of coefficients by category:

```scala
val categoryPriority = Map(
  "Technology" -> 1.5,
  "Furniture" -> 1.2,
  "Office Supplies" -> 1.0
)
```

2. Broadcast this Map

3. Create a UDF that multiplies `Profit` by the category coefficient to create a `Weighted Profit` column

4. Calculate total weighted profit by category
