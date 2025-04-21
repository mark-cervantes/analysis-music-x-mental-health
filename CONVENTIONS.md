# Music-x-Mental-Health Analysis Project Conventions

This document outlines conventions and best practices for the Music Therapy Recommendation System project - a data science project focused on analyzing correlations between music preferences and mental health outcomes.

## Project Structure

```
analysis-music-x-mental-health/
├── data/
│   ├── raw/                 # Original, immutable data
│   └── processed/           # Cleaned and transformed datasets
├── notebooks/               # Jupyter notebooks (numbered for order)
├── outputs/
│   ├── figures/            # Exported visualizations
│   └── observation_logs/   # Model training logs
├── presentations/          # Slide decks and demos
├── scripts/                # Helper scripts (if needed)
├── requirements.txt
├── README.md
└── CONVENTIONS.md
```

## Naming Conventions

### Jupyter Notebooks
- Use incremental numbering: `01_`, `02_`, etc.
- Follow with descriptive names: `01_Data_Overview_and_Quality_Check.ipynb`
- Use underscores instead of spaces
- Maintain logical flow between notebooks

### Files and Directories
- Use lowercase for directory names
- Use snake_case for Python files
- PascalCase for class names
- SCREAMING_SNAKE_CASE for constants
- Data files: descriptive names with underscores (e.g., `mxmh_survey_results.csv`)

### Variables
- `df_` prefix for DataFrames (e.g., `df_survey`)
- `fig_` prefix for figure objects
- `model_` prefix for trained models
- Use descriptive names: avoid single letters except for loops

## Code Style Guidelines

### Notebook Organization
1. **Header Cell**: Title, description, author, date
2. **Import Cell**: All imports at the beginning
3. **Constants Cell**: Configuration and constants
4. **Content Cells**: Logical sections with markdown headers
5. **Documentation Cells**: Explanations before/after major operations

### Python Code Style
```python
# Imports grouped and ordered
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from sklearn.model_selection import train_test_split

# Constants at top
RANDOM_STATE = 42
TEST_SIZE = 0.2

# Function documentation
def preprocess_data(df: pd.DataFrame) -> pd.DataFrame:
    """Preprocess survey data for ML modeling.
    
    Args:
        df: Raw survey DataFrame
    
    Returns:
        Cleaned and transformed DataFrame
    """
    # Implementation
    return df_processed
```

### Data Processing Patterns
1. **Copy DataFrames**: Always work on copies to preserve original data
2. **Chain operations** where possible for readability
3. **Document transformations**: Comment why each transformation is necessary
4. **Check data quality**: Validate after each major transformation

```python
# Example pattern
df_clean = (df.copy()
    .dropna(subset=['Age'])
    .pipe(encode_categorical_features)
    .pipe(normalize_numerical_features))
```

## Visualization Guidelines

### Standard Plot Aesthetics
```python
# Plot configuration
plt.rcParams['figure.figsize'] = (10, 6)
plt.rcParams['font.size'] = 12
plt.style.use('seaborn-v0_8-darkgrid')

# Color palette
PALETTE = ['#1f77b4', '#ff7f0e', '#2ca02c', '#d62728', '#9467bd']
```

### Export Requirements
- High resolution: 300 DPI minimum
- Standard format: PNG for raster, SVG for vector
- Clear labeling: titles, axes, legends
- Consistent styling across all notebooks

## Model Development Standards

### Experiment Tracking
```python
observation_entry = {
    "model": "SVM",
    "hyperparameters": {"kernel": "rbf", "C": 1.0},
    "train_f1_score": 0.85,
    "test_f1_score": 0.82,
    "other_metrics": {"accuracy": 0.83, "precision": 0.84, "recall": 0.81},
    "timestamp": "2025-04-21 10:30:00",
    "notes": "RBF kernel performs better than linear for this dataset"
}
```

### Cross-Validation Protocol
- Use stratified K-fold (k=5) for classification
- Set random state for reproducibility
- Report mean and std of metrics

### Model Saving
```python
import joblib

# Save model
joblib.dump(model, 'outputs/models/svm_final.joblib')

# Load model
model_loaded = joblib.load('outputs/models/svm_final.joblib')
```

## Security Considerations

### Data Privacy
- Never commit raw data with PII to repository
- Anonymize data before sharing
- Use environment variables for sensitive configurations

### Notebook Security
- Clear outputs before committing notebooks
- Use nbstripout for automatic output removal
- Review cells for sensitive information

## Documentation Standards

### Notebook Documentation
- Each notebook starts with purpose and dependencies
- Major sections have markdown headers
- Complex operations explained with comments
- Results interpreted in markdown cells

### Function Documentation
```python
def recommend_genre(demographics: dict, preferences: dict) -> tuple[str, float]:
    """Recommend music genre based on user demographics and preferences.
    
    Args:
        demographics: Dict containing age, streaming_service
        preferences: Dict containing favorite_genre, listening_hours
    
    Returns:
        Tuple of (recommended_genre, confidence_score)
    
    Raises:
        ValueError: If required features are missing
    """
    # Implementation
    return genre, confidence
```

## Testing Practices

### Data Validation
```python
def validate_data(df: pd.DataFrame) -> bool:
    """Validate data meets requirements."""
    required_columns = ['Age', 'Anxiety', 'Depression', 'Music effects']
    
    # Check structure
    if not all(col in df.columns for col in required_columns):
        return False
    
    # Check value ranges
    if not df['Anxiety'].between(0, 10).all():
        return False
    
    return True
```

### Model Validation
- Test edge cases
- Validate input formats
- Check prediction ranges
- Test with synthetic data

## Presentation Standards

### Slide Notebooks
- Use RISE extension for presentations
- Hide code cells for executive summaries
- Include interactive widgets where appropriate
- Export to standalone HTML

### Interactive Demos
```python
import ipywidgets as widgets

@widgets.interact(
    age=widgets.IntSlider(min=18, max=80, value=30),
    favorite_genre=widgets.Dropdown(options=['Rock', 'Classical', 'EDM'])
)
def interactive_recommendation(age, favorite_genre):
    """Interactive demo for recommendation system."""
    # Implementation
    pass
```

## Version Control

### Commit Convention
- Use clear, descriptive commit messages
- Reference task IDs where applicable
- Group related changes
- Keep commits atomic

### Branch Strategy
- `main` for stable analysis
- `develop` for work in progress
- Feature branches: `feature/[task-id]-description`

## Performance Optimization

### Memory Management
- Use chunking for large datasets
- Clear variables not in use
- Monitor memory usage in notebooks

### Computation
- Vectorize operations when possible
- Use appropriate data types (e.g., categories)
- Cache expensive computations

## Quality Assurance

### Code Review Guidelines
- Check for data leakage
- Verify statistical assumptions
- Review feature engineering logic
- Validate evaluation metrics

### Analysis Reproducibility
- Set random seeds
- Document software versions
- Export environment configuration

```bash
# Create environment snapshot
pip freeze > requirements.txt
```

## Continuous Integration

### Pre-commit Hooks
- Format code with black
- Check style with flake8
- Clear notebook outputs
- Run basic data validation

This conventions document serves as a living guide for maintaining consistency and quality throughout the Music-x-Mental-Health analysis project. Update as needed based on project evolution and team feedback.
