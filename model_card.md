# Model Card

Prediction of Remaining Useful Life (RUL) of Batteries.
## Model Description

The goal of this project is to develop a machine learning model that can accurately predict the remaining useful life (RUL) of a battery using only voltage (V) and current (A) measurements, in cases where direct measurement of the battery's capacity (mAH) is not available. The RUL represents the estimated time or usage remaining before the battery reaches a predefined end-of-life condition.
In various applications such as battery health monitoring, IoT devices, electric vehicles, portable electronics, and unmanned aerial vehicles (UAVs), the estimation of RUL becomes crucial when direct capacity measurement is impractical or not feasible. This project aims to address this challenge by leveraging the readily available voltage and current measurements to estimate the battery's RUL accurately.
Battery health monitoring is particularly important when batteries are deployed in remote or inaccessible locations. In such scenarios, direct measurement of battery capacity may not be possible, but voltage and current measurements can be easily obtained. By analyzing and monitoring the voltage and current levels over time, we can develop a machine learning model that captures the underlying patterns and dependencies between these variables and the battery's remaining useful life. This enables us to track the battery's performance and anticipate potential failures or degradation in its useful life.

## Input:

The model takes several inputs to make predictions:
Cycle Index: It represents the number of cycles the battery has undergone. This input provides information about the battery's usage history, allowing the model to consider the effect of repeated charge and discharge cycles on the remaining useful life.
- **F1: Discharge Time (s)**: This input denotes the duration of the battery's discharge process. It measures the time it takes for the battery to discharge its stored energy completely. This information helps the model understand the discharge behavior and estimate the remaining useful life based on the discharge patterns.
- **F2: Time at 4.15V (s)**: It indicates the time duration during which the battery voltage remains around 4.15V. This input is useful in understanding the battery's charging behavior and its voltage stability at a specific level. It contributes to predicting the remaining useful life based on the time spent in the desired voltage range.
- **F3: Time Constant Current (s)**: This input represents the time duration for which the battery operates under constant current conditions. It helps capture the battery's performance during constant current discharge, providing insights into its capacity degradation and estimating the remaining useful life accordingly.
**F4: Decrement 3.6-3.4V (s)**: It refers to the time it takes for the battery voltage to decrease from 3.6V to 3.4V during discharge. This input contributes to understanding the discharge characteristics and estimating the remaining useful life based on the voltage decrement rate.
- **F5: Max. Voltage Discharge (V)**: It represents the maximum voltage achieved by the battery during the discharge process. This input reflects the battery's performance and provides insights into its discharge capacity. The model considers this information to estimate the remaining useful life based on the maximum discharge voltage attained.
- **F6: Min. Voltage Charge (V)**: This input indicates the minimum voltage observed during the battery's charging process. It helps the model understand the charging behavior and estimate the remaining useful life based on the minimum charging voltage reached.
- **F7: Charging Time (s)**: It denotes the duration of the battery's charging process. This input provides information about the time taken to recharge the battery fully. It contributes to estimating the remaining useful life based on the charging patterns and time spent in the charging process.
   
## Output:

- **Remailing useful life**

## Model Architecture:

The model architecture being used in the code is a Random Forest Regressor combined with Bayesian optimization. Here's a breakdown of the architecture:
Random Forest Regressor: This is a supervised learning algorithm that uses an ensemble of decision trees to perform regression tasks. It creates multiple decision trees, each trained on a random subset of the training data, and then combines their predictions to produce the final output.
Bayesian Optimization: It is an optimization technique that aims to find the optimal set of hyperparameters for the Random Forest Regressor. Bayesian optimization uses a surrogate model (Gaussian Process in this case) to model the relationship between the hyperparameters and the objective function (negative mean squared error). It then uses an acquisition function (Upper Confidence Bound in this case) to guide the search for the best hyperparameters by balancing exploration and exploitation.
The process involves iteratively evaluating the objective function with different sets of hyperparameters, updating the surrogate model, and selecting the next set of hyperparameters based on the acquisition function. This iterative process continues until the desired number of iterations is reached.
The best hyperparameters found through Bayesian optimization are then used to create the final Random Forest Regressor model, which is trained on the entire training data. The final model is then used to make predictions on the test data, and the mean squared error is calculated to evaluate its performance.

## Performance

Give a summary graph or metrics of how the model performs. Remember to include how you are measuring the performance and what data you analysed it on. 
To evaluate the performance of the model, the metrics Mean Absolute Error (MAE) was used on a training set of the data. The MAE measures the average absolute difference between the predicted RUL values and the true RUL values. It quantifies the magnitude of prediction errors without considering their direction.
The model showed good results for predicting RUL with an MSE of 760. The model also showed that the automated baysian optimisation converged on hyperparameters quicker that the grid search.

![Screenshot](bayesian_vs_gridsearch.png)
![Screenshot](baysian_opt_Results.png)
![Screenshot](model_performance.png)

## Limitations

- **Limited generalizability**: The model's was trained on NMC-LCO 18650 battery dataset that represented measurements from over 1000 NMC-LCO 18650 cells. Performance of the model is constrained by this specific dataset used for training. The training data is limited in terms of battery types, operating conditions, or usage patterns, the model's predictions may not generalize well to batteries outside this training set. 
- **Lack of interpretability**: The model is a black box, where the underlying relationships and decision-making processes are not easily interpretable. This lack of interpretability can hinder the understanding of how the model arrives at its predictions and limits the ability to extract actionable insights or diagnose potential issues.
- **Sensitivity to input quality**: The accuracy of the model's predictions is influenced by the quality and reliability of the voltage and current measurements. Any measurement errors or noise in the input data can propagate and affect the model's outputs.

## Trade-offs

The model's reliance on historical voltage and current data assumes that the past behaviour of the battery is indicative of its future performance. However, it may not capture sudden changes in degradation patterns or adapt well to unforeseen events or operational conditions outside the training data's scope. The model's performance may be compromised in situations where the battery's behavior deviates significantly from the learned patterns or experiences new usage scenarios.
