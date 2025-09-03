# 📘 Introduction

This repository is a structured journey into **Python for Data Analysis**.  
It’s not just a collection of scripts and visualizations, but a walkthrough of how Python can be applied to explore data, uncover insights, and communicate findings effectively.  

The goal is simple: to bridge the gap between *learning syntax* and *applying Python in real-world data scenarios*.  
Each section is designed to be practical, showing how code connects directly to analysis, visualization, and business understanding.  

---


# The Questions
This analysis revolves around a few key questions that guide the exploration:

1. What are the most demanded skills for the top 3 most popular data roles?  
2. How are in-demand skills trending for Data Analysts?  
3. How well do jobs and skills pay for Data Analysts?  
4. What is the most optimal skill to learn for Data Analysts?  

---

### 🛠️ Tools I Used
To build this project, I combined a set of tools that cover **coding, analysis, visualization, and version control**:

- **Python** → the main language, with key libraries:  
  - Pandas / NumPy → data cleaning and manipulation  
  - Matplotlib / Seaborn → visualization and storytelling with data  

- **Jupyter Notebook** → for interactive coding and analysis  

- **Google Colab** → for running notebooks in the cloud and easy sharing  

- **Visual Studio Code (VS Code)** → for writing and organizing scripts  

- **Git & GitHub** → for version control and project sharing  


# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

View my notebook with detailed steps here:  
[2_Skills_Count.ipynb](project\2_Skills_Count.ipynb)

### Visualize Data

```python
fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_perc[df_skills_perc['job_title_short'] == job_title].head(5) 
    sns.barplot(data=df_plot,x='skill_percent',y='job_skills',ax=ax[i],hue='skill_count', palette='dark:b_r')


plt.show()
```

### Results

![Visualization of Top Skills for Data Jobs](project\images\skill_demand.png)

### Insights

This visualization highlights the likelihood of specific technical skills being requested in U.S. job postings for **Data Analysts, Data Engineers, and Data Scientists**. By comparing the top skills across these roles, we can identify both the **common requirements** that span the data field and the **specialized skills** that distinguish each career path.

---

#### 🧾 Data Analyst
- **SQL** is the most requested skill (51%).
- **Excel** remains highly relevant (41%).
- **Tableau** (28%) is valued for data visualization.
- **Python** (27%) plays a smaller role compared to Data Scientist.

---

#### ⚙️ Data Engineer
- **SQL** (68%) and **Python** (65%) form the core foundation.
- Cloud expertise is in demand, with **AWS** (43%) and **Azure** (32%).
- **Spark** (32%) highlights the importance of big data technologies.

---

#### 🔬 Data Scientist
- **Python** is the dominant skill (72%).
- **SQL** (51%) and **R** (44%) are also highly valued.
- **SAS** and **Tableau** (24% each) are less critical but still relevant.

---

#### 📌 Overall Takeaway
- **SQL** is a universal requirement across all roles.  
- **Python** is the most essential skill for Data Scientists and Data Engineers.  
- **Data Analysts** rely more on practical tools like Excel and Tableau, reflecting their focus on reporting and visualization.  

---

## 2. How are in-demand skills trending for Data Analysts?

### Visualize Data

```python

df_plot = df_DA_US_percent.iloc[:, :5]

sns.lineplot(data=df_plot, dashes=False, palette='tab10')
sns.set_theme(style='ticks')
sns.despine()
plt.title('Trending Top Skills for Data Analysts in US')
plt.ylabel('Likelihood in Job Posting')
plt.xlabel('2023')
plt.legend().remove()

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(PercentFormatter(decimals=0))

colors = sns.color_palette('tab10', n_colors=len(df_plot.columns))

offsets = [1, 1, 0, -2, -1]

for i, col in enumerate(df_plot.columns):
    y = df_plot.iloc[-1, i] + offsets[i]
    plt.text(
        11.2, 
        y, 
        col, 
        color=colors[i],
        fontweight='bold'
    )
```


### Results

![Trending Top Skills for Data Analysts in the US](project\images\trending_skills.png)
*Bar graph visualizing the trending top skills for data analysts in the US in 2023*


### Insights

This visualization shows how the demand for **top technical skills** among Data Analysts in the U.S. evolved throughout 2023. By observing the monthly trends, we can see which skills remained consistent, which ones declined, and where sudden changes occurred.

---

