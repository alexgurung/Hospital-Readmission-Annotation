Hospital Readmission Annotation Dataset

Overview

This repository contains materials for annotating 200 de-identified hospital encounters to predict 30-day readmission risk for patients with diabetes.
The goal is to create a high-quality labeled dataset (YES/NO) to support machine learning and interpretability research.
Dataset Source: Diabetes 130-US Hospitals Dataset (UCI/Kaggle)
Subset: 200 selected encounters
________________________________________
Annotation Labels
•	YES – Patient readmitted within 30 days (<30)
•	NO – Patient not readmitted within 30 days (>30 or NO)
For full rules, examples, and edge cases, see the Annotation Guidelines PDF.
________________________________________
Annotation Interface
•	Tool: Spreadsheet (Excel / Google Sheets)
•	Template: annotation_template.csv
•	Steps:
1.	Open annotation_template.csv
2.	Count strong risk factors (see Guidelines)
3.	Label each encounter as YES or NO in annotated_label column
4.	Save completed file as annotations_completed.csv
For detailed step-by-step instructions, see Annotation Instructions PDF.
________________________________________
Strong Risk Factors
A “strong” risk factor includes:
Factor	Threshold
Prior inpatient admissions	≥ 2
Length of stay	≥ 7 days
Number of diagnoses	≥ 7
Admission type	Emergency (1)
Diabetes medication	Increased (Up)
Labeling Rule:
•	≥2 strong factors → YES
•	0–1 strong factors → NO
________________________________________
Examples
YES (Multiple Strong Factors)
•	Emergency admission
•	9 diagnoses
•	Insulin medication increased
NO (Few or No Strong Factors)
•	3-day stay
•	No prior admissions
•	Stable medication
Borderline Cases:
•	Consult guidelines for 1–2 strong factors
________________________________________
Age and Gender
•	Age and gender are included for context/fairness but do not directly determine labels.
•	Older age + multiple moderate factors may shift borderline cases to YES.
________________________________________
Submission Instructions
1.	Label all 200 encounters in annotated_label column
2.	Save as annotations_completed.csv (CSV format)
3.	Ensure no blank cells or typos
4.	Email file to project team:
o	alexgrg@umich.edu
________________________________________
License
•	Original dataset: Public domain (UCI)
•	Annotations and materials: © 2025–2026 Alex Gurung & Chandra Kala Rai, University of Michigan–Flint
•	For educational and research purposes only. See LICENSE.txt for details.

