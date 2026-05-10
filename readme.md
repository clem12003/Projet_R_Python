# Impaired quality of life after intensive care

# 1. Scientific problem 
## 1.1. Context

Advances in intensive care medicine have significantly reduced ICU mortality over recent decades, leading to a growing population of ICU survivors with persistent physical, psychological, and cognitive impairments after discharge (1, 2). These long-term consequences, commonly grouped under the term Post-Intensive Care Syndrome (PICS), may substantially alter patients’ health-related quality of life (HRQoL) (3).

According to the World Health Organization (WHO), quality of life refers to an individual’s perception of their position in life within the cultural and social context in which they live (4). In the medical field, HRQoL is considered a multidimensional concept reflecting the influence of health status and healthcare on physical, psychological, and social dimensions of health (5). Previous studies have shown that ICU survivors often report lower HRQoL scores than the general population, with only partial recovery over time (6, 7).


## 1.2. Aim 

The aim of this study is to evaluate the quality of life of ICU survivors at 3 and 12 months after discharge, using the SF-36 questionnaire. Specifically, it seeks to assess changes over time in the different dimensions of quality of life, including physical and mental components, in order to better understand recovery trajectories following critical illness.

## 1.3. Method

All ICU survivors were contacted by mail 3 and 12 month after hospital discharge and were asked to complete the SF-36 questionnaire.

### Outcome measure (8, 9)

Quality of life was assesed using the SF-36 questionnaire. This questionnaire evaluate multiple dimensions of quality of life including : Physical Functionning (PF), Role Physical (RP), Bodily Pain (BP), General Health (GH), Vitality (VT), Social Functioning (SF), Role Emotional (RE), Mental Health (MH). 
Then, this dimensions are grouped into two components, the Physical Component Summary (PCS), including PF, RP, BP and GH, and the Mental Component Summary (MCS), including VT, SF, RE and MH.

SF-36 domains were scored according to standard procedures. Scores of each dimension were first computed by summing the values of all items belonging to that dimension and were then linearly transformed to a 0–100 scale. Higher scores indicate better heath status.

The Physical Component Summary (PCS) and Mental Component Summary (MCS) were then calculated using the dimensions scores. Then they were standardized unsing French reference population norms.

Detailed information on SF-36 scoring procedures, including item mapping, score transformation, and computation of PCS and MCS, is provided in the `SF-36 appendix.md`.

### Participants

479 patients who survived ICU and responded to the SF-36 at both 3 and 12 months were included in the study.

The dataset used in this repository is simulated and contains 30 fictitious observations created for demonstration and reproducibility purposes. The methodological description reflects the original study design, but the data do not correspond to real patients.

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
### 2.3.1. Recoding of SF-36 item scores
**Aim**: To recode the SF-36 item responses so that higher scores correspond to a better health status accross all items.  
**Input**: `bazRSF.csv` in `data` folder  
**Output**: A set of SF-36 item scores in which higher values indicate better perceived health status.

### 2.3.2. Calculation and transformation of dimension scores at 3 and 12 months
**Aim**: To compute dimension scores and transform them onto a 0-100 scale for comparability and interpretation  
**Input**: `bazRSF.csv` in `data` folder  
**Calculation**:   
Before computing dimension scores, we perform mean imputation at the dimension level. If at least 50% of items within a dimension are available, missing values are replaced by the mean of the observed items in that dimension. If fewer than 50% of items are present, the dimension score is left as `NA`.  

Then, raw scores for each dimension are computed by summing the values of all items belonging to that dimension.  
Scores are then linearly transformed to a 0–100 scale using the following formula:  

$$
\text{Transformed score} = \frac{\text{Observed score} - \text{Minimum possible score}}{\text{Maximum possible score} - \text{Minimum possible score}} \times 100
$$

In this transformed scale, 0 represents the worst possible health status and 100 represents the best possible health status.  
**Output**: A normalized score for each dimension, ranging between 0 and 100. Exported as `bazP_scores.csv` in the `results` folder  

### 2.3.3. Visualization of the evolution of dimension scores between 3 and 12 months with a radar plot
**Aim**: To visually compare dimension scores between 3 and 12 months, and assess if changes over time is statistically significant, using a radar plot  
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

The reference values from the French general population are provided in the `SF-36 appendix.md` as well as the details of PCS and MCS calculation  
**Output**: A summary score for physical (PCS) and mental (MCS) health status at both time point 

### 3.3.2. Visualization of the distribution of PCS and MCS at 3 and 12 months
**Aim**: To compare the distribution beween PCS and MCS between 3 and 12 months using boxplots to visualize changes over time  
**Input**: `bazP_scores.csv` in `data` folder  
**Output**: Boxplots displaying the distribution of PCS and MCS scores at 3 and 12 months, allowing visual comparison of changes over time  

## 3.4. Conclusion

This workflow provides a structured approach to analyzing longitudinal changes in health-related quality of life after intensive care. It can be used as a reproducible framework for SF-36 data processing, visualization, and statistical comparison over time.

## Tools

Tools such as Claude and Chatgpt were used as methodological and programming support, particularly for debugging and code clarification.  

## 4. References
1. Lilly CM, Swami S, Liu X, Riker RR, Badawi O. Five-Year Trends of Critical Care Practice and Outcomes. Chest. oct 2017;152(4):723‑35. doi:10.1016/j.chest.2017.06.050

2. Geense WW, Zegers M, Peters MAA, Ewalds E, Simons KS, Vermeulen H, et al. New Physical, Mental, and Cognitive Problems 1 Year after ICU Admission: A Prospective Multicenter Study. Am J Respir Crit Care Med. 15 juin 2021;203(12):1512‑21. doi:10.1164/rccm.202009-3381OC

3. Mikkelsen ME, Still M, Anderson BJ, Bienvenu OJ, Brodsky MB, Brummel N, et al. Society of Critical Care Medicine’s International Consensus Conference on Prediction and Identification of Long-Term Impairments After Critical Illness. Crit Care Med. nov 2020;48(11):1670‑9. doi:10.1097/CCM.0000000000004586

4. World Health Organisation. « Introducing the WHOQOL instruments » WHOQOL:Measuring Quality of Life.

5. de Wit M, Hajos T. Health-Related Quality of Life. In: Gellman M, Turner J, éditeurs.
Encyclopedia of Behavioral Medicine. Springer. New York (NY); 2013. https://link.springer.com/rwe/10.1007/978-1-4419-1005-9_753#citeas

6. Oeyen SG, Vandijck DM, Benoit DD, Annemans L, Decruyenaere JM. Quality of life after intensive care: A systematic review of the literature: Crit Care Med. déc 2010;38(12):2386‑400. doi:10.1097/CCM.0b013e3181f3dec5

7. Cuthbertson BH, Roughton S, Jenkinson D, MacLennan G, Vale L. Quality of life in the five years after intensive care: a cohort study. Crit Care. 20 janv 2010;14(1):R6. doi:10.1186/cc8848

8. Ware JE Jr, Sherbourne CD. The MOS 36-ltem Short-Form Health Survey (SF-36) I. Conceptual Framework and Item Selection. Med Care. 1992;30(6):473‑83.
doi:10.1097/00005650-199206000-00002

9. Ware JE, Kosinski M, Keller SD. SF-36 Physical and Mental Health Summary Scales: A User’s Manual. Health Assessment Lab. Boston, MA; 1994.