#### 🧾 SQL
- Stayed the **most in-demand skill** across the entire year.  
- Despite slight fluctuations, it consistently led the chart (~45–55%).  
- Reinforces SQL as the **core competency** for analysts.  

---

#### 📊 Excel
- Maintained steady demand early in the year (~42%).  
- Experienced a **noticeable drop in the fall (Oct–Nov)**, but rebounded in December.  
- Shows Excel remains essential but may be losing ground to modern tools.  

---

#### 📈 Tableau
- Stable trend around the **mid-20% to high-20% range**.  
- Indicates visualization skills are valued but secondary to SQL/Excel.  

---

#### 🐍 Python
- Held a steady presence (~26–30%), slightly below Tableau.  
- Suggests Python is important for analysts but not as dominant as in Data Science roles.  

---

#### 📉 SAS
- Consistently the **least requested skill (~18–22%)**.  
- Highlights its declining relevance compared to modern tools.  

---

#### 📌 Overall Takeaway
- **SQL** remained the anchor skill throughout 2023.  
- **Excel** is still crucial, though showing signs of decline.  
- **Tableau and Python** hold moderate but steady demand.  
- **SAS** continues to lose relevance, signaling a shift toward modern analytics ecosystems.  


## 3. how well do jobs and skills pay for Data Analysts?

### Salary Analysis for Data Jobs

#### visualize Data 

```python
sns.boxplot(data=df_US_top6,x='salary_year_avg',y='job_title_short', order=job_order)

plt.title('Salary Distribution by Job Title in USA')
plt.xlabel('Yearly Salary')
plt.ylabel('')
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos:f'${int(x/1000)}K'))
plt.xlim(0, 600000)

plt.show()
```

#### Results 

![Salary Distributions of Data Jobs in Jobs in the US](project\images\salarry_boxplot.png)
*Box plot visualizing the salary distributions for the top 6 date job titles.*

#### Insights

From the analysis, it’s clear that salary levels follow a consistent hierarchy: **Data Analyst** sits at the bottom, while **Senior Data Scientist** leads with the highest pay. Median salaries show a big jump when moving from Analyst roles (~$70K–$130K) to Engineer/Scientist roles (~$130K–$170K), with Senior Data Scientist pushing even higher (~$150K–$180K).  

I also notice that Analysts have a much **narrower range**, which makes their salaries more predictable, but less rewarding. In contrast, Engineers and Scientists face **much wider spreads**, meaning opportunities for very high salaries exist, especially in top companies. The extreme outliers for Data Scientist and Data Engineer (reaching $500K–$600K) highlight how lucrative these roles can be in rare cases.  

Overall, the data shows that **moving from Analyst to Scientist/Engineer roles is the real game-changer** in terms of growth. Senior positions clearly pay more, but the Analyst-to-Scientist/Engineer jump offers the most dramatic salary boost. 

### Highest Paid & Most Demanded Skills for Data Analysts

#### Visualize Data 

```python
# Top 10 highest Paid Skills for Data Analysts
sns.set_theme(style="ticks")
sns.barplot(data=df_DA_top_pay, x='median',y=df_DA_top_pay.index,ax=ax[0], hue='median',palette='dark:b_r')

# Top 10 Most In-Demand Skills for Data Analysts
sns.barplot(data=df_DA_skills, x='median',y=df_DA_skills.index,ax=ax[1],hue='median',palette='light:b')

plt.show()

```

#### Results

![The Highesst Paid & Most In-Demand Skills for Data Analysts in the US](project\images\The_Highesst_Paid_and_Most_In_Demand_Skills_for_Data_Analysts_in_the_US.png)
*Two separate bar graphs visualizing the highest paid skills and mist in-ddemand skills for data analysts in the US.*


#### Insights

The charts reveal an interesting contrast between **highest paid skills** and **most in-demand skills** for Data Analysts.  

On the salary side, niche and specialized tools like **dplyr ($196K)**, **bitbucket ($189K)**, and **gitlab ($186K)** bring the highest pay, showing that rare technical expertise can significantly boost earnings. However, these skills are not the most widely required, which makes them lucrative but less common in the job market.  

On the demand side, core tools such as **Python ($97K)**, **SQL ($91K)**, and visualization platforms like **Tableau ($92K)** and **Power BI ($90K)** dominate. These are the practical must-have skills for most data analyst roles, but their median salaries are lower compared to the niche skills.  

