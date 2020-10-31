# 工业蒸汽量模型的学习

<font size=4>题目说明：</font>\
&#160; &#160; &#160; &#160;经脱敏后的锅炉传感器采集的数据（采集频率是分钟级别），根据锅炉的工况，预测产生的蒸汽量。(均方方差最小)
>*`问题思路`*：通过提供的V0~V37预测连续值的target，典型的回归问题。常见的回归算法包括线性回归、决策树回归等。
>

****

## 1. 数据分析(demo)

- `变量分析：`  
 连续-连续：散点图、热力图、Q-Q图  
 连续-类型：双向表（频次和频率占比）、[卡方检验](https://blog.csdn.net/ludan_xia/article/details/81737669)  
 连续-类型：小提琴图  
- `缺失值处理：`  
 删除：当特征列或特征行缺失达到90%  
 填充：均值、中位数、相似样本（依据相关度高还原）  
 预测：划分出缺失列，通过模型训练填充
- `异常值检测：`  
 通过箱型图、直方图、散点图查看  
- `异常值处理：`  
删除、转换（归一化）、填充（人为造成）、单独处理（大量异常值）  

****

## 2. 数据转换  

 &#160; &#160; &#160; &#160;通过可视化发现，数据分布不均，故对变量取值进行转换->正态分布  

- `标准化：` 比例缩放，但不改变数据分布  
- `取平方：`右倾（对数、平方立方根、对数）、左倾（平方、立方、指数）  
- `分组：` 按百分比分划分训练  
- `虚变量：` 变量拆分、哑变量（0 1）  

****

## 3. 注意  

- 对训练集和测试集进行特征分析，查看相同变量分布是否一样；

- 若分布不一样，train和test数据拿出来做归一化处理；  

- 大道至简，好的数据和特征选取决定机器学习的上线，模型和算法是逼近这个上限；  

- 一般流程：数据预处理（采集->清洗->采样）；特征处理（补缺失值、归一化、虚变量、转换、降维）  

- 降维：相关系数、信息熵、卡方检验、主成分分析、线性分析

****

## 4. 模型检验（demo1）

- 欠拟合和过拟合  
`欠拟合：`加特征、加多项式、减小lamda  
`过拟合:` 减特征、采集更多数据、增加lamda  
- 模型选择方法  
`正则化：`选择经验风险和模型复杂度低的（Occam's razor）,可理解为惩罚因子  
`交叉检验：` K折、留一交叉验证
