# Robotic Investment for Lending Club Background 

                                    
## Summary
As data is playing an important role in the financial field, lots of trades and investment are supported by robust models and algorithms. The modern investment relies on models with a better win rate than intuition, or we call these models as financial technology. For example, if the bank needs to estimate whether people will pay off the mortgage, it will collect the information including collateral, tax forms, income, credit rates, credit card paid-back condition. Although banks have their own models, which require many criteria such as the value of collateral, quantity of asset, impact of the economic condition and etc., the current evaluation benchmarks grow complex with the development of big data. There are many possible attributes and weakly correlated features we can reach. For example, even the level of aggressiveness of comments on the social network can be a variable added to the model. As more information gathered, institutions can get a model with more predictive power.

There is no free lunch since trades come with risks. As people know, banks in the US normally provide an extremely low-interest rate, which barely equals to zero on saving. On the other side, traditional banks are only willing to loan when the amount is over 30k with collaterals. To fulfill the desire that people want to have a mortgage below 30k to get through the financial difficulties, the market of peer to peer(P2P) lending is growing.

Lending Club, an online P2P platform provides personal loans to borrowers with good credit and solid income. It is the first and largest online lender for personal loans in the United States, having facilitated more than $33.6 billion in loans since it was founded in 2007.

Lending Club enables applicants to borrow between $1,000 and $40,000. The standard loan period is three years. Investors can search and browse the loan listings on Lending Club website and select applicants that they are interested in based on the information supplied by platform, including borrower's income, amount of loan, loan grade, and loan purpose. Investors make money on the paid interest from applicants. Lending Club makes money by charging borrowers origination fees and service fees.

Although Lending Club has already helped investors to separate the credit grade of borrowers according to payback risks, investors still face potential default risks. Furthermore, sometimes borrowers come with lower interest rate and high credit grade will default and on the other hand, some borrowers with a high interest and lower credit grade can fully pay their debt. According to Lending club’s investigation, if investors choose borrowers randomly, there will be a 20% chance that the chosen one can default if the purchased notes of loan are less than 100. 

How to decrease the default rate except purchasing more notes on the platform? We are designing a model for investors to predict whether the customer will fully pay their debt on Lending Club so that to decrease the possible default rate. 



## Process:

### Data ETL: 
Download the data of 2014 and 2015 from lending club website and read from the local path. Choosing these two years is because most of the loans with a term of three years have had a result, which can be our label. 



### Data preparation and cleansing: 
Prepare the data by dealing with NaN values, categorical and numerical features. 

•	Through checking the data, there are too many NAN values in the dataset for some features (over 50%) and we should delete them. 

•	Check the categorical features, we can see the following features are needed to be reformatted:


  o	Suppose to be numerical (term, int_rate, etc.). 

  o	extremely unbalanced (pymnt_plan, application_type, etc.).

  o	date-time features.

  o	include only one value and has no meaning to exist in features.

  o	contained many values but duplicated values due to capitalized words.


•	Check the numerical data and drop the ones with high correlation (>90%).



### Exploratory Data Analysis: 
Through EDA, we take business insights from features to get a better understanding on the project, for example,

•	home_ownership: Only a small portion of applicants owns the home and they are less likely to default. “ANY” provides very limited information on the result so we can drop the column. 

•	debt_settlement_flag: When there is a flag, the applicant is 100% default. In that case, no matter how less the flag is, we need to keep it. 



### Feature engineering: 
Feature combining, expanding and encoding

•	For categorical features with many unique values such as zip code and areas, transfer to the frequency to decrease the dimension.

•	Check features if we can import data outside the website to improve performance. Here, we import the state’s average income from US census.

•	Label encode features such as grade and subgrade to ranks as numbers.

•	One-hot encodes other categorical features to dummy variables.




## Build Models:
Split train, test and validate data set to build models. 

•	If using logistic regression, the data needs to be scaled. 

•	XGBoost doesn’t need to be scaled and provides feature importance.

The accuracy improved 0.2% by switching from logistic regression to XGboost.  







