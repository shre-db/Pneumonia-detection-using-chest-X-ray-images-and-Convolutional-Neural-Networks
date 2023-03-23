# Pneumonia Detection using Chest X-ray Images and Convolutional Neural Networks

Overview
--------
This project involves developing a Convolutional Neural Network (CNN) from scratch using PyTorch to classify chest X-ray images as either normal or pneumonia. The CNN architecture comprises 6 convolution and max pooling layers, each with batch normalization and dropout regularization at 25% probability to prevent overfitting. Additionally, there are 6 fully connected layers, also with dropout regularization at 50% probability. The model has a little over 17 million trainable parameters. The dataset is imbalanced, with the normal class comprising 1349 images and the pneumonia class comprising 3883 images. To address this, a weighted loss function, BCEwithLogitsLoss, was employed. The model was trained with the help of DataLoaders in batches of 32 images, and the Adam optimizer. The primary performance metric used was accuracy. After training for 5 epochs on Colab's GPU accelerated environment, the model achieved a training accuracy of nearly 97% and a test accuracy of 81.41%. However, it became apparent that the model was overfitting and that a change in model architecture and hyperparameter tuning may be necessary. Currently the model is still under development.
