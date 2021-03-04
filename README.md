# People Analytics : Project Overview
* Goal : 
	- Getting valuable insight from the data.
	- Create machine learning classification model to help decion maker in HR Department for predicting Employee Performance.
* Methodology :
	- Data Preprocessing
	- Exploratory Data Analysis
	- Model Building
* Conclusion
* Data source : https://www.kaggle.com/c/bri-data-hackathon-pa/data
* This Project based on [**BRI Data Hackathon 2021**](https://brihackathon.id/) competition.

# Data Overview
- Data Shape : 11153 rows × 22 columns
- Columns : `job_level`, `job_duration_in_current_job_level`, `person_level`, `job_duration_in_current_person_level`, `job_duration_in_current_branch`, `Employee_type`,
	    `gender`, `age`, `marital_status_maried(Y/N)`, `number_of_dependences`, `Education_level`, `GPA`, `year_graduated`, `job_duration_from_training`, `branch_rotation`,
	    `job_rotation`, `assign_of_otherposition`, `annual leave`, `sick_leaves`, `Last_achievement_%`, `Achievement_above_100%_during3quartal`, **`Best Performance`**.

	- For more detail about data description please refer to [data source link](https://www.kaggle.com/c/bri-data-hackathon-pa/data).

# Data Preprocessing
- Remove rows with Null value
- Transform `age` column. For this column the data is employees year born. In order to get employees age, we subtract current year by year of birth
- Transform `year_graduated`. We do the same as trasforming `age` column.
- Transform `GPA` columns. Normally GPA values are between 0.00 to 4.00. In this particular column, `GPA` values lies between 0.00 to 378.00 wich is not normal. In order to fixed this, we filter the data by `job_level` & its normal `GPA` values (0.00-4.00) and then took its median for each of the `job_level`. After that we replaced `GPA` values that are not normal with the median.

	***GPA before transformed***
	<br>
	<br>
	![boxplot gpa before](/master/images/boxplot%20GPA%20before.png "boxplot gpa before")

	***Median Value for normal GPA by job level***
	<br>
	<br>
	![gpa by job level](/images/boxplot%20normal%20GPA%20by%20joblevel.png "gpa by job level")

	***GPA after transformed***
	<br>
	<br>
	![boxplot gpa after](/master/images/boxplot%20GPA%20after.png "boxplot gpa after")


- Manipulate `Best Performance` column.
	- For employee who has `Last_achievement_%` >= 100% & `Achievement_above_100%_during3quartal` = 3, I considered it as a Best Performer. Thus for employees with those categories but has 0 on his `Best Performance` columns, I changed it to 1
	- For employee who has `Last_achievement_%` < 100% & `Achievement_above_100%_during3quartal` = 0, I considered it as a Non Best Performer. Thus for employees with those categories but has 1 on his `Best Performance` columns, I changed it to 0


# EDA
After doing Preprocessing data, On this step we are looking for valuable insight from the data by visualized it with `matplotlib` & `seaborn`.

Below are some examples of the insights I've got:
<br>
![job_level](/images/Employee%20by%20joblevel.png "job_level")
<br>
<br>
![best by job_level](/master/images/Employee%20Best%20performance%20by%20joblevel.png "best by job_level")

# Model Building
First, I transformed the categorical variables into label encoder & dummy variables. I also split the data into train and tests sets with a test size of 30%.   

I tried two different models and evaluated them using accuracy. I chose Accuracy because it is relatively easy to interpret.

- **Logistic Regression**, accuracy : 93%
- **Random Forest Classifier**, accuracy : 98%

# Conclusion
- As beginner data scientist and without having backgroud expertise in Human Resource, I asumed `Last_achievement_%` & `Achievement_above_100%_during3quartal`are fundamental metrics to assess amployee performeance. Thus i manipulated `Best Performance` column on data preprocessing.
- Despite I got very high score on model accuracy, it does not mean this model is perfect. To optimized the model I am very welcome for the critics & feedback.




[Go to my GitHub Pages](https://abdurrahmanshidiq.github.io/People_Analytics/)
