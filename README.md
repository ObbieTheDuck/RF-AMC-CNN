# Robust CNN-Based Automatic Modulation Classification Under Noisy Channel Conditions
Source code for the paper is based off of "AMC-Benchmark" from Richardzhangxx, published on github, and "Deep Learning Based Automatic Modulation Recognition: Models, Datasets, and Challenges", published in Digital Signal Processing.

Representative and up-to-date models in the AMR field are implemented on dataset RML2016.10a.

Github is avaiblbe here: [AMC-Benchmark](https://github.com/Richardzhangxx/AMR-Benchmark)

The article is available here: [Deep Learning Based Automatic Modulation Recognition: Models, Datasets, and Challenges](https://www.sciencedirect.com/science/article/pii/S1051200422002676?via%3Dihub)

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


# Results and Experiments

## Evaluation Metric
• classification accuracy


# Architecture

## Input
128 × 2


## Description
The proposed CNN architecture is designed to efficiently extract temporal and structural features from raw I/Q signal data. The input to the network is a 128 × 2 matrix representing the in-phase and quadrature components of
the signal. The first convolutional layer applies multiple filters with small kernel sizes to capture local variations
in amplitude and phase. These early-stage filters focus on low-level waveform features such as transitions, peaks, and signal continuity.

As the signal propagates through subsequent convolutional layers, the number of filters increases, allowing the network to learn more complex and abstract representations of modulation patterns. Nonlinear activation functions (ReLU) are applied after each convolution to enable the model to capture nonlinear relationships between signal features. Max pooling layers are used to reduce the dimensionality of the feature maps while preserving the most relevant information, improving computational efficiency and robustness.

Dropout layers are incorporated during training to prevent overfitting by randomly disabling neurons, which enhances the model’s ability to generalize to unseen data. The extracted features are then passed to a fully connected layer, which aggregates the learned representations and maps them to the output classes. Finally, a Softmax layer produces a probability distribution over all modulation types, allowing the model to select the most likely classification.


## Extraction Process
The CNN extracts important features from the I/Q signal by using convolutional filters. These filters look for patterns in the signal, such as changes in amplitude, phase, peaks, and transitions.

Real signals can be affected by noise, interference, fading, and distortion. Because of this, the signal shape can change. The CNN helps by learning which features are most useful for classification during training instead of relying on fixed handcrafted features.

In the early layers, the CNN learns simple signal patterns, such as amplitude changes and phase shifts. In deeper layers, it combines those simple patterns into more complex features that are specific to each modulation type.

This helps the model tell the difference between similar modulation types. For example, QPSK and 8PSK can be hard to separate at low SNR because they are both phase-based. The CNN learns small differences between them by looking at patterns across multiple layers.

Max pooling is used to reduce the size of the feature maps while keeping the most important information. This makes the model more efficient and helps reduce overfitting.

Dropout is used during training to prevent the model from relying too much on one specific feature. This helps the CNN perform better on new data.

Finally, the fully connected layer combines all the learned features, and the Softmax layer gives the probability for each modulation type. The model then selects the class with the highest probability.


## Layers
The model consists of the following layers:

• Convolutional layers for feature extraction

• ReLU activation for nonlinearity

• Max pooling for dimensionality reduction

• Dropout layers to prevent overfitting

• Fully connected layer for classification

• Softmax output for probability distribution


## Loss Fuction
categorical cross-entropy loss


## Training Setup
• Batch size: 64 or 128

• Epochs: 20–50

• Learning rate: tuned experimentally


## Contribution
This work evaluates a CNN-based AMC system and analyzes how SNR and training parameters affect classification performance.


# Dataset

**Table2** Main AMR open datasets for SISO systems.
![1658233963147](https://user-images.githubusercontent.com/56213845/179750964-f49c2657-3348-48b2-86bc-dd3855b56378.png)

| Dataset | Link |Notes |
| :-----:| :----: | :----: |
| [RML2016.10a](https://pubs.gnuradio.org/index.php/grcon/article/view/11) | [RML](http://radioml.com) | Other Datasets are available such as [RML2016.10b, RML2018.01a, HisarMod2019.1](https://pubs.gnuradio.org/index.php/grcon/article/view/1), that were used in [AMR-Benchmark](https://github.com/Richardzhangxx/AMR-Benchmark) |



