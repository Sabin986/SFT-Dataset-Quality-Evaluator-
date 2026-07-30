# SFT Dataset Quality Evaluator and Intelligent Scoring System

## Project Overview

The **SFT Dataset Quality Evaluator and Intelligent Scoring System** is a data quality assessment project designed to evaluate the quality and training readiness of a Supervised Fine-Tuning (SFT) dataset.

The project analyzes important dataset quality factors such as completeness, text quality, duplicate samples, uniqueness, domain balance, and source balance. It calculates an overall quality score, generates intelligent recommendations, creates quality visualizations, and provides a final training readiness decision.

A dataset may have no missing values and well-formatted text but still be unsuitable for AI model training if it contains a large number of repeated samples. Therefore, this project evaluates both **data quality** and **dataset diversity** before providing a training recommendation.

The final system provides:

- Dataset loading and inspection
- Missing value analysis
- Empty text detection
- Duplicate ID analysis
- Duplicate instruction analysis
- Duplicate output analysis
- Duplicate SFT sample analysis
- Text length analysis
- Domain analysis
- Source analysis
- Dataset quality scoring
- Intelligent recommendations
- Quality visualization
- Training risk assessment
- Training readiness evaluation
- Final assessment reports

---

# Project Objectives

The main objectives of this project are:

1. Load and inspect an SFT dataset.
2. Identify missing and empty values.
3. Detect duplicate IDs, instructions, outputs, and complete SFT samples.
4. Analyze instruction, input, and output lengths.
5. Evaluate domain distribution and balance.
6. Evaluate source distribution and balance.
7. Calculate the overall dataset quality score.
8. Generate intelligent recommendations based on detected issues.
9. Visualize dataset quality and domain distribution.
10. Determine whether the dataset is suitable for SFT training.
11. Identify training risks.
12. Generate final assessment and recommendation reports.

---

# What is an SFT Dataset?

SFT stands for **Supervised Fine-Tuning**.

An SFT dataset contains examples that teach an AI model how to respond to instructions. Each sample generally contains an instruction, optional input context, and an expected output.

Example:

```text
Instruction:
Explain the concept of machine learning.

Input:
Use simple language for beginners.

Output:
Machine learning is a branch of artificial intelligence in which computers learn patterns from data and use those patterns to make predictions or decisions.
```

During fine-tuning, the AI model learns from many instruction-output examples. Therefore, the quality, correctness, and diversity of the dataset directly affect the performance of the trained model.

---

# Dataset Structure

The dataset contains the following columns:

| Column | Description |
|---|---|
| `id` | Unique identifier for each SFT sample |
| `domain` | Subject or category of the sample |
| `instruction` | Task or request given to the AI model |
| `input` | Additional context or information |
| `output` | Expected response or answer |
| `source` | Origin of the dataset sample |

Example dataset structure:

| id | domain | instruction | input | output | source |
|---|---|---|---|---|---|
| UUID | finance | Calculate compound interest | Principal, rate, and time | Calculated result | synthetic |
| UUID | marketing | Create a campaign slogan | Product details | Suggested slogan | human-curated |

---

# Project Structure

```text
SFT-DATASET-QUALITY-EVALUATOR/
│
├── data/
│   └── raw/
│       └── sft_dataset.csv
│
├── notebooks/
│   ├── 01_data_loading.ipynb
│   ├── 02_quality_checks.ipynb
│   ├── 03_quality_scoring.ipynb
│   ├── 04_intelligent_recommendations.ipynb
│   ├── 05_quality_visualisation.ipynb
│   └── 06_training_readiness.ipynb
│
├── output/
│   ├── charts/
│   │   ├── domain_distribution.png
│   │   └── quality_issues_chart.png
│   │
│   └── reports/
│       ├── final_sft_assessment_report.csv
│       ├── final_training_recommendations.csv
│       ├── intelligent_recommendations.csv
│       ├── quality_penalty_details.csv
│       └── quality_scoring_result.csv
│
└── README.md
```

---

# Project Workflow

