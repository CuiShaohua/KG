# KG
知识图谱
主要对中文分词、词性标注等一些常见算法（HMM、MEMM、CRF和借助深度学习的LSTM进行整理），并且对几个算法的应用进行demo演示  

## HMM 算法
由于仓库中已有关于HMM算法的详细展开说明，我们不在这里啰嗦的再次表达，直接看下对应的公式推导。    
$$
Pr(T|W) = \frac{Pr(W|T)*Pr(T)}{Pr(W)}
$$   
---- Bayes公式--W是观测序列（输入的单词序列），T是隐藏状态（代表输出词性序列）
