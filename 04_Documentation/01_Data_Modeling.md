# 📐 Data Modeling Documentation

## Star Schema Design

### Fact Table: `Fact_Job_Postings`
| Column | Description | Data Type |
|--------|-------------|-----------|
| Job Posting ID | Unique identifier | Integer |
| Company Name | Hiring company | Text |
| Job Location | City/Remote | Text |
| Job Posting Date | Date posted | Date |
| Minimum Pay | Lowest salary offered | Currency |
| Maximum Pay | Highest salary offered | Currency |
| Number of Applicants | Total applicants | Integer |
| Years of Experience | Required experience | Decimal |
| Pay Rate | Hourly/Salary/Yearly | Text |
| Job_Title_Key | FK to Dim_Job_Title | Integer |
| Position_Level_Key | FK to Dim_Position_Level | Integer |
| Position_Type_Key | FK to Dim_Position_Type | Integer |
| Company_Size_Key | FK to Dim_Company_Size | Integer |
| Company_Industry_Key | FK to Dim_Company_Industry | Integer |
| Job Posting Date Key | FK to Dim_Date | Integer |

### Dimension Tables

**Dim_Job_Title**
- Job_Title_Key (PK)
- Job Title
- Job Title Additional Info
- Job Title Full

**Dim_Position_Level**
- Position_Level_Key (PK)
- Job Position Level (Entry, Mid-Senior, Executive, etc.)

**Dim_Position_Type**
- Position_Type_Key (PK)
- Job Position Type (Full-time, Part-time, Contract)

**Dim_Company_Size**
- Company_Size_Key (PK)
- Company Size (1-10, 11-50, 51-200, etc.)

**Dim_Company_Industry**
- Company_Industry_Key (PK)
- Company Industry

**Dim_Date**
- DateKey (PK)
- Date
- Year
- Quarter
- Month
- Month Name
- Day
- Day Name
- IsWeekend

**Dim_Job_Skills** (Bridge Table)
- Job Posting ID (FK)
- Skill
