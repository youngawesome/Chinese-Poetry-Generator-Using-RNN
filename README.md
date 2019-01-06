# 基于 PaddlePaddle0.10.0 利用RNN进行中文古诗句生成
运行本例的方法如下：
1.运行rnn_generate_poetry.ipynb文件，开始train模型（默认使用LSTM），待训练结束，模型会保存在models/ 目录下，根据输入前缀文本input.txt,可以生成诗句。（输入的数据集文本默认为`data/poetrys.txt`，输入的前缀文本默认为`data/input.txt，生成的文本默认保存到`data/gen_result.txt`中。）

 如果需要使用自己的语料、定制模型，需要修改`config.py`中的配置，细节和适配工作详情如下：
   
   （1）.按需调整config.py中如下配置，来修改 rnn 语言模型的网络结果：

    rnn_type = "lstm"  # "gru" or "lstm"
    emb_dim = 256
    hidden_size = 256
    stacked_rnn_num = 2
        1. rnn_type：支持 ”gru“ 或者 ”lstm“ 两种参数，选择使用何种 RNN 单元。 
		2. emb_dim：设置词向量的维度。 
		3. hidden_size：设置 RNN 单元隐层大小。 
		4. stacked_rnn_num：设置堆叠 RNN 单元的个数，构成一个更深的模型。
   （2）.按需调整config.py中如下配置，来修改生成诗句文本的要求：
   
        1. gen_file：指定输入数据文件，每行是一个句子的前缀，需要预先分词。 
	    2. gen_result：指定输出文件路径，生成结果将写入此文件。 
	    3. max_gen_len：指定每一句生成的诗句文本的最长长度，如果模型无法生成出<e>，当生成 max_gen_len 个词语后，生成过程会自动终止。 
	    4. beam_size：Beam Search 算法每一步的展开宽度。 
	    5. model_path：指定训练好的模型的路径。
       其中，gen_file 中保存的是待生成的诗句前缀，每个前缀占一行。
