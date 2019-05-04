# mini_project-1
Slide Rule Mini Project With JSON
Finding the 10 countries with most projects
Findin the top 10 major project themes (using column 'mjtheme_namecode')

# Importing Necessary Libraries
import pandas as pd
import json
from pandas.io.json import json_normalize

# Importing JSON data to a variable dataset
dataset = pd.read_json('data/world_bank_projects.json')

# Checking the first 5 rows of dataset
dataset.head()

# Checking all the coulumns
dataset.columns

# Grouping by the Countries with their respective allocated Project
# Assign that groupby Object Count to a dataframe
countrywise_project_count = pd.DataFrame(dataset.groupby('countryname')['project_name'].count())

# Renaming the Count column to : Project Count
countrywise_project_count.columns = ['Project Count']

# Arranging the Data in Descending order & Extracting the max 10 values
countrywise_project_count.sort_values(by = ['Project Count'], ascending=False).head(10)

# Normalizing the dataset by mjtheme_namecode & extracting the top 10 value of based on theme
json_normalize(json.load(open('data/world_bank_projects.json')), 'mjtheme_namecode')['name'].value_counts()[:10]
