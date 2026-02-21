# MeiStat - Statistical Functions Library

A Python library for statistical analysis built on NumPy. Provides 31 statistical functions organized in intuitive modules.

## Installation

### Quick Start

1. Download the `meistat` folder
2. Place it in your project directory
3. Import and use:
```python
import numpy as np
import meistat as ms

data = np.array([1, 2, 3, 4, 5])
print(ms.stMean(data))  # 3.0
```

### Install as Package (Optional)
```bash
cd /path/to/meistat
pip install -e .
```

## Requirements

- Python >= 3.6
- NumPy >= 1.18.0

## Quick Examples
```python
import numpy as np
import meistat as ms

# Basic statistics
data = np.array([1, 2, 3, 4, 5])
print(ms.stMean(data))      # Mean: 3.0
print(ms.stMed(data))       # Median: 3
print(ms.stStd(data))       # Std dev: 1.41
print(ms.stRange(data))     # Range: 4

# Correlation
x = np.array([1, 2, 3, 4, 5])
y = np.array([2, 4, 6, 8, 10])
print(ms.stCovPirs(x, y))   # Pearson: 1.0

# Normalization
z = ms.stZScore(data)
print(z)                     # Z-scores
```

## Available Functions

### Core Module (4 functions)

Basic aggregation functions:

- `stMin(x, axis=None)` - Minimum value
- `stMax(x, axis=None)` - Maximum value
- `stSum(x, axis=None)` - Sum of elements
- `stMean(x, axis=None)` - Arithmetic mean

### Descriptive Module (15 functions)

Statistical measures of data:

- `stDisp(x, ddof=0, axis=None)` - Variance
- `stStd(x, ddof=0, axis=None)` - Standard deviation
- `stMed(x, axis=None)` - Median
- `stMode(x)` - Mode (most frequent value)
- `stQuantile(x, q)` - Quantile (0-1)
- `stPercentile(x, p, axis=None)` - Percentile (0-100)
- `stQuartiles(x, axis=None)` - Q1, Q2, Q3
- `stRange(x, axis=None)` - Range (max - min)
- `stIQR(x, axis=None)` - Interquartile range
- `stCV(x, axis=None)` - Coefficient of variation (%)
- `stSEM(x, ddof=0, axis=None)` - Standard error of mean
- `stMAD(x, axis=None)` - Median absolute deviation
- `stSkew(x, axis=None)` - Skewness (asymmetry)
- `stKurt(x, axis=None)` - Kurtosis (tailedness)

### Correlation Module (6 functions)

Relationship measures:

- `stCov(x, y, ddof=0)` - Covariance
- `stCovPirs(x, y)` - Pearson correlation
- `stCorMatr(x)` - Correlation matrix
- `stCovMatrix(x, ddof=0)` - Covariance matrix
- `stSpearman(x, y)` - Spearman rank correlation
- `stKendall(x, y)` - Kendall's tau

### Normalization Module (7 functions)

Data transformations:

- `stZScore(x, axis=None)` - Z-score standardization
- `stCumSum(x, axis=None)` - Cumulative sum
- `stCumProd(x, axis=None)` - Cumulative product
- `stProd(x, axis=None)` - Product of elements
- `stGeomMean(x, axis=None)` - Geometric mean
- `stHarmMean(x, axis=None)` - Harmonic mean
- `stTrimMean(x, proportiontocut, axis=None)` - Trimmed mean

## Common Use Cases

### Data Analysis
```python
import numpy as np
import meistat as ms

scores = np.array([85, 92, 78, 95, 88, 76, 91, 83, 89, 94])

print(f"Mean: {ms.stMean(scores):.1f}")
print(f"Median: {ms.stMed(scores):.1f}")
print(f"Std: {ms.stStd(scores, ddof=1):.2f}")
print(f"CV: {ms.stCV(scores):.1f}%")

q1, q2, q3 = ms.stQuartiles(scores)
print(f"Quartiles: {q1:.1f}, {q2:.1f}, {q3:.1f}")
```

### Outlier Detection
```python
import numpy as np
import meistat as ms

data = np.array([12, 14, 15, 13, 16, 14, 15, 50, 12, 15])

q1, q2, q3 = ms.stQuartiles(data)
iqr = ms.stIQR(data)

lower = q1 - 1.5 * iqr
upper = q3 + 1.5 * iqr

outliers = data[(data < lower) | (data > upper)]
print(f"Outliers: {outliers}")
```

### Correlation Analysis
```python
import numpy as np
import meistat as ms

height = np.array([170, 175, 180, 165, 172])
weight = np.array([65, 70, 75, 60, 68])

print(f"Pearson: {ms.stCovPirs(height, weight):.3f}")
print(f"Spearman: {ms.stSpearman(height, weight):.3f}")
```

### Working with Axes
```python
import numpy as np
import meistat as ms

# Matrix: 2 rows, 3 columns
data = np.array([[1, 2, 3],
                 [4, 5, 6]])

ms.stMean(data, axis=0)  # [2.5, 3.5, 4.5] - column means
ms.stMean(data, axis=1)  # [2.0, 5.0] - row means
ms.stMean(data)          # 3.5 - overall mean
```

## Key Features

- **Axis support**: All functions work with multidimensional arrays
- **ddof parameter**: Choose between population (ddof=0) and sample (ddof=1) statistics
- **Bug-free**: Fixed critical bugs in median and quantile calculations
- **Clean API**: Consistent naming (st prefix for all functions)

## Important Notes

### Population vs Sample Statistics
```python
data = np.array([1, 2, 3, 4, 5])

# Population variance (divide by n)
ms.stDisp(data, ddof=0)  # 2.0

# Sample variance (divide by n-1)
ms.stDisp(data, ddof=1)  # 2.5
```

### Correlation Interpretation

- **Pearson**: Linear relationship (-1 to 1)
- **Spearman**: Monotonic relationship (rank-based)
- **Kendall**: Concordance measure (ordinal data)

## Project Structure
```
meistat/
├── __init__.py          # Main imports
├── core.py              # Basic functions
├── descriptive.py       # Descriptive statistics
├── correlation.py       # Correlation measures
└── normalization.py     # Data transformations
```

## Testing
```python
import numpy as np
import meistat as ms

# Test basic functions
data = np.array([1, 2, 3, 4, 5])
assert ms.stMean(data) == 3.0
assert ms.stMed(data) == 3
assert ms.stDisp(data, ddof=1) == 2.5

# Test bug fixes
data_even = np.array([1, 2, 3, 4])
assert ms.stMed(data_even) == 2.5  # Median fix

## Author

Created as a learning project for NumPy and statistical computing.
