# The Analysis

## 1. What are the most demanded skills for the top 3 most popular data roles?

To do this, first I filtered out the most popular job titles among all the data job roles and then get the top 5 skills required for each of the job roles. This query can be used as a highlighted as for which skills to focus more when applying for a specific job title.

View my notebok with detailed steps here:
[Skills_demand.ipynb](Project/Skills_demand.ipynb)

### Visualize Data

```python

fig, ax = plt.subplots(len(job_titles), 1)

sns.set_theme(style='ticks')

for i, job_title in enumerate(job_titles):
    df_plot = df_skills_percent[df_skills_percent['job_title_short'] == job_title].head(5)
    sns.barplot(data=df_plot, x='skills_percent', y='job_skills', ax=ax[i], hue='skill_count', palette='dark:b_r')
    ax[i].set_title(job_title)
    ax[i].set_xlabel('')
    ax[i].set_ylabel('')
    ax[i].set_xlim(0,80)
    ax[i].legend().set_visible(False)
    
    for n, v in enumerate(df_plot['skills_percent']):
        ax[i].text(v+1, n, f'{v:.0f}%', va='center')
    
    if i != len(job_titles) -1:
        ax[i].set_xticks([])

fig.suptitle('Likelihood of Skills in requested in Job postings', fontsize=15)
fig.tight_layout(h_pad=0.5)
plt.show()
```

### Results

![visualization of the top skills](Project/Images/skill_demand.png)

### Insights

## 2. How are in-demand skills trending for Data Analysts?

### Visualise Data

### Results

![trend of the skills](Project/Images/skills_trend.png)

## 3. How well do jobs and skills pay for Data Analysts?

### Salary Analysis

### Visualize Data

```python
sns.boxplot(data=df_US_Top6, x='salary_year_avg', y='job_title_short', order=job_order)

plt.title('Salary Distribution in US')
plt.xlabel('Yearly Salary ($USD)')
plt.ylabel('')
ax = plt.gca()
ax.xaxis.set_major_formatter(plt.FuncFormatter(lambda x, pos: f'${int(x/1000)}K'))

plt.xlim(0, 600000)
plt.show()
```
