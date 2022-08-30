# Mobility-Analysis For Safegraph Data 
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/14TUzE3iTUzeBhXofmm87rBVg8ynf7jem?usp=sharing)
# Abstract
With the spread of the pandemic, people's mobility may change and we try to predict the mobility with the change of time and spave. We select the number of visits as indicator since it is the direct indicator of the mobility in this region. For the dataset, we use the safegraph data in New York City from January 2022 to May 2022 and we assume the week and the cbg region as the minimum unit for temporal and spatial prediction that includes 20 weeks and 1510 cbg regions. For the basic model, we have tried ARIMA model and LSTM model that ignores the spatial interaction between different regions. 
Considering the importance of the interaction between different regions and the difficulty to segment the spatial data into square region, we try to realize the mobility prediction with the thought of paper: *TrafficGAN: Off-Deployment Traffic Estimation with Traffic Generative Adversarial Networks* and revise it by changing the pattern of backpropagtion. Finally, we have tried to segment the features and target feature into grids with 100 * 100 grids and predict the mobility using CNN and compare it with the Traffic GAN. 

# Model 
## Traffic GAN model 
The traffic GAN model has created new Dynamic Layer by introducing the traffic correlation matrix A to consider the interaction between different regions: \
![1](https://user-images.githubusercontent.com/59796732/187321331-04a31d4d-efc5-4a15-93ac-d780b6e00b6d.PNG) \
where H is the feature matrix get in each layer and W is the weight matrix and sigma is the activation function. 
![捕获](https://user-images.githubusercontent.com/59796732/187320582-4e84f384-3162-4b1c-94a9-35765cf36230.PNG) 
From the picture above, we can get the main structure of the traffic Gan that consists of four dynamic layer in Generator Part and Discriminator Part. In Generator Part, we concatenate the feature vectors and noise to get the predicted value for number of visits. Then we put the true value and predicted value to the discriminator part and get the probability of the fake series. We have trained our data using the Traffic GAN but find that the MSE loss cannot converge in training. In this way, we try to revise the model in two ways: 
1. Do not use the mechanism of GAN and directly use the Generator part with backpropagtion of MSE loss. 
2. Use distance function as the indicator of the correlation matrix instead of directly calucating the correlation of time series for each region. 
3. Add the Temporal Analysis by defining the time step and concatenate each features of different week in the time step. 
### Structure of Revised Model
![3](https://user-images.githubusercontent.com/59796732/187327347-bba8ffe0-594d-4377-a66f-fef2df1ba5db.png)

## CNN 
Finally, we segment the data using R Studio with grids of 100 * 100: \
![image](https://user-images.githubusercontent.com/59796732/187326645-a645f68a-a44b-469c-9e8e-ed978d480fa8.png)

For each grids, we calucate its features by the mean feature of all the nearby cbg region. For the grid of sea area, we all assign 0 to it and then go through the backpropgation. The CNN part consists of four layer where each layer includes convolutional nettral network, Batch Normalization, Dropout and Activation Function. 
### Structure of CNN
![2](https://user-images.githubusercontent.com/59796732/187326768-65159f9c-7301-475c-bb0c-da6c888f2b44.PNG)

## Summary of Models 

| Model Name  | 
| ---------- |
| ARIMA     |
| LSTM    |
| Traffic GAN     |
| Revised Traffic GAN      |
| CNN     |
# Result 
