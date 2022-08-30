# Mobility-Analysis For Safegraph Data in Summer Project 
[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/14TUzE3iTUzeBhXofmm87rBVg8ynf7jem?usp=sharing)
# Abstract
With the spread of the pandemic, people's mobility may change and we aim to predict the number of visits for specific region in New York City from January 2022 to May 2022 using different models. For the basic model, we have tried ARIMA model and LSTM model that ignores the interaction between different regions. 
Considering the importance of the interaction between different regions and the difficulty to segment the spatial data into square region, we try to realize the mobility prediction with the thought of paper: *TrafficGAN: Off-Deployment Traffic Estimation with Traffic Generative Adversarial Networks* and revise it by changing the pattern of backpropgation. Finally, we have tried to segment the features and target feature into grids with 100 * 100 grids and predict the mobility using CNN and compare it with the Traffic GAN. 

# Model 
## Traffic GAN model 
The traffic GAN model has created new Dynamic Layer by introducing the traffic correlation matrix A to consider the interaction between different regions: \
![1](https://user-images.githubusercontent.com/59796732/187321331-04a31d4d-efc5-4a15-93ac-d780b6e00b6d.PNG) \
where H is the feature matrix get in each layer and W is the weight matrix and sigma is the activation function. 
![捕获](https://user-images.githubusercontent.com/59796732/187320582-4e84f384-3162-4b1c-94a9-35765cf36230.PNG) \ 
From the picture above, we can 
## CNN 
 
## Summary of Models 

