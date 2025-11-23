# PowerPoint Presentation Guide for CA1 Assignment

**Module:** ST1510 Programming for Data Analytics   
**Assignment:** CA1 - Job Market Analysis Presentation  
**Deadline:** December 1, 2025, 08:00 Hr

---

## Table of Contents

1. [Presentation Requirements](#presentation-requirements)
2. [Slide-by-Slide Guide](#slide-by-slide-guide)
3. [Design Tips](#design-tips)
4. [Speaker Notes](#speaker-notes)
5. [Presentation Delivery](#presentation-delivery)
6. [Q&A Preparation](#qa-preparation)
7. [Common Mistakes to Avoid](#common-mistakes-to-avoid)

---

## Presentation Requirements

### Official Requirements (from Assignment Brief)

**Total Slides:** 9-11 slides maximum

**Required Structure:**
1. ✅ Cover page with name and research question
2. ✅ Summary of analysis steps
3. ✅ Maximum 3 slides for Pandas code
4. ✅ Maximum 3 slides for Matplotlib code
5. ✅ Key insights slide

**Presentation Format:**
- Must be ready to run code during presentation
- Lecturer may ask to run specific code sections
- Time limit will be specified by lecturer (typically 10-15 minutes)
- Q&A session follows presentation

**Grading Weight:** 10% (Presentation) + 10% (Q&A) = 20% total

---

## Slide-by-Slide Guide

### Slide 1: Cover Page ✅

**Purpose:** Professional introduction with clear research question

**Content:**

```
Title: Job Market Analysis for Computing Students
Subtitle: LinkedIn Job Postings Analysis

Student Name: Thoon Wai Si
Student ID: [Your ID]
Class: [Your Class]
Module: ST1510 Programming for Data Analytics
Date: November 2025

Research Question:
"How do salary levels, job location, and experience requirements
differ across technology and data analytics positions?"
```

**Design Tips:**
- Use school colors if available
- Include a relevant icon (chart, graph, briefcase)
- Keep it clean and professional
- Ensure research question is prominent and readable
- Use 24-28pt font for title
- Use 18-20pt font for research question

**Speaker Notes:**
"Good morning/afternoon. My name is Thoon Wai Si, and today I'll present my analysis of LinkedIn job postings data. My research question focuses on understanding salary levels, locations, and experience requirements for technology and data analytics positions. This analysis is particularly relevant for us as computing students preparing to enter the job market."

**Time:** 30 seconds

---

### Slide 2: Dataset Overview & Analysis Steps ✅

**Purpose:** Show what data was used and analysis methodology

**Content:**

**Title:** Dataset Overview & Analysis Methodology

**Datasets Used:**
- 📊 5 LinkedIn Job Posting Datasets
- 🔢 123,849 Total Job Postings
- 🗓️ Data Source: Kaggle (2023)

**Analysis Steps:**
1. **Data Loading** - Imported 5 CSV/Excel files using Pandas
2. **Data Inspection** - Examined structure, data types, missing values
3. **Data Cleaning** - Removed Easter Egg columns, handled missing data
4. **Data Merging** - Combined datasets using job_id as key
5. **Analysis** - Grouped by experience level, location, job type
6. **Visualization** - Created 5 different chart types using Matplotlib

**Key Datasets:**
- postings1.csv: Job titles and companies
- postings2.csv: Job descriptions and max salary
- postings3.csv: Locations and salary ranges
- postings4.csv: Work types and experience levels
- postings5.xlsx: Additional job data

**Speaker Notes:**
"I analyzed LinkedIn job postings from Kaggle, consisting of 5 datasets with over 123,000 job listings. My methodology involved six steps: First, I loaded all datasets using Pandas. Second, I inspected the data structure and identified missing values. Third, I cleaned the data by removing unnecessary Easter Egg columns as required. Fourth, I merged all datasets using job_id as the common key. Fifth, I performed various analyses grouping by experience level, location, and job type. Finally, I created five different visualizations using Matplotlib to present my findings."

**Time:** 1-1.5 minutes

---

### Slide 3: Pandas Analysis #1 - Data Cleaning & Merging ✅

**Purpose:** Show data preparation techniques

**Content:**

**Title:** Pandas Analysis: Data Cleaning & Merging

**Data Cleaning:**
```python
# Remove Easter Egg and Unimportant columns
df1_clean = df1[['job_id', 'company_name', 'title']].copy()

# Original: 21 columns → Cleaned: 3 columns
# Removed 18 unnecessary columns
```

**Data Merging:**
```python
# Merge all datasets using job_id as key
df_merged = df1_clean \
    .merge(df2_clean, on='job_id', how='left') \
    .merge(df3_clean, on='job_id', how='left') \
    .merge(df4_clean, on='job_id', how='left')

# Final merged dataset: 123,849 rows × 28 columns
```

**Key Results:**
- ✅ Removed all Easter Egg columns (requirement met)
- ✅ Successfully merged 5 datasets
- ✅ No data loss during merging
- ✅ Ready for analysis

**Speaker Notes:**
"The first major Pandas task was data cleaning and merging. I removed the Easter Egg and Unimportant columns from datasets 1 and 5, reducing dataset 1 from 21 columns to just 3 essential columns. Then I merged all five datasets using left joins on the job_id column. This preserved all 123,849 jobs while adding relevant columns from each dataset. The final merged dataset has 28 columns and is ready for analysis."

**Time:** 1 minute

---

### Slide 4: Pandas Analysis #2 - Salary by Experience Level ✅

**Purpose:** Demonstrate groupby and aggregation

**Content:**

**Title:** Pandas Analysis: Salary by Experience Level

**Code:**
```python
# Filter jobs with valid salary and experience data
salary_exp = df_merged[
    df_merged['med_salary'].notna() &
    df_merged['formatted_experience_level'].notna()
].copy()

# Group by experience level and calculate statistics
salary_by_exp = salary_exp.groupby('formatted_experience_level') \
    ['med_salary'].agg([
        ('count', 'count'),
        ('mean', 'mean'),
        ('median', 'median'),
        ('min', 'min'),
        ('max', 'max')
    ]).round(2)
```

**Results:**
| Experience Level | Count | Mean Salary | Median Salary |
|-----------------|-------|-------------|---------------|
| Executive | 26 | $137,429.70 | $135,000 |
| Director | 68 | $129,296.46 | $127,500 |
| Mid-Senior | 1,459 | $39,900.84 | $70 |
| Entry level | 2,748 | $10,476.28 | $21.58 |
| Internship | 133 | $2,682.64 | $20 |

**Speaker Notes:**
"This code demonstrates Pandas groupby and aggregation. I first filtered the data to include only jobs with both salary and experience level information, which gave me 4,858 jobs. Then I used groupby to group by experience level and calculated multiple statistics using the agg function - count, mean, median, minimum, and maximum salaries. The results clearly show salary progression: Executives earn an average of $137,430, while Entry-level positions average $10,476. This represents a 13-fold difference, highlighting the value of experience in the job market."

**Time:** 1-1.5 minutes

---

### Slide 5: Pandas Analysis #3 - Technology Jobs & Location Analysis ✅

**Purpose:** Show string filtering and complex queries

**Content:**

**Title:** Pandas Analysis: Tech Jobs & Top Locations

**Technology Jobs Filtering:**
```python
# Filter for technology and data analytics roles
tech_keywords = ['Software', 'Developer', 'Engineer', 'Data',
                 'Analyst', 'Scientist', 'Tech', 'IT', 'AI']

tech_filter = df_merged['title'].str.contains(
    '|'.join(tech_keywords), case=False, na=False
)
tech_jobs = df_merged[tech_filter].copy()

# Result: 48,875 tech jobs (39.5% of all jobs)
```

**Top Locations Analysis:**
```python
# Find top 10 locations by job count
top_locations = df_merged['location'].value_counts().head(10)

# Calculate average salary by location
location_salary = df_merged.groupby('location')['med_salary'] \
    .agg(['count', 'mean', 'median']).round(2)
```

**Key Findings:**
- 🖥️ Tech jobs: 48,875 (39.5% of total)
- 📍 Top location: New York, NY (2,756 jobs)
- 💰 Highest avg salary: United States ($51,876)

**Speaker Notes:**
"Here I demonstrate string filtering using Pandas. I created a list of technology-related keywords and used the str.contains method with a regular expression to filter job titles. The pipe symbol creates an OR condition, matching any title containing these keywords. This revealed that nearly 40% of all jobs are technology-related - great news for computing students! I also analyzed locations using value_counts to find the top cities and groupby to calculate average salaries by location. New York has the most jobs, while remote positions labeled 'United States' offer the highest average salary."

**Time:** 1-1.5 minutes

---

### Slide 6: Matplotlib Visualization #1 - Bar Chart ✅

**Purpose:** Show salary comparison visualization

**Content:**

**Title:** Matplotlib Visualization: Average Salary by Experience Level

**Code:**
```python
# Create bar chart with custom styling
plt.figure(figsize=(16, 8))
bars = plt.bar(range(len(avg_salary_exp)), avg_salary_exp.values,
               color='steelblue', edgecolor='black', linewidth=2)

# Add value labels on bars
for i, (bar, value) in enumerate(zip(bars, avg_salary_exp.values)):
    plt.text(bar.get_x() + bar.get_width()/2,
             bar.get_height() + 4000,
             f'${value:,.0f}', ha='center', va='bottom',
             fontsize=14, fontweight='bold')

plt.xlabel('Experience Level', fontsize=16, fontweight='bold')
plt.ylabel('Average Salary (USD)', fontsize=16, fontweight='bold')
plt.title('Average Salary by Experience Level',
          fontsize=18, fontweight='bold')
plt.grid(axis='y', alpha=0.3)
plt.savefig('../output_charts/Chart1_Bar_Salary_by_Experience.png',
            dpi=300)
```

**[INSERT BAR CHART IMAGE HERE]**

**Key Insight:** Clear salary ladder - Executive level earns 51× more than Internships

**Speaker Notes:**
"This bar chart visualizes salary progression across experience levels. I used Matplotlib's bar function with custom styling - steelblue bars with black borders. I added value labels on top of each bar using a for loop and the text function, making the exact salaries visible. The chart clearly shows a salary ladder: each step up in experience level brings significant salary increases. The gridlines help readers estimate values. This visualization effectively communicates that experience matters significantly in tech careers."

**Time:** 1 minute

---

### Slide 7: Matplotlib Visualization #2 - Box Plot & Histogram ✅

**Purpose:** Show distribution visualizations

**Content:**

**Title:** Matplotlib Visualizations: Distributions

**Box Plot - Salary Distribution:**
```python
plt.boxplot(data_for_box, labels=exp_order, patch_artist=True,
    boxprops=dict(facecolor='lightblue'),
    medianprops=dict(color='red', linewidth=2))
```

**[INSERT BOXPLOT IMAGE - LEFT HALF]**

**Histogram - Overall Salary:**
```python
plt.hist(salary_hist_filtered, bins=30, color='steelblue')
plt.axvline(mean_sal, color='red', linestyle='--',
            label=f'Mean: ${mean_sal:,.0f}')
plt.axvline(median_sal, color='green', linestyle='--',
            label=f'Median: ${median_sal:,.0f}')
```

**[INSERT HISTOGRAM IMAGE - RIGHT HALF]**

**Key Insights:**
- 📊 Box Plot: Shows salary spread and outliers per experience level
- 📈 Histogram: Most salaries cluster around $25,000-$40,000

**Speaker Notes:**
"These two charts show salary distributions. The box plot on the left displays salary ranges for each experience level. The red line shows the median, the box shows the middle 50% of salaries, and the dots are outliers. Notice how senior positions have wider boxes and more outliers, indicating greater salary variance and negotiation potential. The histogram on the right shows the overall salary distribution. I added vertical lines for mean and median using axvline. The distribution is right-skewed, with most jobs paying moderate salaries and fewer high-paying positions."

**Time:** 1-1.5 minutes

---

### Slide 8: Matplotlib Visualization #3 - Pie Chart & Scatter Plot ✅

**Purpose:** Show proportions and relationships

**Content:**

**Title:** Matplotlib Visualizations: Proportions & Relationships

**Pie Chart - Experience Distribution:**
```python
plt.pie(exp_distribution.values, autopct='%1.1f%%',
        colors=colors, explode=explode)
plt.legend(exp_distribution.index, loc='upper left',
           bbox_to_anchor=(1, 0, 0.5, 1))
```

**[INSERT PIE CHART IMAGE - LEFT HALF]**

**Scatter Plot - Salary vs Applications:**
```python
plt.scatter(scatter_data['med_salary'],
            scatter_data['applies'],
            alpha=0.5, s=50, c='steelblue')
```

**[INSERT SCATTER PLOT IMAGE - RIGHT HALF]**

**Key Insights:**
- 🥧 Pie: 43.9% Mid-Senior, 38.9% Entry-level (82% combined)
- 📉 Scatter: Weak correlation - high salary ≠ more applicants

**Speaker Notes:**
"The pie chart shows job distribution by experience level. I used autopct to show percentages and explode to separate slices slightly for clarity. The legend is positioned outside to avoid cluttering the chart. The data shows that Mid-Senior and Entry-level positions together comprise 83% of all jobs - excellent news for career progression. The scatter plot explores the relationship between salary and competition. Each dot represents a job. Surprisingly, there's no strong correlation - some high-paying jobs have few applicants, while some moderate-paying jobs are highly competitive. This suggests other factors like company reputation and location also drive applications."

**Time:** 1-1.5 minutes

---

### Slide 9: Key Insights & Findings ✅

**Purpose:** Summarize actionable insights for computing students

**Content:**

**Title:** Key Insights for Computing Students

**1. Salary Progression is Significant 💰**
- Entry-level: $10,476 average salary
- Mid-Senior: $39,901 (3.8× entry-level)
- Executive: $137,430 (13× entry-level)
- **Takeaway:** Experience dramatically increases earning potential

**2. Strong Job Market for Entry-Level 📈**
- 36,708 entry-level positions (38.9% of jobs)
- 2,748 entry-level positions with salary data
- Technology sector: 917 entry-level tech jobs
- **Takeaway:** Plenty of opportunities to start your career

**3. Geographic Opportunities 🗺️**
- Top cities: New York (2,756), Chicago (1,834), Houston (1,762)
- Highest salaries: Remote/US ($51,876), Atlanta ($49,890)
- Technology hubs offer competitive compensation
- **Takeaway:** Consider relocating or remote work for better opportunities

**4. Technology Sector is Thriving 💻**
- 48,875 tech jobs (39.5% of all postings)
- Popular roles: Software Engineer, Data Analyst
- Tech executives can earn $172,625 average
- **Takeaway:** Focus on developing in-demand tech skills

**5. Career Planning Recommendations 🎯**
- Start with internships to gain experience ($2,683)
- Target entry-level positions ($10,476)
- Aim for Mid-Senior roles within 5-7 years ($39,901)
- Long-term goal: Director/Executive ($129,000+)
- **Takeaway:** Plan your career growth strategically

**Speaker Notes:**
"Let me summarize the key insights from this analysis. First, salary progression is substantial - executives earn 13 times more than entry-level, proving experience is highly valuable. Second, the entry-level job market is strong with over 36,000 positions, including 917 tech-specific roles - great for students like us. Third, major cities offer the most opportunities, with remote work providing access to higher salaries. Fourth, the technology sector is thriving at nearly 40% of all jobs. Finally, for career planning, I recommend starting with internships, targeting entry-level positions after graduation, and aiming for mid-senior roles within 5-7 years. The data shows clear career progression with substantial salary increases at each level."

**Time:** 2 minutes

---

### Slide 10: Conclusion & Research Question Answered ✅

**Purpose:** Tie everything back to research question

**Content:**

**Title:** Conclusion

**Research Question Answered:**
"How do salary levels, job location, and experience requirements differ across technology and data analytics positions?"

**Answer:**

**Salary Levels:**
✅ Strongly correlated with experience level
✅ Range from $2,683 (Internship) to $137,430 (Executive)
✅ Technology sector pays competitively at all levels

**Job Locations:**
✅ Major cities dominate (NY, Chicago, Houston, Dallas)
✅ Remote work offers highest average salaries ($51,876)
✅ Geographic flexibility increases opportunities

**Experience Requirements:**
✅ Most jobs are Mid-Senior (43.9%) or Entry-level (38.9%)
✅ Clear career progression path exists
✅ Entry-level opportunities abundant for new graduates

**Final Takeaway:**
The job market offers excellent opportunities for computing students. By developing in-demand skills, gaining experience, and being geographically flexible, students can build successful careers with substantial earning potential.

**Thank you! Questions?**

**Speaker Notes:**
"To conclude, let me directly answer my research question. Regarding salary levels, I found they're strongly correlated with experience, ranging from $2,683 for internships to $137,430 for executives. The technology sector pays competitively at all levels. For job locations, major cities like New York, Chicago, and Houston have the most opportunities, while remote positions offer the highest average salaries at $51,876. Concerning experience requirements, most jobs are either Mid-Senior or Entry-level, with abundant opportunities for new graduates. The data shows a clear career progression path exists. My final takeaway is that the job market offers excellent opportunities for computing students. By developing in-demand skills, gaining experience through internships, and being open to relocation or remote work, we can build successful careers with substantial earning potential. Thank you for your attention. I'm happy to answer any questions."

**Time:** 1.5 minutes

---

### Optional Slide 11: Technical Details (Backup) ⚠️

**Purpose:** Have ready if asked technical questions

**Content:**

**Title:** Technical Implementation Details

**Pandas Techniques Used:**
- ✅ Data loading: `read_csv()`, `read_excel()`
- ✅ Data inspection: `info()`, `describe()`, `head()`
- ✅ Missing values: `isnull()`, `sum()`, `dropna()`
- ✅ Merging: `merge()` with left joins
- ✅ Grouping: `groupby()` with multiple aggregations
- ✅ Filtering: Boolean indexing, `str.contains()`
- ✅ Statistics: `mean()`, `median()`, `std()`, `agg()`

**Matplotlib Techniques Used:**
- ✅ Bar Chart: `plt.bar()` with value labels
- ✅ Box Plot: `plt.boxplot()` with custom styling
- ✅ Histogram: `plt.hist()` with 30 bins
- ✅ Pie Chart: `plt.pie()` with percentages
- ✅ Scatter Plot: `plt.scatter()` with alpha transparency
- ✅ Customization: Colors, labels, titles, grids, legends
- ✅ Export: `plt.savefig()` at 300 DPI

**Data Quality:**
- Total jobs: 123,849
- Jobs with salary data: 6,280 (5.1%)
- Jobs with experience data: 94,440 (76.3%)
- Data completeness: 67.3%

**Use only if:** Lecturer asks specific technical questions

**Time:** 1 minute if needed

---

## Design Tips

### Overall Design Principles

**Color Scheme:**
- Use professional colors (blue, gray, white)
- Avoid bright, flashy colors
- Maintain consistency across slides
- Use school colors if specified

**Fonts:**
- Title: 28-32pt, bold
- Headings: 20-24pt, bold
- Body text: 16-18pt
- Code: 12-14pt, monospace font (Consolas, Courier New)

**Layout:**
- Leave white space (don't overcrowd)
- Align elements consistently
- Use bullet points, not paragraphs
- Maximum 6-7 bullet points per slide

**Images/Charts:**
- High resolution (300 DPI minimum)
- Clearly visible from distance
- Include captions or labels
- Don't stretch or distort

### Code Formatting

**Do:**
- Use monospace font (Consolas, Courier New)
- Syntax highlighting if possible
- Keep code snippets short (5-10 lines)
- Add comments to explain complex parts
- Use consistent indentation

**Don't:**
- Include entire functions
- Use tiny font sizes
- Show error messages
- Include debugging code

**Example:**
```python
# Good - concise and clear
df_clean = df[['job_id', 'company_name', 'title']].copy()

# Bad - too much code
for i in range(len(df)):
    if df.loc[i, 'salary'] > 0 and df.loc[i, 'salary'] < 1000000:
        cleaned_data.append(df.loc[i, :])
# ... many more lines
```

### Chart Placement

**Option 1: Full Slide Chart**
- Chart takes 80-90% of slide
- Title at top
- Small caption/insight at bottom
- Best for impressive visuals

**Option 2: Split Slide**
- Code on left (40%)
- Chart on right (60%)
- Shows code and result together
- Good for technical audiences

**Option 3: Two Charts**
- Related charts side by side
- Each takes 50% width
- Compare different aspects
- Save slide count

### Professional Touch

**Add:**
- Slide numbers (bottom right)
- Your name (footer)
- Module code (footer)
- Consistent header style

**Check:**
- Spelling and grammar
- Alignment of elements
- Font consistency
- Color consistency
- Image quality

---

## Speaker Notes

### General Tips

**Before Each Slide:**
- Take a breath
- Make eye contact
- Introduce the slide topic
- Then look at slide to reference

**During Slide:**
- Explain, don't just read
- Point to specific elements
- Use "here you can see..."
- Engage with the content

**After Slide:**
- Summarize key point
- Transition to next slide
- "Moving on to..."
- "Now let's look at..."

### Timing Guidelines

**Total Presentation:** 10-15 minutes typical

**Suggested Breakdown:**
- Slide 1 (Cover): 30 seconds
- Slide 2 (Overview): 1-1.5 minutes
- Slide 3 (Pandas 1): 1 minute
- Slide 4 (Pandas 2): 1-1.5 minutes
- Slide 5 (Pandas 3): 1-1.5 minutes
- Slide 6 (Matplotlib 1): 1 minute
- Slide 7 (Matplotlib 2): 1-1.5 minutes
- Slide 8 (Matplotlib 3): 1-1.5 minutes
- Slide 9 (Insights): 2 minutes
- Slide 10 (Conclusion): 1.5 minutes

**Total:** 12-14 minutes (leaves time for questions)

### Voice Tips

**Do:**
- Speak clearly and steadily
- Vary your tone (not monotone)
- Emphasize key points
- Pause between slides
- Show enthusiasm

**Don't:**
- Rush through slides
- Speak too quietly
- Use filler words (um, uh, like)
- Read word-for-word
- Face the screen only

---

## Presentation Delivery

### Before Presentation

**Technical Setup (5 minutes before):**
1. ✅ Open PowerPoint presentation
2. ✅ Open Jupyter notebook (in case asked to run code)
3. ✅ Test projector/screen
4. ✅ Close unnecessary windows
5. ✅ Put phone on silent
6. ✅ Have water ready

**Mental Preparation:**
1. Review slides one last time
2. Practice first 2-3 slides opening
3. Take deep breaths
4. Positive mindset
5. Remember - you know this material!

### During Presentation

**Opening (First 30 seconds):**
```
"Good morning/afternoon [Professor Name] and classmates.

My name is Thoon Wai Si, and today I will present my analysis
of LinkedIn job postings data to understand salary levels, job
locations, and experience requirements in technology and data
analytics positions.

Let's begin with an overview of the datasets I analyzed."

[Click to next slide]
```

**Main Body:**
- Speak to the audience, not the screen
- Use pointer/cursor to highlight
- Explain each chart before showing
- Connect back to research question
- Show enthusiasm for findings

**Transitions:**
- "Moving on to my next analysis..."
- "Now let's look at how I visualized this data..."
- "This brings me to my key findings..."
- "To conclude..."

**Closing:**
```
"To summarize, my analysis shows that the job market offers
excellent opportunities for computing students. By developing
in-demand skills and gaining experience, we can build successful
careers with substantial earning potential.

Thank you for your attention. I'm happy to answer any questions."
```

### If Asked to Run Code

**Preparation:**
1. Have Jupyter notebook open in another window
2. Know which cells correspond to which slides
3. Practice switching between windows

**Steps:**
```
"Certainly, let me show you that code running."

[Switch to Jupyter notebook]

"Here you can see the code in cell [number].
I'll run it now..."

[Shift + Enter to run cell]

"And here are the results, which match what
I showed in the presentation."

[Switch back to PowerPoint]

"Thank you for asking. Any other questions?"
```

**If Code Errors:**
```
"Let me check that... [investigate briefly]

This cell depends on earlier cells. Let me run
from the beginning of this section..."

[If still error: "I'll investigate this after
the presentation and can show you then."]
```

---

## Q&A Preparation

### Common Questions & Answers

**Q1: "Why did you choose this research question?"**

**A:** "I chose this research question because it's directly relevant to us as computing students. Understanding salary levels helps set realistic expectations, knowing top locations helps with career planning, and seeing experience requirements shows us the career path ahead. The insights from this analysis can guide our skill development and job search strategies."

---

**Q2: "What was the biggest challenge in this analysis?"**

**A:** "The biggest challenge was handling missing data. Only about 5% of jobs had complete salary information, which limited my salary analysis. I addressed this by clearly stating the sample size in each analysis and focusing on jobs with complete data for each specific question. I also used multiple datasets to cross-validate findings where possible."

---

**Q3: "Explain how you cleaned the Easter Egg columns."**

**A:** "The Easter Egg columns were in datasets 1 and 5. I removed them by selecting only the relevant columns using bracket notation. For example, for dataset 1, I used: `df1_clean = df1[['job_id', 'company_name', 'title']].copy()`. This kept only the three essential columns and removed all 18 Easter Egg and Unimportant columns, reducing from 21 to 3 columns."

---

**Q4: "Why did you use a left join when merging?"**

**A:** "I used left joins to preserve all jobs from the main dataset. A left join keeps all rows from the left dataframe and adds matching columns from the right dataframe. This ensures no jobs are lost during merging, even if they don't have information in all datasets. Missing values indicate data not available for that specific job, which I handled by filtering in each analysis."

---

**Q5: "Can you explain the groupby operation?"**

**A:** "Certainly. The groupby operation splits the data into groups based on a category, applies a function to each group, and combines the results. For example, when I grouped by experience level and calculated mean salary, Pandas:
1. Split jobs into groups (Executive, Director, Entry-level, etc.)
2. Calculated the mean salary for each group
3. Combined the results into a summary table
This allows us to compare salaries across different experience levels efficiently."

---

**Q6: "Why did you filter salaries to $0-$200,000 for the histogram?"**

**A:** "I filtered extreme outliers to create a more readable visualization. The original data included salaries up to $750,000, which compressed most of the data into a small area on the left. By filtering to $200,000, I could show the distribution where most salaries actually fall, making patterns more visible. I noted this filtering on the chart title for transparency."

---

**Q7: "What does the box plot show exactly?"**

**A:** "A box plot shows five key statistics:
1. The bottom of the box is the 25th percentile (Q1)
2. The red line inside the box is the median (50th percentile)
3. The top of the box is the 75th percentile (Q3)
4. The whiskers extend to 1.5 times the interquartile range
5. Points beyond the whiskers are outliers
This helps us see not just average salary, but the entire salary distribution and identify unusual cases."

---

**Q8: "Did you use any lambda functions?"**

**A:** "Yes, lambda functions were used implicitly in several operations. For example, when filtering with `str.contains()`, Pandas applies a lambda function to each row. I also used lambda logic in the groupby operations, though I didn't write explicit lambda syntax. If needed, I could rewrite operations like the tech job filter using explicit lambda: `df_merged[df_merged['title'].apply(lambda x: any(kw in str(x).lower() for kw in tech_keywords))]`."

---

**Q9: "How reliable is your salary data with only 5% having values?"**

**A:** "That's a great question. With only 5% of jobs having salary data, the sample size is limited, but it's still substantial - over 6,000 jobs. To address reliability, I:
1. Clearly stated sample sizes in each analysis
2. Used median instead of mean to reduce outlier impact
3. Cross-referenced findings across multiple datasets
4. Focused on relative comparisons (e.g., Executive vs Entry-level) rather than absolute values
5. Acknowledged this limitation in my conclusion
The patterns observed (higher experience = higher salary) are strong and consistent, giving me confidence in the findings despite the limited sample."

---

**Q10: "Can you run the code for [specific analysis]?"**

**A:** "Absolutely. Let me open the Jupyter notebook..."

[Navigate to relevant cell]

"This is the code for [specific analysis]. I'll run it now."

[Execute cell]

"As you can see, the results match what I presented. The code [explain what it does]..."

---

### Questions to Prepare For

**Technical Questions:**
- Explain any Pandas function you used
- Explain any Matplotlib parameter
- Why this chart type for this data?
- What do these statistics mean?
- How did you handle missing values?

**Analysis Questions:**
- Why this research question?
- What surprised you in the data?
- What are the limitations?
- How could you improve this analysis?
- What would you investigate next?

**Code Questions:**
- Can you run this section?
- Explain this code line
- Why did you use this method?
- Could you do it differently?
- What does this error mean?

### Answer Framework (S.T.A.R.)

**S** - Situation: "In this analysis..."
**T** - Task: "I needed to..."
**A** - Action: "So I used... / I decided to..."
**R** - Result: "Which showed... / This revealed..."

**Example:**
```
Q: "Why did you use a bar chart for salary comparison?"

Situation: "In this analysis, I wanted to compare average
           salaries across six different experience levels."

Task: "I needed a chart type that clearly shows
      differences in values across categories."

Action: "I chose a bar chart because it's excellent for
        comparing values across categories. I added value
        labels on each bar for exact numbers."

Result: "This makes the salary ladder immediately visible
        and allows viewers to see both relative differences
        and exact amounts at a glance."
```

---

## Common Mistakes to Avoid

### Content Mistakes

**❌ Don't:**
- Read slides word-for-word
- Include too much text per slide
- Use tiny, unreadable fonts
- Show code without explaining it
- Include errors or debugging code
- Use more than 3 slides per section
- Forget to address research question
- Skip the conclusion
- Ignore timing

**✅ Do:**
- Explain and elaborate beyond slide text
- Use bullet points and key phrases
- Use 16pt+ font for all text
- Explain what code does and why
- Test all code before presentation
- Follow slide count limits strictly
- Tie findings back to question
- Summarize key takeaways
- Practice timing beforehand

### Design Mistakes

**❌ Don't:**
- Use busy backgrounds
- Mix too many fonts
- Use red/green together (colorblind)
- Stretch or distort images
- Use low-resolution charts
- Inconsistent styling across slides
- Animation overkill
- Unaligned elements

**✅ Do:**
- Use clean, simple backgrounds
- Stick to 2-3 fonts maximum
- Use colorblind-friendly palettes
- Maintain image aspect ratios
- Use 300 DPI images minimum
- Match colors/fonts on all slides
- Minimal, professional animations
- Align text and images properly

### Delivery Mistakes

**❌ Don't:**
- Face the screen entire time
- Speak too fast (nervous)
- Use filler words constantly
- Apologize unnecessarily
- Go over time limit
- Skip slides if running late
- Panic if code doesn't run
- Give up during Q&A

**✅ Do:**
- Make eye contact with audience
- Speak clearly and steadily
- Pause between thoughts
- Be confident in your work
- Finish within time limit
- Stick to your plan
- Calmly troubleshoot issues
- Answer honestly, ask for clarification

---

## Final Checklist

### Before Creating Slides

- [ ] Read notebook thoroughly
- [ ] Understand all code
- [ ] Identify key findings
- [ ] Select best charts
- [ ] Plan slide structure

### While Creating Slides

- [ ] Follow required structure exactly
- [ ] Stay within slide limits (9-11 slides)
- [ ] Include all 5 charts
- [ ] Use professional design
- [ ] Add speaker notes
- [ ] Check font sizes (readable)
- [ ] Verify image quality
- [ ] Spell check everything

### Before Presenting

- [ ] Practice presentation 3+ times
- [ ] Time yourself (10-15 minutes)
- [ ] Test code execution
- [ ] Prepare for Q&A
- [ ] Have backup plan if tech fails
- [ ] Review common questions
- [ ] Get good rest night before
- [ ] Arrive early to set up

### During Presentation

- [ ] Professional appearance
- [ ] Confident demeanor
- [ ] Clear voice
- [ ] Eye contact
- [ ] Explain, don't read
- [ ] Show enthusiasm
- [ ] Stay within time
- [ ] Handle questions well

---

## Time Breakdown Example

**12-Minute Presentation Plan:**

```
00:00-00:30   Slide 1: Introduction
00:30-02:00   Slide 2: Dataset & methodology
02:00-03:00   Slide 3: Data cleaning
03:00-04:30   Slide 4: Salary analysis
04:30-06:00   Slide 5: Tech jobs & locations
06:00-07:00   Slide 6: Bar chart
07:00-08:30   Slide 7: Box plot & histogram
08:30-10:00   Slide 8: Pie & scatter
10:00-12:00   Slide 9: Key insights
12:00-12:30   Slide 10: Conclusion

Total: 12.5 minutes
Q&A: 5-10 minutes
Grand Total: ~20 minutes
```

---

## Success Formula

**Before = Preparation**
- Understand your work completely
- Create professional slides
- Practice 3-5 times
- Prepare for questions

**During = Delivery**
- Speak clearly and confidently
- Explain, don't just read
- Show enthusiasm
- Engage with audience

**After = Learning**
- Note what went well
- Identify improvements
- Apply to future presentations
- Celebrate your success!

---

## You're Ready! 🎯

You have:
- ✅ Complete analysis with great insights
- ✅ Professional visualizations
- ✅ Clear research question answered
- ✅ This comprehensive guide
- ✅ All the knowledge you need

**Now create those slides and practice!**

**You've got this!** 🚀

---

**Document Created:** November 22, 2025
**Presentation Date:** [TBD - Check with lecturer]
**Time Limit:** 10-15 minutes (confirm with lecturer)
**Q&A:** 5-10 minutes following presentation

**Good luck with your presentation, Thoon Wai Si!** 🎓📊
