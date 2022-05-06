# BDA-Group-11

## Team Members
- Bharath Kumar Reddy Bhoothpur [Leader]
- Teja Vijayudu Rayankula
- Chandana Sai Sri Chirra 
- Nikhil Reddy Muppidi 
- Poojith Chandra Borra

## Communication Plan
We plan on communicating via email, text and Discord. We will schedule Zoom meetings every Sunday to share ideas.

## Data Resource
The data that we plan to work with is the New York City Taxi and Limousine Commission (TLC) Trip Record Data.
The dataset contains data of trips taken by taxis and for-hire vehicles in New York City.

Data Source: https://registry.opendata.aws/nyc-tlc-trip-records-pds/

## Business Problem or Opportunity, Domain Knowledge

Pick-up and drop-off dates/times, pick-up and drop-off locations, trip distances, itemized rates, rate kinds, payment types, and driver-reported passenger counts are all captured in the yellow and green cab trip records. 
Technology providers authorized under the Taxicab and Livery Passenger Enhancement Programs (TPEP/LPEP) collected and supplied the data utilized in the linked datasets to the NYC Taxi and Limousine Commission (TLC). The trip data was not created by TLC, and TLC provides no warranties or representations about its correctness.

The For-Hire Vehicle (“FHV”) trip records include fields capturing the dispatching base license number and the pick-up date, time, and taxi zone location ID (shape file below). These records are generated from the FHV Trip Record submissions made by bases. Note: The TLC publishes base trip record data as submitted by the bases, and we cannot guarantee or confirm their accuracy or completeness. Therefore, this may not represent the total amount of trips dispatched by all TLC-licensed bases. The TLC performs routine reviews of the records and takes enforcement actions when necessary to ensure, to the extent possible, complete and accurate information.

## Research Objectives and Questions
We plan on analysing the data thoroughly and will find any existing trends and relationships that are present in the dataset.

We will then perform predictive analysis on the dataset.

## Narrated Presentation of the project we worked so far
https://youtu.be/9w9z8sgOWB8

## Future work and comments
The data that we used was pretty clean and most of the data is well captured. There were a few NaNs which we replaced with 0s. The feature variable for our models was the trip duration. We had to manually calculate the data for that column by calculating the difference between the dopoff time and the pickup time. For our evaluation, we fit the model on our training data and predicted values on our testing data. We then measured the RMSE on the testing feature data.
We did this for a total of three models, namely, Linear Regression, Logistic Regression and Poisson Regression. The best value and performance out of all these seemed to be of the Linear Regression Model. We did face a few problems while running the models on our models but we didn't clean the data properly. We then took our time to clean the data and changed all the values.
For our future work, we plan on looking into more models and try to reduce the RMSE value even further to find a model that will fit the data better.

# Instructions for running the notebook

## Setup conda packages dependencies
For running distributed dask on SageMaker laptop and fargate cluster, we need more conda packages and newer versions of a few existing packages. Integration of scikit-joblib learn's with dask for distributed dask cluster level processing requires version 0.23. Dask and popular machine learning libraries like Scikit-Learn, XGBoost, and others are used in dask-ml to deliver scalable machine learning in Python. Cloudpickle 1.6.0 is necessary to serialize Python constructs that are not supported by the Python standard library's default pickle module.

**Follow the steps below to install conda_daskpy36 kernel**
1. Open Jupyter > New > Terminal
2. Open text editor e.g. vi and enter the script below
3. Save the file as daskpy36.sh
4. Give run permissions: chmod +x daskpy36.sh
5. Run the script: ./daskpy36.sh

=======script begin===========
!/bin/bash
set -e
sudo -u ec2-user -i << EOF
echo ". /home/ec2-user/anaconda3/etc/profile.d/conda.sh" >> ~/.bashrc
conda create --name daskpy36 python=3.6.10 dask=2.14 distributed=2.14 s3fs=0.4.0 dask-glm=0.2.0 cytoolz=0.8.2 pandas=1.0.1 scikit-learn=0.23.2 matplotlib dask-ml=1.6.0 ipykernel -y
source /home/ec2-user/anaconda3/bin/activate daskpy36
python -m ipykernel install --user --name daskpy36 --display-name conda_daskpy36
source /home/ec2-user/anaconda3/bin/deactivate
EOF
=======script end===========
