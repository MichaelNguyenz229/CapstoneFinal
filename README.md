# Predicting Human Cognitive Performance - Capstone Project

**Author:** Michael Viet Nguyen  
**Program:** Berkeley Haas Machine Learning & AI Professional Certificate  
**Module:** 24 - Final Report and Analysis

---

## Executive Summary

This project successfully identifies which measurable lifestyle factors most strongly predict an individual's calculated Cognitive Score. Through comprehensive machine learning analysis of 80,000 samples, the study demonstrates that cognitive performance is highly predictable (R² = 0.98) from lifestyle choices, with **Stress Level** and **Exercise Frequency** emerging as the dominant predictors.

### Key Findings:
- **Stress Level**: Strongest predictor with negative correlation of -0.228
- **Exercise Frequency**: 14.21 point difference between high/low activity groups  
- **Model Performance**: Random Forest achieved R² = 0.98 (98% variance explained)
- **Minimal Impact**: Gender and Diet Type showed negligible predictive power (0.34 points)

---

## Research Question

**Which measurable lifestyle factors most strongly predict an individual's calculated Cognitive Score?**

---

## Project Structure

### Technical Deliverables
- **`Capstone_Final_Notebook.ipynb`** - Complete Jupyter notebook with:
  - Data loading and exploration
  - Comprehensive EDA with visualizations
  - Data preprocessing and feature engineering
  - Model development (Linear Regression baseline, Random Forest)
  - Hyperparameter tuning with GridSearchCV
  - Model evaluation and comparison
  - Feature importance analysis
  - Detailed findings and conclusions

### Non-Technical Deliverables
- **`Capstone_Final_Report.docx`** - Professional report covering:
  1. Problem Statement
  2. Model Outcomes/Predictions  
  3. Data Acquisition
  4. Data Preprocessing
  5. Modeling Methodology
  6. Model Evaluation
  7. Key Findings
  8. Conclusions and Recommendations

---

## Methodology

### 1. Data Acquisition
- **Dataset**: Samharison's "Human Cognitive Performance Analysis" from Kaggle
- **Size**: 80,000 samples
- **Features**: 13 features including demographics, lifestyle factors, and cognitive measures
- **Quality**: Zero missing values, zero duplicates

### 2. Data Preprocessing
- **Missing Values**: None detected - exceptional data quality
- **Outlier Analysis**: Box plots revealed natural variation, no removal needed
- **Feature Scaling**: StandardScaler applied to numeric features (Age, Sleep_Duration, Stress_Level, Daily_Screen_Time, Caffeine_Intake)
- **Feature Encoding**: One-Hot Encoding for categorical features (Gender, Diet_Type, Exercise_Frequency)
- **Train-Test Split**: 80% training (64,000), 20% testing (16,000)
- **Excluded Features**: User_ID, Reaction_Time, Memory_Test_Score, AI_Predicted_Score

### 3. Exploratory Data Analysis
- **Correlation Analysis**: Identified Stress_Level as strongest linear correlate (-0.227639)
- **Categorical Analysis**: Exercise_Frequency showed largest impact (14.21 points)
- **Distribution Analysis**: Target variable (Cognitive_Score) normally distributed
- **Visualization**: Comprehensive plots for all numeric and categorical predictors

### 4. Modeling

#### Baseline Model: Linear Regression
- **Purpose**: Establish performance benchmark and understand linear relationships
- **Results**: R² ≈ 0.05 (modest performance, indicating non-linear relationships)

#### Primary Model: Random Forest Regressor
- **Initial Training**: Default parameters (100 estimators)
- **Hyperparameter Tuning**: GridSearchCV with 3-fold cross-validation
- **Parameter Grid**:
  - n_estimators: [100, 200]
  - max_depth: [10, 20, None]
  - min_samples_split: [2, 5]
  - min_samples_leaf: [1, 2]
- **Final Performance**: R² ≈ 0.98 (exceptional predictive accuracy)

### 5. Model Evaluation

#### Metrics Used:
- **R² Score**: Primary metric measuring variance explained
- **RMSE**: Root Mean Squared Error (approximately 2.4)
- **MAE**: Mean Absolute Error (approximately 1.45)

#### Model Comparison:
| Model | Test R² | Test RMSE | Test MAE |
|-------|---------|-----------|----------|
| Linear Regression | ~0.05 | ~19.00 | ~15.00 |
| Random Forest (Default) | ~0.98 | ~2.50 | ~1.50 |
| Random Forest (Optimized) | ~0.98 | ~2.40 | ~1.45 |

