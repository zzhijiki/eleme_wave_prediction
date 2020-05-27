# README

## 运行：

- 由 `/project/feature/feature.ipynb`得到特征文件`/project/user_data/tmp_data/feature_train.pkl`和`/project/user_data/tmp_data/feature_test.pkl`

- 再通过 `/project/model/model.ipynb`得到提交文件`/project/action_predict/`

- `/project/code/` 下的两个文件就是  `feature.ipynb`  和`model.ipynb`的copy 
- 最后一次调试用的是`/project/code/`里的文件，两者应该都能运行成功。

## 算法：

- 将每个波次的训练集划分上下两部分，上半部分为last_data，预测下面的future_data的第一个数据，future_data的其余数据作为负样本，进行了两分类的建模。

- 对future中的样本（train和test）都做了筛选，将没有被pick的deliver样本全部删除。

- 利用`lightgbm`进行5折交叉验证的分类任务，答案取每个波次被预测概率为1的最大值。

## 特征工程：

提取了较多的常规特征和时序特征，对不同类型的数据做了不同的数据转换和归一化操作，

但是最后用上的不多，一共7个。

包括

`grid_distance`: 从上个action到这个action需要的距离

`target_tan` : 从上个action到这个action的tan角度

`target_MHD`: 从上个action到这个action的曼哈顿距离

骑手信息： `speed`，`max_load`，`level`和

`load`:当前骑手的负载单数



