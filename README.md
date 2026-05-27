# 气体传感器信号灰度图像分类

基于深度学习的气体传感器信号分类项目，使用ResNet18模型对10种不同气体的传感器响应信号进行分类。

## 📋 项目简介

本项目将气体传感器的时序信号转换为二维灰度图像，使用卷积神经网络（CNN）进行分类。这种方法能够有效捕捉传感器响应的时空特征，提高气体识别的准确率。
<img width="1408" height="768" alt="EN" src="https://github.com/user-attachments/assets/64c4171b-747e-4f7c-9a61-3622a0a780c7" />


### 支持的气体类别

1. Acetaldehyde (乙醛)
2. Acetone (丙酮)
3. Ammonia (氨气)
4. Benzene (苯)
5. Butanol (丁醇)
6. CO (一氧化碳)
7. Ethylene (乙烯)
8. Methane (甲烷)
9. Methanol (甲醇)
10. Toluene (甲苯)

## 🚀 快速开始

### 环境要求

- Python 3.8+
- PyTorch 1.9+
- torchvision
- PIL (Pillow)
- scikit-learn
- matplotlib
- seaborn
- tqdm

### 安装依赖

```bash
pip install -r requirements.txt
```

### 使用预训练模型进行预测

```bash
python predict_gas.py
```

预测脚本会自动加载 `best_model.pth` 模型并对示例图像进行预测。

### 自定义预测

修改 `predict_gas.py` 中的路径：

```python
# 预测单张图像
test_image_path = "path/to/your/image.jpg"

# 预测文件夹中的所有图像
test_folder = "path/to/your/folder"
```

## 📚 数据处理说明

### 原始数据集

本项目使用的气体传感器数据来自 [CNN-Models-for-Public-Gas-Dataset](https://github.com/ShowHsiang/CNN-Models-for-Public-Gas-Dataset)。

### 数据转换逻辑

1. **原始数据**：72个传感器的时序响应信号
2. **转换为图像**：将时间轴作为x轴，传感器通道作为y轴，响应强度作为灰度值
3. **图像格式**：灰度图像，保留了原始的时空信息

### 为什么转换为图像？

- **解决交叉敏感性**：不同气体的传感器响应模式相似，但时序特征存在差异
- **利用CNN优势**：卷积神经网络擅长提取局部特征和空间模式
- **平移不变性**：对时间偏移不敏感，提高鲁棒性

## 🧠 模型架构

### ResNet18

- **输入**：224×224 灰度图像（转换为3通道）
- ** backbone **：ResNet18（18层残差网络）
- ** 输出**：10个气体类别的概率分布

### 残差连接的优势

- 解决深度网络的梯度消失问题
- 允许训练更深的网络
- 提高特征复用效率

## 📊 实验结果

训练完成后会生成以下可视化结果：

- **训练曲线**：损失和准确率随epoch的变化
-<img width="4170" height="1466" alt="曲线图" src="https://github.com/user-attachments/assets/d37a4f95-b706-4a65-a54c-25139a4598da" />


- **混淆矩阵**：测试集的分类结果可视化
- <img width="3387" height="2963" alt="混淆矩阵" src="https://github.com/user-attachments/assets/39400267-3f79-40f4-9055-df15f26eff0b" />


## 📁 项目结构

```
.
├── README.md              # 项目说明
├── LICENSE               # MIT许可证
├── requirements.txt      # Python依赖包
├── train_gas_model.py    # 模型训练脚本
├── predict_gas.py        # 预测脚本
├── test_model.py         # 测试脚本
├── use_model_example.py  # 使用示例
├── best_model.pth        # 预训练模型（134MB）
├── 曲线图.png            # 训练曲线
├── 混淆矩阵.png          # 混淆矩阵
```

## 🔧 使用说明

### 训练模型

```bash
python train_gas_model.py
```

训练参数可在 `train_gas_model.py` 中调整：

- `batch_size`: 批次大小（默认32）
- `num_epochs`: 训练轮数（默认20）
- `learning_rate`: 学习率（默认0.0005）

### 测试模型

```bash
python test_model.py
```

### 使用示例

```bash
python use_model_example.py
```

## 📈 性能指标

- **验证准确率**：约 90%+（取决于数据集和训练参数）
- **测试准确率**：约 85%+（取决于数据集和训练参数）

## 🤝 贡献

欢迎提交Issue和Pull Request！

## 📄 许可证

本项目采用 [MIT许可证](LICENSE)。

## 📖 引用

如果本项目对您的研究有帮助，请考虑引用：

```bibtex
@misc{gas-sensor-classification,
  author = {yiyezhangmu},
  title = {Gas Sensor Signal Grayscale Image Classification},
  year = {2026},
  publisher = {GitHub},
  journal = {GitHub repository},
}
```

## 🔗 相关资源

- [UCI Gas Sensor Array Drift Dataset](https://archive.ics.uci.edu/ml/datasets/gas+sensor+array+drift+dataset)
- [PyTorch官方文档](https://pytorch.org/docs/stable/index.html)
- [ResNet论文](https://arxiv.org/abs/1512.03385)

---

**注意**：本项目使用的原始数据集遵循其自身的许可证要求，请在使用前查阅相关条款。
