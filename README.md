**forked from nlpyang/structured**

## 数据准备

数据均放在该目录的data下面。

* `data/train.txt` 训练集
* `data/test.txt` 测试集
* `data/infer.txt`  预测集

以上三个文件，需要提前分词好。

## Run

### 数据处理

相关参数：`prepare_data.py`11行，设置最多的句子数量`max_sents`，单个句子最多token数量`max_tokens`， 超过则过滤掉。 `data_structure.py`112,114行 word2vec参数设置。

```
python prepare_data.py data/train.txt data/dev.txt data/test.txt
```

### 训练

```
python cli.py --data_file data/save-all.pkl  --rnn_cell lstm --batch_size 16 --dim_str 50 --dim_sem 75 --dim_output 8 --keep_prob 0.7 --opt Adagrad --lr 0.05 --norm 1e-4 --gpu -1 --sent_attention max --doc_attention max --log_period 5000
```

自行调节上面的参数，batch_size可以大一点，设置gpu等。

最后预测结果在`inference_answers.txt`， 每一行8个数值，代表每一个类别的概率。