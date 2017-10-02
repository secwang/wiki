---  
title: "r and machinelearning"   
date: 2017-08-20 17:08
---  
[TOC]  
  
## basic r usage
starndard Deviation(SD)   标准差  sd()  
$$
\sigma_N = \sqrt{\frac{1}{N}\sum_{i=1}^{N}(x_i-\overline{x})^2}
$$

Variance:(SD^2)  var()  
$$
\sigma^2 = \frac{1}{N}\sum_{i=1}^{N}(x_i -\overline{x})^2
$$

Range:(Max-min)  
$$
min - max
$$

Quartiles 抽样 quantile()  
Inter quartile Range(IQE) 
coefficient of variation :  

$$
CV = \frac{SD}{\overline{x}} *100
$$

```

```


## bivariate analysis
问题就是做 相关性检验，比如有两列数据，是否可以判断有相关性。


### Continuous verus continuous:
cor.test
### Continuous Versus categorical:
anovamod
### categorical versus categorical:
chisq.test




