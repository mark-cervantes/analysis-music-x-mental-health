# Music and Mental Health Analysis Project

## Overview
This project analyzes the relationship between music preferences, listening habits, and self-reported mental health using survey data. It involves data cleaning, exploratory data analysis (EDA), feature engineering, and aims to build machine learning models to predict music's effect on mental well-being.

## Project Structure
- `data/`: Contains raw (`raw/`) and processed (`processed/`) data files.
- `notebooks/`: Jupyter notebooks for the analysis workflow (01-Data Overview to 06-Feature Engineering, etc.).
- `outputs/`: Stores generated figures (`figures/`) and potentially other outputs.
- `requirements.txt`: Lists Python dependencies.
- `README.md`: This file.
- `*.md`: Other documentation files (PRD, SRS, task breakdown).

## Setup and Installation

### Option 1: Running on Google Colab

1.  **Prepare Project:** Download the project repository as a ZIP file from GitHub or ZIP your local project folder.
2.  **Upload to Google Drive:** Upload the ZIP file to your Google Drive.
3.  **Open Colab:** Go to [colab.research.google.com](https://colab.research.google.com/) and create a new notebook.
4.  **Mount Drive:** Run this cell in Colab:
    ```python
    from google.colab import drive
    drive.mount('/content/drive')
    ```
5.  **Unzip Project:** Run this command in a cell, replacing the path with yours:
    ```bash
    !unzip /content/drive/MyDrive/YourProjectName.zip -d /content/project
    ```
6.  **Change Directory:** Run this cell:
    ```bash
    %cd /content/project
    ```
7.  **Install Dependencies:** Run this cell:
    ```bash
    !pip install -r requirements.txt
    ```
8.  **Run Notebooks:** Use the file browser on the left to navigate into `/content/project/notebooks/` and open the `.ipynb` files sequentially.

### Option 2: Running Locally on Windows (No WSL)

1.  **Prerequisites:** Install Python (3.8+) from [python.org](https://www.python.org/) (ensure "Add Python to PATH" is checked) and Git from [git-scm.com](https://git-scm.com/).
2.  **Clone Repository:** Open Command Prompt (`cmd`) or PowerShell, navigate to your desired directory, and run:
    ```bash
    git clone <repository_url>
    cd <repository_directory_name>
    ```
3.  **Create Virtual Environment:** In the project root directory, run:
    ```bash
    python -m venv venv
    ```
4.  **Activate Environment:** Run:
    ```bash
    venv\Scripts\activate
    ```
5.  **Install Dependencies:** Run:
    ```bash
    pip install -r requirements.txt
    ```
6.  **Start Jupyter:** Run:
    ```bash
    jupyter lab
    ```
    or
    ```bash
    jupyter notebook
    ```
7.  **Run Notebooks:** Navigate to the `notebooks` folder in the Jupyter interface and run the `.ipynb` files sequentially.

## Usage
The analysis is performed through the Jupyter notebooks in the `/notebooks` directory. Please run them in numerical order (01, 02, 03, ...) as later notebooks often depend on outputs from earlier ones.

1.  `01_Data_Overview_and_Quality_Check.ipynb`: Load and inspect raw data.
2.  `02_Data_Cleaning_and_Preprocessing.ipynb`: Clean data, handle missing values.
3.  `03_EDA_Demographic_Analysis.ipynb`: Explore demographic distributions.
4.  `04_EDA_Music_and_Mental_Health.ipynb`: Explore music/mental health relationships.
5.  `05_EDA_Key_Insights_Summary.ipynb`: Summarize EDA findings.
6.  `06_Feature_Engineering.ipynb`: Prepare data features for modeling.
7.  *(Subsequent notebooks will cover modeling, evaluation, etc.)*
