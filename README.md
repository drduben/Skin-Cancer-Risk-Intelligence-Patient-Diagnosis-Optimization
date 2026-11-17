Skin Cancer Risk Intelligence & Patient Diagnosis Optimization

A healthcare data analytics case study using PostgreSQL Dermalife Oncology & Research Institute (DORI) | 10Alytics Data Analytics Capstone

Overview

DORI has seen a rise in late-stage skin cancer diagnoses but had no structured way to identify which patients, body regions, symptoms and risk factors matter most. As the Healthcare Data Analyst Consultant, I used SQL to analyse 1,088 patient and lesion records and turn the results into screening and prevention recommendations.

Business questions

The analysis answers 20 questions across four areas:

Area	Focus
1. Patient demographic risk	Age, gender, body region, prior skin cancer history
2. Lesion growth and diagnosis	Diagnosis mix, growth, symptoms, biopsies, lesion size
3. Environmental healthcare	Cases and biopsies by region, access to piped water and sewage
4. Lifestyle and behavioural risk	Smoking, alcohol, pesticide exposure
Data

Two PostgreSQL tables linked by patient_id:

table1 (patients): age, gender, smoking, alcohol, pesticide exposure, ancestry, cancer history, sanitation access.
table2 (lesions): body region, diameters, symptoms (itch, grew, hurt, changed, bleed, elevation), biopsy flag and final diagnosis.

Both tables hold 1,088 rows and 1,088 distinct patients, so each patient has exactly one lesion and joins do not inflate counts. The dataset was supplied for the 10Alytics capstone and is not redistributed in this repository.

Definition used: malignant = BCC, SCC or MEL (346 lesions, 31.8%). ACK (pre-cancerous), NEV and SEK are non-malignant. All 346 malignant lesions were biopsy-confirmed.

Approach
Checked the data first: row counts, distinct patients, category values, and NULLs in every flag column (none found).
Wrote one query per question, plus supporting queries that convert raw counts into rates so groups of different sizes can be compared fairly.
Reconciled every result back to control totals (1,088 patients; 346 malignant cases).
Reported group sizes next to percentages and avoided causal claims.

SQL techniques: joins, GROUP BY, CASE expressions, CTEs, window functions (SUM() OVER), conditional aggregation with FILTER, UNION ALL, subqueries, NULLIF and numeric casting.

Key findings
Age: malignancy rises from 5.3% (ages 18-29) to 40.7% (70+). 85% of cancers (295 of 346) are in patients aged 50+.
Gender: men have more cases (189 vs 157), but women have the higher rate (43.4% vs 26.0%).
Prior history: 224 patients (20.6%) have had skin cancer; 70.1% of them have a malignant diagnosis now, vs 21.9% of the rest.
Body region: the face has the most cancers (102). The nose has the highest risk (69.1%), then the neck (54.1%) and ear (53.1%).
Warning signs: bleeding (52.0% of cancers vs 5.7% of non-cancers) and pain (37.0% vs 3.1%) are the most specific. Growth (74.9% vs 33.8%) and elevation (82.7% vs 43.8%) catch more cancers but flag more benign lesions.
Size: mean diameter is 10.0-14.1 for malignant types vs 0.7-2.6 for the rest; melanoma is the largest.
Lifestyle and exposure: pesticide exposure (+48.0 points), smoking (+46.7) and alcohol (+44.9) are each strongly associated with malignancy. Smokers and drinkers together reach 82.1% (23 of 28), though that group is small. Still, 65% of cancers occurred in patients who neither smoke nor drink.
Sanitation: 71.9% of patients lack piped water and 74.9% lack sewage, but they had a lower malignancy rate (about 19-22% vs about 62-64%). This runs against the initial hypothesis and was not adjusted for age or occupation.
Recommendations
Prioritise screening for patients aged 50+ and those with prior skin cancer history.
Fast-track lesions on the nose, ear and neck; urgent referral for bleeding or painful lesions.
Use growth, elevation and size as a triage prompt to reduce non-cancer biopsies (112 of 458 biopsies, about 1 in 4).
Target prevention at pesticide-exposed workers, with smoking and alcohol counselling.
Record lesion onset dates, and test age and occupation before any sanitation programme.
Limitations

Findings are associations from one clinic cohort, not proof of cause. Some groups are small (smokers n=62; smoke-and-drink n=28). The data has no dates, so diagnostic delay could not be measured.

Repository contents
File	Description

README.md	This file

Author

Njabulo Dube | Data Analyst LinkedIn: www.linkedin.com/in/njabulo-d-b38a22148| GitHub:https://github.com/drduben
