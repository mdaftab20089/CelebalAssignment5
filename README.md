# CelebalAssignment5

# 🏠 Ames Housing Price Prediction Project

This project aims to **predict home sale prices** using the [Ames Housing dataset](http://jse.amstat.org/v19n3/decock.pdf), which provides comprehensive data describing the sale of individual residential properties in Ames, Iowa.

---

## 📁 Project Overview

The project covers the complete machine learning pipeline:

✅ Data Preprocessing  
✅ Missing Value Imputation  
✅ Feature Engineering  
✅ Categorical Encoding  
✅ Feature Scaling  
✅ Data Alignment between Training and Test Sets  

---

## 📊 Exploratory Data Analysis (EDA)

During EDA, we:

- Inspected all **81 variables** in the dataset.
- Identified columns with **significant missing values**, such as:
  - `PoolQC`, `MiscFeature`, `Alley`, `Fence`, `FireplaceQu`
- Reviewed **distributions of numeric features** (e.g., `LotArea`, `GrLivArea`) and detected skewness.
- Examined **categorical features** and their frequency distributions (e.g., `Neighborhood`, `MSZoning`).
- Verified **relationships with SalePrice**, noting especially:
  - `OverallQual` and `GrLivArea` are strong predictors.

---

## 🛠️ Data Preprocessing

### 1️⃣ Handling Missing Values

**Categorical features with many missing values:**
- Filled with `'None'`:
  - `PoolQC`, `MiscFeature`, `Alley`, `Fence`, `FireplaceQu`

**Numerical features:**
- `LotFrontage`: Filled with median.
- `MasVnrArea`: Filled with `0`.
- `GarageYrBlt`: Filled with `YearBuilt`.

**Basement & Garage categorical variables:**
- Filled with `'None'`.

**Other categorical features:**
- Filled with the **mode**.

**Additional missing values in test data:**
- `MSZoning`, `Utilities`, `Exterior1st`, `Exterior2nd`, `KitchenQual`, `Functional`, `SaleType`: Filled with mode.
- `Bsmt*` and `Garage*` numeric fields: Filled with `0`.

---

### 2️⃣ Feature Engineering

We created **new derived features** to capture more predictive signals:

| New Feature         | Description |
|---------------------|-------------|
| `HouseAge`          | Year sold minus year built |
| `GarageAge`         | Year sold minus garage year built |
| `Remodeled`         | Binary flag if remodeled |
| `TotalBath`         | Total number of bathrooms (including basement) |
| `TotalPorchSF`      | Sum of all porch areas |
| `HasPool`           | Binary flag for presence of a pool |
| `HasFireplace`      | Binary flag for fireplaces |
| `HasGarage`         | Binary flag for garage presence |

---

### 3️⃣ Encoding Categorical Variables

**Ordinal Encoding:**
- Mapped quality ratings (`ExterQual`, `KitchenQual`, `HeatingQC`, etc.) to numeric scale (0-5).

**One-Hot Encoding:**
- Applied to nominal categorical columns such as:
  - `MSZoning`, `Neighborhood`, `BldgType`, `HouseStyle`, `SaleCondition`
- Used `pd.get_dummies()` with `drop_first=True`.

---

### 4️⃣ Feature Scaling

**Standardization:**
- Numeric features were standardized using `StandardScaler` (mean = 0, std = 1).
- Applied **the same scaler trained on the training data** to transform the test set.

---

### 5️⃣ Dataset Alignment

- After encoding, we aligned test data columns to match training data:
  - Added missing columns with zeros.
  - Ensured all features had identical structure.
- Final Shapes:
  - **Train:** 1460 rows × 209 columns (includes `SalePrice`)
  - **Test:** 1459 rows × 208 columns

---

## 🗂️ Dataset Feature Reference

Below is a **summary of important variables**:

### 🏘️ Property and Dwelling Type

| Feature          | Description |
|------------------|-------------|
| `MSSubClass`     | Type of dwelling (e.g., 1-Story, 2-Story, Duplex, PUD) |
| `MSZoning`       | General zoning classification |
| `LotFrontage`    | Linear feet of street connected to property |
| `LotArea`        | Lot size in square feet |
| `Street`         | Road access type (Gravel or Paved) |
| `Alley`          | Alley access type |
| `LotShape`       | General shape of property |
| `LandContour`    | Flatness of property |
| `Utilities`      | Type of utilities available |
| `LotConfig`      | Lot configuration |
| `LandSlope`      | Slope of property |

---

### 🏡 Location and Neighborhood

| Feature          | Description |
|------------------|-------------|
| `Neighborhood`   | Physical locations within Ames city limits |
| `Condition1`     | Proximity to main roads, railroads, or positive features |
| `Condition2`     | Additional proximity conditions |

---

### 🏗️ Building Characteristics

| Feature           | Description |
|-------------------|-------------|
| `BldgType`        | Type of dwelling |
| `HouseStyle`      | Style of dwelling |
| `OverallQual`     | Overall material and finish quality (1–10) |
| `OverallCond`     | Overall condition rating (1–10) |
| `YearBuilt`       | Year the house was built |
| `YearRemodAdd`    | Year of last remodel |
| `RoofStyle`       | Type of roof |
| `RoofMatl`        | Roof material |
| `Exterior1st`     | Exterior covering |
| `Exterior2nd`     | Additional exterior covering |
| `MasVnrType`      | Masonry veneer type |
| `MasVnrArea`      | Masonry veneer area |

---

### 🏚️ Basement and Foundation

| Feature         | Description |
|-----------------|-------------|
| `Foundation`    | Foundation type |
| `BsmtQual`      | Basement height |
| `BsmtCond`      | Basement condition |
| `BsmtExposure`  | Basement exposure |
| `BsmtFinType1`  | Basement finished area type 1 |
| `BsmtFinSF1`    | Finished area square feet (type 1) |
| `BsmtFinType2`  | Basement finished area type 2 |
| `BsmtFinSF2`    | Finished area square feet (type 2) |
| `BsmtUnfSF`     | Unfinished area square feet |
| `TotalBsmtSF`   | Total basement area |

---

### 🏢 Interior

| Feature           | Description |
|-------------------|-------------|
| `GrLivArea`       | Above ground living area |
| `FullBath`        | Full baths above ground |
| `HalfBath`        | Half baths above ground |
| `BedroomAbvGr`    | Bedrooms above ground |
| `KitchenAbvGr`    | Kitchens above ground |
| `KitchenQual`     | Kitchen quality |
| `TotRmsAbvGrd`    | Total rooms above ground |
| `Functional`      | Home functionality rating |

---

### 🏡 Garage and Parking

| Feature         | Description |
|-----------------|-------------|
| `GarageType`    | Garage location |
| `GarageYrBlt`   | Year garage was built |
| `GarageFinish`  | Interior finish of garage |
| `GarageCars`    | Garage capacity |
| `GarageArea`    | Garage size |
| `GarageQual`    | Garage quality |
| `GarageCond`    | Garage condition |
| `PavedDrive`    | Paved driveway |

---

### 🌿 Outdoor Features

| Feature          | Description |
|------------------|-------------|
| `WoodDeckSF`     | Wood deck area |
| `OpenPorchSF`    | Open porch area |
| `EnclosedPorch`  | Enclosed porch area |
| `3SsnPorch`      | Three season porch area |
| `ScreenPorch`    | Screen porch area |
| `PoolArea`       | Pool area |
| `PoolQC`         | Pool quality |
| `Fence`          | Fence quality |
| `MiscFeature`    | Miscellaneous features |

---

### 🏷️ Sale Information

| Feature          | Description |
|------------------|-------------|
| `MoSold`         | Month sold |
| `YrSold`         | Year sold |
| `SaleType`       | Type of sale |
| `SaleCondition`  | Sale condition |

---

## 💡 Next Steps

1. **Model Training**
   - Linear Regression
   - Random Forest
   - XGBoost
2. **Hyperparameter Tuning**
3. **Model Evaluation**
4. **Generating predictions on test data**

---

## ✨ References

- [De Cock, D. (2011). Ames Housing Data](http://jse.amstat.org/v19n3/decock.pdf)
- [Kaggle Competition](https://www.kaggle.com/c/house-prices-advanced-regression-techniques)

---

## 📬 Contact

Feel free to reach out if you have questions or suggestions!
