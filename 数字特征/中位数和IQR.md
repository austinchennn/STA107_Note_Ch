## 1. 中位数 (Median) 在分布中的含义

中位数是将一组数据从小到大排列后，处于最中间位置的数值（第 50 百分位数）。它将概率分布切分为面积相等的两部分。

### 中位数 vs. 平均值 (Mean)

- **物理意义**：
    
    - **平均值** 是分布的“重心”或“平衡点”。
        
    - **中位数** 是分布的“地理中心”，即有一半的观测值比它大，一半比它小。
        
- **鲁棒性 (Robustness)**：
    
    - **平均值** 对异常值（Outliers）极其敏感。一个极大的数值会显著拉高平均值。
        
    - **中位数** 具有鲁棒性。即使序列中出现极端的异常值，中位数也几乎不受影响。
        
- **偏态分布中的关系**：
    
    - **右偏（正偏）分布**：Mean > Median（长尾在右侧，拉高了均值）。
        
    - **左偏（负偏）分布**：Mean < Median（长尾在左侧，拉低了均值）。
        
    - **对称分布**：Mean ≈ Median。
        

![](https://encrypted-tbn0.gstatic.com/licensed-image?q=tbn:ANd9GcRHb0iOFJMLR5uympNwhdLvQfoK5QZ5orzu_y2fxhKgBpHPA_-1c8NeeZ5aVxEDlOemzGAXzZPEsfNeasrIj8yfbcySWYe-Kj0-lEa3jC9ZHdhEgNU)

---

## 2. 四分位距 (IQR) 的计算

IQR 衡量的是数据中间 50% 的离散程度。

### 计算步骤

1. **确定四分位数**：
    
    - **Q1 (First Quartile)**：第 25 百分位数，即数据下半部分的中位数。
        
    - **Q3 (Third Quartile)**：第 75 百分位数，即数据上半部分的中位数。
        
2. **公式**：
    
    $$IQR = Q3 - Q1$$
    

### 应用：异常值判定 (1.5 IQR Rule)

在统计描述中，通常使用以下范围判定异常值：

- 下限：$Q1 - 1.5 \times IQR$
    
- 上限：$Q3 + 1.5 \times IQR$
    

![](https://encrypted-tbn3.gstatic.com/licensed-image?q=tbn:ANd9GcSNxfyVIeSBHTjdE_D88NlTINPKZv9L6uaRglyIippXSwo8cNi2Z2oOZ-kh1KXwqGo-C72WrJf4YzmgNQJ09K0Jlar6nc27rMKfsa1oMB6mh62woAs)

---

## 3. 使用 Z-score 计算正态分布下的 Median 与 IQR

在标准正态分布 $Z \sim N(0, 1)$ 中，我们可以通过累计分布函数（CDF）的反函数直接得出这些数值。

- **Median (Q2)**：
    
    对应累积概率为 0.5。在标准正态分布中，$Z = 0$。
    
- **Q1**：
    
    对应累积概率为 0.25。查表或计算可知：$Z_{Q1} \approx -0.674$。
    
- **Q3**：
    
    对应累积概率为 0.75。由于正态分布的对称性：$Z_{Q3} \approx 0.674$。
    
- **IQR**：
    
    在标准正态分布下，$IQR = 0.674 - (-0.674) = 1.348$。
    

**任意正态分布 $N(\mu, \sigma^2)$ 的转化：**

- $Q1 = \mu - 0.674\sigma$
    
- $Q3 = \mu + 0.674\sigma$
    
- $IQR = 1.348\sigma$
    

---

## 4. 什么时候用哪套组合？

在描述一个分布时，通常成对使用统计量：**Mean + Variance/SD** 或 **Median + IQR**。

### 方案 A：Mean + Variance (Standard Deviation)

- **适用场景**：
    
    - 数据呈**正态分布**或接近对称。
        
    - 数据中没有明显的异常值。
        
- **优势**：
    
    - 利用了所有数据点的信息。
        
    - 数学性质优良，方便进行后续的推断统计（如假设检验、方差分析）。
        

### 方案 B：Median + IQR

- **适用场景**：
    
    - 数据呈**偏态分布**（如家庭收入、房价、互联网点击量）。
        
    - 数据中存在显著的**异常值**。
        
- **优势**：
    
    - 能够真实反映“典型”数据的情况，不会被极端值带偏。
        
    - 在描述性统计中更具代表性，尤其是在处理具有“长尾”特征的金融或社交媒体数据时。
        
