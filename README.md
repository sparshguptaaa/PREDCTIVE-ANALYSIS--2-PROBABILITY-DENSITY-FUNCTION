# Probability Density Function Parameter Estimation

## Project Overview
This project focuses on performing a non-linear data transformation on the **India Air Quality Dataset** and learning the parameters of a specific Probability Density Function (PDF). The transformation and model are parameterized based on an individual's university roll number to ensure unique results.

## Dataset
The project utilizes the `no2` feature from the **India Air Quality Data** available on Kaggle.
* **Feature ($x$):** Nitrogen Dioxide ($NO_2$) levels.
* **Source:** [India Air Quality Data](https://www.kaggle.com/datasets/shrutibhargava94/india-air-quality-data)

## Methodology

### 1. Data Transformation
Each value of the feature $x$ is transformed into a new variable $z$ using a roll-number-parameterized function:
$$z = x + a_r \sin(b_r x)$$

**Constants Calculation:**
* $a_r = 0.05 \times (r \pmod 7)$
* $b_r = 0.3 \times ((r \pmod 5) + 1)$
*(where $r$ is your University Roll Number)*

### 2. Parameter Learning
The goal is to estimate the parameters $\lambda$, $\mu$, and $c$ for the following PDF:
$$\hat{p}(z) = c \cdot e^{-\lambda(z-\mu)^2}$$



This estimation is performed using the `scipy.optimize.curve_fit` library, which applies non-linear least squares to fit the model to a probability density histogram of the transformed data.

## Implementation Details
* **Data Cleaning:** Handled `UnicodeDecodeError` by using `ISO-8859-1` encoding and converted the `no2` column to numeric values while dropping `NaN` entries.
* **Optimization:** Used an initial guess based on the data's mean and maximum density to help the optimizer converge and avoid overflows.

## Requirements
* Python 3.12+
* Pandas
* NumPy
* SciPy

  ```mermaid
  flowchart TD
    A[Load Air Quality Dataset] --> B[Extract NO2 Feature]
    B --> C[Data Cleaning and Preprocessing]
    C --> D[Compute ar and br from Roll Number]
    D --> E[Apply Non-linear Transformation]
    E --> F[Construct Probability Density Histogram]
    F --> G[Define Gaussian-like PDF]
    G --> H[Estimate PDF Parameters]
  ```


## Results
The script outputs three primary parameters required for submission:
1. **$c$**: The normalization constant/peak height. = 0.030840
2. **$\lambda$**: The precision parameter. = 0.003145
3. **$\mu$**: The location parameter (mean of the transformed data). = 19.995340
4. alpha (ar): 0.3000
5. beta (br): 1.2000



## Academic Integrity
**Note:** This solution was developed following specific assignment constraints regarding non-linear modeling and statistical estimation techniques.
