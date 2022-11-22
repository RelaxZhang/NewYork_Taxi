# MAST30034 Project 1 - Quantitative Analysis
- Student Name: Chi Zhang
- Student ID: 1067750
- Due Date: Monday 16th of August 11:59:00 am (AEST).
- Report Link: https://www.overleaf.com/read/gbfynwfmxjys


# Dependencies
- Language: Python 3.8.3 (written in Jupyter Notebook)
- Packages / Libraries: Packages need pip install: pyarrow, geopandas


# Datasets
- NYC TLC: https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page

- External dataset 1: https://www.meteoblue.com/en/weather/archive/export/new-york_united-states-of-america_5128581
  This external data's csv file is already downloaded to ../raw_data/raw folder
  
- External dataset 2: https://data.cityofnewyork.us/Health/COVID-19-Daily-Counts-of-Cases-Hospitalizations-an/rc75-m7u3
  This external data is downloaded and already downloaded to ../raw_data/raw folder


# Directory
Structure of the submitted repository
- `raw_data`: Contains two folders including: "raw", "first_preprocess"
    
    `raw` folder contains: raw data of yellow taxis' records from 2019.12~2020.11, covid raw data, weather raw data, shape file of taxis
    
    `first_preprocess` folder contains: first_preprocessed taxi data (already merge the columns of covid and comfort_index data)
    
- `preprocessed_data`: Contains two folders including "geospatial_data", "model_data"
    
    `geospatial_data` folder contains: generated csv files (after all preprocessing steps) for plotting the geo-spatial graph
    
    `model_data` folder contains: generated csv files (after all preprocessing steps) for fitting and testing the linear model
    
- `plots`: folder contains: plots of distribution of target value, correlation heatmap between features, pairplots, geo-spatial graph in html format

- `code`: Six Jupyter Notebook & How to run the Code
    - Notebook "Download_Data": Download raw data csv files of yellow taxi (running this code is not recommended)
      
      As this code takes too long to download files, download by hand from website is recommended
      
      website: https://www1.nyc.gov/site/tlc/about/tlc-trip-record-data.page (Download 2019.12~2020.11 Yellow Taxi csv files)
      
    - Notebook "ExternalPreprocess": Read in external datasets and create preprocessed external data for merging usage
      1. Run the first block to load, preprocess and create new covid.csv file for merging usage
      2. Run the second block to load, preprocess and create new comfortIndex.csv file for merging use
      3. It takes around 30 seconds to proceed the code
      
    - Notebook "CleanMerge": Read in raw data and preprocessed external datasets to do preprocessing
      
      Main functionality: drop irrational instance & remove useless columns (features) & merge raw data with external datasets
      1. Run the first block to load raw yellow taxis' data and two preprocessed external data
      2. Run the second and fourth blocks to load the function of cleaning, merging and constructing first_preprocessed csv files
      3. Run the third and fifth blocks to run the two functions
      4. It takes around 13~15 minutes to proceed the code
      
    - Notebook "FinalPreprocess": Read in first_preprocessed data file to do outliers removing and generate visualisation plots
      
      Main functionality: drop outliers, plot distribution plot of target feature, plot correlation heatmap
      
      Main functionality: remove uncorrelated features, generate csv files for geo-spatial plotting and model construction
      1. Run the first block to load first_preprocessed data
      3. Run the second block to remove outliers from training and test sett base on selected feature
      4. Run blocks 3~5 to generate distribution plot for tip, tip & simulate normal distribution and log(tip)
      5. Run block 6 to generate correlation heatmap for all features
      6. Run block 7 to drop uncorrelated columns proven by the data from block 8's correlation heatmap data
      7. Run block 8 to convert the payment_type columns into one-hot encoding style and drop payment_type feature
      8. Run block 9 to generate concise correlation heatmap to investigate the interested features
      9. Run block 10 to plot pairplots between target (tip_amount) with interested features (predictors)
      10. Run block 11 to remove the redundent features which has perfect correlation with the features of interest
      10. Run block 12 to generate preprocessed csv file for geo-spatial graph drawing
      11. Run blocks 13-14 to remove the useless features for model construction and generate csv for model fitting and testing
      12. It takes around 5 minutes to proceed the code
      
    - Notebook "Geospatial": Read in preprocessed data for geo-spatial graphing and generate graph for tip_amount and tip_duration_ratio
      
      Main functionality: generate geo-spatial graphs for tip & pickup zone, tip_duration_ratio & pickup zone
      1. Run blocks 1-3 to install Packages pyarrow and geopandas before running the following blocks
      2. Run blocks 4-5 to import libraries and load csv files as well as file for generating geo-spatial graph
      3. Run blocks 6-7 to merge location data with taxi data and create json type data
      4. Run blocks 8-10 to generate dataframe of average tip_amount and scaled average tip_amount and print out top five zones
      5. Run blocks 11-12 to generate geo-spatial plots of tip, scale_tip in pickup zones
      6. It takes aronud 3 minutes to proceed the code
    
    - Notebook "TipAmount_Model": Read in preprocessed data for model construction and generates linear model for predicting tip_amount
      
      Main functionality: Operate feature selection (Backward), fit and test the linear model with training and test sets
      1. Run blocks 1-2 to import libraries and load in preprocessed data
      2. Run block 3 to observe the summary of model and operate backward elimination base on p-values (alpha = 0.05)
      3. Run block 4 to remove feature "covid_count" and observe the summary of model (no elimination is needed)
      4. Run blocks 5-7 to plot the learning curve of the linear model with stratificied subsample of training set (10%)
      5. Run block 8 to fit the linear model with stratified training set (10%) 
      6. Run block 9 to test and score the model with stratified test set (10%), print out the score (R2), coefficients and intercept of the linear model
      7. It takes around 7 minutes to proceed the code
      
- `deprecated`: A folder to store "old code" (No code is included in this folder)


# Other
# Tips for running the Jupyter notebooks
- Notebook "Download_Data" is not recommended to run as it takes too long to download files (download by hand link is provided above)
- Run the Notebook in the order:
  "ExternalPreprocess" -> "CleanMerge" -> "FinalPreprocess" -> "Geospatiao" -> TipAmount_Model
- Once the "finish" is printed (only included in some block which takes a bit longer to run), the next block can be run or process finish
- Run the code (blocks) in each Jupyter Notebook following the order provided above
- All raw, first_preprocessed, preprocessed taxi data and plots are not included in this project repository
- Only external raw data for covid, weather, taxi_zone information files are included in this project repository "raw" folder
- Once the above Jupyter notebooks are run, the preprocessed data and plot would be generated to its allocated folder described above
- the `requirements.txt` file only include lines for pip install packages for geo-spatial graphing
  (these packages should be installed by running the blocks described in "Geospatial" notebook without this txt file)