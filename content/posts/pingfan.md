# 使用matlab进行预测性维护

环境：matlab live script 

  
  
# 导入数据

```matlab:Code
load("MachineData.mat")
trainData
```

| |ch1|ch2|ch3|label|
|:--:|:--:|:--:|:--:|:--:|
|1|70000x1 double|70000x1 double|70000x1 double|Before|
|2|70000x1 double|70000x1 double|70000x1 double|Before|
|3|70000x1 double|70000x1 double|70000x1 double|Before|
|4|70000x1 double|70000x1 double|70000x1 double|Before|
|5|70000x1 double|70000x1 double|70000x1 double|Before|
|6|70000x1 double|70000x1 double|70000x1 double|Before|
|7|70000x1 double|70000x1 double|70000x1 double|Before|
|8|70000x1 double|70000x1 double|70000x1 double|Before|
|9|70000x1 double|70000x1 double|70000x1 double|Before|
|10|70000x1 double|70000x1 double|70000x1 double|Before|
|11|70000x1 double|70000x1 double|70000x1 double|Before|
|12|70000x1 double|70000x1 double|70000x1 double|Before|
|13|70000x1 double|70000x1 double|70000x1 double|Before|
|14|70000x1 double|70000x1 double|70000x1 double|Before|

## 简单的数据可视化，大概看一下数据
  

一共有三个channel，同时对应之前的三列数据。

每一个子图有两条线，蓝色表示维修前的数据，红色代表维修后的数据

```matlab:Code
ensMember = 4;
helperPlotVibrationData(trainData, ensMember)
```

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/figure_0.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/figure_0.png
)

# 用predictive maintenance toolbox做特征工程

一共有三个特征，但是我们不知道哪个**状态指标**最合适，用原始数据做的话会很没有效率。

比如说我们来形容某个国家的发展状况，就会有人均GDP，国家总的GDP，人均住宅面积等各种指标，但是指标太多了，所以我们要选择最能反映发展状况的那个

所以说我们需要找最合适的**状态指标**，状态指标设计器可以让我们选择出最有效的那个指标去做异常检测。

Matlab中的预测性维护工具包-predictive maintenance toolbox中的diagnostic feature designer就是用来做这个的。

使用这个这个工具，分为 步

  
## 第一步，打开designer

在command window中输入 **`diagnosticFeatureDesigner`**

  

 、![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_0.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_0.png
)

  

稍等片刻就会出现这个界面

  

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_1.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_1.png
)

接下来进行数据集的选择，完成这三步后进行import 导入。

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_2.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_2.png
)

然后我们可以对单个属性进行可视化操作。

  

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_3.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_3.png
)

  

这些数据是所有的数据，包括了维修前和维修后，所以为了区分，我们可以将数据进行分组。

  

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_4.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_4.png
)

然后做**Filtering \& Averaging > Time-Synchronous Averaging**

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_5.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_5.png
)

**然后做TSA ，生成时域信息**

  

p

历史记录

  

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_6.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_6.png
)

参数

  

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_7.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_7.png
)

  

然后提取出它得谱功率

  

可以从参数那一栏看到更多的信息

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_8.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_8.png
)

选择TSA数据，选择时域特征-信号特征

  

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_9.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_9.png
)

  

生成的信号特征中，我们要选择一个最好的信号。蓝色为维修后，橙色为维修前，那么交叉的地方就是深蓝色

  

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_10.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_10.png
)

  

根据这个原则，Kurtosis就是一个不错的信号。

  

当然这些步骤是为了可视化选择信号的这个过程，其实也可以用代码代替这些步骤。

  

```matlab:Code
trainFeatures = generateFeatures(trainData);
head(trainFeatures)
```

