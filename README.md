# Factors-affecting-overweight-and-obesity

- The purpose of the project: To predict obesity/overweight risks amongst individuals based on various lifestyle factors
- Data source used: https://www.kaggle.com/datasets/kalpanatiwari30/dataset-for-obesity/data
- Data overview:
  +	Gender: Gender of patient
  +	Age: Age of patient
  +	Height: Height of patient
  +	Weight: Weight of patient
  +	Family_history_of_overweight: Family history of overweight
  +	FAVC: Frequent consumption of high caloric food
  +	FCVC: Frequency of consumption of vegetables
  +	NCP: Number of main meals
  +	CAEC: Consumption of food between meals
  +	SMOKE: Smoke
  +	CH2O: Consumption of water daily
  +	SCC: Calories consumption monitoring
  +	FAF: Physical activity frequency
  +	TUE: Time using technology devices
  +	CALC: Consumption of alcohol
  +	MTRANS: Transporatation used
  +	NObeyesdad: The categorical target
    
|index|id|Gender|Age|Height|Weight|family\_history\_with\_overweight|FAVC|FCVC|NCP|CAEC|SMOKE|CH2O|SCC|FAF|TUE|CALC|MTRANS|NObeyesdad|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|0|0|0|25|1\.7|81\.7|yes|0|2\.0|2\.983297|1|0|2\.763573|0|0\.0|0\.976473|1|3|Overweight\_Level\_II|
|1|1|1|18|1\.56|57\.0|yes|0|2\.0|3\.0|2|0|2\.0|0|1\.0|1\.0|0|0|Normal\_Weight|
|2|2|1|18|1\.72|50\.2|yes|0|1\.880534|1\.411685|1|0|1\.910378|0|0\.866045|1\.673584|0|3|Insufficient\_Weight|
|3|3|1|21|1\.72|131\.3|yes|0|3\.0|3\.0|1|0|1\.674061|0|1\.467863|0\.780199|1|3|Obesity\_Type\_III|
|4|4|0|32|1\.92|93\.8|yes|0|2\.679664|1\.971472|1|0|1\.979848|0|1\.967973|0\.931721|1|3|Overweight\_Level\_II|
|5|5|0|19|1\.75|51\.6|yes|0|2\.919751|3\.0|1|0|2\.13755|0|1\.930033|1\.0|1|3|Insufficient\_Weight|
|6|6|0|30|1\.76|112\.8|yes|0|1\.99124|3\.0|1|0|2\.0|0|0\.0|0\.696948|1|0|Obesity\_Type\_II|
|7|7|0|30|1\.76|118\.3|yes|0|1\.397468|3\.0|1|0|2\.0|0|0\.598655|0\.0|1|0|Obesity\_Type\_II|
|8|8|0|17|1\.7|70\.0|no|0|2\.0|3\.0|1|0|3\.0|1|1\.0|1\.0|0|3|Overweight\_Level\_I|
|9|9|1|26|1\.64|111\.3|yes|0|3\.0|3\.0|1|0|2\.632253|0|0\.0|0\.218645|1|3|Obesity\_Type\_III|

- Tool and technologies applied
  + Data cleaning: Handle missing values, correct data types, and remove duplicates.
    +To check the value Null
    ```
    df.isnull().sum()
    ```
  + EDA: Generate summary statistics, visualize distributions, and explore relationships between variables.
  + Analysis: Perform correlation analysis
  + Visualization: Create visualizations such as bar charts, histograms, and heatmaps to support the analysis.
  + Data storytelling: Present the findings
    
## Key insights discovered
  ### The disease classification
df["NObeyesdad"].value_counts()

  ### To overview the distribution of disease classsication by Alcolhol Use Frequency for Males
male_data = df[df['Gender'] == 0]
disease_distribution = male_data.groupby(['CALC', 'NObeyesdad']).size().reset_index(name='Count')
print(disease_distribution)
plt.figure(figsize=(10, 6))
sns.barplot(data=disease_distribution, x='CALC', y='Count', hue='NObeyesdad', palette='viridis')
plt.title('Distribution of Disease Classification by Alcohol Use Frequency for Males')
plt.xlabel('Alcohol Use Frequency (CALC)')
plt.ylabel('Count')
plt.xticks(rotation=45)
plt.legend(title='Disease Classification')
plt.tight_layout()
plt.show()

  ### To overview the distribution of disease classsication by Alcolhol Use Frequency for Females
