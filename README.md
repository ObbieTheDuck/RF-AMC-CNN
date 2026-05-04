# Robust CNN-Based Automatic Modulation Classification Under Noisy Channel Conditions
Source code for the paper is based off of "AMC-Benchmark" from Richardzhangxx, published on github, and "Deep Learning Based Automatic Modulation Recognition: Models, Datasets, and Challenges", published in Digital Signal Processing.

Representative and up-to-date models in the AMR field are implemented on four different datasets (RML2016.10a, RML2016.10b, RML2018.01a, HisarMod2019.1).

Github is avaiblbe here:[AMC-Benchmark](https://github.com/Richardzhangxx/AMR-Benchmark)

The article is available here:[Deep Learning Based Automatic Modulation Recognition: Models, Datasets, and Challenges](https://www.sciencedirect.com/science/article/pii/S1051200422002676?via%3Dihub)

# Abstract
Automatic modulation classification (AMC) plays a critical role in modern wireless communication systems. Traditional methods rely on handcrafted features and perform
poorly under noisy conditions. In this work, we implement a convolutional neural network (CNN)-based approach to classify modulation types directly from raw I/Q
data. Using a RadioML-style dataset, we evaluate performance across different signal-to-noise ratio (SNR) levels
and analyze the impact of training parameters on classification accuracy.

# Related Work
Recent advances in deep learning have significantly
improved AMC performance. Convolutional neural networks (CNNs) can extract features directly from raw
in-phase and quadrature (I/Q) data without manual feature engineering. These methods show strong robustness
across varying SNR levels.

Several architectures have been proposed, including
CNN-based models, recurrent neural networks (RNNs),
and hybrid models such as CNN-LSTM and CLDNN.
Benchmark studies have evaluated models such as
ResNet, DenseNet, and GRU on datasets like RadioML
2016.10A.

In this work, we focus on implementing a CNN-based
modulation classification model and analyzing its performance under different SNR conditions and training configurations.

# Architecture
## Experimental
### Accuracy
