# Predicting Human Cognitive Performance
## Final Capstone Project

**Author:** Michael Viet Nguyen  
**Berkeley Machine Learning & AI Professional Certificate**  
**Date:** January 2026

---

## Executive Summary

This project identifies which measurable lifestyle factors most strongly predict cognitive performance in individuals. Using machine learning analysis on 80,000 samples, the study reveals that **stress level** and **exercise frequency** are the dominant predictors of cognitive scores, explaining 98% of performance variance.

**Key Takeaway:** Organizations can significantly improve cognitive performance by focusing on stress reduction programs and exercise initiatives, rather than investing in factors with minimal impact like specific diet programs.

---

## 1. Problem Statement

### The Challenge

Organizations today struggle to identify which wellness interventions actually improve employee cognitive performance. Companies spend billions on wellness programs without knowing which components deliver results. This project answers a critical question: **Which measurable lifestyle factors most strongly predict an individual's cognitive performance?**

### Why This Matters

Understanding the strongest predictors of cognitive performance allows:
- **Employers** to design targeted wellness programs that maximize ROI
- **Educators** to optimize student learning environments  
- **Healthcare providers** to recommend evidence-based lifestyle interventions
- **Individuals** to focus efforts on high-impact behaviors

### Real-World Application

For example, if stress levels are confirmed as the dominant negative predictor, a company can focus its wellness budget on stress reduction programs (therapy, flexible schedules, mindfulness training) rather than expensive generalized initiatives. Similarly, if exercise shows strong predictive power, organizations can invest confidently in fitness programs knowing they'll yield measurable cognitive benefits.

### Project Goals

1. Identify which lifestyle factors are most predictive of cognitive performance
2. Quantify the impact of each factor to guide resource allocation
3. Provide actionable recommendations for organizations and individuals
4. Build a predictive model that can estimate cognitive performance from lifestyle choices

---

## 2. Model Outcomes and Predictions

### What We're Predicting

The project predicts **Cognitive Score** - a continuous numeric value ranging from approximately 10 to 100 that represents overall cognitive performance based on reaction time and memory test results.

### Type of Machine Learning

This is a **supervised learning regression problem**:
- **Supervised** because we have labeled data (known cognitive scores)
- **Regression** because we're predicting a continuous numeric value (not categories)

### Models Used

**Baseline Model - Linear Regression:**
- Purpose: Establish performance benchmark
- Helps understand basic linear relationships
- Performance: R² ≈ 0.05 (modest, confirming non-linear relationships exist)

**Primary Model - Random Forest Regressor:**
- Handles complex non-linear relationships between lifestyle factors
- Provides interpretable feature importance rankings
- Resistant to overfitting through ensemble of decision trees
- Performance: R² ≈ 0.98 (exceptional - explains 98% of variance)

### What the Model Tells Us

The Random Forest model provides two key outputs:
1. **Predicted cognitive scores** for individuals based on their lifestyle factors
2. **Feature importance rankings** that directly answer which factors matter most

This allows organizations to estimate expected cognitive performance improvements from lifestyle interventions and prioritize resources accordingly.

---

## 3. Data Acquisition

### Data Source

**Dataset:** "Human Cognitive Performance Analysis: Lifestyle & AI Predictions" by Samharison (Kaggle)  
**Size:** 80,000 individual samples  
**Quality:** Exceptional - zero missing values, zero duplicates

### Why This Dataset

This dataset was selected because it:
- Contains comprehensive measurable lifestyle factors that organizations can actually influence
- Provides substantial statistical power with 80,000 samples
- Includes diverse features allowing comprehensive analysis
- Represents real-world scenarios applicable to workplace and educational settings

### Features Included

**Demographic Attributes:**
- Age
- Gender (Male, Female, Other)

**Lifestyle Factors:**
- Sleep Duration (hours per night)
- Stress Level (scale 1-10)
- Diet Type (Non-Vegetarian, Vegetarian, Vegan)
- Daily Screen Time (hours)
- Exercise Frequency (Low, Medium, High)
- Caffeine Intake (mg per day)

**Target Variable:**
- Cognitive Score (computed from reaction time and memory tests)

