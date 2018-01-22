# Market-Trend-Prediction

This is a course project of Building Knowledge Graph. The goal of this project is to predict the trend of the Dow Jones Industrial Average (DJIA) based on the integration of historical stock prices of the 30 component companies of DJIA and general opinions towards them extracted from social media posts and news reports.

## Approach

### Data Collection

1. **Sturctured data**: leveraging official APIs to crawl historical stock price data from Yahoo Finance and posts from Facebook and Twitter.
2. **Unstructured data**: using [ACHE](https://github.com/ViDA-NYU/ache) to scrape Business Insider articles and Reddit financial threads.
3. Product golssary: the names of products of each company were collected from [DBpedia](http://wiki.dbpedia.org), [Wikipedia](https://www.wikipedia.org) and their official websites. The glossary may not be exhaustive but was sufficient enough for the project purpose.

Data collecting range: Aug 1, 2016 to Nov 30, 2017.  
Training data range: Aug 1, 2016 to Oct 31, 2017.  
Number of records: Business Insider (2,017), Reddit Finance (4,383), Facebook (11,528), Yahoo Finance(10,478), Twitter (24,271).

### Data Manipulation

1. Data cleaning: filter out only the content, namely articles, posts and web pages, relating to the DJIA 30 component companies. This is done by fuzzy string matching company names and their corresponding product names with text from each post or web page.
2. Information extraction: utilize NLP to determine the opinion polarities of articles and posts, followed by properly tagging along with the corresponding company name.
3. Data integration: combine and organize data from different sources into one CSV file for machine learning, and another several JSON Lines files for generating knowledge graph in [myDIG](https://github.com/usc-isi-i2/dig-etl-engine).

### Prediction Results
1. Please refer to [this link](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/Dow%20Jones%20Industrial%20Average%20Prediction%20with%20Media%20Channel%20Info-with%20Social%20Info.ipynb) for the Jupyter code of prediction results with social media information as part of the input features.
2. Please refer to [this link](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/Dow%20Jones%20Industrial%20Average%20Prediction%20without%20Social%20media%20data.ipynb) for the Jupyter code of prediction results without including social media features.

```text
                Next-day Prediction

              precision    recall  f1-score   support

Decrease       0.00      0.00      0.00         7
Increase       0.70      1.00      0.82        16

avg / total    0.48      0.70      0.57        23

               Next-month Prediction

              precision    recall  f1-score   support

Increase       1.00      1.00      1.00        23

avg / total    1.00      1.00      1.00        23 
```

### Program list

|Program|Description|Link|
|------|------|--------|
|[JSONLines](https://github.com/Cheng-Lin-Li/KnowledgeGraph/tree/master/CDR_JSONLines)|Json Lines aggregate all of the crawled web pages into a single file, each line of which is a single JSON object representing one page.| [Source Code](https://github.com/Cheng-Lin-Li/KnowledgeGraph/blob/master/CDR_JSONLines/jsonlines.py)|
|[JSONLines Content Classifier](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/classify.py)|Process a JSON Lines file to a new one containing only the records relevant to Dow 30 companies based on glossary. New tags containing company and product names will be added to HTML body to make it convenient for [Inferlink](https://github.com/inferlink/extraction). [NLTK](http://www.nltk.org) was used for determining opinion polarity while [RLTK](https://github.com/usc-isi-i2/rltk) was adopted to perform fuzzy string matching.|[Source Code](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/classify.py)|
|[Data Integration](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/dataintegration.py)| This program combines the daily stock prices of and public opinions about the Dow 30 companies in the aforementioned data range into one CSV file as the input of training prediction model. |[Source Code](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/dataintegration.py)|
|[Facebook Crawler for Dow30](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/facebook-crawler-dow30.py)| This script is to crawl Facebook posts via Facebook graph API. A special Facebook ID and Dow 30 companies dictionary are integrated into this version. A CSV file with numbers of likes and dislikes will be generated for machine learning. |[Source Code](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/facebook-crawler-dow30.py)|
|[Yahoo Crawler for Dow30](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/yahoo_quote_crawler.py)| This crawler scrapes Yahoo Finance stock prices via Yahoo API. A special ticker ID and Dow 30 companies dictionary are integrated into this version. A CSV with full company names will be generated for machine learning purpose.|[Source Code](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/yahoo_quote_crawler.py)|
|[Twitter Crawler for Dow30](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/tweetScraper.py)| This script utilizes official API to scrape posts of the offcial Twitter accounts of the Dow components. |[Source Code](https://github.com/Cheng-Lin-Li/Market-Trend-Prediction/blob/master/source/tweetScraper.py)|

### Team members

[Cheng-Lin Li](https://github.com/Cheng-Lin-Li/) & [YuCheng Guo](https://github.com/li0near)

### Date: Project kick off date

Oct., 2017@University of Southern California

## Contact Information

Cheng-Lin Li: chenglil@usc.edu  
Yucheng Guo: yuchengg@usc.edu
