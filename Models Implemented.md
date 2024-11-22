# Section 1

**File:** `Will-K-Means.ipynb`

**Goal**: Generate clusers using K-Means for data in `primary.csv`.

**Reason**: After our Data Exploration phase and visualizing correlations (or the lack thereof) with different numerical variables revealed that it might be difficult to find any strong explanatory variables from our scraped dataset. For this reason, our first step was to generate clusters of data from a K-Means approach, to try and discern whether our dataset contained any identifiable groups with relevant features that would be worth predicting.

**Preprocessing:**\
Before implementing the K-Means model, some processing had to be done on the dataset. Below is a snippet of what the dataset looked like before processing:

![1](milestone-3-visualizations/1.png)

Note that this snippet does not contain all columns of the dataset. 

<i>Transformation</i>

Notice the presence of many columns containing long strings or dictionaries of text information. K-Means models can only be conducted with numerical data. Our data contained a column called ‘sentiment’ with string values containing a numerical score along with explanations and other indicators of sentiment, such as numbers of positive/negative words within each article. It was decided that sentiment score might be a useful attribute to try and create clusters from, so the numerical part of this string needed to be separated. This numerical score was first extracted and put into a new column with the following code:  



text **test** 2

*test*

> test
>
> test 2

test

1. test
2. test

_test_

1. test

![Profiles](visualizations/profiles.png)

<a href="https://wihi1131.github.io/Data-Mining-Project/">Home</a>
