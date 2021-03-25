# Generative Model For Music

* 效果上能够生成曲子而且包括歌词
* VAE variable auto encoder,传统encoder-decoder模型压缩图像到一个向量或者矩阵，VAE在中间的表整层，采用表征向量作为参数来参数描述三个高斯函数，再从三个高斯函数中采样一个三维矩阵喂给decoder
* VQ-VAE 中间的表征层是针对一个code book采样的“参考书”，encoder、code book、decoder都是训练得来的
* 多粒度地训练encoder和decoder
* 训练神经网络做到高斯函数采样->低采样->中采样->高采样的生成器
* 这样一个高斯函数可以生成一个适用于decoder的3个vector分别代表低采用、中采样、高采样，经过decoder可以生成我们想要的音乐
* how to combine?——through upsample （一个网络）和conditioning information(另一个网络)来合并多个层级的特征
* lyrics conditioning

