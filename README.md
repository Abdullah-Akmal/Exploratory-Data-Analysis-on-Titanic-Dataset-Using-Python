# Titanic-Eda

## Description
### Inspecting Dataset Information and Shape:

In this code snippet, we are performing two key tasks:
1. **Getting Basic Info**: We use the `.info()` method to obtain concise details about the DataFrame such as the number of non-null entries, data types of each column, and memory usage.
2. **Shape of the Dataset**: We use `.shape` to get the dimensions (rows and columns) of the dataset. This is useful for understanding the size of the dataset before diving into analysis.

#### Output:
- **`df.info()`**: Provides an overview of the dataset, including data types and missing values.
- **`df.shape`**: Returns the number of rows and columns as a tuple `(rows, columns)`.

## Methodology / Steps
- ### Loading the Titanic Dataset:

This code snippet reads a CSV file containing the Titanic dataset into a pandas DataFrame and displays the first 10 rows. The Titanic dataset contains information about passengers who were aboard the Titanic, including details like their class, age, fare, and whether they survived.

#### Steps:
1. **Reading CSV File**: We use `pd.read_csv()` to load the dataset from a specified file path.
2. **Viewing Data**: The `.head(10)` function is used to display the first 10 rows of the DataFrame. This helps us get a quick overview of the structure of the data.
- ### Analyzing Missing Data:

This code snippet calculates the number of missing values in each column and their percentage representation. It then displays the results in a DataFrame, sorted by the percentage of missing values.

#### Steps:
1. **Count of Missing Values**: We use the `isnull()` function followed by `.sum()` to calculate the total number of missing values per column.
2. **Percentage of Missing Values**: We calculate the percentage of missing values by using `isnull().mean()` and multiplying by 100 to convert it into a percentage.
3. **Creating a DataFrame**: The results are stored in a new DataFrame, `missing_df`, with two columns: 'Missing Values' and 'Percentage (%)'.
4. **Sorting the Results**: We use `.sort_values()` to sort the columns by the percentage of missing data, in descending order.

#### Output:
- The final result is a sorted list of columns with missing data, starting from the column with the highest percentage of missing values.
``
- ### Dropping Columns with High Percentage of Missing Values:

In this code, we are removing columns from the DataFrame that have more than 60% missing values. This helps in cleaning the dataset by eliminating features that are too incomplete to be useful for analysis.

#### Steps:
1. **Identify Columns with High Missing Data**: We use the `percent_missing` variable to find columns with more than 60% missing values.
2. **Drop Columns**: The `.drop()` method is applied to remove these columns from the DataFrame.
3. **Display Remaining Columns**: Finally, we check the remaining columns using `.columns`.

#### Output:
- The result is a DataFrame without the columns that had more than 60% missing values.
- ### Imputing Missing Values in the 'Age' Column:

In this code, we are filling the missing values in the 'Age' column with the **median** of the non-missing values in the same column. Imputation helps retain the row data without losing any rows due to missing values.

#### Steps:
1. **Impute Missing Data with Median**: The missing values in the 'Age' column are replaced with the median value of the column, using the `.fillna()` method.
2. **Verify the Imputation**: We use `.isnull().sum()` to check if there are any remaining missing values in the dataset.

#### Output:
- The result will show that there are no more missing values in the 'Age' column after the imputation.
- ### Generating Summary Statistics of the Dataset:

The `describe()` function provides a quick overview of the statistical summary of numerical columns in the dataset. Transposing the result (`.T`) allows us to view the summary statistics for each column in a more readable format.

#### Steps:
1. **Generate Descriptive Statistics**: The `describe()` method generates summary statistics for numeric columns like count, mean, standard deviation, min, and max values, along with quartiles (25%, 50%, and 75%).
2. **Transpose the Output**: The `.T` transposes the result, flipping rows and columns, making it easier to read when working with many features.

#### Output:
- A transposed table will display key statistics such as mean, standard deviation, minimum, maximum, and percentiles for each numeric column in the dataset.
- ### Handling Outliers in 'Age' and 'Fare' Columns Using IQR:

