# 图像分类问题经典论文

* 最近刚刚开始规律阅读论文，一篇论文往往篇幅受限或者由于本人学术水平有限不能够很好的把握文章的要义，所以在起步阶段我想先通过视频导读的方式来接触一些学术的概念
* [B站百大经典论文导读分享](https://www.bilibili.com/video/BV1tU4y147Ah?p=1&share_medium=android&share_plat=android&share_source=COPY&share_tag=s_i&timestamp=1614401105&unique_k=xJu09h)现在先基于这个链接中的内容广泛了解AI领域的概念，有一定基础后跟读固定领域内的文章
* 整篇文章讨论的问题：ImageNet数据上表现良好的模型是否存在过拟合到了testing data的程度？如果我们重新构建一个testing data set是否会出现模型效果变差的情况
* 实验结果：新构建的test data set并没有形成一个曲线，而同样是一条跟原有test data set在accuracy上一致的直线，但是存在着与理想状况下50%-50%的线段基本平行的情况
* 论文假设：这样的现象说明准确性由数据集合决定，模型通过超参数的调优仍然具有较好的泛化性能，数据集的差异性体现在adaptive gap、distribution gap、generalization gap三个方面，drop的出现主要是distribution gap 导致的
* 个人理解:adaptive gap是作者假设成立的根源，但根据实际的实验结果来看,adaptive gap并没有随着model在v1 test data上的performance 提高而变大，所以accuracy 曲线呈现为直线，而不是作者假设的一条坍缩的曲线
