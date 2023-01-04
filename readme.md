## 极简英中翻译系统

#### 项目说明

​	本项目是作者一门课的期末作业，因此模型复杂度和模型性能都比较一般，模型主体只基于一个简单的标准nn.transformer，其余部分基本手动实现。

​	tokenizer部分因为手动实现的效果在大数据上较差，因此改成了调用基于Bert的tokenizer。手动实现的tokenizer和调用的tokenizer调用方式不同，若实验复现请注意。

​	引入的库有一部分没用过，时间有限就没一个一个删。

#### 数据说明

​	两份数据来源都是CSDN博客，不知最初来源是哪里。

​	第一份1000万对句子对，过于巨大，经测试构建词表就需要2小时以上，而且训练时极难收敛。数据存放在dataset文件夹中。

​	第二份21033对句子对，数据量较小，而且中文部分为繁体，作者训练时1分钟一个epoch，约70个epoch后不再继续收敛。数据存放在transdata_2w文件夹中。

#### 代码说明(只有一部分)

​	获得数据：def getEnZh(data=’train‘): return en,zh,len(train_data) 返回英文字符串列表，中文字符串列表和数据集长度

​	分词器：class Mytokenizer(): 使用基于bert的分词器，拥有方法def en(s:str): return self.entokenizer.tokenize(s) ;def zh(s:str): return self.zhtokenizer.tokenize(s)

​	词表类：class Vocab: 封装了几个词表方法，包括：

* 词表生成器：def vocab_generator(self,en,zh,mytokenizer): return vocab_en,vocab_zh 返回值类型list
* 词表存储器：def vocab_save(self,vocab:list,name='vocab.txt'): 无返回值
* 词表读取器：def vocab_loader(self,dir='./vocab/',name=['vocab_en.txt','vocab_zh.txt']): return vocab_en,vocab_zh 返回值类型list

词表参数化方法：def get_index(data, lan): return idx 输入token和语言（'en','zh'）返回其在词表中的位置。封装不完整，需整个代码块一起运行。

#### 模型效果

​	训练好的模型存放在model_dir中，没有进行model.eval()，使用时需先model.eval()再进行预测，预测效果如下：

![R7QP4S$FCIU5PUD@]JGQRD9](img/R7QP4S$FCIU5PUD@]JGQRD9.png)