In this code, we handle the outliers in the 'Age' and 'Fare' columns by applying the **Interquartile Range (IQR)** method. Outliers are defined as values that fall outside of the acceptable range determined by the IQR.

#### Steps:
1. **Calculate the IQR**: For each of the columns ('Age' and 'Fare'), we calculate the first (Q1) and third quartile (Q3), and then compute the IQR (difference between Q3 and Q1).
2. **Define Outlier Bounds**: Using the IQR, we define the lower and upper bounds as `lower_bound = Q1 - 1.5 * IQR` and `upper_bound = Q3 + 1.5 * IQR`.
3. **Collect Outliers (Optional)**: We identify the outliers, which are values outside these bounds. This is done using a filtering condition.
4. **Clip the Values**: To handle the outliers, we "clip" the values within the bounds, effectively replacing any values below the lower bound with the lower bound and any values above the upper bound with the upper bound.

#### Output:
- The dataset will have its outliers in the 'Age' and 'Fare' columns clipped to the defined bounds. The statistical summary of the columns will be updated, and outliers will no longer skew the data.
- ### Exploring Categorical Features Using `df.describe(include="O")`:

In this section of the code, we explore the descriptive statistics for categorical columns in the dataset using the `describe()` function with the `include="O"` parameter.

#### Steps:
- **`df.describe(include="O")`**: This command generates a summary of statistics for **object** (categorical) columns. Object columns typically include strings, dates, or any data type that isn't numeric.
- **Why Use `include="O"`?**: By default, `df.describe()` provides statistics for numeric columns. To focus on categorical features, we use `include="O"`, which targets object (categorical) data types.
- **Key Statistics Provided**:
  - **`count`**: The number of non-null entries in each categorical column.
  - **`unique`**: The number of unique categories or values within the column.
  - **`top`**: The most frequent category or value.
  - **`freq`**: The frequency (count) of the most common category.

#### Output:
- The output will give you insights into the distribution and frequency of categorical features, helping in understanding the diversity of values and identifying potential issues such as rare categories.
- ### Mapping Categorical Values in the 'Embarked' Column:

In this section of the code, we map the abbreviated port names in the **'Embarked'** column to their full names using a dictionary. The `replace()` function is used to transform the abbreviations into more meaningful values.

#### Steps:
- **`embark_mapping = {'S': 'Southampton', 'Q': 'Queenstown', 'C': 'Cherbourg'}`**: We define a dictionary where each key corresponds to an abbreviated port name, and the associated value is the full name of the port.
- **`df['Embarked'] = df['Embarked'].replace(embark_mapping)`**: The `replace()` function is used to apply this dictionary transformation to the 'Embarked' column. This will replace all occurrences of 'S' with 'Southampton', 'Q' with 'Queenstown', and 'C' with 'Cherbourg'.
- **`df['Embarked'].value_counts()`**: This returns the count of each unique value in the 'Embarked' column after the transformation, allowing us to verify the changes.

#### Why do we do this?
- The transformation makes the data more readable by replacing the abbreviated port names with their full names. This enhances the interpretability of the data, especially in a real-world analysis or report.
- ### Creating a Pivot Table to Analyze Survival Rate by Sex and Pclass:

In this section, we create a **pivot table** to explore the relationship between survival rates (`Survived`) and the two categorical variables, **'Sex'** and **'Pclass'**.

#### Steps:
- **`df.pivot_table(values='Survived', index='Sex', columns='Pclass', aggfunc='mean')`**: This line of code creates a pivot table from the Titanic dataset using the following:
  - **`values='Survived'`**: We are interested in the survival status of passengers, which is represented by the **'Survived'** column. We will aggregate this data by calculating the mean survival rate for different groups.
  - **`index='Sex'`**: The pivot table will have rows grouped by the passengers' **sex** (either male or female).
  - **`columns='Pclass'`**: The pivot table will have columns grouped by the **Pclass** (passenger class), which is an ordinal feature (1st, 2nd, or 3rd class).
  - **`aggfunc='mean'`**: The aggregation function applied is the **mean**, which calculates the average survival rate for each combination of **Sex** and **Pclass**.

