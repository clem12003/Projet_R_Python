# Appendix

This appendix provides additional methodological details regarding the SF-36 questionnaire. It includes the mapping of SF-36 items to their respectives dimensions, dimensions transformation procedures, and the calculation of the physical and mental component (PCS and MCS).

## SF-36 mapping
The 36 item of the questionnaire then form 8 dimensions.

|          Dimension        | Items corresponding |
|:-------------------------:|:-------------------:|
| Physical Functioning (PF) |       3a to 3i      |
| Role Physical (RP)        |       4a to 4d      |
| Bodily Pain (BP)          |       7 and 8       |
| General Health (GH)       |    1, 11a to 11d    |
| Vitality (VT)             |    9a, 9e, 9g, 9i   |
| Social Functioning (SF)   |       6 and 10      |
| Role Emotional (RE)       |       5a to 5c      |
| Mental Health (MH)        | 9b, 9c, 9d, 9f, 9h  |
| Health Transition(HT)     |          2          |

Physical Functioning (PF): item 3a, 3b, 3c, 3d, 3e, 3f, 3g, 3h, 3i  
Role Physical (RP): item 4a, 4b, 4c, 4d  
Bodily Pain (BP): item 7, 8  
General Health (GH): item 1, 11a, 11b, 11c, 11d  
Vitality (VT): item 9a, 9e, 9g, 9i  
Social Functioning (SF): item 6, 10  
Role Emotional (RE): item 5a, 5b, 5c  
Mental Health (MH): item 9b, 9c, 9d, 9f, 9h  
Health Transition(HT): item 2  

## Dimensions transformation procedure

All the dimensions are normalized to have a score between 0 and 100 using this formula:

$$
\text{Transformed score} = \frac{\text{Observed score} - \text{Minimum possible score}}{\text{Maximum possible score} - \text{Minimum possible score}} \times 100
$$

Here are the minimum and maximal posible scores for each dimension.

|          Dimension        |     Minimum posible score    |     Maximum posible score     |
|:-------------------------:|:----------------------------:|:-----------------------------:|
| Physical Functioning (PF) |              10              |              30               |
| Role Physical (RP)        |              4               |              8                |
| Bodily Pain (BP)          |              2               |              12               |
| General Health (GH)       |              5               |              25               |
| Vitality (VT)             |              4               |              24               |
| Social Functioning (SF)   |              2               |              10               |
| Role Emotional (RE)       |              3               |              6                |
| Mental Health (MH)        |              5               |              30               |
| Health Transition (HT)    |              1               |              5                |


## Calculation of the physical and mental components (PCS and MCS)

The SF-36 domain scores were then standardized into z-scores using reference values from the French general population in order to compute the Physical Component Summary (PCS) and Mental Component Summary (MCS).


$$
Z = \frac{\text{Observed dimension score} - \text{Mean of the French general population}}{\text{Standard deviation of the French general population}}
$$

### French general population norms for each dimension (INSEE 2002-2003):

|          Dimension        |     French norms    |
|:-------------------------:|:-------------------:|
| Physical Functioning (PF) |     85.3 ± 22.3     |
| Role Physical (RP)        | 82.2 ± 32.2         |
| Bodily Pain (BP)          | 73.0 ± 24.6         |
| General Health (GH)       | 67.8 ± 18.9         |
| Vitality (VT)             | 57.4 ± 18.0         |
| Social Functioning (SF)   | 80.9 ± 21.2         |
| Role Emotional (RE)       | 82.0 ± 32.9         |
| Mental Health (MH)        | 66.7 ± 17.7         |


### PCS and MCS computation

The Physical and Mental Component Summary scores were calculated using a weighted linear combination of standardized SF-36 domain scores. The coefficients correspond to empirically derived weights from the SF-36 scoring system, reflecting the contribution of each domain to overall health status, with scores standardized to a mean of 50 and SD of 10.  

$$
\text{PCS} = \left[
(PF_z \times 0.42402) + (RP_z \times 0.31754) + (BP_z \times 0.31754) + (GH_z \times 0.24954) + (VT_z \times 0.02877) + (SF_z \times -0.00753) + (RE_z \times -0.19206) + (MH_z \times -0.2069) \right] \times 10 + 50
$$


$$
\text{MCS} = \left[
(PF_z \times -0.22999) + (RP_z \times -0.12329) + (BP_z \times -0.09731) + (GH_z \times -0.01571) + (VT_z \times 0.23534) + (SF_z \times 0.26876) + (RE_z \times 0.43407) + (MH_z \times 0.48581)\right] \times 10 + 50
$$