| |label|ch1_stats/Col1_CrestFactor|ch1_stats/Col1_Kurtosis|ch1_stats/Col1_RMS|ch1_stats/Col1_Std|ch2_stats/Col1_Mean|ch2_stats/Col1_RMS|ch2_stats/Col1_Skewness|ch2_stats/Col1_Std|ch3_stats/Col1_CrestFactor|ch3_stats/Col1_SINAD|ch3_stats/Col1_SNR|ch3_stats/Col1_THD|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1|Before|2.2811|1.8087|2.3074|2.3071|-0.0323|0.6496|4.5230|0.6488|11.9725|-15.9450|-15.8864|-2.7320|
|2|Before|2.3276|1.8379|2.2613|2.2610|-0.0333|0.5946|5.5480|0.5937|10.2843|-15.9843|-15.9265|-2.7507|
|3|Before|2.3276|1.8626|2.2613|2.2612|-0.0121|0.4825|4.3638|0.4823|8.9125|-15.8585|-15.7984|-2.7104|
|4|Before|2.8781|2.1986|1.8288|1.8285|-0.0050|0.3498|2.3324|0.3498|11.7945|-16.1911|-16.1400|-3.0683|
|5|Before|2.8911|2.0600|1.8205|1.8203|-0.0019|0.2737|1.7661|0.2737|11.3953|-15.9466|-15.8930|-3.1126|
|6|Before|2.8979|2.1204|1.8163|1.8162|-0.0044|0.3674|2.8969|0.3674|11.6849|-15.9628|-15.9076|-2.9761|
|7|Before|2.9494|1.9200|1.7846|1.7844|-0.0067|0.3626|4.1308|0.3626|12.3964|-15.9988|-15.9422|-2.8281|
|8|Before|2.5106|1.6774|1.7513|1.7511|-0.0090|0.3235|3.7691|0.3234|8.8808|-15.7903|-15.7324|-2.9532|

我们可以看到

  

然后我们就可以在完整的数据集上做信号选择

```matlab:Code
load("FeatureEntire.mat")
head(featureAll)
```

| |label|ch1_stats/Col1_CrestFactor|ch1_stats/Col1_Kurtosis|ch1_stats/Col1_RMS|ch1_stats/Col1_Std|ch2_stats/Col1_Mean|ch2_stats/Col1_RMS|ch2_stats/Col1_Skewness|ch2_stats/Col1_Std|ch3_stats/Col1_CrestFactor|ch3_stats/Col1_SINAD|ch3_stats/Col1_SNR|ch3_stats/Col1_THD|
|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|:--:|
|1|Before|2.3683|1.9270|2.2225|2.2225|-0.0151|0.6251|4.2931|0.6249|5.6569|-5.4476|-4.9977|-4.4608|
|2|Before|2.4020|1.9206|2.1807|2.1803|-0.0183|0.5677|3.9985|0.5674|8.7481|-12.5315|-12.4187|-3.2353|
|3|Before|2.4157|1.9523|2.1789|2.1788|-0.0064|0.4565|2.8886|0.4564|8.3111|-12.9766|-12.8685|-2.9591|
|4|Before|2.4595|1.8205|2.1400|2.1401|0.0017|0.4142|2.0635|0.4142|7.2318|-13.5657|-13.4678|-2.7944|
|5|Before|2.2502|1.8609|2.3391|2.3390|-0.0082|0.3694|3.3498|0.3693|6.8134|-13.3301|-13.2249|-2.7182|
|6|Before|2.4211|2.2479|2.1286|2.1285|0.0111|0.3664|1.8602|0.3662|7.4712|-13.3239|-13.2258|-3.0313|
|7|Before|3.3111|4.0304|1.5896|1.5896|-0.0081|0.4722|2.1132|0.4721|8.2412|-13.8503|-13.7584|-2.7822|
|8|Before|2.2655|2.0656|2.3233|2.3233|-0.0049|0.3783|2.4936|0.3783|7.6947|-13.7814|-13.6830|-2.5601|

切分数据集`cvpartition`

```matlab:Code
rng(0) % set for reproducibility
idx = cvpartition(featureAll.label, 'holdout', 0.1);
featureTrain = featureAll(idx.training, :);
featureTest = featureAll(idx.test, :);
```

检查下数据集

```matlab:Code
size(featureTrain)
```

```text:Output
ans = 1x2    
       15878          13

```

把维修后的数据单独提取出来，因为这部分数据是被视为normal 的。

```matlab:Code
trueAnomaliesTest = featureTest.label;
featureNormal = featureTrain(featureTrain.label=='After', :);
```

  
# 用SVM做检测
  

训练一个svm模型

```matlab:Code
mdlSVM = fitcsvm(featureNormal, 'label', 'Standardize', true, 'OutlierFraction', 0);
```

然后用训练好的模型对测试集做预测