---

## Results

### Feature Importance Rankings (Top Predictors)
The Random Forest model identified the following factors as most important for predicting Cognitive Score:

1. **Stress_Level** - Highest importance, strong negative correlation
2. **Exercise_Frequency** (categorical bins) - Substantial impact on cognitive scores
3. **Sleep_Duration** - Measurable positive influence
4. **Daily_Screen_Time** - Moderate predictive power
5. **Age** - Smaller but significant effect
6. **Caffeine_Intake** - Measurable contribution

### Categorical Feature Analysis
- **Exercise Frequency**: Maximum difference of 14.21 points between high and low groups
- **Gender**: Maximum difference of only 0.34 points (minimal impact)
- **Diet Type**: Maximum difference of only 0.34 points (minimal impact)

---

## Practical Implications

### For Organizations
1. **Prioritize stress reduction programs** - Highest impact on cognitive performance
2. **Promote exercise initiatives** - Substantial measurable benefits (14+ point improvement)
3. **Support healthy sleep schedules** - Clear positive correlation with performance
4. **Manage screen time exposure** - Moderate but actionable impact
5. **Avoid overinvestment in low-impact factors** - Gender and diet programs show minimal ROI

### For Individuals
1. **Stress management** is the single most important factor - seek therapy, meditation, or time management support
2. **Regular exercise** (3-4x per week minimum) shows dramatic cognitive benefits
3. **Adequate sleep** (7-9 hours) is essential for optimal performance
4. **Limited screen time** and regular breaks improve cognitive function

---

## Conclusions

This capstone project successfully answers the research question by quantifying which lifestyle factors most strongly predict cognitive performance. The **Optimized Random Forest model** achieved exceptional accuracy (R² = 0.98), demonstrating that:

1. **Cognitive performance is highly predictable** from measurable lifestyle choices
2. **Stress Level and Exercise Frequency** are the dominant predictors requiring organizational focus
3. **Non-linear relationships** are critical - simple linear models cannot capture the complexity
4. **Organizations have clear, actionable levers** for improving human cognitive performance

The findings provide a data-driven foundation for designing wellness programs, allocating intervention resources, and making evidence-based decisions about human performance optimization.

---

## Limitations

- **Cross-sectional data**: Establishes correlation, not definitive causation
- **Single time point**: Cannot capture temporal dynamics or longitudinal effects  
- **Specific population**: Results should be validated across diverse demographic groups
- **Unmeasured factors**: Social connections, nutrition quality, and other factors not captured

---

## Future Directions

1. **Longitudinal studies** to establish causal relationships over time
2. **Intervention trials** to test effectiveness of recommended programs
3. **Interaction analysis** to understand how factors combine (e.g., does exercise mitigate stress?)
4. **Expanded cognitive metrics** beyond single composite score
5. **Deep learning approaches** to capture even more complex patterns
6. **Cost-benefit analysis** to quantify ROI of interventions

---

## Technical Requirements

### Python Libraries Used
```python
pandas>=1.3.0
numpy>=1.21.0
matplotlib>=3.4.0
seaborn>=0.11.0
scikit-learn>=1.0.0
```

### Jupyter Notebook Execution
The notebook is self-contained and requires only the dataset file: `human_cognitive_performance.csv`

All code cells are executable in sequence, with clear markdown sections documenting each step.

---

## Files in This Repository

- **`Capstone_Final_Notebook.ipynb`** - Complete technical analysis (Jupyter notebook)
- **`Capstone_Final_Report.docx`** - Non-technical final report (Word document)
- **`README.md`** - This file (project overview and documentation)
- **`human_cognitive_performance.csv`** - Dataset (80,000 samples)

---

## Contact

**Michael Viet Nguyen**  
Berkeley Haas Machine Learning & AI Professional Certificate Program  
Module 24 Final Submission

---

## Acknowledgments

- **Dataset**: Samharison (Kaggle) - "Human Cognitive Performance Analysis: Lifestyle & AI Predictions"
- **Program**: Berkeley Haas School of Business
- **Instructor/Program Leader**: [Program Leader Name]

---

## License

This project is submitted as part of the Berkeley Haas Machine Learning & AI Professional Certificate Program capstone requirement.
