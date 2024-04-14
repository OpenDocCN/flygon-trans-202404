### 导航

+   [索引](genindex.html "总索引")

+   [下一步](a_little_book_of_python_for_multivariate_analysis.html "Python 多元分析小册子") |

+   [Python 多元分析小册子 0.1 文档](#) »

# Python 多元分析小册子

本小册子告诉您如何使用 Python 生态系统进行一些简单的多元分析，重点是主成分分析（PCA）和线性判别分析（LDA）。

jupyter notebook 可以在其[github 仓库](https://github.com/yianni/a_little_book_of_python_for_multivariate_analysis) [https://github.com/yianni/a_little_book_of_python_for_multivariate_analysis]找到。

## 笔记

本小册子假设读者具有一些多元分析的基础知识，而且小册子的主要重点不是解释多元分析，而是解释如何使用 Python 进行这些分析。

函数中的命名约定保持与原始源的一致性。变量被重命名为更通用的名称，因此如果您的数据的第一列包含数据类，则可以加载自己的数据集并运行笔记本。请参阅读取数据的单元格。

Python 代码旨在易于理解，就像原始源中的 R 代码一样，而不是具有计算和内存效率。

## 目录

+   [Python 多元分析小册子](a_little_book_of_python_for_multivariate_analysis.html)

    +   [设置 Python 环境](a_little_book_of_python_for_multivariate_analysis.html#setting-up-the-python-environment)

        +   [安装 Python](a_little_book_of_python_for_multivariate_analysis.html#install-python)

        +   [库](a_little_book_of_python_for_multivariate_analysis.html#libraries)

        +   [导入库](a_little_book_of_python_for_multivariate_analysis.html#importing-the-libraries)

        +   [Python 控制台](a_little_book_of_python_for_multivariate_analysis.html#python-console)

    +   [将多元分析数据读入 Python](a_little_book_of_python_for_multivariate_analysis.html#reading-multivariate-analysis-data-into-python)

    +   [绘制多元数据](a_little_book_of_python_for_multivariate_analysis.html#plotting-multivariate-data)

        +   [矩阵散点图](a_little_book_of_python_for_multivariate_analysis.html#a-matrix-scatterplot)

        +   [带有数据点标签的散点图](a_little_book_of_python_for_multivariate_analysis.html#a-scatterplot-with-the-data-points-labelled-by-their-group)

        +   [概要图](a_little_book_of_python_for_multivariate_analysis.html#a-profile-plot)

    +   [计算多元数据的汇总统计信息](a_little_book_of_python_for_multivariate_analysis.html#calculating-summary-statistics-for-multivariate-data)

        +   [每个组的平均值和方差](a_little_book_of_python_for_multivariate_analysis.html#means-and-variances-per-group)

        +   [一个变量的组间方差和组内方差](a_little_book_of_python_for_multivariate_analysis.html#between-groups-variance-and-within-groups-variance-for-a-variable)

        +   [两个变量的组间协方差和组内协方差](a_little_book_of_python_for_multivariate_analysis.html#between-groups-covariance-and-within-groups-covariance-for-two-variables)

        +   [计算多元数据的相关性](a_little_book_of_python_for_multivariate_analysis.html#calculating-correlations-for-multivariate-data)

        +   [变量标准化](a_little_book_of_python_for_multivariate_analysis.html#standardising-variables)

    +   [主成分分析](a_little_book_of_python_for_multivariate_analysis.html#principal-component-analysis)

        +   [确定保留多少主成分](a_little_book_of_python_for_multivariate_analysis.html#deciding-how-many-principal-components-to-retain)

        +   [主成分的载荷](a_little_book_of_python_for_multivariate_analysis.html#loadings-for-the-principal-components)

        +   [主成分的散点图](a_little_book_of_python_for_multivariate_analysis.html#scatterplots-of-the-principal-components)

    +   [线性判别分析](a_little_book_of_python_for_multivariate_analysis.html#linear-discriminant-analysis)

        +   [判别函数的载荷](a_little_book_of_python_for_multivariate_analysis.html#loadings-for-the-discriminant-functions)

        +   [判别函数实现的分离度](a_little_book_of_python_for_multivariate_analysis.html#separation-achieved-by-the-discriminant-functions)

        +   [LDA值的堆叠直方图](a_little_book_of_python_for_multivariate_analysis.html#a-stacked-histogram-of-the-lda-values)

        +   [判别函数的散点图](a_little_book_of_python_for_multivariate_analysis.html#scatterplots-of-the-discriminant-functions)

        +   [分配规则和误分类率](a_little_book_of_python_for_multivariate_analysis.html#allocation-rules-and-misclassification-rate)

            +   [Python方式](a_little_book_of_python_for_multivariate_analysis.html#the-python-way)

    +   [链接和进一步阅读](a_little_book_of_python_for_multivariate_analysis.html#links-and-further-reading)

    +   [致谢](a_little_book_of_python_for_multivariate_analysis.html#acknowledgements)

    +   [联系方式](a_little_book_of_python_for_multivariate_analysis.html#contact)

    +   [许可证](a_little_book_of_python_for_multivariate_analysis.html#license)

## 许可证

[![知识共享许可证](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

《Python多元分析小书》由Yiannis Gatsoulis根据[知识共享署名-相同方式共享4.0国际许可协议](http://creativecommons.org/licenses/by-sa/4.0/)许可。

基于 Avril Coghlan 的 [《R 多元分析小册子》](https://little-book-of-r-for-multivariate-analysis.readthedocs.org/en/latest/src/multivariateanalysis.html) 的作品，使用 [CC-BY-3.0](http://creativecommons.org/licenses/by/3.0/) 许可。© 2016 版权所有，Yiannis Gatsoulis 创作。使用 [Sphinx](http://sphinx-doc.org/) 1.3.4 创建。
