# Project Overview

This project focuses on building a predictive model using a structured workflow that includes data preprocessing, exploratory data analysis (EDA), and machine learning techniques. Advanced methods such as balancing datasets with SMOTETomek and automated machine learning with PyCaret are applied to enhance model performance and robustness.

---

## Key Features

1. **Comprehensive Data Preprocessing:**
    - Handling of missing values, duplicate records, and irrelevant columns.
    - Conversion of categorical variables into numerical representations via One-Hot Encoding and Label Encoding.
    - Balancing of imbalanced datasets using SMOTETomek.
2. **Exploratory Data Analysis (EDA):**
    - Analysis of the target variable's distribution.
    - Insightful visualizations for categorical, continuous, and relational data.
3. **Feature Engineering:**
    - Categorization of features into categorical, continuous, and bivariate types.
    - Selection of significant features for modeling.
4. **Automated Machine Learning:**
    - Use of PyCaret’s `setup` function for efficient preprocessing.
    - Model comparison and selection of the best-performing classifier.
5. **Custom Pipeline Integration:**
    - Application of `RandomUnderSampler` for additional imbalance handling.
    - Use of Scikit-learn and PyCaret to evaluate and compare multiple classification models.

---

## Tools Used

The following Python libraries and frameworks were utilized:

- **Data Handling:** `pandas`, `numpy`
- **Visualization:** `matplotlib`, `seaborn`
- **Preprocessing and Balancing:** `scikit-learn`, `imblearn` (SMOTETomek)
- **Automated ML:** `pycaret.classification`

---

## Data Sources

The dataset is structured in CSV format and contains:

- Categorical, continuous, and relational (bivariate) variables.
- A target variable (`TARGET`) for classification purposes.

---

## Data Cleaning and Transformation

1. **Initial Steps:**
    - Dropped irrelevant columns and ensured consistent data types.
    - Handled missing and duplicate values.
2. **Encoding Categorical Variables:**
    - Applied One-Hot Encoding for non-ordinal categories.
    - Used Label Encoding for ordinal features where applicable.
3. **Balancing the Dataset:**
    - Implemented SMOTETomek to address class imbalance.
4. **Data Preparation for Modeling:**
    - Created a resampled dataset with balanced classes by combining oversampling (SMOTE) and undersampling (Tomek Links).
    - Constructed a final DataFrame ready for modeling with both predictors and the target variable.
    
    ---
    
    ## Analysis Insights
    
    1. **Target Variable Distribution:**
        - Comprehensive examination of the target class proportions before and after balancing, ensuring a fair training set for the model.
    2. **Feature Importance:**
        - Leveraged PyCaret's automated feature ranking to identify key predictors of the target variable.
    3. **Performance Metrics:**
        - Evaluated models using accuracy, precision, recall, F1 score, and area under the curve (AUC) to determine their effectiveness.
    4. **Model Comparisons:**
        - Conducted a side-by-side comparison of various classifiers to select the best-performing model for deployment.
    
    ---
    
    ## How to Use
    
    1. **Setup:**
        - Install the required Python packages.
        - Place the dataset in the same directory as the project files.
    2. **Execution Steps:**
        - Open and run the Jupyter Notebook (`Master final.ipynb`) in your preferred environment (e.g., Jupyter Lab, VSCode).
        - Follow the step-by-step cells to preprocess, balance, and analyze the dataset.
        - Review the model comparison outputs to identify the best-performing classifier.
    3. **Customizing the Pipeline:**
        - Modify the `setup` parameters in PyCaret for normalization, transformation, and sampling methods.
        - Adjust SMOTETomek parameters to tailor the balancing process for your dataset.
    4. **Export and Deploy:**
        - Export the trained model from PyCaret for deployment using `save_model()`.
        - Deploy the model in production to make predictions on new data.
    
    ---
    
    ## Future Enhancements
    
    1. Implement advanced feature selection techniques such as Recursive Feature Elimination (RFE).
    2. Explore ensemble learning methods like stacking or blending for improved performance.
    3. Integrate hyperparameter tuning frameworks such as Optuna or GridSearchCV for further optimization.
    
    ---
    
    ## Contributions
    
    Contributions are welcome! If you have ideas for improvement or want to collaborate, feel free to create a pull request or reach out with suggestions.
    
    ---
    
    ## License
    
    This project is open-source and provided for educational and research purposes. Please adhere to the license terms for non-commercial use.
