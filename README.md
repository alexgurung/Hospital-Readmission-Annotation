Hospital Readmission Annotation Dataset
1. Dataset Description
•	Source: Diabetes 130-US Hospitals (UCI/Kaggle), de-identified
•	Subset: 200 selected encounters
•	Goal: Annotate binary readmission within 30 days (YES/NO)
Dataset Link: Google Drive
________________________________________
2. Label Definitions
•	YES = Readmitted within 30 days
•	NO = Not readmitted within 30 days
Full rules, examples, and edge cases are in Hospital Readmission Data Annotation Guidelines section.
________________________________________
3. Annotation Interface
Tool: Spreadsheet (Excel / Google Sheets)
•	Open annotation_template.csv
•	Fill the annotated_label column with YES or NO
•	Save as annotations_completed.csv
Full step-by-step instructions are in Annotation_Instructions.pdf.
________________________________________
4. License
•	Original data: Public domain (UCI)
•	Our annotation content: © 2025–2026 Alex Gurung, Chandra Kala Rai, University of Michigan–Flint
This dataset and annotation materials may be used for educational and research purposes only.
See LICENSE.txt for full details.
 
Hospital Readmission Data Annotation Guidelines
1. Overview of Annotation Task
You will be reviewing patient hospital visit records to ensure data quality and validate key information that will be used to predict 30-day hospital readmissions. 
Your tasks:
•	Review patient records for data quality issues
•	Assign YES / NO for 30-day readmission
•	Assess comorbidity severity based on diagnosis codes
•	Flag records that contain ambiguous or potentially erroneous information
Time Estimate: Each record should take approximately 2-3 minutes to annotate.
No medical expertise required: You will be working with coded data and clear decision rules. 
2. Label Set and Descriptions
For each patient hospital encounter, you will assign one label indicating whether the patient was readmitted within 30 days after discharge. This is based on the “readmitted” field in the dataset.
Label 1 - YES (Readmitted Within 30 Days)
Assign this label when the patient returned to the hospital within 30 days of discharge.
•	Look for the value “<30” in the original dataset’s “readmitted” field.
•	Any explicit record showing readmission within 30 days counts as YES.
Label 2 - NO (Not Readmitted Within 30 Days)
Assign this label when the patient was not readmitted within 30 days.
•	Original value “NO” → no readmission
•	Original value “>30” → readmission occurred after 30 days
 
3. Annotation Rules and Criteria
Use the following rules to assign labels. These are heuristic-based (not causal) and reflect patterns observed in hospital readmission literature.

Key Risk Factors (ordered by typical strength):

A. Prior Utilization (number of prior inpatient admissions in the past year)
Value 	Risk
0	Low	First admission in past year
1	Low-Moderate	One prior admission
2	Moderate-High	Multiple prior admission suggest ongoing instability
Interpretation: Patients with recent hospitalizations are more likely to need readmission because they have active or recurring health issues.

 B. Length of Hospital Stay (time_in_hospital, in days)
Value	Risk Level
1-3 days	Low	Brief, routine admission
4-6 days	Moderate	Standard medicical stay
>= 7 days	Moderate-High	Prolonged stay suggests complexity, slower recovery, or complications
Interpretation: Longer stays often indicate more severe illness or slower discharge preparation, both increasing readmission risk.

C. Number of Diagnoses During This Admission
Diagnoses	Risk
<=3	Low	Focused, likely single-system problem
4-6	Moderate	Multiple issues, more complex care
>=7	High 	Severe comorbidity burden increases risk
Interpretation: Patients with many concurrent diagnoses are managing multiple conditions and are at higher readmission risk.
D. Admission Type
Value	Risk
1	Moderate-High	Urgent/umplanned admission
2	Moderate	Urgent but perhaps partially planned
>=3	Low	Planned, stable, controlled admission
Interpretation: Emergency admissions indicate acute decompensation and 3 and above are elective admissions are for planned procedures or controlled issues.

E. Diabetes Medication Prescribed & Change During Stay
Insulin Meds	Risk
No/Down	Low	Patient may not have diabetes, medication reduced suggests improvement
Steady	Moderate	Medication stabe, no acute changes
Up	High	Medication increased, indicates worsening control 
Interpretation: Medication increases suggest worsening disease; stable medication suggests consistent management.

Overall Labeling Algorithm
Step 1: Count the number of "strong risk factors" present in each encounter:

A strong risk factor is one of:
- Prior inpatient admissions ≥ 2
- Length of stay ≥ 7 days
- Number of diagnoses ≥ 7
- Admission type = 1 (Emergency)
- Diabetes medication Up

Step 2: Apply the rule:
Strong Factors	Label	Rationale
>=2	Yes	Multiple risk factors suggest complex case needing close follow-up
0-1	No	Few risk factor, stable presentation, loe readmission risk

 4. Examples

Example 1: Clear YES (Multiple Strong Factors)
Encounter ID: 266753892
Field	Values	Risk Assessment
Age	40-50	Moderate
Time in hospital	5	Moderate
No of inpatients	0	Low
No of diagnoses	9	High
Admission type	1	HIgh
Insulin meds	up	High
Count: 3 strong factors (no of diagnoses ≥7, emergency admission, and med change up)  
Decision: YES, will be readmitted within 30 days.
Reasoning: This encounter has multiple converging risk factors: emergency admission, insulin medication up, and medication escalation all point to a complex, unstable patient needing close post-discharge follow-up. Readmission within 30 days is likely.

Example 2: Clear NO (Few/No Strong Factors)
Encounter ID: 25726860
Field	Value	Risk
Time in hospital	3	Low
Nos of inpatient	0	Low
Nos of diagnoses	4	Moderate
Admission type	6	Low
Insulin med	steady	Moderate
Count: 0 strong
Decision: NO, the brief 3-day stay, lack of prior admissions, and stable management suggest an acute but well-controlled event. Low readmission risk.

Example 3: Borderline (1–2 Factors, Need Judgment)
Encounter ID: 214277418
Field	Value	Risk
Time in hospital	3	Low
Nos of inpatient	0	Low
Nos of diagnoses	9	High
Admission type	1	High
Insulin med	steady	Moderate
Count: 2 strong factors (admission type= 1, number of diagnoses ≥7)  
Decision: YES – Readmitted within 30 days (marginal, but 2 strong factors triggers a YES)  
Reasoning: admission type (1) and high diagnosis count (7) suggests medical complexity despite age. The combination warrants YES to be conservative, complex cases often readmit.

5. Age and Gender
Rule: Age and gender are present in the data but are not primary decision drivers in these guidelines.
a)	Context: Older age (≥ 80) + multiple moderate factors may shift a borderline case toward YES
b)	Complication: Gender is included for fairness analysis in the full project; use clinical judgment, not gender stereotypes

6. Consistency Tips
a)	Use a consistent threshold for "≥7 diagnoses" and "≥7 days." Re-read examples if unsure.
b)	 Document any encounters you are unsure about and include in your submission comments.
c)	 Do not second-guess: Once you apply the rules, commit to the label and move forward.
d)	 Missing values should be ignored and no attempt should be made to estimate or fill missing values. Decisions can be based only on columns that contain valid data and if a decision cannot be made because too many columns are missing, label it as a NO.
7. Contact Information

Questions or ambiguities:
•	Emails: alexgrg@umich.edu, ckrai@umich.edu
•	Include Encounter ID in the subject line
________________________________________
Thank you! Your careful annotation ensures high-quality data, supports machine learning model reliability, and improves interpretability for hospital readmission prediction research.


