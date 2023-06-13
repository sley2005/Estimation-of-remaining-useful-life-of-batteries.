# Remaining-useful-life-estimation--Battery
## Project summary
This project aims to predict how much longer a battery can be used before it reaches the end of its life, using only voltage and current measurements. When the battery's capacity cannot be directly measured, we rely on these measurements to estimate its remaining useful life (RUL). By developing a machine learning model, we can analyze patterns in the voltage and current data to make accurate predictions about the battery's future performance. This information is valuable for various applications, such as battery health monitoring in remote locations, ensuring optimal usage of batteries in devices, and predicting potential failures before they occur.
## DATA
A summary of the data you’re using, remembering to include where you got it and any relevant citations. 
The data I am using  is the HNEI Hawaii Natural Energy Institute NMC-LCO 18650 Battery Dataset is a publicly available resource created by the University of Hawaii at Manoa. It was developed to support battery model development, control algorithm research, and the study of battery safety and reliability. The dataset includes measurements from over 1000 NMC-LCO 18650 cells, covering voltage, current, temperature, resistance, and state of health information. The data was collected between 2013 and 2014, focusing on degradation variability in Li-ion batteries.
The dataset underwent preprocessing by Ignacio Vinuales, who created seven features for predicting the remaining useful life (RUL). These features were used in training the model for this project. There feature where:
•	Discharge Time (s)
•	Time at 4.15V (s)
•	Time Constant Current (s)
•	Decrement 3.6-3.4V (s)
•	Max. Voltage Discharge (V)
•	Min. Voltage Charge (V)
•	Charging Time (s)
Distribution: The dataset has been distributed through the battery archive website, https://www.batteryarchive.org/list.html, and GitHub. It is subject to the Creative Commons Attribution 4.0 International License.
Maintenance: The dataset is currently maintained by Ignacio Vinuales and Battery archive. The GitHub repository (https://github.com/ignavinuales/Battery_RUL_Prediction) and the HNEI website (https://www.batteryarchive.org/faq.html) provide additional information and support for the dataset.

## MODEL 
A summary of the model you’re using and why you chose it. 
The Random Forest Regression algorithm was chosen to predict the remaining useful life (RUL) of batteries. I initially implemented several regression models using default parameters and the Random Forest algorithm performed best. It is a powerful ensemble learning method that combines multiple decision trees to make accurate predictions.
I chose the Random Forest model for this project because of the initial performance seen and it offers several advantages. Firstly, it can handle both numerical and categorical features, making it suitable for the diverse set of input variables we have, such as voltage and current measurements. Additionally, Random Forest models are less prone to overfitting compared to individual decision trees, which helps to generalize well to unseen data.
Moreover, Random Forest models are robust to outliers and missing data, allowing us to work with real-world battery datasets that may contain noise or incomplete information. The ensemble nature of the model also provides built-in feature importance measures, enabling us to identify the most influential variables for RUL prediction.

## HYPERPARAMETER OPTIMSATION
Description of which hyperparameters you have and how you chose to optimise them. 
The hyperparameters  used for the RandomForestRegressor model are:
•	n_estimators: The number of decision trees in the random forest.
•	max_depth: The maximum depth of each decision tree.
•	min_samples_split: The minimum number of samples required to split an internal node.
•	min_samples_leaf: The minimum number of samples required to be at a leaf node.
The number of potential combinations for these hyper parameters is quite high so Bayesian optimisation was used. A random search was used to find the initial set of datapoints to be used for the baysian optimisation process.  The optimization process iteratively selects candidate hyperparameters based on Upper confidence bounds criterion and evaluates their performance using the mean squared error (MSE). The process continues for a specified number of iterations, updating the best MSE and hyperparameters along the way.
Finally, the best hyperparameters are used to train a final random forest model, and its performance is evaluated on the test data using the MSE metric. The MSE indicates how well the model predicts the RUL values, with lower values indicating better performance.

## RESULTS
A summary of your results and what you can learn from your model 

You can include images of plots using the code below:
![Screenshot](image.png)

## (OPTIONAL: CONTACT DETAILS)
If you are planning on making your github repo public you may wish to include some contact information such as a link to your twitter or an email address. 