```matlab:Code
featureTestNoLabels = featureTest(:, 2:end);
[~,scoreSVM] = predict(mdlSVM,featureTestNoLabels);
isanomalySVM = scoreSVM<0;
predSVM = categorical(isanomalySVM, [1, 0], ["Anomaly", "Normal"]);
trueAnomaliesTest = renamecats(trueAnomaliesTest,["After","Before"], ["Normal","Anomaly"]);
figure;
confusionchart(trueAnomaliesTest, predSVM, Title="Anomaly Detection with One-class SVM", Normalization="row-normalized");
```

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/figure_1.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/figure_1.png
)

  

```matlab:Code

featureDimension = 1;

% Define biLSTM network layers
layers = [ sequenceInputLayer(featureDimension, 'Name', 'in')
   bilstmLayer(16, 'Name', 'bilstm1')
   reluLayer('Name', 'relu1')
   bilstmLayer(32, 'Name', 'bilstm2')
   reluLayer('Name', 'relu2')
   bilstmLayer(16, 'Name', 'bilstm3')
   reluLayer('Name', 'relu3')
   fullyConnectedLayer(featureDimension, 'Name', 'fc')
   regressionLayer('Name', 'out') ];

% Set Training Options
options = trainingOptions('adam', ...
   'Plots', 'training-progress', ...
   'MiniBatchSize', 500,...
   'MaxEpochs',200);
```

ff 

```matlab:Code
net = trainNetwork(featuresAfter, featuresAfter, layers, options);
```

