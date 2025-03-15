# Introduction
With mental health illnesses on the rise everyday, this project explores how various mental illnesses affects college students, with respect to thir GPA.

The data came from the kaggle dataset: [Student Mental Health](https://www.kaggle.com/datasets/shariful07/student-mental-health), and provides all the information used in this data analysis.

## Dashboard File

My final dashboard is in [Student_Mental_Health]()

## Tools I Used

To tackle these questions, I sought out these key tools:

- **Kaggle**: Website used to access data
- **R**: The primary language for accessing and manipulating the dataset
- **Visual Studio Code**: Database platform for carrying out my R code
- **Github**: Sharing and uploading my R scripts

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

![Age_Distribution png](https://github.com/user-attachments/assets/8ffff4fb-7fac-4116-b626-be4bc3f648c0)

*Pie chart visualizing the age distribution for college students in this dataset*

**Age and Gender Distribution - Bar Chart**

![Gender_Age_Distribution png](https://github.com/user-attachments/assets/362c2124-93c1-4dc8-8922-0c40897df1ee)

*Bar chart visualizing the gender and age distribution for college students*

**Presence of Depression for College Students - Pie Chart**

![Presence_of_Depression png](https://github.com/user-attachments/assets/2d4fa725-0720-4542-af9a-585f238132fc)

*Pie chart visualizing the percentage of students with and without depression*

**Current GPA by Anxiety Status - Bar Chart**

![CGPA_Anxiety png](https://github.com/user-attachments/assets/8fa89ff5-9480-4a06-8b14-7db8b0be2ba2)

*Bar chart visualizing the current gpa for college students, depending on their anxiety status*

**Current GPA by Panic Attack Status - Bar Chart**

![CGPA_Panic_Attack png](https://github.com/user-attachments/assets/df9a231b-351b-425b-a711-4b8d41998e0e)

*Bar chart visualizing the current gpa for college students, depending on their panic attack status*

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
