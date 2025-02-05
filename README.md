数据分析步骤：

一、读取数据
df = pd.read_csv("data.csv")  # 读取 CSV
df = pd.read_excel("data.xlsx", engine='openpyxl')  # 读取 Excel

二、初步查看数据
print(df.head())  # 查看前5行
print(df.info())  # 查看列类型、缺失值
print(df.describe())  # 查看数值列的统计信息
print(df.isnull().sum())  # 统计缺失值数量
print(df.duplicated().sum())  # 统计重复行的数量

三、处理缺失值
方法 1：删除缺失值 df.dropna()  # 删除所有含有 NaN 的行
方法 2：填充缺失值 df["城市"].fillna("未知", inplace=True)  # 用 '未知' 填充文本列

四、处理重复值
df.drop_duplicates()
按特定列去重：df.drop_duplicates(subset=["姓名"])

五、处理异常值
找到异常值 print(df[df["工资"] > 100000])  # 假设工资超过 10w 是异常值
删除异常值 df = df[df["工资"] <= 100000]  # 只保留工资小于 10w 的数据
用中位数替换异常值
import numpy as np
median_salary = df["工资"].median()
df["工资"] = np.where(df["工资"] > 100000, median_salary, df["工资"])

六、处理数据格式不一致
df["日期"] = pd.to_datetime(df["日期"])
df["年龄"] = df["年龄"].astype(int)  # 转换为整数
df["价格"] = df["价格"].astype(float)  # 转换为浮点数
df["价格"] = df["价格"].str.replace("￥", "").astype(float) #删除货币符号，转换为数值

七、处理分类变量（文本数据）
df["性别"] = df["性别"].str.strip().str.lower()  # 统一去空格，转小写
df["性别"] = df["性别"].replace({"male": "男", "female": "女"})  # 统一性别分类

八、数据清理后检查
print(df.info())  # 检查数据类型
print(df.isnull().sum())  # 确保没有缺失值
print(df.duplicated().sum())  # 确保没有重复值