female_data = df[df['Gender'] == 1]
disease_distribution_female = female_data.groupby(['CALC', 'NObeyesdad']).size().reset_index(name='Count')
print(disease_distribution_female)
plt.figure(figsize=(10, 6))
sns.barplot(data=disease_distribution_female, x='CALC', y='Count', hue='NObeyesdad', palette='viridis')
plt.title('Distribution of Disease Classification by Alcohol Use Frequency for Females')
plt.xlabel('Alcohol Use Frequency (CALC)')
plt.ylabel('Count')
plt.xticks(rotation=45)
plt.legend(title='Disease Classification')
plt.tight_layout()
plt.show()

  ### Top 20 Who has Highest Weight
top_20_weights = df.sort_values(by="Weight", ascending=False).head(20)
print(top_20_weights)

  ### Top 10 Age Groups with Highest Total Weight
  plt.figure(figsize=(10, 6))
plt.style.use('seaborn-darkgrid')

df.groupby("Age")["Weight"].sum().sort_values(ascending=False).head(10).plot(kind="bar", color='skyblue')

plt.xlabel("Age", fontsize=12)
plt.ylabel("Total Weight (kg)", fontsize=12)
plt.title("Top 10 Age Groups with Highest Total Weight", fontsize=14)
plt.xticks(rotation=45, ha='right')

for i, v in enumerate(df.groupby("Age")["Weight"].sum().sort_values(ascending=False).head(10)):
    plt.text(i, v + 1, str(v), ha='center', va='bottom', fontsize=10)

plt.tight_layout()
plt.show()

  ### Distribution of Survey Respondents
df['Age'].value_counts()
  
  ### Distribution of CAEC Values
df['CAEC'] = df['CAEC'].replace({0: 'No', 1: 'Sometimes', 2: 'Frequently', 3: 'Always'})
plt.figure(figsize=(8, 6))
caec_labels = df['CAEC'].unique()
colors = ['#7fcdbb', '#41b6c4', '#2c7fb8']
caec=df["CAEC"].value_counts().plot(kind="pie",autopct='%1.1f%%', colors=colors, startangle=140)
plt.title('Distribution of CAEC Values')
plt.gca().set_aspect('equal')
plt.legend(labels=caec_labels, loc='best')
plt.tight_layout()
plt.show()

  ### Distribution of CALC Values
``
df['CALC'] = df['CALC'].replace({0: 'No', 1: 'Sometimes', 2: 'Frequently'})
plt.figure(figsize=(8, 6))
caec_labels = df['CALC'].unique()
colors = ['#D04B18', '#EE8C3D', '#EFB87E']
caec=df["CALC"].value_counts().plot(kind="pie",autopct='%1.1f%%', colors=colors, startangle=140)
plt.title('Distribution of CALC Values')
plt.gca().set_aspect('equal')
plt.legend(labels=caec_labels, loc='best')
plt.tight_layout()
plt.show()

  ### The Correlation between Variables to Obesity/Overweight
```
correlation=df[["Gender","Height","Weight","Age","FAVC","FCVC","NCP","CAEC","SMOKE","CH2O","SCC","FAF","TUE","CALC","MTRANS"]].corr()
plt.figure(figsize=(10, 6))
sns.heatmap(correlation, annot=True, cmap="coolwarm", fmt='.2f', square=True, cbar=True)
plt.xticks(rotation=45)
plt.yticks(rotation=45)
plt.title('Correlation Matrix')
plt.tight_layout()
plt.show()
```

- Recommendations based on analysis results
  + Need to distribute survey objects more evenly across all ages.
  + Need to increase the use of bicycles, instead of the other means of transportation
  + Limit alcohol usage at all ages.
  + Healthy diet
  + Do exercise regularly
  + Drink enough water

