## Step 1. Create a GitHub Repo with README.md
Go to GitHub and create a new GitHub repo in your browser for Project 6 (use the name the specification requires). Be sure to add a default README.md when you first create the repository - it makes the easiest workflow.

## Step 2. Clone Repo
Copy the URL of your new GitHub repo into your clipboard (CTRL+A, then CTRL+C, or CMD if on Mac).
Open a Git Bash, Terminal, or PowerShell terminal in your Documents folder (the parent folder of where you want your repo) and type:  git clone paste_your_repo_URL_here

## Step 3.  Create a Project Virtual Environment
python3 -m venv .venv

## Step 4. Activate Project Virtual Environment
source .venv/bin/activate

## Step 5. Manage Your Project Requirements

## Step 6. Git Add and Commit Your Changes
.venv/
.gitignore - see the spec .gitignore for suggested contentsLinks to an external site. 
.venv/
.ipynb_checkpoints/
README.md
requirements.txt
git add .
git commit -m "initial commit"

## Step 7. Git Push To GitHub
git push origin main

## Choose Your Data Set
Choose one of the data sets and use it to practice all the skills that go into a Python Exploratory Data Analysis project. 
https://github.com/mwaskom/seaborn-data/blob/master/titanic.csv

## Document Your Data Set
Add a description of your dataset and a clickable link to your README.md file. Choose one of the following options. 
Option 1. Add Dataset Description & Link Locally - the Easy, Safe Way
Edit your README.md on your machine using VS Code, and git add, commit, and push your data addition to the GitHub repository. If you always edit on your machine, it's easy to keep things in sync with git add/commit/push and avoid dreaded merge conflicts.

## I wll be looking at the titanic data set from seaborn. It is a built in data set, so no other imports were needed. I displayed the head to help observe the data.

```bash
# Load the Titanic dataset
titanic_df = sns.load_dataset('titanic')

# Display the first few rows of the dataset
print(titanic_df.head())

#Downloaded the data set to a CSV
titanic_df.to_csv('titanic_dataset.csv', index=False)
```

## We will look at information pertaining to the death rates by gender and class.

## Graph of age distribution
```bash
# Bar graph of the age distribution
plt.figure(figsize=(6, 4))
sns.histplot(titanic_df['age'].dropna(), bins=30, kde=False)
plt.title('Age Distribution')
plt.xlabel('Age')
plt.ylabel('Count')
plt.show()
print(f'Average Age: {titanic_df.age.mean():.2f}')
print(f'Q1: {titanic_df.age.quantile(.25)}')
print(f'Q3: {titanic_df.age.quantile(.75)}')
```

## Graph of gender distribution
```bash
# Bar graph of the gender distribution
plt.figure(figsize=(2, 3))
ax = sns.countplot(data=titanic_df, x='sex')
plt.title('Gender Distribution')
plt.xlabel('Gender')
plt.ylabel('Count')

# Adding values on the bars
for p in ax.patches:
    ax.annotate(format(p.get_height(), '.0f'), 
                (p.get_x() + p.get_width() / 2., p.get_height()/2), 
                ha = 'center', va = 'center', 
                xytext = (0, 0), 
                textcoords = 'offset points')

# Assigns bar colors
colors = ['lightblue', 'hotpink']
for bar, color in zip(ax.patches, colors):
    bar.set_color(color)

plt.show()
print(f'Percent male: {round((577/(577+314)*100))}%')
print(f'Percent female: {round((314/(577+314))*100)}%')
```

