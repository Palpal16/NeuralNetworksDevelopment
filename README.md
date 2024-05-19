# Neural netwoeks development

In this repository are implemented two neural networks. Respectively focused on:
1. Image Classification
2. Time Series Forecasting

## Project 1: Image Classification
<p align="center">
	<img src="images/plants.png" height="250" />
</p>

In this challenge, the goal was to train a classifier to correctly predict whether an image represented a **healthy** or **unhealthy** plant.
We tried many different approaches to improve the accuracy of the model. Mainly we focused on:
- Custom CNNs (with convulutional, dense, inception and skip layers)
- Transfer Learning + Fine Tuning of Pre-trained models

**Transfer Learning** + **Fine-Tuning** turned out to be the best formula for this type of problem.

Moreover, because the provided dataset only consisted of 5000 images, **Data augmentation** was a critical part of this challenge. For this reason, we developed a custom random augmentation pipeline which included: rotation, translation, flips, zoom, contrast, brightness and sharpness.

Also, since the distribution of images wasn't even, we balanced the two classes. The best approach was given by a cost sensitive training through the a custom loss function: 'weighted_categorical_crossentropy'. 

Finally another practice that proved to be usefull on the images was test time augumentation on the prediction images.


For a more in-depth overview of the challenge, methods, and models built, please refer to the **[report](/docs/Report1.pdf)** and the **[notebooks](/notebooks/Project1/)**.

### Results

In conclusion we found the best model to be EfficientNetV2S with a classifier made of two dense layers of 128 and 64 both with Relu activation functions, He initialization and L2 regularization and dropout with a rate of $\frac{1}{6}$ trained through the custom loss function 'weighted_categorical_crossentropy'. This model achieved a test-set accuracy of **0.81**.






 ## Project 2: Time Series Forecasting
 <p align="center">
 	<img src="images/timeseries.png" height="250" />
 </p>
 In this challenge, the goal was to train a model to correctly predict future timesteps of a given time series. The amount of time steps to predict varied between Development and Final phases, increasing from 9 to 18.

 This time, using pre-trained models was not allowed, thus our focus shifted to a different set of approaches:
 - Adapting SOTA models in TS Forecasting
 - Custom RNN architectures (using LSTMs, GRUs)
 - Transformer architectures
 - Model Ensembles

 All of these yielded notable results, specifically **Model Ensembles** of GRU and *Dlinear* (Transformer-based model) proved to be the most effective of the approaches presented.

 The dataset provided consisted of significantly more data points, totaling at 48000 Time series of variable length. This data came with a set of critical issues, among which:
 - Scarcity of some classes compared to others
 - TS already normalized in the range [0,1]
 - Lack of information on: Data sampling, Temporal scale, etc.

 These issues proved difficult to work with because we had no prior information on any signal: for this reason we had no working criteria to remove potential outlier signals.

  In some cases, signals would show imperfections (clipping, spikes) in some portions, while being perfectly fine in others. To see if something could be done about this, we tried plotting correlations/autocorrelations between signals, but even though we managed to detect and remove some outliers, this did not prove to be beneficial for our model.

 Thus, we settled on analyzing *windows* obtained by cutting the signals to 200 points, and concluded that the only windows worth removing were the ones containing long flat trends.

 For a more in-depth overview of the challenge, methods, and models built, please refer to the **[report](/docs/Report.pdf)** and the **[notebooks](/notebooks/Project2/)**.

 ### Results

 Our best model achieved a test-set MSE of **0.01051**, placing our team in the **top 30%** among over 580 participants.

 ## Team Members
 [Leonardo Brusini](https://github.com/LeonardoBrusini)
 <p>

 [Marco Scarpelli](https://github.com/ScarpMarc)
<p>

 [Davide Tenedini](https://github.com/DavideTenediniPoliMi)
<p>

 [Federico Toschi](https://github.com/ftoschi14)
 <p>
 
 Team name: Drip Mac
