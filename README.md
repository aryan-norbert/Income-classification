# People with the highest education level, and who are either husbands or wifes make more money



## Table of Contents

- [Business problem](#business-problem)
- [Data source](#data-source)
- [Methods](#methods)
- [Tech Stack](#tech-stack)
- [Quick glance at the results](#quick-glance-at-the-results)
- [Lessons learned and recommendation](#lessons-learned-and-recommendation)
- [Limitation and what can be improved](#limitation-and-what-can-be-improved)
- [Run Locally](#run-locally)
- [Explore the notebook](#explore-the-notebook)
- [Deployment on streamlit](#deployment-on-streamlit)
- [App deployed on Streamlit](#app-deployed-on-streamlit)
- [Repository structure](#repository-structure)
- [Contribution](#contribution)



## Business problem

This an app to predict if someone make more or less than 50k/year using different features. 
This app can be used when that information is not available or is confidential during a loan application at any financial institution or car financing application to have a better financial picture of the applicant.
## Data source

- [Kaggle Income classification](https://www.kaggle.com/lodetomasi1995/income-classification) (Main dataset)
- [GDP group dataset](https://www.kaggle.com/nitishabharathi/gdp-per-capita-all-countries) (Dataset used to enriched the main dataset with the countrie's GDP grouping)
## Methods

- Exploratory data analysis
- Bivariate analysis
- Multivariate correlation
- Feature engineering
- Feature selection
- S3 bucket model hosting
- Model deployment
## Tech Stack

- Python (refer to requirement.txt for the packages used in this project)
- Streamlit (interface for the model)
- AWS S3 (model storage)


## Quick glance at the results

Most correlated features to the target.

![heatmap](https://github.com/aryan-norbert/Income-classification/blob/main/heatmap.png)

Confusion matrix of random forest (Best estimator with the best parameters)

![Confusion matrix](https://github.com/aryan-norbert/Income-classification/blob/main/confusion_matrix.png)

ROC curve of random forest (Best estimator with the best parameters)

![ROC curve](https://github.com/aryan-norbert/Income-classification/blob/main/roc.png)

Top 5 models after hyper parameter tuning

| Model     	        | Precision score 	|
|-------------------	|------------------	|
| Random Forest     	| 87% 	            |
| Neural Network    	| 81% 	            |
| KNN               	| 83% 	            |
| Gradient Boosting 	| 90% 	            |
| Bagging           	| 87% 	            |

- ***The final model used is: Random forest classifier***
- ***Metrics used: Precision (87%)***
- ***Why choosing random forest yet gradient boosting had 90%, well because Gradient boosting was overfitting***
- ***Why choose precision as metrics: Because a financial instituation would rather get make sure that the people the loan is given do actually make more than 50k. Even though that it means approving fewer applicants. Thus prioritizing precision over recall.***


## Lessons learned and recommendation

- Based on the analysis on this project, we found out that the education level and type of relationship are the most predictive features to determine if someone makes more or less than 50K. Other features like Capital gain, hours work and age are also usefull. The least usefull features are: their occupation and the workclass they belong to.
- Recommendation would be to focus more on the most predictive feature when looking at the applicant profile, and pay less attention on their occupation and workclass.
## Limitation and what can be improved

- Speed: since the model is stored on AWS S3, it can take some few seconds to load. Solution: cache the model with the Streamlit @st.experimental_singleton for faster reload.
- Dataset used: the dataset used is from 1990, inflation has not been taken into consideration and the countries's economies have changed since then. Solution: retrain with a more recent dataset.
- Hyperparameter tuning: I used RandomeSearchCV to save time but could be improved by couple of % with GridSearchCV.


## Run Locally
Initialize git

```bash
git init
```


Clone the project

```bash
git clone https://github.com/semasuka/Income-classification.git
```

enter the project directory

```bash
cd Income-classification
```

Create a conda virtual environment and install all the packages from the environment.yml (recommended)

```bash
conda env create --prefix <env_name> --file assets/environment.yml
```

Activate the conda environment

```bash
conda activate <env_name>
```

List all the packages installed

```bash
conda list
```

Start the streamlit server locally

```bash
streamlit run income_class_st.py
```
If you are having issue with streamlit, please follow [this tutorial on how to set up streamlit](https://docs.streamlit.io/library/get-started/installation)

## Explore the notebook

To explore the notebook file [here](https://nbviewer.org/github/semasuka/Income-classification/blob/master/Income_Classification.ipynb)

## Deployment on streamlit

To deploy this project on streamlit share, follow these steps:

- first, make sure you upload your files on Github, including a requirements.txt file
- go to [streamlit share](https://share.streamlit.io/)
- login with Github, Google, etc.
- click on new app button
- select the Github repo name, branch, python file with the streamlit codes
- click advanced settings, select python version 3.9 and add the secret keys if your model is stored on AWS or GCP bucket
- then save and deploy!

## App deployed on Streamlit

![Streamlit GIF](https://github.com/aryan-norbert/Income-classification/blob/main/gif_streamlit.gif)

Video to gif [tool](https://ezgif.com/)
## Repository structure


```

├── confusion_matrix.png        <- confusion matrix image used in the README.
├── gif_streamlit.gif           <- gif file used in the README.
├── heatmap.png                 <- heatmap image used in the README.
├── Income_classification_banner.png   <- banner image used in the README.
├── environment.yml             <- list of all the dependencies with their versions(for conda environment).
├── roc.png                     <- ROC image used in the README.
├── GDP.csv                     <- the data used to feature engineering/enriched the original data.
├── test.csv                    <- the test data.
├── train.csv                   <- the train data.
│
├── income_class_profile.html   <- exported panda profile html file.
│
│
├── .gitignore                      <- used to ignore certain folder and files that won't be commit to git.
│
│
├── Income_Classification.ipynb     <- main python notebook where all the analysis and modeling are done.
│
│
├── LICENSE                         <- license file.
│
│
├── income_class_st.py              <- file with the best model and best hyperparameter with streamlit component for rendering the interface.
│
│
├── README.md                       <- this readme file.
│
│
├── requirements.txt                <- list of all the dependencies with their versions(used for Streamlit ).

```
## Contribution

Pull requests are welcome! For major changes, please open an issue first to discuss what you would like to change or contribute.