```text
SFT Dataset
      ↓
Dataset Loading
      ↓
Data Inspection
      ↓
Quality Checks
      ↓
Quality Scoring
      ↓
Intelligent Recommendations
      ↓
Quality Visualization
      ↓
Training Readiness Assessment
      ↓
Final Reports
```

---

# Step 1: Dataset Loading

**Notebook:**

`notebooks/01_data_loading.ipynb`

The original SFT dataset is stored in:

`data/raw/sft_dataset.csv`

The dataset is loaded using Pandas.

The following information is inspected:

- Number of rows
- Number of columns
- Dataset shape
- Column names
- Data types
- First few samples
- General dataset information
- Missing values

This step provides an initial understanding of the dataset before performing detailed quality analysis.

---

# Step 2: Data Quality Checks

**Notebook:**

`notebooks/02_quality_checks.ipynb`

The dataset is checked for multiple quality issues.

## Missing Value Check

The system checks whether any of the required columns contain missing values.

The following columns are evaluated:

```text
id
domain
instruction
input
output
source
```

This check helps identify incomplete SFT samples.

## Empty Text Check

The system checks whether the text columns contain empty or blank values.

The following columns are evaluated:

```text
instruction
input
output
```

This check helps identify samples that may not provide useful information during model training.

## Duplicate ID Check

The system checks whether multiple rows use the same ID.

Duplicate IDs may indicate data generation or data management problems.

## Duplicate Instruction Check

The system checks whether the same instruction appears multiple times.

Repeated instructions may reduce dataset diversity.

## Duplicate Output Check

The system checks whether the same output appears multiple times.

Repeated outputs may indicate limited response diversity.

## Duplicate SFT Sample Check

The system checks whether the same combination of instruction, input, and output appears multiple times.

The following columns are used:

```text
instruction
input
output
```

Duplicate SFT samples are important because repeated training examples may reduce the effective diversity of the dataset.

A high duplicate rate can cause:

- Limited training diversity
- Repeated learning patterns
- Increased risk of overfitting
- Weak generalization to new instructions
- Inefficient use of training resources

---

# Step 3: Text Length Analysis

The system calculates the length of:

- Instructions
- Inputs
- Outputs

The following quality checks are performed:

- Very short instructions
- Very short inputs
- Very short outputs
- Very long outputs

The purpose of this analysis is to identify incomplete, low-information, unusually short, or unusually long SFT samples.

---

# Step 4: Domain Analysis

The dataset contains multiple domains, including:

```text
code
education
finance
healthcare
law
marketing
productivity
psychology
sports
travel
```

The number of samples in each domain is calculated.

The domain analysis helps determine whether the dataset is reasonably balanced across different subject areas.

A balanced domain distribution helps prevent the dataset from being heavily dominated by a single domain.

The domain distribution chart is saved as:

`output/charts/domain_distribution.png`

---

# Step 5: Source Analysis

The dataset contains the following sources:

```text
synthetic

human-curated
```

The number of samples from each source is calculated.

The source analysis helps determine whether the dataset is reasonably balanced between different data sources.

---

# Step 6: Quality Scoring

**Notebook:**

`notebooks/03_quality_scoring.ipynb`

The quality scoring system evaluates the overall quality of the SFT dataset.

The scoring process considers important quality factors such as:

- Dataset completeness
- Text quality
- Dataset uniqueness
- Duplicate information
- Domain balance
- Source balance

The final quality score is calculated on a scale from:

```text
0 to 100
```

A higher score indicates better overall dataset quality.

The quality scoring result is saved as:

`output/reports/quality_scoring_result.csv`

Detailed quality scoring information is saved as:

`output/reports/quality_penalty_details.csv`

---

# Step 7: Intelligent Recommendations

**Notebook:**

`notebooks/04_intelligent_recommendations.ipynb`

The system generates recommendations based on the quality issues detected during dataset analysis.

The recommendations may include:

