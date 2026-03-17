# 📚 Data Dictionary

| Column Name | Description | Data Type | Example |
|-------------|-------------|-----------|---------|
| Job Posting ID | Unique identifier for each job | Integer | 1002345 |
| Job Title | Position title | Text | "Data Scientist" |
| Job Title Additional Info | Specialization | Text | "NLP Specialist" |
| Job Title Full | Complete title | Text | "Senior Data Scientist - NLP" |
| Company Name | Hiring organization | Text | "Toptal" |
| Company Industry | Industry sector | Text | "Internet" |
| Company Size | Employee count category | Text | "1,001-5,000 employees" |
| Job Location | City or Remote | Text | "Remote / San Francisco" |
| Job Position Level | Seniority level | Text | "Mid-Senior level" |
| Job Position Type | Employment type | Text | "Full-time" |
| Job Posting Date | Date posted | Date | "2021-03-15" |
| Job Skills | Comma-separated skills | List | ['SQL', 'Python', 'AWS', 'ML'] |
| Minimum Pay | Lowest salary offered | Currency | 95000 |
| Maximum Pay | Highest salary offered | Currency | 135000 |
| Pay Rate | Payment period | Text | "Yearly" |
| Number of Applicants | Total applicants | Integer | 24 |
| Years of Experience | Required experience | Decimal | 5.5 |

## Notes
- Data covers period: 2017-2021
- Total records: 25,116 job postings
- Data records: 9556 job postings
- Source: Aggregated from public job boards
- Skills column was parsed to create Dim_Job_Skills table
