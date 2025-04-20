# Software Requirements Specification (SRS)
## Music Therapy Recommendation System

### 1. System Overview

#### 1.1 Purpose
A machine learning proof-of-concept system that recommends music genres to patients based on demographic and mental health data to potentially alleviate symptoms of anxiety, depression, insomnia, and OCD.

#### 1.2 Scope
- Compare three ML algorithms: SVM, Logistic Regression, Decision Tree
- Develop basic recommendation prototype
- Analyze correlations between music preferences and mental health
- Focus on feasibility demonstration

#### 1.3 Technical Stack
- Python 3.x
- scikit-learn, pandas, numpy, matplotlib, seaborn
- Jupyter Notebook environment

### 2. Data Requirements

#### 2.1 Input Dataset Structure
**Primary CSV**: `mxmh_survey_results.csv`

**Key Columns**:
- Demographics: Age
- Behavior: Hours per day, While working
- Music Background: Instrumentalist, Composer, Exploratory
- Preferences: Fav genre, BPM, Foreign languages
- Genre Frequencies: 16 columns (Classical, Country, EDM, Folk, Gospel, Hip hop, Jazz, K pop, Latin, Lofi, Metal, Pop, R&B, Rap, Rock, Video game music)
- Mental Health Scores: Anxiety, Depression, Insomnia, OCD (scale 0-10)
- Target: Music effects ("Improve", "No effect", "Worsen")

#### 2.2 Data Quality Requirements
- Handle missing/empty values (Age, BPM, Music effects have nulls)
- Standardize frequency values (Never, Rarely, Sometimes, Very frequently)
- Validate mental health scores (0-10 scale)
- Clean categorical values (streaming services, genres)

### 3. Functional Requirements

#### 3.1 Data Preprocessing
- **FR-1**: Load and validate CSV data
- **FR-2**: Handle missing values
  - Age: Impute with median
  - BPM: Impute with mean/median by genre
  - Music effects: Remove or impute as "No effect"
- **FR-3**: Encode categorical variables
  - One-hot encoding: Primary streaming service, Fav genre, Music effects
  - Ordinal encoding: Frequency columns (Never:0 → Very frequently:3)
  - Binary encoding: While working, Instrumentalist, Composer, Exploratory
- **FR-4**: Normalize numerical features (Age, Hours per day, BPM)
- **FR-5**: Create composite mental health score (average of 4 conditions)

#### 3.2 Exploratory Data Analysis
- **FR-6**: Generate basic statistics
- **FR-7**: Create visualizations:
  - Heatmap: Genre frequency vs mental health scores
  - Bar charts: Music effects distribution by genre
  - Scatter plots: Age vs music preferences
  - Box plots: Mental health scores by streaming service
- **FR-8**: Perform correlation analysis

#### 3.3 ML Model Development
- **FR-9**: Split dataset (train:test = 80:20, stratified)
- **FR-10**: Implement SVM classifier
  - Test linear, RBF, polynomial kernels
  - Grid search for C, gamma parameters
- **FR-11**: Implement Logistic Regression
  - Test L1/L2 regularization
  - Grid search for C parameter
- **FR-12**: Implement Decision Tree
  - Test max_depth (3-10), min_samples_split
  - Grid search for optimal parameters
- **FR-13**: Evaluate each model using:
  - 5-fold cross-validation
  - F1-score (primary), Accuracy, Precision, Recall
  - Confusion matrix

#### 3.4 Recommendation System
- **FR-14**: Create recommendation function
  - Input: demographic data, music preferences
  - Output: recommended genres with confidence scores
- **FR-15**: Generate sample predictions with explanations
- **FR-16**: Create use case flow diagram

### 4. Non-Functional Requirements

#### 4.1 Performance
- **NFR-1**: Model training time < 5 minutes per algorithm
- **NFR-2**: Prediction inference time < 100ms
- **NFR-3**: Memory usage < 4GB during processing

#### 4.2 Usability
- **NFR-4**: Clear documentation in Jupyter notebooks
- **NFR-5**: Well-commented code following PEP 8
- **NFR-6**: Visual outputs as PNG/SVG for presentations

#### 4.3 Reliability
- **NFR-7**: Handle edge cases gracefully
- **NFR-8**: Validate input data formats
- **NFR-9**: Log errors and warnings

### 5. Experiment Framework

#### 5.1 Observation Log Format
```python
observation_entry = {
    "model": str,           # Algorithm name
    "hyperparameters": dict,
    "train_f1_score": float,
    "test_f1_score": float,
    "other_metrics": dict,  # accuracy, precision, recall
    "timestamp": datetime,
    "notes": str           # observations, issues, insights
}
```

#### 5.2 Experimentation Process
1. Baseline model performance
2. Hyperparameter tuning
3. Cross-validation assessment
4. Final evaluation on test set
5. Document all results

### 6. Deliverables

#### 6.1 Primary Outputs
- Trained ML models (saved as pickle files)
- Performance comparison table
- Algorithm performance visualizations
- Observation logs (JSON/CSV format)
- Model parameters and metrics documentation

#### 6.2 Secondary Outputs
- `recommend_genre()` function with API documentation
- Sample prediction notebook with explanations
- Use case flow diagram (SVG/PNG)

### 7. Data Flow

```
Input Data → Data Preprocessing → Feature Engineering →
Model Training → Evaluation → Recommendation System
```

### 8. Success Criteria
1. All three algorithms successfully trained
2. Clear performance comparison with statistically significant results
3. F1-score > 0.65 for at least one algorithm
4. Working recommendation prototype
5. Insights on genre-mental health relationships

### 9. System Architecture

#### Class Structure (High-Level):
```
DataProcessor
├── load_data()
├── handle_missing_values()
├── encode_features()
└── split_data()

ModelTrainer
├── train_svm()
├── train_logistic_regression()
├── train_decision_tree()
└── evaluate_model()

RecommendationEngine
├── predict_genre()
├── get_confidence_scores()
└── generate_explanation()
```

### 10. Risk Management
- Data quality issues → Implement robust preprocessing
- Class imbalance → Use stratified sampling, SMOTE
- Overfitting → Cross-validation, regularization
- Missing values → Multiple imputation strategies
- Model interpretability → SHAP values, feature importance