- **`print(pivot_table1)`**: Finally, the pivot table is printed to display the results.

#### Why do we do this?
- The pivot table allows us to examine how survival rates differ across different **passenger sexes** and **classes**. This provides insights into the factors that may have influenced survival, such as gender and class.
- ### Creating a Pivot Table to Analyze the Average Age by Survival Status:

In this section, we create a **pivot table** to examine the average age of passengers who survived and those who did not survive.

#### Steps:
- **`df.pivot_table(values='Age', index='Survived', aggfunc='mean')`**: This line of code generates a pivot table that calculates the average age of passengers grouped by their survival status.
  - **`values='Age'`**: The target column for aggregation is **'Age'**. We want to calculate the average age for each survival group.
  - **`index='Survived'`**: The rows of the pivot table are grouped by **'Survived'**, so the data will be split into two groups: passengers who survived (1) and those who did not survive (0).
  - **`aggfunc='mean'`**: The aggregation function used is **mean**, which calculates the average age for each survival group.

- **`print(pivot_table2)`**: The pivot table is printed to display the results, showing the average age for each group (survived vs. not survived).

#### Why do we do this?
- This analysis allows us to compare the average age of passengers who survived and those who did not survive. It can help us understand if age had any significant impact on survival chances.
- ### Bar Chart for Passenger Class Distribution:

In this section, we generate a **bar chart** to visualize the distribution of passengers across different passenger classes.

#### Steps:
- **`sns.countplot(x='Pclass', data=df)`**: This line of code creates a **countplot**, which is a type of bar plot used to show the frequency of occurrences for each class in the **'Pclass'** column.
  - **`x='Pclass'`**: This specifies that we want to visualize the distribution based on the **'Pclass'** column, which represents the passenger class (1st, 2nd, and 3rd class).
  - **`data=df`**: This tells seaborn to use the DataFrame `df` for plotting.

- **`plt.title("Passenger Class Distribution")`**: Sets the title of the chart to "Passenger Class Distribution."

- **`plt.xlabel("Pclass (1=1st class, 2=2nd Class, 3=3rd class)")`**: This sets the x-axis label, indicating what each number in the **'Pclass'** column represents (1st, 2nd, and 3rd class).

- **`plt.ylabel("Count")`**: Sets the y-axis label to indicate that we are counting the number of passengers in each class.

- **`plt.show()`**: Displays the plot.

#### Why do we do this?
- The bar chart helps to quickly understand the distribution of passengers across the three classes, giving insights into which class had the most or least passengers.
- ### Bar Chart for Gender Distribution:

In this section, we generate a **bar chart** to visualize the distribution of passengers by gender.

#### Steps:
- **`sns.countplot(x='Sex', data=df)`**: This line of code creates a **countplot**, which is a bar plot used to show the frequency of occurrences for each gender in the **'Sex'** column.
  - **`x='Sex'`**: This specifies that we want to visualize the distribution based on the **'Sex'** column, which represents the gender of passengers.
  - **`data=df`**: This tells seaborn to use the DataFrame `df` for plotting.

- **`plt.title("Gender Distribution")`**: Sets the title of the chart to "Gender Distribution."

- **`plt.xlabel("Sex")`**: This sets the x-axis label to "Sex", indicating that we are visualizing gender.

- **`plt.ylabel("Count")`**: Sets the y-axis label to indicate that we are counting the number of passengers for each gender.

- **`plt.show()`**: Displays the plot.

#### Why do we do this?
- The bar chart helps to quickly understand the gender distribution of passengers, which could be insightful when analyzing survival rates across genders.
- ### Bar Chart for Port of Embarkation:

This section visualizes the distribution of passengers across different embarkation ports using a **bar chart**.

#### Steps:
- **`sns.countplot(x='Embarked', data=df)`**: This creates a **countplot** (a type of bar chart) to show the frequency of passengers who boarded at each port.
  - **`x='Embarked'`**: This specifies that the **'Embarked'** column is used to categorize passengers by their embarkation port (Southampton, Queenstown, Cherbourg).
  - **`data=df`**: This tells seaborn to use the `df` DataFrame to plot the data.