```text:Output
在单 GPU 上训练。
｜＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝｜
｜　　轮　　｜　　迭代　　｜　　　　经过的时间　　　　　｜　　小批量　ＲＭＳＥ　　｜　　小批量损失　　｜　　基础学习率　　｜
｜　　　　　｜　　　　　　｜　　（ｈｈ：ｍｍ：ｓｓ）　　｜　　　　　　　　　　　　｜　　　　　　　　　｜　　　　　　　　　｜
｜＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝｜
｜　　　１　｜　　　　１　｜　　　　　００：００：０１　｜　　　　　　　６．０９　｜　　　　１８．５　｜　　０．００１０　｜
｜　　　３　｜　　　５０　｜　　　　　００：００：０２　｜　　　　　　　４．８０　｜　　　　１１．５　｜　　０．００１０　｜
｜　　　５　｜　　１００　｜　　　　　００：００：０３　｜　　　　　　　４．２３　｜　　　　　８．９　｜　　０．００１０　｜
｜　　　８　｜　　１５０　｜　　　　　００：００：０４　｜　　　　　　　３．４７　｜　　　　　６．０　｜　　０．００１０　｜
｜　　１０　｜　　２００　｜　　　　　００：００：０６　｜　　　　　　　３．７０　｜　　　　　６．８　｜　　０．００１０　｜
｜　　１３　｜　　２５０　｜　　　　　００：００：０７　｜　　　　　　　２．９６　｜　　　　　４．４　｜　　０．００１０　｜
｜　　１５　｜　　３００　｜　　　　　００：００：０８　｜　　　　　　　３．３０　｜　　　　　５．４　｜　　０．００１０　｜
｜　　１８　｜　　３５０　｜　　　　　００：００：０９　｜　　　　　　　２．５６　｜　　　　　３．３　｜　　０．００１０　｜
｜　　２０　｜　　４００　｜　　　　　００：００：１０　｜　　　　　　　３．０２　｜　　　　　４．６　｜　　０．００１０　｜
｜　　２３　｜　　４５０　｜　　　　　００：００：１２　｜　　　　　　　２．２６　｜　　　　　２．６　｜　　０．００１０　｜
｜　　２５　｜　　５００　｜　　　　　００：００：１３　｜　　　　　　　２．７８　｜　　　　　３．９　｜　　０．００１０　｜
｜　　２８　｜　　５５０　｜　　　　　００：００：１４　｜　　　　　　　２．０２　｜　　　　　２．０　｜　　０．００１０　｜
｜　　３０　｜　　６００　｜　　　　　００：００：１５　｜　　　　　　　２．５７　｜　　　　　３．３　｜　　０．００１０　｜
｜　　３３　｜　　６５０　｜　　　　　００：００：１６　｜　　　　　　　１．８３　｜　　　　　１．７　｜　　０．００１０　｜
｜　　３５　｜　　７００　｜　　　　　００：００：１７　｜　　　　　　　２．４１　｜　　　　　２．９　｜　　０．００１０　｜
｜　　３８　｜　　７５０　｜　　　　　００：００：１９　｜　　　　　　　１．６７　｜　　　　　１．４　｜　　０．００１０　｜
｜　　４０　｜　　８００　｜　　　　　００：００：２０　｜　　　　　　　２．２８　｜　　　　　２．６　｜　　０．００１０　｜
｜　　４３　｜　　８５０　｜　　　　　００：００：２１　｜　　　　　　　１．５４　｜　　　　　１．２　｜　　０．００１０　｜
｜　　４５　｜　　９００　｜　　　　　００：００：２２　｜　　　　　　　２．１８　｜　　　　　２．４　｜　　０．００１０　｜
｜　　４８　｜　　９５０　｜　　　　　００：００：２３　｜　　　　　　　１．４３　｜　　　　　１．０　｜　　０．００１０　｜
｜　　５０　｜　１０００　｜　　　　　００：００：２５　｜　　　　　　　２．０８　｜　　　　　２．２　｜　　０．００１０　｜
｜　　５３　｜　１０５０　｜　　　　　００：００：２６　｜　　　　　　　１．３１　｜　　　　　０．９　｜　　０．００１０　｜
｜　　５５　｜　１１００　｜　　　　　００：００：２７　｜　　　　　　　１．９８　｜　　　　　２．０　｜　　０．００１０　｜
｜　　５８　｜　１１５０　｜　　　　　００：００：２８　｜　　　　　　　１．１８　｜　　　　　０．７　｜　　０．００１０　｜
｜　　６０　｜　１２００　｜　　　　　００：００：２９　｜　　　　　　　１．８９　｜　　　　　１．８　｜　　０．００１０　｜
｜　　６３　｜　１２５０　｜　　　　　００：００：３０　｜　　　　　　　１．０７　｜　　　　　０．６　｜　　０．００１０　｜
｜　　６５　｜　１３００　｜　　　　　００：００：３２　｜　　　　　　　１．８０　｜　　　　　１．６　｜　　０．００１０　｜
｜　　６８　｜　１３５０　｜　　　　　００：００：３３　｜　　　　　　　０．９６　｜　　　　　０．５　｜　　０．００１０　｜
｜　　７０　｜　１４００　｜　　　　　００：００：３４　｜　　　　　　　１．７３　｜　　　　　１．５　｜　　０．００１０　｜
｜　　７３　｜　１４５０　｜　　　　　００：００：３５　｜　　　　　　　０．８６　｜　　　　　０．４　｜　　０．００１０　｜
｜　　７５　｜　１５００　｜　　　　　００：００：３６　｜　　　　　　　１．６６　｜　　　　　１．４　｜　　０．００１０　｜
｜　　７８　｜　１５５０　｜　　　　　００：００：３７　｜　　　　　　　０．７６　｜　　　　　０．３　｜　　０．００１０　｜
｜　　８０　｜　１６００　｜　　　　　００：００：３９　｜　　　　　　　１．６１　｜　　　　　１．３　｜　　０．００１０　｜
｜　　８３　｜　１６５０　｜　　　　　００：００：４０　｜　　　　　　　０．６８　｜　　　　　０．２　｜　　０．００１０　｜
｜　　８５　｜　１７００　｜　　　　　００：００：４１　｜　　　　　　　１．５６　｜　　　　　１．２　｜　　０．００１０　｜
｜　　８８　｜　１７５０　｜　　　　　００：００：４２　｜　　　　　　　０．６２　｜　　　　　０．２　｜　　０．００１０　｜
｜　　９０　｜　１８００　｜　　　　　００：００：４３　｜　　　　　　　１．５２　｜　　　　　１．１　｜　　０．００１０　｜
｜　　９３　｜　１８５０　｜　　　　　００：００：４４　｜　　　　　　　０．５５　｜　　　　　０．２　｜　　０．００１０　｜
｜　　９５　｜　１９００　｜　　　　　００：００：４６　｜　　　　　　　１．４８　｜　　　　　１．１　｜　　０．００１０　｜
｜　　９８　｜　１９５０　｜　　　　　００：００：４７　｜　　　　　　　０．５０　｜　　　　　０．１　｜　　０．００１０　｜
｜　１００　｜　２０００　｜　　　　　００：００：４８　｜　　　　　　　１．４４　｜　　　　　１．０　｜　　０．００１０　｜
｜　１０３　｜　２０５０　｜　　　　　００：００：４９　｜　　　　　　　０．４５　｜　　　　　０．１　｜　　０．００１０　｜
｜　１０５　｜　２１００　｜　　　　　００：００：５０　｜　　　　　　　１．４１　｜　　　　　１．０　｜　　０．００１０　｜
｜　１０８　｜　２１５０　｜　　　　　００：００：５１　｜　　　　　　　０．４１　｜　８．５ｅ－０２　｜　　０．００１０　｜
｜　１１０　｜　２２００　｜　　　　　００：００：５３　｜　　　　　　　１．３９　｜　　　　　１．０　｜　　０．００１０　｜
｜　１１３　｜　２２５０　｜　　　　　００：００：５４　｜　　　　　　　０．３７　｜　７．０ｅ－０２　｜　　０．００１０　｜
｜　１１５　｜　２３００　｜　　　　　００：００：５５　｜　　　　　　　１．３６　｜　　　　　０．９　｜　　０．００１０　｜
｜　１１８　｜　２３５０　｜　　　　　００：００：５６　｜　　　　　　　０．３３　｜　５．４ｅ－０２　｜　　０．００１０　｜
｜　１２０　｜　２４００　｜　　　　　００：００：５７　｜　　　　　　　１．３４　｜　　　　　０．９　｜　　０．００１０　｜
｜　１２３　｜　２４５０　｜　　　　　００：００：５８　｜　　　　　　　０．２９　｜　４．２ｅ－０２　｜　　０．００１０　｜
｜　１２５　｜　２５００　｜　　　　　００：０１：００　｜　　　　　　　１．３２　｜　　　　　０．９　｜　　０．００１０　｜
｜　１２８　｜　２５５０　｜　　　　　００：０１：０１　｜　　　　　　　０．２５　｜　３．２ｅ－０２　｜　　０．００１０　｜
｜　１３０　｜　２６００　｜　　　　　００：０１：０２　｜　　　　　　　１．２９　｜　　　　　０．８　｜　　０．００１０　｜
｜　１３３　｜　２６５０　｜　　　　　００：０１：０３　｜　　　　　　　０．２２　｜　２．５ｅ－０２　｜　　０．００１０　｜
｜　１３５　｜　２７００　｜　　　　　００：０１：０４　｜　　　　　　　１．２８　｜　　　　　０．８　｜　　０．００１０　｜
｜　１３８　｜　２７５０　｜　　　　　００：０１：０５　｜　　　　　　　０．２０　｜　２．０ｅ－０２　｜　　０．００１０　｜
｜　１４０　｜　２８００　｜　　　　　００：０１：０６　｜　　　　　　　１．２６　｜　　　　　０．８　｜　　０．００１０　｜
｜　１４３　｜　２８５０　｜　　　　　００：０１：０８　｜　　　　　　　０．１８　｜　１．６ｅ－０２　｜　　０．００１０　｜
｜　１４５　｜　２９００　｜　　　　　００：０１：０９　｜　　　　　　　１．２４　｜　　　　　０．８　｜　　０．００１０　｜
｜　１４８　｜　２９５０　｜　　　　　００：０１：１０　｜　　　　　　　０．１６　｜　１．３ｅ－０２　｜　　０．００１０　｜
｜　１５０　｜　３０００　｜　　　　　００：０１：１１　｜　　　　　　　１．２３　｜　　　　　０．８　｜　　０．００１０　｜
｜　１５３　｜　３０５０　｜　　　　　００：０１：１２　｜　　　　　　　０．１５　｜　１．１ｅ－０２　｜　　０．００１０　｜
｜　１５５　｜　３１００　｜　　　　　００：０１：１４　｜　　　　　　　１．２１　｜　　　　　０．７　｜　　０．００１０　｜
｜　１５８　｜　３１５０　｜　　　　　００：０１：１５　｜　　　　　　　０．１３　｜　８．４ｅ－０３　｜　　０．００１０　｜
｜　１６０　｜　３２００　｜　　　　　００：０１：１６　｜　　　　　　　１．２０　｜　　　　　０．７　｜　　０．００１０　｜
｜　１６３　｜　３２５０　｜　　　　　００：０１：１７　｜　　　　　　　０．１２　｜　６．８ｅ－０３　｜　　０．００１０　｜
｜　１６５　｜　３３００　｜　　　　　００：０１：１８　｜　　　　　　　１．１８　｜　　　　　０．７　｜　　０．００１０　｜
｜　１６８　｜　３３５０　｜　　　　　００：０１：１９　｜　　　　　　　０．１１　｜　５．６ｅ－０３　｜　　０．００１０　｜
｜　１７０　｜　３４００　｜　　　　　００：０１：２０　｜　　　　　　　１．１７　｜　　　　　０．７　｜　　０．００１０　｜
｜　１７３　｜　３４５０　｜　　　　　００：０１：２２　｜　　　　　　　０．１０　｜　４．８ｅ－０３　｜　　０．００１０　｜
｜　１７５　｜　３５００　｜　　　　　００：０１：２３　｜　　　　　　　１．１５　｜　　　　　０．７　｜　　０．００１０　｜
｜　１７８　｜　３５５０　｜　　　　　００：０１：２４　｜　　　　　　　０．０９　｜　４．１ｅ－０３　｜　　０．００１０　｜
｜　１８０　｜　３６００　｜　　　　　００：０１：２５　｜　　　　　　　１．１４　｜　　　　　０．７　｜　　０．００１０　｜
｜　１８３　｜　３６５０　｜　　　　　００：０１：２６　｜　　　　　　　０．０９　｜　３．８ｅ－０３　｜　　０．００１０　｜
｜　１８５　｜　３７００　｜　　　　　００：０１：２７　｜　　　　　　　１．１３　｜　　　　　０．６　｜　　０．００１０　｜
｜　１８８　｜　３７５０　｜　　　　　００：０１：２９　｜　　　　　　　０．０８　｜　３．６ｅ－０３　｜　　０．００１０　｜
｜　１９０　｜　３８００　｜　　　　　００：０１：３０　｜　　　　　　　１．１１　｜　　　　　０．６　｜　　０．００１０　｜
｜　１９３　｜　３８５０　｜　　　　　００：０１：３１　｜　　　　　　　０．０８　｜　３．２ｅ－０３　｜　　０．００１０　｜
｜　１９５　｜　３９００　｜　　　　　００：０１：３２　｜　　　　　　　１．１０　｜　　　　　０．６　｜　　０．００１０　｜
｜　１９８　｜　３９５０　｜　　　　　００：０１：３３　｜　　　　　　　０．０７　｜　２．５ｅ－０３　｜　　０．００１０　｜
｜　２００　｜　４０００　｜　　　　　００：０１：３４　｜　　　　　　　１．０８　｜　　　　　０．６　｜　　０．００１０　｜
｜＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝＝｜
训练结束: 已完成最大轮数。
```

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/figure_2.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/figure_2.png
)

