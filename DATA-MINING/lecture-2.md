# Data Basics and Similarity Measures

## What is Data?
Data is a collection of **objects** (also called records, points, cases) and **attributes** (features or variables).  
**Example:** A table of customers where each row is a customer (object) and columns are attributes like age, name, or income.

## Objects and Attributes
- **Objects:** Entities to be described.  
  *Example:* A student, a transaction.
- **Attributes:** Properties of objects.  
  *Example:* Height, name, price.

---

## Discrete and Continuous Attributes
- **Discrete:** Finite or countable values.  
  *Example:* Number of children.
- **Continuous:** Infinite or real-number values.  
  *Example:* Temperature, height.

## Nominal, Ordinal, Interval, and Ratio Attributes
- **Nominal:** Categories without order.  
  *Example:* Gender, color.
- **Ordinal:** Categories with a meaningful order.  
  *Example:* Rank, education level.
- **Interval:** Ordered, with meaningful differences but no true zero.  
  *Example:* Temperature in Celsius.
- **Ratio:** Ordered, with true zero.  
  *Example:* Weight, age, income.

## Binary Attribute
Only two values: 0 or 1, True or False.  
**Example:** Is student (Yes/No)

### Symmetric and Asymmetric Binary Attributes
- **Symmetric:** Both outcomes are equally important.  
  *Example:* Gender (Male/Female)
- **Asymmetric:** One outcome is more important.  
  *Example:* Disease present (Yes) vs (No)

## Numeric Attribute
Quantitative, measurable values.  
**Example:** Salary, age.

---

## Types of Data Sets
- **Record Data Set:** Structured as rows and columns.  
  *Example:* CSV file.
- **Graph Data Set:** Data with nodes and edges.  
  *Example:* Social network.
- **Ordered Data Set:** Sequence matters.  
  *Example:* Time series, text.

---

## General Characteristics of Datasets
- **Dimensionality:** Number of attributes.  
  *Example:* 100 features → high dimensional.
- **Sparsity:** Many values are zero or missing.  
  *Example:* Text vector representation.
- **Resolution:** Level of detail in data.  
  *Example:* Daily vs hourly temperature.

---

## Transaction / Market Basket Data
Data where each record is a set of items purchased.  
**Example:**  
`T1: {Bread, Milk}`,  
`T2: {Bread, Diaper, Beer}`

---

## Data Similarity and Dissimilarity
- **Similarity:** Measures how alike two objects are.
- **Dissimilarity:** Measures how different two objects are.

---

# Proximity Measures

## For Nominal Attributes
- **Similarity (Simple Matching Coefficient):**  
  `S = (Number of matches) / (Total attributes)`
- **Dissimilarity:**  
  `D = 1 - S`

## For Ordinal Attributes
1. Assign rank to categories.  
2. Normalize to [0,1].  
3. Use distance metrics like Euclidean or Manhattan.

## For Binary Attributes

### Symmetric Binary
- **D = (f01 + f10) / (f00 + f01 + f10 + f11)**  
- **S = (f11 + f00) / (Total)**

### Asymmetric Binary
- **Jaccard Coefficient:**  
  `S = f11 / (f01 + f10 + f11)`  
  `D = 1 - S`

> *f11 = both 1, f10 = first 1 second 0, etc.*

## For Numerical Attributes

- **Euclidean Distance:**  
  `D(i, j) = sqrt(Σ(xi - xj)²)`
- **Manhattan Distance:**  
  `D(i, j) = Σ|xi - xj|`
- **Minkowski Distance (general form):**  
  `D(i, j) = (Σ|xi - xj|^p)^(1/p)` (p ≥ 1)
- **Supremum (L∞ norm):**  
  `D(i, j) = max|xi - xj|`
