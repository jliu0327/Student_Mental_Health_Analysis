# Introduction
With mental health illnesses on the rise everyday, this project explores how various mental illnesses affects college students, with respect to thir GPA.

The data came from the kaggle dataset: [Student Mental Health](https://www.kaggle.com/datasets/shariful07/student-mental-health), and provides all the information used in this data analysis.

## Dashboard File

My final dashboard is in [Student_Mental_Health]()

## R Skills Used

The following R skills were utilized for analysis:

- **dplyr**
- **ggplot**
- **chisq test**

## Student Mental Health Dataset

As mentioned, the dataset used for this project came from kaggle, and includes detailed information on:

- **Gender**
- **Age**
- **Depression Status**
- **Anxiety Status**
- **Panic Attack Status**

# Dashboard Build

## Charts

**Age Distribution of College Students - Pie Chart**

(Insert photo here)

**Age and Gender Distribution - Bar Chart**

(Insert photo here)

**Current GPA by Depression Status - Bar Chart**

(Insert photo here)

**Current GPA by Anxiety Status - Bar Chart**

(Insert photo here)

**Current GPA by Panic Attack Status - Bar Chart**

(Insert photo here)

## Formulas and Functions

**Current GPA and Depression Status**

```R
## CGPA and depression status
cgpa_dep_df <- student_health %>%
  select(Depression = Depression_Status, CGPA) %>%
  mutate(CGPA = case_when(
    CGPA == "3.50 - 4.00 " ~ "3.50 - 4.00",
    TRUE ~ CGPA
  )) %>%
  group_by(Depression, CGPA) %>%
  summarise(count = n(), .groups = "drop") %>%
  complete(CGPA, Depression, fill = list(count = 0))
## plot
ggplot(cgpa_dep_df, aes(x = CGPA, y = count, fill = Depression)) +
  geom_bar(stat = "identity", position = "dodge") +
  labs(title = "Comparison of Current GPA by Depression Status",
       x = "Current GPA", y = "Frequency", fill = "Depression")
```

- 

```R
dep_contingency_table <- xtabs(count ~ Depression + CGPA, data = cgpa_dep_df)
dep_chi_square_test <- chisq.test(dep_contingency_table)
```
