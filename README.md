# KG
知识图谱
主要对中文分词、词性标注等一些常见算法（HMM、MEMM、CRF和借助深度学习的LSTM进行整理），并且对几个算法的应用进行demo演示  

## HMM 算法
由于仓库中已有关于HMM算法的详细展开说明，我们不在这里啰嗦的再次表达，直接看下对应的公式推导。    
![Image text](https://www.zhihu.com/equation?tex=%5Cbegin%7Bequation%7D+%5Cbegin%7Bsplit%7D+Pr%28T%5Cmid+W%29+%26%3D+%5Cfrac%7BPr%28W%5Cmid+T%29%2APr%28T%29%7D%7BPr%28W%29%7D%5C%5C+Pr%28W%2CT%29+%26%3D++Pr%28W%5Cmid+T%29%2APr%28T%29%5C%5C+++%26%3D+%5Cprod_%7Bi%3D1%7D%5E%7Bn%7DPr%28w_i%5Cmid+T%29%2APr%28T%29%5C%5C+++%26%3D+%5Cprod_%7Bi%3D1%7D%5E%7Bn%7DPr%28w_i%5Cmid+t_i%29%2APr%28T%29%5C%5C+++%26%3D+%5Cprod_%7Bi%3D1%7D%5E%7Bn%7DPr%28w_i%5Cmid+t_i%29%2APr%28t_i%5Cmid+t_%7Bi-1%7D%29+%5Cend%7Bsplit%7D+%5Cend%7Bequation%7D)  
Bayes公式和联合概率。--W是观测序列（输入的单词序列），T是隐藏状态（代表输出词性序列）   

词性标注的任务（或者NER任务）的目的就是为了求解这样的一个概率，而对于HMM来讲，这个概率需要满足3个假设条件，我们且看：   
假设1： HMM认为词与词之间是条件独立的，即第1个词和第2词都是随机出现的。我们利用这条可以得到![Image text](https://www.zhihu.com/equation?tex=%5Cprod_%7Bi%3D1%7D%5E%7Bn%7DPr%28w_i%5Cmid+T%29)    
假设2： 一个词出现的概率只取决于它自身的词性标注tag，而与其他的词性标注无关。利用这个可以得到发射概率，即由隐藏状态指向观测状态的概率。![Image](https://www.zhihu.com/equation?tex=%5Cprod_%7Bi%3D1%7D%5E%7Bn%7DPr%28w_i%5Cmid+t_i%29)     
假设3： 基于马尔科夫性（隐藏状态的短依赖关系），类似bi_gram得到![image](https://www.zhihu.com/equation?tex=%5Cprod_%7Bi%3D1%7D%5E%7Bn%7DPr%28w_i%5Cmid+t_i%29)      
这些假设使得HMM能够计算出给定一个词和它可能的词性的联合概率分布。换句话说，HMM假设了两类特征，一是当前词词性与上一个词词性的关系，以及当前词语和当前词性的关系，分别对应着转移概率和发射概率。HMM的学习过程就是在训练集中学习这两个概率矩阵(大小为(t*t),(w*t))。  