**Excluded from Analysis:**
- Reaction Time and Memory Test Score (used to compute target - would cause data leakage)
- User ID (identifier with no predictive value)
- AI Predicted Score (another model's output, not an input feature)

### Data Visualization and Assessment

Initial exploratory analysis revealed:
- **Normal distribution** of cognitive scores across the population
- **Strong negative correlation** between stress and cognitive performance
- **Substantial differences** in cognitive scores based on exercise frequency
- **Minimal impact** from demographic factors like gender
- **Clean data** with no severe outliers requiring removal

This confirmed the dataset's suitability for answering the research question.

---

## 4. Data Preprocessing and Preparation

### Data Cleaning Process

**Missing Values:**  
Comprehensive analysis confirmed zero missing values across all 13 features. This exceptional data quality eliminated the need for imputation strategies and simplified the preprocessing workflow.

**Duplicate Records:**  
No duplicate entries were found, confirming each of the 80,000 samples represents a unique individual.

**Outlier Analysis:**  
Box plots were generated for all numeric predictors to identify potential anomalies. While some data points fell outside the interquartile range, these represented natural human variation rather than errors. No outliers were removed to preserve the full range of natural variability.

### Feature Preparation

**Numeric Features - Standardization:**  
All numeric features (Age, Sleep Duration, Stress Level, Daily Screen Time, Caffeine Intake) were standardized to have mean=0 and standard deviation=1. This ensures:
- Features with larger numeric ranges don't dominate the model
- Fair comparison of feature importance values
- Improved model training efficiency

**Categorical Features - One-Hot Encoding:**  
The three categorical features were converted to binary indicators:
- Gender (3 categories) → 2 binary features
- Diet Type (3 categories) → 2 binary features  
- Exercise Frequency (3 categories) → 2 binary features

Using "drop first" encoding, one category per variable serves as the reference baseline, avoiding redundancy while preserving all information. This prevents multicollinearity issues in the model.

**Final Feature Count:**  
The preprocessing transformed 8 original predictors into **11 processed features** (5 numeric + 6 categorical binary).

### Train-Test Split

The dataset was divided using standard machine learning practice:
- **Training Set:** 64,000 samples (80%) for model learning
- **Testing Set:** 16,000 samples (20%) for unbiased performance evaluation
- **Random State:** Fixed at 42 to ensure reproducible results

This split balances having enough data for training while reserving sufficient samples to validate the model generalizes to new, unseen data.

---

## 5. Modeling Approach

### Model Selection Strategy

Two regression algorithms were implemented with increasing sophistication:

**Step 1: Baseline Model (Linear Regression)**  
Started with Linear Regression to:
- Establish performance benchmark
- Understand linear relationships in the data
- Provide comparison point for more complex models

**Results:** R² ≈ 0.05, indicating linear relationships alone cannot capture the complexity of cognitive performance prediction.

**Step 2: Advanced Model (Random Forest Regressor)**  
Implemented Random Forest because it:
- Captures non-linear relationships between lifestyle factors
- Provides clear feature importance rankings (directly answers our research question)
- Resists overfitting through ensemble of multiple decision trees
- Handles interactions between features automatically

**Initial Results:** Default Random Forest achieved R² ≈ 0.98, dramatically outperforming the baseline.

### Hyperparameter Optimization

To maximize model performance, systematic hyperparameter tuning was performed using GridSearchCV with 3-fold cross-validation.

**Parameters Tested:**
- Number of trees: 100 vs. 200
- Maximum tree depth: 10, 20, or unlimited
- Minimum samples to split a node: 2 vs. 5
- Minimum samples in leaf nodes: 1 vs. 2

**Optimization Process:**  
The grid search tested 24 different parameter combinations, using R² score as the optimization metric. The best configuration balanced model complexity with generalization ability.

**Final Model:**  
The optimized Random Forest achieved R² ≈ 0.98 on the test set, with minimal overfitting (training and testing scores nearly identical).

---

## 6. Model Evaluation and Results

### Evaluation Metrics Used

**R² Score (Coefficient of Determination):**  
Primary metric measuring the proportion of variance in cognitive scores explained by the model. Values range from 0 to 1, with 1 being perfect prediction. Our model achieved **R² = 0.98**, meaning it explains 98% of the variance in cognitive performance.

**RMSE (Root Mean Squared Error):**  
Measures average prediction error in the same units as cognitive scores (points). Final model RMSE ≈ 2.4 points, meaning predictions are typically within 2-3 points of actual scores.

**MAE (Mean Absolute Error):**  
Average absolute difference between predicted and actual scores. Final model MAE ≈ 1.45 points, providing intuitive interpretation of typical prediction error.

### Model Comparison Results

| Model | Test R² | Test RMSE | Test MAE | Interpretation |
|-------|---------|-----------|----------|----------------|
| Linear Regression | 0.05 | 19.0 | 15.0 | Poor - cannot capture complexity |
| Random Forest (Default) | 0.98 | 2.5 | 1.5 | Excellent performance |
| Random Forest (Optimized) | 0.98 | 2.4 | 1.45 | Best - slight improvement |

### Why Random Forest Was Selected

The optimized Random Forest was selected as the final model because:

1. **Exceptional Accuracy:** Explains 98% of variance in cognitive scores
2. **Strong Generalization:** Nearly identical performance on training and testing data (no overfitting)
3. **Interpretability:** Provides clear feature importance rankings
4. **Practical Value:** Prediction errors of ~2.4 points are acceptable for organizational decision-making

The dramatic improvement over Linear Regression (0.05 → 0.98 R²) confirms that lifestyle factors have complex, non-linear relationships with cognitive performance.

### Feature Importance Rankings - Answering the Research Question

**Which lifestyle factors most strongly predict cognitive performance?**

The Random Forest model ranked factors by predictive importance:

**Top Predictors (Highest Impact):**
1. **Stress Level** - Most important predictor, strong negative correlation (-0.228)
2. **Exercise Frequency (High vs. Low)** - Substantial impact: 14.21 point difference in mean cognitive scores
3. **Sleep Duration** - Measurable positive influence on performance
4. **Daily Screen Time** - Moderate predictive power
5. **Age** - Smaller but significant effect

**Low Impact Predictors:**
- **Gender** - Maximum difference of only 0.34 points (negligible)
- **Diet Type** - Maximum difference of only 0.34 points (negligible)
- **Caffeine Intake** - Minimal predictive power

### Key Findings

**1. Stress Management is Critical:**  
Stress level emerged as the single strongest predictor with a negative correlation of -0.228. Higher stress consistently correlates with lower cognitive performance, validating intuitions about stress's detrimental effects on mental function.

**2. Exercise Shows Dramatic Impact:**  
Individuals with high exercise frequency score an average of 14.21 points higher than those with low exercise frequency. This substantial gap demonstrates that regular physical activity is not just correlated with, but potentially causal to, improved cognitive performance.

**3. Demographics Have Minimal Effect:**  
Gender and diet type showed negligible predictive power (0.34 point difference), suggesting these factors have minimal direct impact on cognitive scores in this population. This is important for resource allocation - organizations should not over-invest in demographic-specific or diet-specific programs.

**4. The Model is Highly Reliable:**  
With R² = 0.98, the model demonstrates that cognitive performance is highly predictable from measurable lifestyle choices. This validates that organizations have actionable levers for improvement.

---

## Conclusions and Recommendations

### Summary of Findings

This capstone project successfully identified which lifestyle factors most strongly predict human cognitive performance. Through machine learning analysis of 80,000 samples, we can conclusively answer the research question:

**Stress Level and Exercise Frequency are the dominant predictors of cognitive performance, with quantifiable, substantial impacts that organizations can leverage for targeted interventions.**

The optimized Random Forest model achieved exceptional accuracy (R² = 0.98), demonstrating that cognitive performance is highly predictable from lifestyle choices alone.

### Actionable Recommendations

#### For Organizations and Employers

**HIGH-PRIORITY ACTIONS (Proven High Impact):**

1. **Implement Comprehensive Stress Management Programs**
   - Offer mindfulness and meditation training
   - Provide access to mental health counseling and therapy
   - Create flexible work arrangements to reduce work-life stress
   - Train managers in stress-reduction leadership techniques
   - **Expected Impact:** Stress is the #1 predictor - this is the highest-ROI investment

2. **Establish Exercise Promotion Initiatives**
   - Subsidize gym memberships or on-site fitness facilities
   - Offer fitness classes during work hours
   - Implement "active break" policies (walking meetings, stretch breaks)
   - Create exercise challenges with incentives
   - **Expected Impact:** 14+ point improvement in cognitive scores between high/low exercise groups

3. **Support Healthy Sleep Schedules**
   - Discourage after-hours communications
   - Offer flexible start times
   - Educate employees on sleep hygiene
   - **Expected Impact:** Measurable positive correlation with performance

4. **Manage Screen Time Exposure**
   - Implement mandatory breaks from screens
   - Provide ergonomic workstation setups
   - Encourage screen-free meetings when appropriate
   - **Expected Impact:** Moderate but actionable improvement

**LOW-PRIORITY ACTIONS (Minimal Impact):**
- Gender-specific programs (0.34 point difference - not worth heavy investment)
- Specific diet programs (0.34 point difference - minimal ROI)

#### For Educators and Academic Institutions

1. **Minimize Student Stress**
   - Design balanced curricula with reasonable workloads
   - Provide adequate preparation time before major assessments
   - Offer stress management workshops and counseling services

2. **Integrate Physical Activity**
   - Incorporate movement into lessons (active learning methods)
   - Ensure adequate PE class time
   - Provide "brain breaks" between intensive academic sessions

3. **Educate About Lifestyle-Performance Relationships**
   - Share this research with students to motivate healthy choices
   - Integrate wellness education into curriculum

#### For Individuals

**Your Personal Action Plan:**

1. **Prioritize Stress Reduction** (Most Important)
   - Practice daily meditation or mindfulness (even 10 minutes helps)
   - Seek therapy or counseling if experiencing chronic stress
   - Improve time management to reduce deadline pressure
   - Set clear work-life boundaries

2. **Maintain Regular Exercise** (Dramatic Benefits)
   - Aim for minimum 3-4 exercise sessions per week
   - Choose activities you enjoy to ensure consistency
   - Even moderate activity (walking, yoga) shows benefits

3. **Ensure Adequate Sleep**
   - Target 7-9 hours per night consistently
   - Establish regular sleep schedule
   - Create sleep-friendly environment (dark, cool, quiet)

4. **Manage Screen Time**
   - Take 5-minute breaks every hour from screens
   - Implement screen-free periods (especially before bed)
   - Use blue light filters in evening

### Limitations and Considerations

**Cross-Sectional Data:**  
This analysis uses data from a single time point, which establishes correlation but not definitive causation. While the relationships are strong, longitudinal studies would be needed to confirm causal mechanisms over time.

**Generalizability:**  
The dataset represents a specific population sample. Results should be validated across different demographic groups, cultures, and occupational contexts before universal application.

**Unmeasured Factors:**  
Additional lifestyle factors not captured in this dataset (such as social connection quality, sense of purpose, nutrition quality beyond diet type) may also influence cognitive performance.

**Individual Variation:**  
While the model predicts population trends accurately, individual responses to interventions may vary. Personalized approaches may be needed for optimal results.

### Next Steps and Future Research

**For This Project:**
1. Test the model with new data to confirm generalizability
2. Conduct cost-benefit analysis to quantify ROI of recommended interventions
3. Develop personalized recommendation system based on individual profiles

**For Future Research:**
1. **Longitudinal Studies:** Track individuals over time to establish causal relationships
2. **Intervention Trials:** Conduct randomized controlled trials testing specific programs (e.g., 12-week stress reduction program)
3. **Interaction Analysis:** Investigate how factors combine (Does exercise mitigate stress effects? Is there an optimal sleep-exercise combination?)
4. **Expanded Cognitive Metrics:** Include specific cognitive domains (memory, attention, processing speed) rather than single composite score
5. **Deep Learning Approaches:** Explore neural networks to potentially capture even more complex patterns
6. **Demographic-Specific Models:** Build separate models for different populations to identify if predictors vary by age group or occupation

### Final Conclusion

This project demonstrates that cognitive performance is highly predictable from measurable lifestyle factors, with stress management and exercise promotion emerging as the most impactful intervention targets. Organizations that implement data-driven wellness programs focused on these high-impact factors can expect measurable improvements in cognitive performance across their populations.

The exceptional model performance (R² = 0.98) validates that lifestyle optimization is a powerful, actionable strategy for enhancing human cognitive capability. By focusing resources on factors with quantified, substantial effects—and avoiding overinvestment in low-impact factors—organizations can maximize return on investment while supporting both individual wellbeing and organizational performance goals.

Most importantly, these findings are immediately actionable. Every individual and organization can begin implementing stress reduction and exercise programs today, with confidence that these interventions will yield measurable cognitive benefits backed by data-driven evidence.

---

## Technical Details

### Repository Contents

- **`Capstone_Final_Notebook.ipynb`** - Complete technical analysis with code, visualizations, and detailed methodology
- **`README.md`** - This non-technical report
- **`human_cognitive_performance.csv`** - Source dataset (80,000 samples)

### How to Run the Analysis

1. Ensure Python 3.7+ is installed with required libraries:
   - pandas, numpy, matplotlib, seaborn, scikit-learn

2. Place the dataset file in the same directory as the notebook

3. Run all cells in `Capstone_Final_Notebook.ipynb` sequentially

4. The notebook is fully self-contained and reproducible (random_state=42)

### Model Specifications

- **Algorithm:** Random Forest Regressor (scikit-learn)
- **Hyperparameters:** Optimized via GridSearchCV with 3-fold cross-validation
- **Features:** 11 (5 numeric + 6 one-hot encoded categorical)
- **Training Samples:** 64,000
- **Testing Samples:** 16,000
- **Performance:** R² = 0.98, RMSE = 2.4, MAE = 1.45

---

## Contact

**Michael Viet Nguyen**  
UC Berkeley Machine Learning & AI Professional Certificate Program  
Capstone Project

---

## Acknowledgments

- **Dataset:** Samharison (Kaggle) - "Human Cognitive Performance Analysis: Lifestyle & AI Predictions"
- **Program:** UC Berkeley Machine Learning & AI Certificate