可以看到我们目前用的cpu，而matlab是支持gpu的，gpu的速度要比cpu，快很多，这时候我们安装parallel computing toolbox

  

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_11.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_11.png
)

是

```matlab:Code
testNormal = {featureTest(1200, 2:end).Variables};
testAnomaly = {featureTest(200, 2:end).Variables};

% Predict decoded signal for both
decodedNormal = predict(net,testNormal);
decodedAnomaly = predict(net,testAnomaly);

% Visualize
helperVisualizeModelBehavior(testNormal, testAnomaly, decodedNormal, decodedAnomaly)
```

```text:Output
函数或变量 'helperVisualizeModelBehavior' 无法识别。
```

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_12.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_12.png
)

  

```matlab:Code
% Extract data Before maintenance
XTestBefore = helperExtractLabeledData(featureTest, "Before");

% Predict output before maintenance and calculate error
yHatBefore = predict(net, XTestBefore);
errorBefore = helperCalculateError(XTestBefore, yHatBefore);

% Extract data after maintenance
XTestAfter = helperExtractLabeledData(featureTest, "After");

% Predict output after maintenance and calculate error
yHatAfter = predict(net, XTestAfter);
errorAfter = helperCalculateError(XTestAfter, yHatAfter);

helperVisualizeError(errorBefore, errorAfter);
```

![/Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_13.png
](pingfan_images//Users/macowner/Documents/MATLAB/Examples/R2022a/predmaint_deeplearning/AnomalyDetectionUsing3axisVibrationDataExample/pingfan_images/image_13.png
)