## Graph of survivors by gender
```bash
# Bar graph of survivors by gender
plt.figure(figsize=(4, 4))
ax = sns.countplot(data=titanic_df, x='sex', hue='survived')
plt.title('Survival by Gender')
plt.xlabel('Gender')
plt.ylabel('Count')
plt.legend(title='Survived', labels=['No', 'Yes'])

# Adding values on the bars
for p in ax.patches:
    ax.annotate(format(p.get_height(), '.0f'), 
                (p.get_x() + p.get_width() / 2., p.get_height()/2), 
                ha = 'center', va = 'center', 
                xytext = (0, 0), 
                textcoords = 'offset points')

# Assigns bar colors
colors = ['red', 'red','lightblue', 'hotpink']
for bar, color in zip(ax.patches, colors):
    bar.set_color(color)

# Change legend colors
colors = ['lightblue', 'hotpink', 'red']
legend_labels = ['Male Survived', 'Female Survived', 'Died']
handles = [plt.Line2D([0], [0], marker='o', color='w', markerfacecolor=color, markersize=10) for color in colors]
ax.legend(handles, legend_labels, title='Gender')

plt.show()

print(f'Percent male Death: {round((468/(577)*100))}%')
print(f'Percent female Death: {round((81/(314))*100)}%')
```
## Graph of survivors by class
```bash
# Bar graph of class vs. survival
plt.figure(figsize=(6, 4))
ax = sns.countplot(data=titanic_df, x='class', hue='survived')
plt.title('Survival by Passenger Class')
plt.xlabel('Class')
plt.ylabel('Count')

# Adding values on the bars
for p in ax.patches:
    ax.annotate(format(p.get_height(), '.0f'), 
                (p.get_x() + p.get_width() / 2., p.get_height()/2), 
                ha='center', va='center', 
                xytext=(0, 0), 
                textcoords='offset points')

# Customize legend
colors = ['red', 'gold', 'silver', 'brown']
legend_labels =['died', 'Survived 1st-class', 'Survived 2nd-class','Survived 3rd-class']
handles = [plt.Line2D([0], [0], marker='o', color='w', markerfacecolor=color, markersize=10) for color in colors]
ax.legend(handles, legend_labels, title='Survival')

# Assigns bar colors
colors = ['red', 'red', 'red', 'gold', 'silver', 'brown']
for bar, color in zip(ax.patches, colors):
    bar.set_color(color)

plt.show()

print(f'Percent Death 1st class: {round((80/(80+136)*100))}%')
print(f'Percent Death 2nd class: {round((97/(97+87))*100)}%')
print(f'Percent Death 3rd class: {round((372/(372+119))*100)}%')
```

## Graph of survivors by class and gender
```bash
# Create a FacetGrid for the different classes
g = sns.FacetGrid(titanic_df, col='class', height=4, aspect=1.2)

# Create the bar plot on each facet
g.map_dataframe(sns.countplot, x='sex', hue='survived', palette='Set1')

# Add titles and labels
g.set_axis_labels("Sex", "Count")
g.add_legend(title='Deaths by Gender and Class', label_order=['died', 'survived'],labelcolor=['red', 'blue'])
g.set_titles(col_template="{col_name} Class")

# Add counts and percentages on the bars
for ax in g.axes.flat:
    for p in ax.patches:
        count = p.get_height()
        total = len(titanic_df[(titanic_df['class'] == ax.get_title().split()[0]) & (titanic_df['sex'] == p.get_x())])
        ax.annotate(f'{count}',
                    (p.get_x() + p.get_width() / 2., p.get_height()), 
                    ha='center', va='center', 
                    xytext=(0, 5), 
                    textcoords='offset points')

plt.show()

print(f'Percent Death 1st class Male: {round((3/(94)*100))}%')
print(f'Percent Death 1st class Female: {round((77/(122)*100))}%')
print(f'Percent Death 2nd class Male: {round((6/(76))*100)}%')
print(f'Percent Death 2nd class Female: {round((91/(108))*100)}%')
print(f'Percent Death 3rd class Male: {round((300/(347))*100)}%')
print(f'Percent Death 3rd class Female: {round((72/(144))*100)}%')
```
## Box plot of survival and ticket price
```bash
# Create the box plot
plt.figure(figsize=(5, 6))
sns.boxplot(data=titanic_df, x='survived', y='fare', showfliers=False, palette={0: 'red', 1: 'blue'})

# Add titles and labels
plt.title('Ticket Price vs. Survival Status')
plt.xlabel('Survived')
plt.ylabel('Ticket Price')
plt.xticks([0, 1], ['Died', 'Survived'])

plt.show()

```

## Source
## This project was built to the following specification:
- [datafun-06-eda](https://github.com/denisecase/datafun-06-spec)
