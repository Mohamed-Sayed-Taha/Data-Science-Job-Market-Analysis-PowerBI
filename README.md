# 📊 Data Science Job Market Analysis - Power BI Dashboard

![Dashboard Preview](02_Screenshots/Home Page.png)

## 📌 Overview
This project analyzes **9,556 job postings** in the Data Science field to provide insights into market demand, skill requirements, salary trends, and company hiring patterns. The interactive dashboard helps job seekers, HR professionals, and business leaders make data-driven decisions.

---

## 🎯 Business Questions Answered

### Jobs Page
- What is the distribution of job postings across seniority levels?
- How does salary correlate with years of experience?
- Which job titles are most in-demand?
- How did COVID-19 impact the job market?

### Skills Page
- What are the top 15 most in-demand skills?
- How do skill requirements differ by job title?
- Which skills are growing fastest?
- What skill combinations yield highest salaries?

### Company Page
- Which companies hire the most data professionals?
- How does company size affect salaries and competition?
- What industries have the highest demand?
- Where are the "sweet spots" for job seekers?

---

## 🗃️ Data Structure

### Source Data
- **9,556 job postings** (2017-2021)
- **166 distinct skills** identified
- **15+ industries** represented
- **7 company size categories**

### Star Schema Model

```
┌─────────────────┐     ┌──────────────────┐
│  Dim_Job_Title  │     │ Fact_Job_Postings│
├─────────────────┤     ├──────────────────┤   
│ Job_Title_Key   │◄────┤ Job_Title_Key    │
│ Job Title       │     │ Company_Name     │
└─────────────────┘     │ Job_Location     │
                        │ Min/Max Pay      │
┌─────────────────┐     │ Num_Applicants   │
│ Dim_Position_Lvl│     │ Years_Exp        │
├─────────────────┤     │ Job_Posting_Date │
│ Position_Lvl_Key│◄────┤ Position_Lvl_Key │
│ Position_Level  │     │ Position_Type_Key│
└─────────────────┘     │ Company_Size_Key │
                        │ Company_Indus_Key│
┌─────────────────┐     └────────┬─────────┘
│ Dim_Company_Size│               │
├─────────────────┤               ▼
│ Company_Size_Key│◄────┐  ┌──────────────┐
│ Company_Size    │     │  │ Dim_Job_Skills│
└─────────────────┘     │  ├──────────────┤
                        └──┤ Job_Posting_ID│
┌─────────────────┐        │ Skill         │
│Dim_Company_Industry│      └──────────────┘
├─────────────────┤
│Company_Indus_Key│◄────┐                     │
│Company_Industry │     │                     │
└─────────────────┘     │                     │
                        │                     │
┌─────────────────┐     │                     │
│ Dim_Position_Type│    │                     │
├─────────────────┤     │                     │
│Position_Type_Key│◄────┤─────────────────────│
│Position_Type    │     │
└─────────────────┘     │
                        │
┌─────────────────┐     │
│    Dim_Date     │     │
├─────────────────┤     │
│    DateKey      │◄────┘
│    Date         │
│    Year         │
│    Quarter      │
│    Month        │
└─────────────────┘
```

---

## ⚙️ Power Query M Code

### Date Table Creation
```m
// Create Dim_Date Table
let
    StartDate = #date(2017,1,1),
    EndDate = #date(2021,12,31),
    NumberOfDays = Duration.Days(EndDate - StartDate) + 1,
    DateList = List.Dates(StartDate, NumberOfDays, #duration(1,0,0,0)),
    TableFromList = Table.FromList(DateList, Splitter.SplitByNothing()),
    #"Renamed Columns" = Table.RenameColumns(TableFromList,{{"Column1", "Date"}}),
    #"Added Year" = Table.AddColumn(#"Renamed Columns", "Year", each Date.Year([Date])),
    #"Added Quarter" = Table.AddColumn(#"Added Year", "Quarter", each "Q" & Number.ToText(Date.QuarterOfYear([Date]))),
    #"Added Month" = Table.AddColumn(#"Added Quarter", "Month", each Date.Month([Date])),
    #"Added Month Name" = Table.AddColumn(#"Added Month", "Month Name", each Date.MonthName([Date])),
    #"Added DateKey" = Table.AddColumn(#"Added Month Name", "DateKey", each [Year] * 10000 + [Month] * 100 + Date.Day([Date]))
in
    #"Added DateKey"
```

---

## 📐 Key DAX Measures

```DAX
// Total Job Posts
CountJobPosting = COUNTROWS(Fact_Job_Postings)

// Average Salary
AvgPayperPost = 
AVERAGEX(Fact_Job_Postings, DIVIDE(Fact_Job_Postings[Maximum Pay] + Fact_Job_Postings[Minimum Pay], 2))

// Number of Skills
CountofSkills = 
COUNTROWS(Dim_Job_Skills)

// Number of Job posts
CountofSkills = 
COUNTROWS(Dim_Job_Skills)

// Skills Demand %
%SkillinPosting = 
DIVIDE([CountofSkills], [CountJobPosting])


```

---

## 📈 Key Insights

### 🔵 Jobs Page
| Insight | Finding |
|---------|---------|
| **Market Dominance** | Mid-Senior level = 58.5% of all jobs |
| **Top Role** | Data Engineer = 36.2% of posts, $134K avg salary |
| **Career Paths** | DE/DS: 65% Mid-Senior \| DA/BA: 35% Associate |
| **COVID Impact** | -15.7% Q1 2020 → +98.9% Q2 2020 |

### 🟢 Skills Page
| Rank | Skill | Demand | Category |
|------|-------|--------|----------|
| #1 | SQL | 45.8% | Database |
| #2 | Python | 43.3% | Programming |
| #3 | Cloud | 34.6% | Infrastructure |
| #4 | AWS | 31.8% | Cloud Platform |
| #5 | ML | 21.3% | Data Science |

**Fastest Growing (2019-2021):**
- Cloud (+100%)
- AWS (+100%)
- Azure (+101%)
- Agile (+101%)
- ETL (+100%)

### 🟠 Company Page
| Category | Top Performer | Stat |
|----------|--------------|------|
| **Company Size** | 1,001-5,000 employees | 42% of market |
| **Highest Pay** | 51-200 employees | $133K avg |
| **Top Industry** | Internet | 25% of posts, $139K |
| **Top Company** | Toptal | 17.8% market share |

---

## 🛠️ Tools Used

| Tool | Purpose |
|------|---------|
| **Power BI Desktop** | Dashboard design & visualization |
| **Power Query (M)** | Data transformation & ETL |
| **DAX** | Advanced calculations & measures |
| **Excel** | Initial data exploration |
| **GitHub** | Version control & portfolio |

---

## 🚀 How to Use This Dashboard

1. **Download** the `.pbix` file from the `02_Dashboard/` folder
2. **Open** with Power BI Desktop (free)
3. **Explore** interactive visualizations
4. **Filter** by industry, company size, date, etc.
5. **Hover** over charts for detailed tooltips

---

## 📂 Repository Structure

```
├── 01_Documentation/     # Detailed documentation
├── 02_Screenshots/       # Dashboard images
└── README.md            # You are here
```

---

## 📬 Contact

**Mohamed Sayed Taha**  
[www.linkedin.com/in/mohamed-sayed71]
[https://github.com/Mohamed-Sayed-Taha]  
[mohamedsaidtaha1@gmail.com]


---

### ⭐ If you find this project useful, please consider giving it a star!
