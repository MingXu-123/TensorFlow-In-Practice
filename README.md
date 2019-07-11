# TensorFlow-In-Practice
 Notebooks for learning TensorFlow for deep learning.


## Some notes:
*1. Introduction to TensorFlow for Artificial Intelligence, Machine Learning, and Deep Learning*
- **Convolution**: isolate features in images
- **Pooling**: reduce the information in an image while maintaining features
- After passing a 3x3 filter over a 28x28 image, the output will become `26x26` [(28-(3-1))x(28-(3-1))]
- After max pooling a 26x26 image with a 2x2 filter, the output will become `13x13` [(26/2)x(26/2)]

*2. Convolutional Neural Networks in TensorFlow*
- Some concepts:  
(1) **iteration**：表示1次迭代（也叫training step），每次迭代更新1次网络结构的参数；  
(2) **batch-size**：1次迭代所使用的样本量；  
(3) **epoch**：1个epoch表示过了1遍训练集中的所有样本。  
值得注意的是，在深度学习领域中，常用带mini-batch的随机梯度下降算法（Stochastic Gradient Descent, SGD）训练深层结构，它有一个好处就是并不需要遍历全部的样本，当数据量非常大时十分有效。此时，可根据实际问题来定义epoch，例如定义10000次迭代为1个epoch，若每次迭代的batch-size设为256，那么1个epoch相当于过了2560000个训练样本。  ([Adopted from Zhihu](https://www.zhihu.com/question/43673341/answer/257382587))

- **Transfer Learning**: take the layers from an existing model, and make them so that they don't get retrained -- i.e. you freeze (or lock) the already learned convolutions into your model. Then add your own DNN at the bottom of these, which you can retrain to your data. 
- **Dropouts**: used to prevent over-fitting by removing a random number of neurons in your neural network. This works very well for two reasons: The first is that neighboring neurons often end up with similar weights, which can lead to overfitting, so dropping some out at random can remove this. The second is that often a neuron can over-weigh the input from a neuron in the previous layer, and can over specialize as a result. Thus, dropping out can break the neural network out of this potential bad habit!

*3. Natural Language Processing in TensorFlow*
- **OOV**: out of vocabulary `oov_token=<Token>`. Create a special token for words unseen in the train data but seen in the test data. If you don’t use a token for out of vocabulary words, the word isn’t encoded, and is skipped in the sequence.
- **Padding**: if you have a number of sequences of different lengths, you need to use the `pad_sequences` object from the `tensorflow.keras.preprocessing.sequence` namespace, so that they are understood when fed into a neural network. (by default they’ll get padded to the length of the longest sequence by adding zeros to the beginning of shorter ones; but if you want the padding to be at the end of the sequence i.e., zeros after the sequence, pass `padding=’post’` to pad_sequences when initializing it)
- **Enbedding**: the vectors for each word with their associated sentiment.