- Review duplicate samples
- Remove unnecessary repeated samples
- Increase the number of unique SFT examples
- Improve incomplete text
- Review low-quality instructions or outputs
- Improve domain balance
- Improve source balance
- Perform manual review before model training

The recommendations are generated automatically according to the detected dataset quality issues.

The generated recommendations are saved as:

`output/reports/intelligent_recommendations.csv`

---

# Step 8: Quality Visualization

**Notebook:**

`notebooks/05_quality_visualisation.ipynb`

The project creates charts to make the quality analysis easier to understand.

## Domain Distribution Chart

File:

`output/charts/domain_distribution.png`

This chart shows how dataset samples are distributed across different domains.

## Quality Issues Chart

File:

`output/charts/quality_issues_chart.png`

This chart visualizes the number of detected dataset quality issues.

The visualizations help users quickly identify important dataset patterns and quality problems.

---

# Step 9: Training Readiness Assessment

**Notebook:**

`notebooks/06_training_readiness.ipynb`

The training readiness system evaluates whether the SFT dataset is suitable for AI model training.

The assessment considers:

- Overall quality score
- Dataset completeness
- Text quality
- Dataset uniqueness
- Duplicate rate
- Domain balance
- Source balance

The system provides:

- Training readiness decision
- Training risk level
- Final training recommendations

Possible training decisions include:

```text
Ready for Training

Ready After Minor Review

Needs Quality Improvement

Not Recommended for Training
```

The final SFT dataset assessment is saved as:

`output/reports/final_sft_assessment_report.csv`

The final training recommendations are saved as:

`output/reports/final_training_recommendations.csv`

---

# Training Risk Assessment

The system assigns a training risk level based on the detected dataset quality issues.

Possible risk levels include:

```text
Low

Medium

High

Critical
```

A high duplicate rate or very low dataset uniqueness can increase the training risk.

The training risk assessment helps determine whether the dataset should be used directly or improved before SFT training.

---

# Generated Output

## Charts

| File | Description |
|---|---|
| `domain_distribution.png` | Shows the distribution of samples across different domains |
| `quality_issues_chart.png` | Visualizes the detected dataset quality issues |

## Reports

| Report | Description |
|---|---|
| `quality_scoring_result.csv` | Contains the final dataset quality score and quality status |
| `quality_penalty_details.csv` | Contains detailed information used during quality scoring |
| `intelligent_recommendations.csv` | Contains automatically generated dataset improvement recommendations |
| `final_sft_assessment_report.csv` | Contains the final SFT dataset quality and training assessment |
| `final_training_recommendations.csv` | Contains final recommendations before AI model training |

---

# Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Jupyter Notebook
- CSV

---

# Installation

Install the required Python libraries:

```bash
pip install pandas numpy matplotlib jupyter
```

---

# How to Run the Project

Run the Jupyter notebooks in the following order:

```text
1. 01_data_loading.ipynb

2. 02_quality_checks.ipynb

3. 03_quality_scoring.ipynb

4. 04_intelligent_recommendations.ipynb

5. 05_quality_visualisation.ipynb

6. 06_training_readiness.ipynb
```

Running the notebooks in this order ensures that the output from one stage is available for the next stage.

---

# Final Outcome

After running the complete project, the system provides:

- Dataset inspection results
- Missing value analysis
- Empty text analysis
- Duplicate data analysis
- Text length analysis
- Domain analysis
- Source analysis
- Overall dataset quality score
- Quality status
- Intelligent recommendations
- Quality visualizations
- Training risk assessment
- Training readiness decision
- Final dataset assessment report
- Final training recommendations

---

# Conclusion

This project provides a complete workflow for evaluating an SFT dataset before using it for AI model training.

The system checks important dataset quality issues such as missing values, empty text, duplicate samples, text quality, domain distribution, and source distribution.

The project does not rely only on a single quality score. It also generates intelligent recommendations, quality visualizations, training risk information, and a final training readiness decision.

This makes the evaluation more useful for deciding whether the dataset can be used for SFT training or should be improved before training.

---


# Author

**Sabin Bhattarai**