- **`plt.title("Port of Embarkation")`**: This sets the title of the chart to "Port of Embarkation" for context.

- **`plt.xlabel("Port")`**: This labels the x-axis to indicate the embarkation port where passengers boarded the Titanic.

- **`plt.ylabel("Count")`**: This labels the y-axis to show the number of passengers at each port.

- **`plt.show()`**: This displays the plot.

#### Why do we do this?
- The bar chart allows us to quickly identify the number of passengers that embarked from each of the three ports: Southampton, Queenstown, and Cherbourg. It helps in understanding the distribution of passengers before analyzing other factors like survival rates or demographics.
- ### Bar Chart for Survival by Gender:

This section visualizes the survival distribution based on **gender** using a **bar chart**.

#### Steps:
- **`sns.countplot(x='Sex', hue='Survived', data=df)`**: This creates a **countplot** to show the number of survivors (and non-survivors) by gender.
  - **`x='Sex'`**: This specifies that the x-axis will represent the **'Sex'** column, categorizing the passengers by gender (Male and Female).
  - **`hue='Survived'`**: This separates the bars by survival status (0 = No, 1 = Yes), allowing us to visualize the number of survivors and non-survivors within each gender group.
  - **`data=df`**: This tells seaborn to use the `df` DataFrame for the data.

- **`plt.title("Survival by Gender")`**: This sets the title of the plot to "Survival by Gender", providing context for what the chart represents.

- **`plt.xlabel("Sex")`**: This labels the x-axis to indicate the gender of the passengers.

- **`plt.ylabel("Count")`**: This labels the y-axis to show the count of passengers for each category.

- **`plt.legend(title='Survived', labels=['No','Yes'])`**: This customizes the **legend** by giving it a title "Survived" and labels 'No' for non-survivors and 'Yes' for survivors.

- **`plt.show()`**: This displays the plot.

#### Why do we do this?
- The bar chart helps us quickly compare the number of survivors and non-survivors based on gender. It offers insights into whether one gender had a higher survival rate than the other.
- ### Histogram for Age Distribution:

This section visualizes the distribution of passengers' **ages** using a **histogram**.

#### Steps:
- **`sns.histplot(df['Age'], bins=20, kde=False, color='skyblue')`**: This command creates a histogram for the **'Age'** column in the dataset.
  - **`df['Age']`**: This specifies that the **Age** column of the DataFrame `df` will be plotted.
  - **`bins=20`**: This divides the data into 20 bins, which determines the number of bars in the histogram. Adjusting the number of bins can change the resolution of the distribution.
  - **`kde=False`**: This disables the Kernel Density Estimate (KDE) plot, meaning only the histogram (bar chart) is shown without the smoothed curve.
  - **`color='skyblue'`**: This sets the color of the bars to **skyblue**, giving the chart a light, aesthetically pleasing tone.

- **`plt.title("Age Distribution")`**: This sets the title of the plot to "Age Distribution", indicating that the plot represents the age distribution of passengers.

- **`plt.xlabel("Age")`**: This labels the x-axis as "Age", indicating that the horizontal axis represents passengers' ages.

- **`plt.ylabel("Count")`**: This labels the y-axis as "Count", showing the number of passengers in each age bin.

- **`plt.show()`**: This displays the plot.

#### Why do we do this?
- The histogram helps to understand the **distribution** of passengers' ages. It gives an insight into how many passengers were in different age groups.
- We can use this chart to analyze the age distribution (e.g., if there were more children or elderly passengers) and check for **outliers** or skewness in age.
- ### Histogram for Fare Distribution:

This section visualizes the distribution of passengers' **fares** using a **histogram**.

