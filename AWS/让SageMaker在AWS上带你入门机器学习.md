# 让SageMaker在AWS上带你入门机器学习

## 什么是机器学习？

### **人工智能(AI)**

制造智能机器和程序

- **强人工智能：通用性智能，类似人类思考**
- **弱人工智能：特殊的应用，本身并不智慧**

### **机器学习**

无需严格编程就具备学习能力

- **弱人工智能的一种方法**
- **采用数据集训练模型**
- **根据模型来做一个预测**

### **深度学习**

基于深度神经网络科学

- **机器学习的一种方法(Method)**

总得来说，他们三者之间的关系大致如下图：

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD.png?raw=true)

### 人工智能与机器学习正在影响各行各业

- 媒体与娱乐
- 健康与医疗
- 个性化推荐
- 金融服务交易
- 客户体验

### **亚马逊在人工智能领域的大量深度创新**

- 商品智能推荐
- 机器人与物流创库
- 新产品
- 供应链管理
- 智慧呼叫中心
- 无人值守商店

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/%E4%BA%BA%E5%B7%A5%E6%99%BA%E8%83%BD%E5%92%8C%E6%9C%BA%E5%99%A8%E5%AD%A6%E4%B9%A0.png?raw=true)
## 机器学习需要做什么？

### **构建训练管道**

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/%E6%9E%84%E5%BB%BA%E8%AE%AD%E7%BB%83%E7%AE%A1%E9%81%93.png?raw=true)

### **机器学习的简单分类**

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/机器学习的简单分类2.png?raw=true)

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/机器学习的简单分类.png?raw=true)

**监督学习（Supervised Learning）**就是已经有了数据和数据对应的正确**标签**，比如猫狗的图片分类。常用经典算法分类、线性回归、逻辑回归、支持向量机、决策树、朴素贝叶斯分类器等等。

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/猫狗图片-监督学习.png?raw=true)

**非监督学习（Unsupervised Learning）**就是已经有了数据，但是**没有**数据所对应的**标签**，比如手写体的识别。K-Means算法、PCA（主成分分析）等算法。

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/猫狗图片-非监督学习.png?raw=true)

**强化学习（Reinforcement Learning 简称RL）**就是在某个**特定的环境下**自主行动的个体，透过和环境之间的**互动**，而不断**改进**它的行为。简单来说，就是让计算机实现从一开始什么都不懂, 脑袋里没有一点想法, 通过不断地尝试, 从错误中学习, 最后找到规律, 学会了达到目的的方法. 这就是一个完整的强化学习过程. 实际中的强化学习例子有很多. 比如近期最有名的 Alpha go、无人驾驶。

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/强化学习.png?raw=true)

总得来说，**监督学习**中有已知的输入数据和输出数据，相当于看着样本学习。**非监督学习**中没有输出数据，相当于自己学习。其学习目的是找到输入数据中存在的结构(Structure)和模式(Pattern)。**强化学习**即没有输入数据也没有输出数据，只有**某种规则**，相当于试错学习。其目的是在大量可能路径中寻找最佳决策或者路径。

## **基于人工神经网络的深度学习**

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/人工神经网络.png?raw=true)

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/输入层-隐含层-输出层.png?raw=true)

所谓的**人工神经网络**，就是所有神经元之间的连接都是**固定不可更换的**， 这也就是说,，在人工神经网络里,，没有凭空产生新联结这回事。人工神经网络典型的一种学习方式就是，我已经知道吃到糖果时，手会如何动，但是我想让神经网络学着帮我做这件动动手的事情。所以我预先准备好非常多吃糖的学习数据，然后将这些数据一次次放入这套人工神经网络系统中，糖的信号会通过这套系统传递到手。然后通过对比这次信号传递后，手的动作是不是”讨糖”动作，来修改人工神经网络当中的神经元强度。这种修改在专业术语中叫做”误差反向传递”，也可以看作是再一次将传过来的信号传回去，看看这个负责传递信号神经元对于”讨糖”的动作到底有没有贡献，让它好好反思与改正，争取下次做出更好的贡献。

人工神经网络靠的是正向和反向传播来更新神经元，从而形成一个好的神经系统，本质上, 这是一个能让计算机处理和优化的数学模型。

## 深度学习浪潮

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/深度学习浪潮.png?raw=true)

## **机器学习工作流程**

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/机器学习工作流程.png?raw=true)

## 什么是 Amazon SageMaker？

Amazon SageMaker **是一项完全托管的机器学习服务**。借助 Amazon SageMaker，**数据科学家和开发人员可以快速、轻松地构建和训练机器学习模型，然后直接将模型部署到生产就绪托管环境中**。它提供了一个集成的 **Jupyter** 编写笔记本实例，供您轻松访问数据源以便进行探索和分析，因此您无需管理服务器。此外，它还可以提供常见的机器学习算法，这些算法经过了优化，可以在分布式环境中高效处理非常大的数据。借助对自带算法和框架的原生支持，Amazon SageMaker 可以提供灵活并且适合具体工作流程的分布式训练选项。通过在 Amazon SageMaker 控制台中单击来启动模型，即可将模型部署到安全的、可扩展的环境。训练和托管按使用分钟数计费，没有最低费用，也不需要前期承诺。

### 机器学习对日常开发来说太复杂	

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/机器学习对日常开发来说太复杂.png?raw=true)

### 机器学习对日常开发来说不复杂

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/机器学习对日常开发来说不复杂.png?raw=true)

## Amazon SageMaker组件

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/Amazon%20SageMaker%E7%BB%84%E4%BB%B6.png?raw=true)

### 1、Amazon SageMaker Notebook 计算环境

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/计算环境.png?raw=true)

### 2、Amazon SageMaker 算法

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/算法.png?raw=true)

### 3、Amazon SageMaker 训练服务

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/训练服务.png?raw=true)

### 4、Amazon SageMaker 部署服务

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/部署服务.png?raw=true)

## 围绕数据的 “飞轮 ”

![](https://github.com/wuhanhao/Blogs/raw/master/Pictures/AWS/围绕数据的飞轮.png?raw=true)
