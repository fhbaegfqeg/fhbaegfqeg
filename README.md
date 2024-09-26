- 👋 Hi, I’m @fhbaegfqeg
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...

<!---

import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
from statsmodels.tsa.stattools import adfuller
from statsmodels.tsa.arima.model import ARIMA
from statsmodels.graphics.tsaplots import plot_acf, plot_pacf
import requests
from io import StringIO
import matplotlib.font_manager as fm

# 设置中文字体
zh_font = fm.FontProperties(fname='C:/Windows/Fonts/SimHei.ttf')  # 替换为实际字体路径

# 尝试使用不同的数据源
url = 'https://solarscience.msfc.nasa.gov/greenwch/spot_num.txt'

# 下载数据
response = requests.get(url)
data = response.text

# 检查下载的内容是否正确
if data.startswith('<!DOCTYPE'):
    raise ValueError("下载的数据文件不是纯文本格式，请检查URL是否正确。")

# 打印数据前几行以检查格式
print(data.split('\n')[:10])

# 预处理数据
data = StringIO(data)
columns = ['Year', 'Month', 'Sunspot', 'Dev']
df = pd.read_csv(data, delim_whitespace=True, header=0, names=columns)

# 创建日期列
df['Date'] = pd.to_datetime(df[['Year', 'Month']].assign(DAY=1))

# 设置日期为索引
df.set_index('Date', inplace=True)

# 删除不必要的列
df.drop(columns=['Year', 'Month', 'Dev'], inplace=True)

# 可视化数据
df.plot(title='每月太阳黑子数量')
plt.xlabel('日期', fontproperties=zh_font)
plt.ylabel('太阳黑子数量', fontproperties=zh_font)
plt.title('每月太阳黑子数量', fontproperties=zh_font)
plt.show()

# 检查数据的平稳性
result = adfuller(df['Sunspot'])
print('ADF Statistic:', result[0])
print('p-value:', result[1])

# 差分处理（如有必要）
df_diff = df.diff().dropna()
df_diff.plot(title='差分后太阳黑子数量')
plt.xlabel('日期', fontproperties=zh_font)
plt.ylabel('差分后太阳黑子数量', fontproperties=zh_font)
plt.title('差分后太阳黑子数量', fontproperties=zh_font)
plt.show()

# 确定ARIMA模型的参数
plot_acf(df_diff)
plt.title('自相关函数', fontproperties=zh_font)
plt.xlabel('滞后数', fontproperties=zh_font)
plt.ylabel('自相关', fontproperties=zh_font)
plt.show()

plot_pacf(df_diff)
plt.title('偏自相关函数', fontproperties=zh_font)
plt.xlabel('滞后数', fontproperties=zh_font)
plt.ylabel('偏自相关', fontproperties=zh_font)
plt.show()

# 假设参数为p=2, d=1, q=2
# 建立ARIMA模型
model = ARIMA(df['Sunspot'], order=(2, 1, 2))
model_fit = model.fit()
print(model_fit.summary())

# 进行预测
forecast = model_fit.forecast(steps=12)
forecast_df = pd.DataFrame(forecast, index=pd.date_range(start=df.index[-1], periods=13, freq='M')[1:], columns=['Forecast'])

# 可视化预测结果
plt.figure(figsize=(10, 6))
plt.plot(df['Sunspot'], label='历史太阳黑子数量')
plt.plot(forecast_df, label='预测太阳黑子数量', color='red')
plt.legend(prop=zh_font)
plt.title('太阳黑子数量预测', fontproperties=zh_font)
plt.xlabel('日期', fontproperties=zh_font)
plt.ylabel('太阳黑子数量', fontproperties=zh_font)
plt.show()


--->
