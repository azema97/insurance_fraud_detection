# 🕵️ Fraud Detection - Insurance Company project

An insurance company hires a team of data scientists to work as consultants in the fraud department. Currently, policies that are issued are monitored and any claims submitted are reviewed and evaluated, manually, to determine legitimacy and final approval for payment by the organization. 

**It is the role of the fraud team to determine which claims submitted should be approved and which should be should be rejected**.

Team's task is to answer the following question: **Are there particular trends in the groups of claims submitted that may be indicative of fraud?**

<img src='img/thumbnail.jpg' width='500' style='border: 1px solid grey;'>


---

### Data preview

The finance department has provided them with data on all recent claims made by 1,000 customers. The data is not labeled; that is, there is no variable to tell us which of these claims are fraudulent or not.

Data provided is a table, which fields (columns) are:
- **case_id**: A unique identifier for each insurance case or claim. This field is likely a numerical value that differentiates one case from another.
- **income**: The annual income of the individual associated with the insurance case. This field is represented as a floating-point number and indicates the financial status of the policyholder.
- **age**: The age of the individual associated with the insurance case. This is an integer value representing how old the person is.
- **sex**: The gender of the individual associated with the insurance case. It is likely represented as 'M' for male and 'F' for female.
- **approval**: The status of the insurance claim. This field indicates whether the claim was "Approved" or "Denied."
- **fraud**: A categorical field indicating whether the insurance claim is under investigation for fraud. It might show values like "No" for non-fraudulent claims and "Under Review" or "Fraud" for those under suspicion.
- **claims**: The monetary amount of the insurance claims made by the individual. This field is a floating-point number representing the total value of the claims. ​

Since this is a small and synthetic dataset, there are no null values that we need to take care of.
Also, there are no wrong categories inside categorical fields (fraud, sex and approval), or ages "out of normal range".

We can skip data cleaning process.

---

### Exploratory Data Analysis 🔎

Before analyzing any tendency available in monetary amounts, we need to confirm what is the distribution of the categorial fields of the data provided:

- In terms of sex, we almost have **equal quantity values of both genders** (507 females and 493 males).
- **79.7% insurance claims were approved**, while 20.3 % were rejected.
- **83% of the cases are registered as no fraud**, 11.5 % as fraud, and 5.5 % are under review.

<img src='img/distribution_of_fraud_categories.png' width='400' style='border: 1px solid grey;'>

<br>

- There are no significant differences in the distributions based on gender.
- We can observe a large group of claims around the income range of 20,000-45,000 (typical income values)
- There is a "strip" of claims with incomes between 45,000-100,000, worthing approximately 5,000 on average claims. It is not quite clear how to describe them, but they could be everyday things that wealthier people can deal with (for example, car accident claims).
- There is another strip of claims for at least 20,000 among people who only earn 10,000, which is unusual and may consist of fraudulent claims.

<img src='img/claims_vs_income_sexcolor.png' width='400' style='border: 1px solid grey;'>
<img src='img/claims_vs_income_fraudcolor.png' width='400' style='border: 1px solid grey;'>

<br>

- There is a range of people who earn 10,000 at all ages (minimum wage).
- There is a large group of people who earn between 30,000-40,000 at all ages (average salary)
- There are many people with higher incomes (60,000-100,000) just before the age of 60. At the age of 59 is when people in the U.S. can start withdrawing savings from their retirement accounts, so this may have something to do with this pattern.

<img src='img/income_vs_age_sexcolor.png' width='400' style='border: 1px solid grey;'>
<img src='img/income_vs_age_fraudcolor.png' width='400' style='border: 1px solid grey;'>

---

### Data Preprocessing ♻️

Data preprocessing is crucial in machine learning as it directly impacts the outcomes of any algorithm. Machine learning algorithms don't perform well when the input numerical attributes have very different scales. This is why it's better to scaled our data.

For this section we are going to use `MinMaxScaler()`, which is a python library designed for data preprocessing used to normalize or rescale features (numeric variables) to a fixed range, typically 0 to 1, or -1 to 1 if there are negative values in your data.

<img src='img/data_scaling.png' width='800'>

For categorical columns, since they are not numerical, we are going to use another type of encoding. 

One-hot encoding is a process of converting categorical data variables so they can be provided to machine learning algorithms to improve predictions. With one-hot, we convert each categorical value into a new categorical column and assign a binary value of 1 or 0. Each integer value is represented as a binary vector. 

Thankfully, Scikit-Learn provide us a solution for us if we import `OneHotEncoder()` scaler.

<img src='img/data_encoding.png' width='800'>

---
### Data Modelling 📝

We are going to train a **k-means clustering algorithm**. K Means is a widely used clustering algorithm in machine learning and data mining. Its goal is to divide a set of data into groups or clusters based on similarities among the data. The "K" in K Means represents the number of clusters that the algorithm should create. Since we preprocess our data, we can create several different models, using N columns. 

**We are going to split dataset into 4 groups, creating a model based on income and claims**. The reason of why I choose income and claims columns only is that, based from the insights from EDA, these are two fields that can explain answer better the question of team need to answer ("Are there particular trends in the groups of claims submitted that may be indicative of fraud?").

Since the purpose of this project is to determine fraudulent claims ourselves, we are going to drop fraud category columns.


<img src='img/final_analysis.png' width='500' style='border: 1px solid grey;'>

With this picture, we can determine 4 groups:

- **🔵 Blue group: High income and low claims**. These are likely ordinary claims made by affluent families. It is very likely that these are not fraudulent and that the insurer will accept them.
- **🟢 Green group: Moderate income with moderate claim values**. These are quite abundant and could be everyday items like car claims. They are most likely to be accepted.
- **🟠 Orange group: Moderate income and high claims**. This could be plausible if it's something that middle-income people need but can't always afford, but it is recommended to investigate this further.
- **🟡 Yellow group: Low income but very high claims**. These are clearly not affordable and could be attempts to get free cash. It is recommended to reject these.

---
### Conclusion

On this project we learned the importance of exploring our data before creating a model. Picking the correct or incorrect columns will determine the results of your machine learning model, and this will impact your business or organization sooner or later.

This is not only "running all of the scripts and see what is the result". Understanding the business, thinking outside of the box and being creative are some of the soft skills we need to have to provide a good data visualization, data model, data report or anything inside this area.