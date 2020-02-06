# KG
知识图谱
主要对中文分词、词性标注等一些常见算法（HMM、MEMM、CRF和借助深度学习的LSTM进行整理），并且对几个算法的应用进行demo演示  

## HMM 算法
由于仓库中已有关于HMM算法的详细展开说明，我们不在这里啰嗦的再次表达，直接看下对应的公式推导。    
![Image text](https://github.com/CuiShaohua/KG/blob/master/images/equation01.svg)  
![Image text](https://github.com/CuiShaohua/KG/blob/master/images/equation02.svg)
Bayes公式和联合概率。--W是观测序列（输入的单词序列），T是隐藏状态（代表输出词性序列）   

词性标注的任务（或者NER任务）的目的就是为了求解这样的一个概率，而对于HMM来讲，这个概率需要满足3个假设条件，我们且看：   
假设1： HMM认为词与词之间是条件独立的，即第1个词和第2词都是随机出现的。我们利用这条可以得到![Image text](https://github.com/CuiShaohua/KG/blob/master/images/equation1.svg)    
假设2： 一个词出现的概率只取决于它自身的词性标注tag，而与其他的词性标注无关。利用这个可以得到发射概率，即由隐藏状态指向观测状态的概率。![Image text](https://github.com/CuiShaohua/KG/blob/master/images/equation2.svg)     
假设3： 基于马尔科夫性（隐藏状态的短依赖关系），类似bi_gram得到![image](https://github.com/CuiShaohua/KG/blob/master/images/equation3.svg)   

这些假设使得HMM能够计算出给定一个词和它可能的词性的联合概率分布。换句话说，HMM假设了两类特征，一是当前词词性与上一个词词性的关系，以及当前词语和当前词性的关系，分别对应着转移概率和发射概率。HMM的学习过程就是在训练集中学习这两个概率矩阵(大小为(t*t),(w*t))。 

## CRF 算法
CRF算法与HMM算法明显不同，CRF没有做出如上的假设，而是采用了更为抽象的特征函数来表达特征，弥补了马尔科夫性，添加了较长的依赖关系，其中两类特征函数，一个可以比作观测状态指向隐藏状态的特征函数，另一个是隐藏状态序列之间的特征函数，如果是线性链的CRF，那么隐藏状态之间的特征函数是上一个状态指向下一个状态，而如果不是线性链的CRF，其可以指代任意多个隐藏状态对当前状态的影响。



