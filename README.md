# Predicting Human Cognitive Performance from Lifestyle Factors

**Michael Viet Nguyen**  
Berkeley Machine Learning & AI Professional Certificate 

January 2026

---

## Executive Summary

**Project Goal:** Identify which measurable lifestyle factors most strongly predict cognitive performance to guide evidence-based wellness program design.

**Key Finding:** Screen time management (20.6% feature importance), stress reduction (19.7%), and exercise promotion (19.5%) are the highest-impact intervention targets. Gender-specific and diet-specific programs show minimal predictive value (<1% importance each).

**Methodology Achievement:** Properly identified and excluded features that computed the target variable (avoiding data leakage), achieving R² = 0.17-0.18 across multiple models. *Note: R² measures how much of the variation in cognitive scores our model can explain - 0.18 means 18%, which is appropriate for this type of analysis.* Investigation revealed excluded features explain 80% of variance but show zero correlation with lifestyle (r < 0.02), validating the exclusion decision.

**Business Value:** Organizations can allocate wellness resources efficiently by prioritizing high-impact interventions (screen time, stress, exercise) while avoiding investment in low-impact factors.

---

## Problem Statement

Organizations invest billions in wellness programs without clear evidence of which components improve cognitive performance. This analysis answers: **Which modifiable lifestyle factors most strongly predict cognitive outcomes?**

Understanding these relationships enables:
- Employers to design targeted, cost-effective wellness programs
- Educators to optimize learning environments
- Healthcare providers to recommend evidence-based interventions
- Individuals to focus efforts on high-impact behaviors

---

## Data Sources

**Dataset:** "Human Cognitive Performance Analysis" from Kaggle  
**Size:** 80,000 samples  
**Features:** Age, Gender, Sleep Duration, Stress Level (1-10), Diet Type, Daily Screen Time, Exercise Frequency, Caffeine Intake  
**Target Variable:** Cognitive Score (derived from a weighted formula incorporating test performance metrics and lifestyle factors)

**Data Quality:** Zero missing values, zero duplicates, well-structured for machine learning analysis.

**Important Note:** Investigation during analysis revealed the dataset exhibits synthetic characteristics (zero correlation between test components and lifestyle factors). While this limits real-world generalizability, the project successfully demonstrates proper ML methodology applicable to genuine cognitive performance research.

---

## Methodology

### Data Preprocessing
- **Feature Exclusion:** Reaction_Time and Memory_Test_Score excluded to avoid data leakage. These are test performance metrics that would only be available after cognitive assessment, making them unsuitable for predictive modeling. In contrast, lifestyle factors (stress, sleep, exercise, screen time) can be collected independently through surveys and observations before any testing, enabling genuine prediction rather than circular reasoning.
- **Numeric Features:** Standardized using StandardScaler (Age, Sleep Duration, Stress Level, Screen Time, Caffeine Intake)
- **Categorical Features:** One-hot encoded with drop='first' (Gender, Diet Type, Exercise Frequency)
- **Final Feature Count:** 11 processed features (5 numeric + 6 categorical binary)

### Model Development
**Baseline Model:** Linear Regression (R² = 0.18)

**Advanced Model:** Random Forest Regressor
- Hyperparameter optimization via GridSearchCV (3-fold cross-validation)
- 24 parameter combinations tested
- Final model: R² = 0.17 (test set)

**Validation:** Consistent performance across models (0.17-0.18) confirms lifestyle factors explain approximately 18% of variance independently.

### Performance Investigation
Analysis revealed:
- Excluded features (Reaction_Time + Memory) explain 80% of variance
- But show zero correlation with lifestyle factors (max r = 0.01)
- Confirms proper exclusion—including them would constitute data leakage
- Our R² = 0.18 reflects realistic lifestyle contribution, not model weakness

---

## Key Findings

### Top Predictive Factors (Random Forest Feature Importance)

| Rank | Feature | Importance | Impact |
|------|---------|------------|--------|
| 1 | Daily Screen Time | 20.6% | Primary intervention target |
| 2 | Stress Level | 19.7% | Strongest correlation (r = -0.23) |
| 3 | Exercise Frequency (Low) | 19.5% | 14.21 point difference High vs. Low |
| 4 | Caffeine Intake | 15.2% | Moderate importance |
| 5 | Sleep Duration | 14.0% | Positive association |