Overall, the data suggests a clear trade-off:  
- **High demand skills** (Python, SQL, Tableau) secure more job opportunities but come with moderate pay.  
- **High paying skills** (dplyr, bitbucket, gitlab) are less common but can unlock exceptional salaries for those who master them.  


## 4. What is the most optimal skill to learn for Data Analysts?
 
#### Visualize Data

```python

sns.scatterplot(
    data=df_DA_skills_tech_high_demand,
    x='skill_percent',
    y='median_salary',
    hue='technology'
)

sns.despine()
sns.set_theme(style='ticks')

# Prepare texts for adjustText
texts = []
for i, txt in enumerate(df_DA_skills_high_demand.index):
    texts.append(plt.text(df_DA_skills_high_demand['skill_percent'].iloc[i], df_DA_skills_high_demand['median_salary'].iloc[i], txt))



# Set axis labels, title, and legend
plt.xlabel('Percent of Data Analyst Jobs')
plt.ylabel('Median Yearly Salary')
plt.title('Most Optimal Skills for Data Analysts in the US')
plt.legend(title='Technology')

from matplotlib.ticker import PercentFormatter
ax = plt.gca()
ax.yaxis.set_major_formatter(plt.FuncFormatter(lambda y, pos: f'${int(y/1000)}K'))
ax.xaxis.set_major_formatter(PercentFormatter(decimals=0))

# Adjust layout and display plot 
plt.tight_layout()
plt.show()

```
#### Results

![The Highesst Paid & Most In-Demand Skills for Data Analysts in the US](project\images\optimal_skills.png)
*A scatter plot visualizing the most optimal skills (high paying & high demand) for data analysis in the US.*


#### Insights

- **Most common ≠ highest salary**  
  - SQL is the most in-demand skill (55–60% of jobs) but doesn’t have the highest pay (~$90K).  
  - Python is less common (~30%) but commands the top salary (~$98K).  

- **Office tools = lower pay**  
  - Excel, Word, and PowerPoint are widely required, especially Excel (~45%), but they link to lower salaries ($82K–$85K).  
  - Relying only on these skills won’t maximize salary potential.  

- **Specialized database skills pay more**  
  - Oracle and SQL Server aren’t as common (~10–15%) but lead to higher salaries ($92K–$97K).  
  - Niche database expertise offers strong competitive advantage.  

- **Visualization tools are mid-range**  
  - Tableau and Power BI appear in 20–30% of jobs with salaries around $90K–$93K.  
  - They’re valuable but not as highly paid as Python or Oracle.  

- **Balance between demand and salary**  
  - For job security: SQL + Excel.  
  - For higher salary: Python + advanced databases (Oracle, SQL Server).  

---

# What I Learned
Through this project, I moved far beyond practicing code snippets and started to understand how data analysis works in practice.  
I learned how to approach problems step by step — from cleaning raw datasets, to applying the right Python libraries, to creating visuals that actually communicate insights.  

I also discovered the difference between *just running analysis* and *telling a story with data*.  
This meant comparing job roles, exploring skill trends, and linking technical results back to real business implications.  

On the technical side, I became more confident with Python libraries like **pandas, matplotlib, seaborn**, and with tools such as **Jupyter, Google Colab, Git, and GitHub**.  
On the analytical side, I developed the habit of asking better questions and structuring my work more clearly, so that each result leads logically to the next.
Overall, the biggest lesson was learning how to combine **technical skills** with **analytical thinking** to generate insights that are useful, not just correct.


# Overall Insights
- Success in data analysis comes from balancing **high-demand tools** (SQL, Excel, Tableau) with **high-value skills** (Python, advanced databases).
- Different roles (Analyst, Engineer, Scientist) require distinct skill mixes, which directly influence **salary** and **career trajectory**.
- Trends show traditional tools remain relevant, but **programming and cloud-oriented skills** are steadily becoming essential.
- The true edge is turning raw data into **clear, actionable insights** that drive real business impact.



# 📌 Conclusion  
This project was more than just practicing Python — it was about connecting technical skills to real-world questions.  
By exploring job roles, skill demand, salary trends, and optimal learning paths, I learned how to move from **raw data** to **meaningful insights**.  

The journey showed me that the real value of data analysis lies not only in writing code or making charts, but in **telling a story that supports decisions**.  
This is the mindset I’ll carry forward into future projects and my career path in data.  




