# PRODIGY_DS_05
In this task, I analyzed incident patterns by mapping the Diabetes dataset variables to real-world risk factors such as time, conditions, and contributing elements. Visualizations helped identify high-risk patterns and hotspots, strengthening my analytical and problem-solving skills.
def time_group(age):
    if age < 30:
        return 'Morning'
    elif age < 50:
        return 'Afternoon'
    else:
        return 'Night'

df['Time_of_Day'] = df['Age'].apply(time_group)
df['Time_of_Day']

def weather(glucose):
    if glucose < 120:
        return 'Clear'
    elif glucose < 160:
        return 'Rainy'
    else:
        return 'Foggy'

df['Weather'] = df['Glucose'].apply(weather)
df['Weather']

def road(bmi):
    if bmi < 25:
        return 'Dry'
    elif bmi < 30:
        return 'Wet'
    else:
        return 'Slippery'

df['Road_Condition'] = df['BMI'].apply(road)

df['Road_Condition']

df['Outcome'].value_counts().plot(kind='bar')
plt.xlabel('Accident (0 = No, 1 = Yes)')
plt.ylabel('Count')
plt.title('Accident Occurrence Distribution')
plt.show()


pd.crosstab(df['Time_of_Day'], df['Outcome']).plot(kind='bar')
plt.xlabel('Time of Day')
plt.ylabel('Number of Accidents')
plt.title('Accidents by Time of Day')
plt.show()

pd.crosstab(df['Weather'], df['Outcome']).plot(kind='bar')
plt.xlabel('Weather Condition')
plt.ylabel('Number of Accidents')
plt.title('Accidents by Weather Condition')
plt.show()

pd.crosstab(df['Road_Condition'], df['Outcome']).plot(kind='bar')
plt.xlabel('Road Condition')
plt.ylabel('Number of Accidents')
plt.title('Accidents by Road Condition')
plt.show()


hotspots = df[df['Outcome'] == 1].groupby(
    ['Time_of_Day', 'Weather', 'Road_Condition']
).size().sort_values(ascending=False)

hotspots.head()