#### Steps:
- **`sns.histplot(df['Fare'], bins=30, kde=False, color='lightgreen')`**: This command creates a histogram for the **'Fare'** column in the dataset.
  - **`df['Fare']`**: Specifies that the **Fare** column of the DataFrame `df` will be plotted.
  - **`bins=30`**: This divides the fare data into 30 bins, determining the number of bars in the histogram. Adjusting the number of bins can affect the chart’s resolution.
  - **`kde=False`**: Disables the Kernel Density Estimate (KDE) plot, so only the histogram (bar chart) is shown.
  - **`color='lightgreen'`**: The bars of the histogram will be colored **light green**, providing a softer visual tone.

- **`plt.title("Fare Distribution")`**: Sets the title of the plot to "Fare Distribution," clearly indicating the data being visualized.

- **`plt.xlabel("Fare")`**: Labels the x-axis as "Fare," indicating that the horizontal axis represents the fare prices passengers paid.

- **`plt.ylabel("Count")`**: Labels the y-axis as "Count," showing the number of passengers in each fare bin.

- **`plt.show()`**: Displays the plot.

#### Why do we do this?
- The histogram helps to understand the **distribution** of the fares passengers paid. It shows the number of passengers who paid fares in specific ranges.
- This chart can help identify **outliers**, patterns in the fare distribution, and possible **skewness** in the fare prices (e.g., many passengers paying low fares, with a few paying high fares).

## Tools & Libraries Used
#, ##, ###, ####, 'Age',, 'Fare'., 'Fare']].corr()`**:, 'Fare']]`**:, 'Parch',, 'Pclass',, 'SibSp',, 'Survived',, (EDA),, (perfect, (rounded, (working, **Compute, **Correlation, **Insights, **Pearson, **Plot, **Title, **`.corr()`**:, **`annot=True`**:, **`cmap="coolwarm"`**:, **`corr, **`corr`**:, **`df[['Survived',, **`fmt=".2f"`**:, **`plt.figure(figsize=(6,5))`**:, **`plt.show()`**:, **`plt.title("Correlation, **`sns.heatmap(corr,, **`vmin=-1,, **correlations**, **heatmap**., **matplotlib.pyplot**:, **numpy**:, **pandas**:, **seaborn**, **seaborn**:, **warnings**:, +1, -, -1, 0, 1., 2, 2., 3., 4., 5., =, A, Adds, Adjusts, Analysis**:, By, Computes, Correlation, Correlation**:, Correlations:**, DataFrame, DataFrames)., Dataset, Defines, Display:**, Displays, Features")`**:, Features:, Heatmap, Heatmap:**, Imported:, Kagle, Libraries, Manages, Numeric, Plots, Provides, Selects, Sets, Source:, Specifies, Steps:, Strong, The, This, Titanic, Used, Why, `df`., `matplotlib`., a, analysis, analysis., analyzing, and, annot=True,, ant, are, array, avoid, basic, be, between, built, calculates, can, cells, cells., clarity., clean,, clutter, cmap="coolwarm",, coefficient**, coefficients, color, colors, columns, columns:, command, cooler, correlated, correlation, correlation), correlation),, correlation., correlations, correlations., data, dataset, datasets,, decimal, df[['Survived',, do, each, engineering, ensuring, essential, exploratory, feature, features, features., figure, fmt=".2f",, for, format, from, further, graphing., handling., heatmap, heatmap,, heatmap., help, highly, how, https://www.kaggle.com/competitions/titanic/data, ideal, identify, ignores, important, in, indicate, indicating, ing, is, it, learning, libraries, library, machine, make, manipulation, manner., matplotlib.pyplot, matrix, matrix., maximum, may, might, minimum, models., more, negative, no, non-intrusive, not, np, numbers, numeric, numerical, numpy, of, on, operations, or, other., output., palette, pand, patterns, pd, performing, places)., plotted., plotting, plt, positive, provides, ranges, readable., related, relationships, relevant, represent, representation, results, scale,, seaborn, section, selection, setup, size, sns, specified, statistical, support, that, the, this?, title, to, top, using, values, variables,, various, visual, visualization, visualize, visualizes, visualizing, vmax=1)`**:, vmax=1`**:, vmin=-1,, warmer, warnings, warnings.filterwarnings('ignore'), we, where, which, with, within, working
