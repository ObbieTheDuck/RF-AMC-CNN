# Robust CNN-Based Automatic Modulation Classification Under Noisy Channel Conditions
Source code for the paper is based off of "AMC-Benchmark" from Richardzhangxx, published on github, and "Deep Learning Based Automatic Modulation Recognition: Models, Datasets, and Challenges", published in Digital Signal Processing.

Representative and up-to-date models in the AMR field are implemented on dataset RML2016.10a.

Github is available here: [AMC-Benchmark](https://github.com/Richardzhangxx/AMR-Benchmark)

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



# Experiments and Results

## *Dataset*
The dataset used in this work is based on a RadioML-style dataset that contains multiple digital modulation schemes across a wide range of signal-to-noise ratio (SNR) values. The modulation types included in the dataset are BPSK, QPSK, 8PSK, 16QAM, and 64QAM, which represent commonly used communication schemes with varying levels of complexity. 

Each sample in the dataset consists of 128 time-domain signal points, represented as a 128 × 2 matrix corresponding to the in-phase (I) and quadrature (Q) components.
This representation preserves both amplitude and phase information, which are essential for distinguishing between modulation types. 

The dataset includes signals with SNR values ranging from -20 dB to +18 dB, allowing evaluation under both highly noisy and relatively clean signal conditions. The data is split into training and testing sets to ensure that the model is evaluated on unseen samples, providing a realistic measure of generalization performance.


## *Evaluation Metric*
• classification accuracy

![ClasAcc](https://github.com/ObbieTheDuck/RF-AMC-CNN/blob/main/GitHubRFAMCCNNPictures/ClasAcc.PNG)

**Fig.1**: classification Cccuracy Equation


## *Results*
The experimental results indicate that the CNN model is capable of learning meaningful patterns from raw I/Q data. The classification accuracy improves significantly as the SNR increases, which is consistent with communication theory. At very low SNR levels, the signal is heavily corrupted by noise, which limits the model’s ability to extract reliable features. This results in low classification accuracy. However, as the SNR increases, the signal becomes more distinguishable, allowing the model to correctly identify modulation types.

The model is trained using the Adam optimizer with batch sizes of 64 and 128 over 20 to 50 epochs. The trained model is then tested on unseen data to evaluate its generalization performance.  At low SNR values (e.g., -20
dB), the signal is highly distorted by noise, resulting in low classification accuracy. As the SNR increases, the signal becomes clearer and the model achieves significantly higher accuracy.


###  SNR Impact

![ClasAccVsSNR](https://github.com/ObbieTheDuck/RF-AMC-CNN/blob/main/GitHubRFAMCCNNPictures/ClasAccVsSNR.PNG)

**Fig.2**: Classification Accuracy Versus SNR

This trend highlights the dependence of deep learningbased AMC systems on signal quality and emphasizes the
need for robust models in low-SNR environments.

• At low SNR (-20 dB): the accuracy is approximately
10–20%

• At medium SNR (0 dB): the accuracy improves to
around 70–80%

• At high SNR (≥ 10 dB): accuracy reaches 85–95%


### Confusion Matrix

![PerClasClasAcc](https://github.com/ObbieTheDuck/RF-AMC-CNN/blob/main/GitHubRFAMCCNNPictures/PerClasClasAcc.PNG)

**Table 1**: Per-Class Classification Accuracy

![ConMatrixModClas](https://github.com/ObbieTheDuck/RF-AMC-CNN/blob/main/GitHubRFAMCCNNPictures/ConMatrixModClas.PNG)

**Fig.3**: Confusion Matrix for Modulation Classification

Misclassification errors primarily occur between modulation types with similar signal characteristics. For example, QPSK and 8PSK are frequently confused due to their similar phase-based representations. Similarly, higherorder QAM schemes such as 16QAM and 64QAM exhibit overlapping amplitude and phase patterns, making them more difficult to distinguish, especially at lower SNR levels.

These errors highlight the limitations of the model in distinguishing between closely related modulation schemes and suggest that more advanced architectures may improve performance.


### Hyperparameter Sensitivity

The performance of the CNN model is sensitive to changes in hyperparameters such as learning rate, batch size, and number of training epochs.

![ClasAccDifSNRLvl](https://github.com/ObbieTheDuck/RF-AMC-CNN/blob/main/GitHubRFAMCCNNPictures/ClasAccDifSNRLvl.PNG)

**Table 2**: Classification Accuracy at Different SNR Levels

![TrainConfigPara](https://github.com/ObbieTheDuck/RF-AMC-CNN/blob/main/GitHubRFAMCCNNPictures/TrainConfigPara.PNG)

**Table 3**: Training Configuration Parameters


The performance of the CNN model is influenced by several hyperparameters. Increasing the number of training epochs generally improves accuracy up to a certain
point, after which overfitting may occur. 

Batch size also affects performance. Smaller batch sizes lead to more stable convergence but increase training time, while larger batch sizes speed up training but may reduce generalization performance. 

The learning rate controls how quickly the model updates its weights. A high learning rate may cause instability, while a low learning rate may slow down convergence.

These observations demonstrate the importance of carefully selecting hyperparameters to achieve optimal performance.

![TrainLossEpochs](https://github.com/ObbieTheDuck/RF-AMC-CNN/blob/main/GitHubRFAMCCNNPictures/TrainLossEpochs.PNG)

**Fig.4**: Training Loss as a Function of Epochs

![EffectsTrainEpochClasAcc](https://github.com/ObbieTheDuck/RF-AMC-CNN/blob/main/GitHubRFAMCCNNPictures/EffectsTrainEpochClasAcc.PNG)

**Fig.5**: Effect of Training Epochs on Classification Accuracy

![EffectsBatchSizeClasAcc](https://github.com/ObbieTheDuck/RF-AMC-CNN/blob/main/GitHubRFAMCCNNPictures/EffectsBatchSizeClasAcc.PNG)

**Fig.6**: Effect of Batch Size on Classification Accuracy


### Benchmark Model Comparison

Benchmark implementations, such as those provided in the AMR Benchmark repository, demonstrate that deeper networks and hybrid models can achieve high classification accuracy, particularly at moderate and high SNR levels. These models are designed to capture both spatial and temporal dependencies in the signal, which can improve performance for complex modulation schemes.

Compared to these models, the proposed CNN architecture provides a simpler and more computationally efficient solution. While it may not achieve the same level of performance as more complex architectures in all scenarios, it demonstrates strong classification accuracy across a wide range of SNR values.

One advantage of the proposed model is its ability to learn directly from raw I/Q data without requiring additional preprocessing or feature engineering. This simplifies implementation and reduces computational overhead.

However, benchmark models that incorporate recurrent layers or deeper convolutional structures may provide improved performance in challenging conditions, such as very low SNR levels or when distinguishing between similar modulation types

![CompCNNBenchmarks](https://github.com/ObbieTheDuck/RF-AMC-CNN/blob/main/GitHubRFAMCCNNPictures/CompCNNBenchmarks.PNG)

**Fig.7**: Comparison of Proposed CNN with Benchmark Models

# Architecture

## *Input*
128 × 2


## *Description*
The proposed CNN architecture is designed to efficiently extract temporal and structural features from raw I/Q signal data. The input to the network is a 128 × 2 matrix representing the in-phase and quadrature components of
the signal. The first convolutional layer applies multiple filters with small kernel sizes to capture local variations
in amplitude and phase. These early-stage filters focus on low-level waveform features such as transitions, peaks, and signal continuity.

As the signal propagates through subsequent convolutional layers, the number of filters increases, allowing the network to learn more complex and abstract representations of modulation patterns. Nonlinear activation functions (ReLU) are applied after each convolution to enable the model to capture nonlinear relationships between signal features. Max pooling layers are used to reduce the dimensionality of the feature maps while preserving the most relevant information, improving computational efficiency and robustness.

Dropout layers are incorporated during training to prevent overfitting by randomly disabling neurons, which enhances the model’s ability to generalize to unseen data. The extracted features are then passed to a fully connected layer, which aggregates the learned representations and maps them to the output classes. Finally, a Softmax layer produces a probability distribution over all modulation types, allowing the model to select the most likely classification.


## *Extraction Process*
The CNN extracts important features from the I/Q signal by using convolutional filters. These filters look for patterns in the signal, such as changes in amplitude, phase, peaks, and transitions.

Real signals can be affected by noise, interference, fading, and distortion. Because of this, the signal shape can change. The CNN helps by learning which features are most useful for classification during training instead of relying on fixed handcrafted features.

In the early layers, the CNN learns simple signal patterns, such as amplitude changes and phase shifts. In deeper layers, it combines those simple patterns into more complex features that are specific to each modulation type.

This helps the model tell the difference between similar modulation types. For example, QPSK and 8PSK can be hard to separate at low SNR because they are both phase-based. The CNN learns small differences between them by looking at patterns across multiple layers.

Max pooling is used to reduce the size of the feature maps while keeping the most important information. This makes the model more efficient and helps reduce overfitting.

Dropout is used during training to prevent the model from relying too much on one specific feature. This helps the CNN perform better on new data.

Finally, the fully connected layer combines all the learned features, and the Softmax layer gives the probability for each modulation type. The model then selects the class with the highest probability.


## *Layers*
The model consists of the following layers:

• Convolutional layers for feature extraction

• ReLU activation for nonlinearity

• Max pooling for dimensionality reduction

• Dropout layers to prevent overfitting

• Fully connected layer for classification

• Softmax output for probability distribution


## *Loss Fuction*
categorical cross-entropy loss

![LossFuc](https://github.com/ObbieTheDuck/RF-AMC-CNN/blob/main/GitHubRFAMCCNNPictures/LossFuc.PNG)

**Fig.1** classification Cccuracy Equation

## *Training Setup*
• Batch size: 64 or 128

• Epochs: 20–50

• Learning rate: tuned experimentally


## *Contribution*
This work evaluates a CNN-based AMC system and analyzes how SNR and training parameters affect classification performance.


# Dataset

| Dataset | Link |Notes |
| :-----:| :----: | :----: |
| [RML2016.10a](https://pubs.gnuradio.org/index.php/grcon/article/view/11) | [RML](http://radioml.com) | Other Datasets are available such as [RML2016.10b](https://pubs.gnuradio.org/index.php/grcon/article/view/11), [RML2018.01a](https://ieeexplore.ieee.org/abstract/document/8267032), [HisarMod2019.1](https://ieeexplore.ieee.org/abstract/document/9128408), that were used in [AMR-Benchmark](https://github.com/Richardzhangxx/AMR-Benchmark) |

**Table2** All possible datasets that can be used for AMC.
![1658233963147](https://user-images.githubusercontent.com/56213845/179750964-f49c2657-3348-48b2-86bc-dd3855b56378.png)



# Related Papers

| Model | Paper name | Publication year |
| :-----:| :----: | :----: |
| CNN1| [Convolutional Radio Modulation Recognition Networks](https://link.springer.com/chapter/10.1007/978-3-319-44188-7_16) | 2016  |
|CNN2| [Robust and Fast Automatic Modulation Classification with CNN under Multipath Fading Channels](https://ieeexplore.ieee.org/abstract/document/9128408)  | 2020   |
|MCNET| [MCNet: An Efficient CNN Architecture for Robust Automatic Modulation Classification](https://ieeexplore.ieee.org/abstract/document/8963964)  |  2020  |
|IC-AMCNET| [CNN-Based Automatic Modulation Classification for Beyond 5G Communications](https://ieeexplore.ieee.org/abstract/document/8977561) | 2020   |
|ResNet|[Deep neural network architectures for modulation classification](https://ieeexplore.ieee.org/abstract/document/8335483)   |  2017  |
|DenseNet|[Deep neural network architectures for modulation classification](https://ieeexplore.ieee.org/abstract/document/8335483)    |  2017  |
|GRU| [Automatic Modulation Classification using Recurrent Neural Networks](https://ieeexplore.ieee.org/abstract/document/8322633)  | 2017   |
|LSTM|[Deep Learning Models for Wireless Signal Classification With Distributed Low-Cost Spectrum Sensors](https://ieeexplore.ieee.org/abstract/document/8357902)  |   2018 |
|DAE|[Real-Time Radio Technology and Modulation Classification via an LSTM Auto-Encoder](https://ieeexplore.ieee.org/abstract/document/9487492)| 2022   |
|MCLDNN| [A Spatiotemporal Multi-Channel Learning Framework for Automatic Modulation Recognition](https://ieeexplore.ieee.org/abstract/document/9106397)  | 2020   |
|CLDNN|[Deep Architectures for Modulation Recognition](https://ieeexplore.ieee.org/abstract/document/7920754) |2017    |
|CLDNN2|[Deep neural network architectures for modulation classification](https://ieeexplore.ieee.org/abstract/document/8335483)    |  2017  |
|CGDNet| [CGDNet: Efficient Hybrid Deep Learning Model for Robust Automatic Modulation Recognition](https://ieeexplore.ieee.org/abstract/document/9349627)  | 2021   |
|PET-CGDNN|[An Efficient Deep Learning Model for Automatic Modulation Recognition Based on Parameter Estimation and Transformation](https://ieeexplore.ieee.org/abstract/document/9507514)|2021    |
|1DCNN-PF|[Automatic Modulation Classification Using Parallel Fusion of Convolutional Neural Networks](https://scholar.google.com/scholar?hl=en&as_sdt=0%2C5&q=Automatic+Modulation+Classification+Using+Parallel+Fusion+of+Convolutional+Neural+Networks&btnG=)   | 2019   |



# Acknowledgement
Our work is based on [Fuxin "Richardzhangxx" Zhang](https://github.com/Richardzhangxx).

# Citation
Please cite the literature we refer to if they are helpful to your work.
If our work is helpful to your research, please cite:








