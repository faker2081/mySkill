## 多模态

### 什么叫做多模态机器学习？



首先，什么叫做模态（Modality）呢？

每一种信息的来源或者形式，都可以称为一种模态。例如，人有触觉，听觉，视觉，嗅觉；信息的媒介，有语音、视频、文字等；多种多样的传感器，如雷达、红外、加速度计等。以上的每一种都可以称为一种模态。

同时，模态也可以有非常广泛的定义，比如我们可以把两种不同的语言当做是两种模态，甚至在两种不同情况下采集到的数据集，亦可认为是两种模态。

因此，多模态机器学习，英文全称 MultiModal Machine Learning (MMML)，旨在通过机器学习的方法实现处理和理解多源模态信息的能力。目前比较热门的研究方向是图像、视频、音频、语义之间的多模态学习。

多模态学习从1970年代起步，经历了几个发展阶段，在2010后全面步入Deep Learning阶段。

人其实是一个多模态学习的总和，所以也有”砖家“说了，多模态学习才是真正的人工智能发展方向。

### 多模态学习分类：

多模态学习可以划分为以下五个研究方向：

1. **多模态表示学习 Multimodal Representation**
2. **模态转化 Translation**
3. **对齐 Alignment**
4. **多模态融合 Multimodal Fusion**
5. **协同学习 Co-learning**

#### 1. 多模态表示学习

单模态的表示学习负责将信息表示为计算机可以处理的数值向量或者进一步抽象为更高层的特征向量，而多模态表示学习是指通过利用多模态之间的互补性，剔除模态间的冗余性，从而学习到更好的特征表示。主要包括两大研究方向：**联合表示（Joint Representations）**和**协同表示（Coordinated Representations）**。

1、联合表示将多个模态的信息一起映射到一个统一的多模态向量空间；

2、协同表示负责将多模态中的每个模态分别映射到各自的表示空间，但映射后的向量之间满足一定的相关性约束（例如线性相关）。

![img](https://pic1.zhimg.com/80/v2-2395a0e94ab8a8ab26f3f96848df07d4_720w.jpg)

利用多模态表示学习到的特征可以用来做信息检索，也可以用于的分类/回归任务。下面列举几个经典的应用。

在来自 NIPS 2012 的 《Multimodal learning with deep boltzmann machines》一文中提出将 deep boltzmann machines（DBM） 结构扩充到多模态领域，通过 Multimodal DBM，可以学习到多模态的联合概率分布。

![img](https://pic4.zhimg.com/80/v2-2363961db42e284b7c45b865c048facf_720w.jpg)



# CV

**顶级会议： ICLR、NIPS、CVPR、ICCV、ECCV**

## 目标检测

### 发展历史

![img](https://img-blog.csdnimg.cn/2018112408385566.jpeg?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0dlbnRsZW1hbl9RaW4=,size_16,color_FFFFFF,t_70)

![img](https://img-blog.csdnimg.cn/2018112408564724.JPG?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L0dlbnRsZW1hbl9RaW4=,size_16,color_FFFFFF,t_70)

#### YOLO

##### 创新

YOLO将物体检测作为回归问题求解。基于一个单独的end-to-end网络，完成从原始图像的输入到物体位置和类别的输出。从网络设计上，YOLO与rcnn、fast rcnn及faster rcnn的区别如下：

1. YOLO训练和检测均是在一个单独网络中进行。YOLO没有显示地求取region proposal的过程。而rcnn/fast rcnn 采用分离的模块（独立于网络之外的selective search方法）求取候选框（可能会包含物体的矩形区域），训练过程因此也是分成多个模块进行。Faster rcnn使用RPN（region proposal network）卷积网络替代rcnn/fast rcnn的selective search模块，将RPN集成到fast rcnn检测网络中，得到一个统一的检测网络。尽管RPN与fast rcnn共享卷积层，但是在模型训练过程中，需要反复训练RPN网络和fast rcnn网络（注意这两个网络核心卷积层是参数共享的）。
2. YOLO将物体检测作为一个回归问题进行求解，输入图像经过一次inference，便能得到图像中所有物体的位置和其所属类别及相应的置信概率。而rcnn/fast rcnn/faster rcnn将检测结果分为两部分求解：物体类别（分类问题），物体位置即bounding box（回归问题）。![img](https://pic4.zhimg.com/80/v2-181f533e731b216a98b238af42ffbb2b_720w.png)

##### 核心思想

###### loss函数

YOLO使用均方和误差作为loss函数来优化模型参数，即网络输出的$S*S*(B*5 + C)$维向量与真实图像的对应$ S*S*(B*5 + C) $ 维向量的均方和误差。如下式所示。其中，![[公式]](https://www.zhihu.com/equation?tex=coordError)、*iouError*和*classError*分别代表预测数据与标定数据之间的坐标误差、IOU误差和分类误差。

![[公式]](https://www.zhihu.com/equation?tex=loss%3D%5Csum_%7Bi%3D0%7D%5E%7BS%5E%7B2%7D+%7D%7BcoordError+%2B+iouError+%2B+classError%7D+)

YOLO对上式loss的计算进行了如下修正。

1. 位置相关误差（坐标、IOU）与分类误差对网络loss的贡献值是不同的，因此YOLO在计算loss时，使用![[公式]](https://www.zhihu.com/equation?tex=%5Clambda+_%7Bcoord%7D+%3D5)修正![[公式]](https://www.zhihu.com/equation?tex=coordError)。
2. 在计算IOU误差时，包含物体的格子与不包含物体的格子，二者的IOU误差对网络loss的贡献值是不同的。若采用相同的权值，那么不包含物体的格子的confidence值近似为0，变相放大了包含物体的格子的confidence误差在计算网络参数梯度时的影响。为解决这个问题，YOLO 使用![[公式]](https://www.zhihu.com/equation?tex=%5Clambda+_%7Bnoobj%7D+%3D0.5)修正![[公式]](https://www.zhihu.com/equation?tex=iouError)。（*注此处的‘包含’是指存在一个物体，它的中心坐标落入到格子内*)。
3. 对于相等的误差值，大物体误差对检测的影响应小于小物体误差对检测的影响。这是因为，相同的位置偏差占大物体的比例远小于同等偏差占小物体的比例。YOLO将物体大小的信息项（w和h）进行求平方根来改进这个问题。（*注：这个方法并不能完全解决这个问题*）。



###### 综上，YOLO具有如下优点：

- 快。YOLO将物体检测作为回归问题进行求解，整个检测网络pipeline简单。在titan x GPU上，在保证检测准确率的前提下（63.4% mAP，VOC 2007 test set），可以达到45fps的检测速度。
- 背景误检率低。YOLO在训练和推理过程中能‘看到’整张图像的整体信息，而基于region proposal的物体检测方法（如rcnn/fast rcnn），在检测过程中，只‘看到’候选框内的局部图像信息。因此，若当图像背景（非物体）中的部分数据被包含在候选框中送入检测网络进行检测时，容易被误检测成物体。测试证明，YOLO对于背景图像的误检率低于fast rcnn误检率的一半。



- 通用性强。YOLO对于艺术类作品中的物体检测同样适用。它对非自然图像物体的检测率远远高于DPM和RCNN系列检测方法。



###### 但相比RCNN系列物体检测方法，YOLO具有以下缺点：

- 识别物体位置精准性差。
- 召回率低。



# nlp

### 预处理

```python
import collections
import re
from d2l import torch as d2l


#@save
d2l.DATA_HUB['time_machine'] = (d2l.DATA_URL + 'timemachine.txt',
                                '090b5e7e70c295757f55df93cb0a180b9691891a')

def read_time_machine():  #@save
    """Load the time machine dataset into a list of text lines."""
    with open(d2l.download('time_machine'), 'r') as f:
        lines = f.readlines()
    # 忽略标点符号和大写
    return [re.sub('[^A-Za-z]+', ' ', line).strip().lower() for line in lines]

lines = read_time_machine()
print(f'# text lines: {len(lines)}')
print(lines[0])
print(lines[10])




def tokenize(lines, token='word'):  #@save
    """将文本行拆分为单词或字符词元。"""
    if token == 'word':
        return [line.split() for line in lines]
    elif token == 'char':
        return [list(line) for line in lines]
    else:
        print('错误：未知词元类型：' + token)

tokens = tokenize(lines)
for i in range(11):
    print(tokens[i])

    
    
class Vocab:  #@save
    """文本词汇表"""
    def __init__(self, tokens=None, min_freq=0, reserved_tokens=None):
        if tokens is None:
            tokens = []
        if reserved_tokens is None:
            reserved_tokens = []
        # 按出现频率排序
        counter = count_corpus(tokens)
        self.token_freqs = sorted(counter.items(), key=lambda x: x[1],
                                  reverse=True)
        # 未知词元的索引为0
        self.unk, uniq_tokens = 0, ['<unk>'] + reserved_tokens
        uniq_tokens += [token for token, freq in self.token_freqs
                        if freq >= min_freq and token not in uniq_tokens]
        self.idx_to_token, self.token_to_idx = [], dict()
        for token in uniq_tokens:
            self.idx_to_token.append(token)
            self.token_to_idx[token] = len(self.idx_to_token) - 1

    def __len__(self):
        return len(self.idx_to_token)

    def __getitem__(self, tokens):
        if not isinstance(tokens, (list, tuple)):
            return self.token_to_idx.get(tokens, self.unk)
        return [self.__getitem__(token) for token in tokens]

    def to_tokens(self, indices):
        if not isinstance(indices, (list, tuple)):
            return self.idx_to_token[indices]
        return [self.idx_to_token[index] for index in indices]

def count_corpus(tokens):  #@save
    """统计词元的频率。"""
    # 这里的 `tokens` 是 1D 列表或 2D 列表
    if len(tokens) == 0 or isinstance(tokens[0], list):
        # 将词元列表展平成使用词元填充的一个列表
        tokens = [token for line in tokens for token in line]
    return collections.Counter(tokens)




vocab = Vocab(tokens)
print(list(vocab.token_to_idx.items())[:10])


for i in [0, 10]:
    print('words:', tokens[i])
    print('indices:', vocab[tokens[i]])
    
    

```

在使用上述函数时，我们将所有功能打包到load_corpus_time_machine函数中，该函数返回 corpus（词元索引列表）和 vocab（时光机器语料库的词汇表）。 我们在这里所做的改变是： 1. 为了简化后面章节中的训练，我们使用字符（而不是单词）实现文本词元化； 2. 时光机器数据集中的每个文本行不一定是一个句子或一个段落，还可能是一个单词，因此返回的 corpus 仅处理为单个列表，而不是使用多个词元列表构成的一个列表。

```python
def load_corpus_time_machine(max_tokens=-1):  #@save
    """返回时光机器数据集的词元索引列表和词汇表。"""
    lines = read_time_machine()
    tokens = tokenize(lines, 'char')
    vocab = Vocab(tokens)
    # 因为时光机器数据集中的每个文本行不一定是一个句子或一个段落，
    # 所以将所有文本行展平到一个列表中
    corpus = [vocab[token] for line in tokens for token in line]
    if max_tokens > 0:
        corpus = corpus[:max_tokens]
    return corpus, vocab

corpus, vocab = load_corpus_time_machine()
len(corpus), len(vocab)
```

## 语言模型和数据集

##### 一元

```python
import random
import torch
from d2l import torch as d2l


tokens = d2l.tokenize(d2l.read_time_machine())
# 因为每个文本行不一定是一个句子或一个段落，因此我们把所有文本行拼接到一起
corpus = [token for line in tokens for token in line]
vocab = d2l.Vocab(corpus)
vocab.token_freqs[:10]
```

##### 二元

```python
bigram_tokens = [pair for pair in zip(corpus[:-1], corpus[1:])]
bigram_vocab = d2l.Vocab(bigram_tokens)
bigram_vocab.token_freqs[:10]
```



##### 三元

```python
trigram_tokens = [triple for triple in zip(
    corpus[:-2], corpus[1:-1], corpus[2:])]
trigram_vocab = d2l.Vocab(trigram_tokens)
trigram_vocab.token_freqs[:10]
```



