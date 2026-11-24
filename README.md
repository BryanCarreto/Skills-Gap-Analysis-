# Workforce Skills Gap Analysis: Construction Workforce 

**Author:** Bryan Carreto Colorado
**Tools:** [Excel / SQL / Python / Tableau. List what you actually used]
**Status:** [In progress / Complete]

> **About the data:** This dataset is **synthetic**. It was generated to mirror the structure of a company-wide skills assessment program I supported as HR Operations & Training Coordinator at a heavy civil construction company. No real employee, company or performance data is included.

---

## 1. Business Problem

A paving and grading contractor with about 220 field and shop employees ran a company-wide skills assessment in mid-2025, delivered targeted training, and reassessed employees in late 2025. Leadership wanted to know where the workforce falls short of role requirements, whether training closed those gaps, and whether the company is at compliance risk from lapsed certifications.

## 2. Business Questions

1. **Skill gaps:** Which skills, roles and departments have the largest gap between required and assessed proficiency?
2. **Training effectiveness:** Did employees who completed training improve more than those who didn't? Did training language (English vs. Spanish) make a difference?
3. **Certification compliance:** What percentage of required certifications are current, which have expired, and which expire in the next 90 days (as of Dec 31, 2025)?

## 3. Data

| File | Rows | Description |
|---|---|---|
| `data/employees.csv` | 220 | One row per employee |
| `data/skills.csv` | 16 | Skill catalog |
| `data/role_requirements.csv` | 52 | Required proficiency level per skill for each department + role |
| `data/assessments.csv` | 2,868 | Baseline (Jun–Jul 2025) and reassessment (Nov–Dec 2025) scores |
| `data/certifications.csv` | 373 | Certifications held, with issue and expiration dates |

### Data dictionary

**employees.csv**
- `employee_id`: unique ID (E1001…)
- `department`: Paving, Grading, Trucking, Equipment Shop
- `job_role`: Laborer, Equipment Operator, Foreman, Truck Driver, Mechanic
- `crew_id`: crew assignment
- `hire_date`: date hired
- `primary_language`: English or Spanish

**skills.csv**
- `skill_id`, `skill_name`
- `skill_category`: Safety, Equipment, Technical, Leadership

**role_requirements.csv**
- `department`, `job_role`, `skill_id`
- `required_level`: 1 = Basic, 2 = Developing, 3 = Proficient, 4 = Expert

**assessments.csv**
- `assessment_id`, `employee_id`, `skill_id`
- `assessment_round`: Baseline or Reassessment
- `assessment_date`
- `score`: 1–4, same scale as `required_level` (blank = not assessed)
- `training_completed`: Yes/No (reassessment rows only)
- `training_language`: English/Spanish if trained (reassessment rows only)

**certifications.csv**
- `employee_id`, `certification`, `issue_date`, `expiration_date`

### Key relationships
- `assessments` → `employees` on `employee_id`
- `assessments` → `skills` on `skill_id`
- `employees` + `assessments` → `role_requirements` on `department`, `job_role`, `skill_id`

**Gap formula:** `gap = required_level − score` (a gap of 0 or below means the employee meets the requirement)

## 4. Approach

1. **Data cleaning:** [How you handled blank reassessment scores, checked for duplicates, validated dates]
2. **Gap analysis:** [How you joined tables and calculated gaps by skill, role and department]
3. **Training impact:** [How you compared score change for trained vs. untrained employees, and by training language]
4. **Compliance check:** [How you classified certifications as Current, Expiring ≤90 days, or Expired. Also check for employees missing a required certification entirely]

## 5. Key Findings

> Fill in after your analysis. Lead each finding with a number.

1. **[Finding 1]**: e.g., "X skill had the largest average gap (__ levels), concentrated in __ role."
2. **[Finding 2]**: e.g., "Trained employees improved __ levels on average vs. __ for untrained."
3. **[Finding 3]**: e.g., "__% of certifications are expired or expire within 90 days."

![Chart 1](images/chart1.png)
![Chart 2](images/chart2.png)

## 6. Recommendations

1. [What should the company train on first, and for whom?]
2. [What should change about how training is delivered?]
3. [What should HR do about certifications?]

## 7. Limitations & Next Steps

- Data is synthetic. Real results would vary.
- Assessment scores are assessor ratings and may contain rater bias.
- Next step: link skill scores to safety incident data to test whether skill gaps predict incidents.

## 8. Repository Structure

```
skills-gap-analysis/
├── README.md
├── data/          # raw CSV files
├── analysis/      # Excel workbook, SQL queries or Python notebook
└── images/        # charts used in this README
```