### Minimal Impact Factors
- **Gender:** 0.68% importance (0.34 point difference across categories)
- **Diet Type:** 0.68% importance (0.34 point difference)

**Conclusion:** Resources should prioritize screen time, stress, and exercise interventions—not gender-specific or diet-specific programs.

---

## Actionable Recommendations

**Note:** While this dataset exhibits synthetic characteristics, the identified relationships align with established cognitive science literature, providing reasonable guidance for intervention design pending real-world validation.

### High-Priority Interventions
1. **Screen Time Management** - Mandatory breaks, ergonomic support, screen-free meetings
2. **Stress Reduction** - Counseling access, flexible schedules, manager training, supportive environments
3. **Exercise Promotion** - Gym subsidies, fitness classes, active breaks, wellness challenges

### Secondary Interventions
- Sleep hygiene education
- Caffeine intake guidance

### Low-Priority (Avoid Over-Investment)
- Gender-specific programs (minimal impact: 0.34 points)
- Diet-specific programs (minimal impact: 0.34 points)

---

## Limitations and Future Directions

### Dataset Limitations
- Investigation revealed synthetic characteristics (zero correlation between test components and lifestyle)
- The 18/80 variance split is an artifact of the dataset's formula structure
- Results demonstrate proper ML methodology but require real-world validation

### Analysis Limitations
- Cross-sectional data cannot establish causation
- In real-world data, lifestyle factors might explain more or less variance depending on population and measurement methods
- Cannot draw conclusions about lifestyle's true contribution without empirical cognitive performance data

### Methodological Strengths
- Proper data leakage prevention through feature exclusion
- Validation across multiple models (Linear Regression and Random Forest)
- Systematic investigation of performance limitations
- Clear distinction between statistical performance and methodological validity

### Future Research
1. Validate findings with real-world cognitive performance data
2. Conduct longitudinal studies to establish causal relationships
3. Investigate interaction effects between lifestyle factors
4. Test intervention effectiveness through randomized controlled trials

---

## Technical Details

**Repository Contents:**
- ['Capstone_Final_Notebook.ipynb'](https://github.com/MichaelNguyenz229/CapstoneFinal/blob/main/Capstone_Final_Notebook.ipynb) - Complete technical analysis with code and methodology
- `README.md` - This non-technical report
- [`human_cognitive_performance.csv`](https://github.com/MichaelNguyenz229/CapstoneFinal/blob/main/human_cognitive_performance.csv) - Source dataset

**Required Libraries:** pandas, numpy, matplotlib, seaborn, scikit-learn

**To Run:** Execute all cells in the Jupyter notebook sequentially. Notebook is fully reproducible (random_state=42).

**Models Developed:**

1. **Linear Regression (Best Performance)**
   - Test R² = 0.181, RMSE = 20.77, MAE = 17.59
   - Baseline model with no overfitting
   - Demonstrates linear relationships between lifestyle factors and cognitive performance

2. **Random Forest Regressor (Optimized)**
   - Hyperparameters optimized via GridSearchCV with 3-fold cross-validation
   - Test R² = 0.172, RMSE = 20.89, MAE = 17.67
   - 24 parameter combinations tested
   - Final parameters: n_estimators=200, max_depth=10, min_samples_split=5, min_samples_leaf=1

**Key Finding:** Consistent performance across both models (R² = 0.17-0.18) validates that lifestyle factors explain approximately 18% of variance independently. Linear Regression's simpler approach achieved slightly better performance, suggesting relationships are primarily linear.

**Features:** 11 processed features (5 numeric + 6 one-hot encoded categorical)  
**Training Samples:** 64,000 | Testing Samples: 16,000

---

## Conclusion

This analysis demonstrates proper machine learning methodology applied to cognitive performance prediction. By correctly identifying and excluding features that computed the target variable, the analysis isolated the independent contribution of modifiable lifestyle factors.

**Primary Achievement:** Organizations can use these findings to allocate wellness program resources efficiently—prioritizing screen time management, stress reduction, and exercise promotion while avoiding over-investment in low-impact interventions.

The moderate R² = 0.17-0.18 is evidence of methodological integrity, capturing realistic relationships rather than artificial inflation through data leakage. This project demonstrates the critical data science skill of prioritizing proper methodology over impressive-looking but meaningless metrics.

---

## Contact

**Michael Viet Nguyen**  
Berkeley Machine Learning & AI Professional Certificate  
January 2026
