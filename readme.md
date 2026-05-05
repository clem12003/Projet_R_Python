# Impaired quality of life after intensive care

# 1. Scientific problem 
## 1.1. Context

Admission to an intensive care unit (ICU) is often associated with severe, life-threatening conditions requiring advanced medical support. While improvements in critical care have increased survival rates, many patients experience long-term consequences after discharge. These sequelae are commonly grouped under the term post-intensive care syndrome (PICS), which can significantly impact patients’ daily functioning and overall well-being.

Quality of life (QoL) has therefore become a key outcome in the follow-up of ICU survivors. It is frequently assessed using standardized and validated tools such as the SF-36 (Short Form 36 Health Survey), which evaluates multiple dimensions including physical functioning, mental health, and social participation. Studies have shown that QoL is often impaired after ICU discharge, particularly in the first months, with variable recovery trajectories over time.

Assessing QoL at different time points, such as 3 and 12 months after ICU discharge, allows for a better understanding of recovery patterns and the persistence of impairments. It also helps identify patients at risk of long-term disability and informs post-ICU care strategies.

What we are looking for: Evaluate the Qol of ICU survivors at 3 and 12 months after discharge using the SF-36, and analyze its evolution over time.

## 1.2. Aim

The aim of this study is to evaluate the quality of life of ICU survivors at 3 and 12 months after discharge, using the SF-36 questionnaire. Specifically, it seeks to assess changes over time in the different dimensions of quality of life, including physical and mental components, in order to better understand recovery trajectories following critical illness.

## 1.3. Method

All ICU survivors were contacted by mail 3 and 12 month after hospital discharge and were asked to complete the SF-36 questionnaire.

### Outcome measure

Quality of life was assesed using the SF-36 questionnaire. This questionnaire evaluate multiple dimensions of quality of life including : Physical Functionning (PF), Role Physical (RP), Bodily Pain (BP), General Health (GH), Vitality (VT), Social Functioning (SF), Role Emotional (RE), Mental Health (MH). 
Then, this dimensions are grouped into two components, the Physical Component Summary (PCS), including PF, RP, BP and GH, and the Mental Component Summary (MCS), including VT, SF, RE and MH.

SF-36 domains were scored according to standard procedures. Scores of each dimension were first computed by summing the values of all items belonging to that dimension and were then linearly transformed to a 0–100 scale. Higher scores indicate better heath status.

The Physical Component Summary (PCS) and Mental Component Summary (MCS) were then calculated using the dimensions scores. Then they were standardized unsing French reference population norms, with a mean of 50 and a standard deviation of 10.

Detailed information on SF-36 scoring procedures, including item mapping, score transformation, and computation of PCS and MCS, is provided in the `SF-36 appendix.md`.

### Participants

479 patients who survived ICU and responded to the SF-36 at both 3 and 12 months were included in the study.

# 2. RStudio project
## 2.1. Aim

The aim of this project is to assess SF-36 dimension scores at 3 and 12 months after ICU discharge. In addition, a radar chart will be generated to visualize changes in quality of life dimensions over time.

## 2.2. Data organization
File: `bazRSF.csv`  
Colums:  
`ID`: Patient ID, corresponding to their number of inclusion  
`SF_3m_Q[y]`: SF-36 score at 3 months for question y (where y is the question number e.g. 1, 2, 3a, ...)   
`SF_12m_Q[y]`: SF-36 score at 12 months for question y (where y is the question number e.g. 1, 2, 3a, ...)  

## 2.3. Script organization
### 2.3.1 Calculation and transformation of dimension scores at 3 and 12 months
**Aim**: To compute dimension scores and transform them onto a 0-100 scale for comparability and interpretation  
**Input**: `bazRSF.csv` in `data` folder  
**Calculation**:   
Raw scores for each dimension are first computed by summing the values of all items belonging to that dimension.  
Scores are then linearly transformed to a 0–100 scale using the following formula:  

$$
\text{Transformed score} = \frac{\text{Observed score} - \text{Minimum possible score}}{\text{Maximum possible score} - \text{Minimum possible score}} \times 100
$$

In this transformed scale, 0 represents the worst possible health status and 100 represents the best possible health status.  
**Output**: A standardized score for each dimension, ranging between 0 and 100  

### 2.3.2 Visualization of the evolution of dimension scores between 3 and 12 months
**Aim**: To visually compare dimension scores between 3 and 12 months, and assess if changes over time is statistically significant  
**Input**: `bazRSF.csv` in `data` folder  
**Output**: A radar plot comparing dimension scores at 3 and 12 months with p-values indicating whether changes over time reflect a significant improvement or not  

# 3. Python Project
## 3.1. Aim
To compute Physical Component Summary (PCS) and Mental Component Summary (MCS) scores and compare their distribution at 3 and 12 months using boxplots to assess changes over time.  

## 3.2. Data organization
File: `bazP_scores.csv`  
Colums:  
`ID`: Patient ID, corresponding to their number of inclusion  
`SF_3m_Q[x]`: SF-36 score at 3 months for question y (where x is the question number e.g. 1, 2, 3a, ...)   
`SF_12m_Q[x]`: SF-36 score at 12 months for question y (where x is the question number e.g. 1, 2, 3a, ...)   
`[y]transformed_3m`: Transformed SF-36 dimension scores at 3 months (where y is the name of the dimension, e.g. PF, RP, BP, ...)   
`[y]transformed_12m`: Transformed SF-36 dimension scores at 12 months (where y is the name of the dimension, e.g. PF, RP, BP, ...)  

## 3.3. Script organization
### 3.3.1. Calculation of the Physical and Mental Component Summay (PCS and MCS)
**Aim**: To compute summary scores representing overall physical (PCS) and mental (MCS) health status from SF-36 dimensions
**Input**: `bazP_scores.csv` in `data` folder  
**Calculation**:
Each SF-36 dimension score is first standardized into a z-score using the reference values of the French population :
$$
Z = \frac{\text{Observed dimension score} - \text{Mean of the French general population}}{\text{Standard deviation of the French general population}}
$$

PCS and MCS are then computed as weighted linear combinations of these standardized dimension scores using the respective scoring coefficients.

**Output**: A summary score for physical (PCS) and mental (MCS) health status at both time point 




