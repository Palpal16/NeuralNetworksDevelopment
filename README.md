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


For a more in-depth overview of the project, methods, and models built, please refer to the **[report](/docs/Report1.pdf)** and the **[notebooks](/notebooks/Project1/)**.

### Results

In conclusion we found the best model to be EfficientNetV2S with a classifier made of two dense layers of 128 and 64 both with Relu activation functions, He initialization and L2 regularization and dropout with a rate of $\frac{1}{6}$ trained through the custom loss function 'weighted_categorical_crossentropy'. This model achieved a test-set accuracy of **0.81**.






 ## Project 2: Time Series Forecasting
 <p align="center">
 	<img src="images/timeseries.png" height="250" />
 </p>
 In this challenge, the goal was to train a model to correctly predict future timesteps of a given time series. The amount of time steps to predict varied between 9 and 18.

 The dataset provided consisted of 48000 time series of variable length, with an average of 200 time steps. This data came with a set of critical issues:
 - Scarcity of some classes compared to others
 - TS already normalized in the range [0,1]
 - Lack of information on: Data sampling, Temporal scale, etc.

 To improve the data quality we tried many different approaches, among which:
 - Transformations like square root, cubic root, log and second-order differentiation
 - Removed noise with rolling mean smoothing, exponential smoothing, and polynomial interpolation
 - Padding in different ways for short sequences
 - Analyze *windows*, instead of full series, obtained by cutting the signals to length between 100 and 200 points.
 - Time series decomposition into trend, seasonality, and noise.
 - Fourier trasform to exploit periodicity, wihch showed spikes of frequencies of 12 time steps, probably indicating that the data was annaul.
 - Time2Vec embedding, to insert time-related features into the data.


 Our focus was on models that could have memory, we tried using LSTM, GRU and RNN layers and to those we added, with significant results, a multi-head attention layer from Keras.

 For a more in-depth overview of the project, methods, and models built, please refer to the **[report](/docs/Report2.pdf)** and the **[notebooks](/notebooks/Project2/)**.

 ### Results

 The final model we implemented consisted of the time to vec embedding, with 2 bidirectional Gru layers and 3 convolutional 1D layers. This model achieved a test-set MSE of **0.0096**.
