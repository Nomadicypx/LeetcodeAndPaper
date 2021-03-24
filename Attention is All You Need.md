# Attention is All You Need

* 这篇论文如雷贯耳，上学期上深度学习课的时候就没听懂，现在重新看一遍还是没懂，只能聊一聊感性认识
* attention是早就有了的一个东西，最早应用于sequence-sequence with self attention的模型中，改模型将所有hidden state存储起来并且算出一个score vector作为选择窗口决定喂到decoder里头的输入参数这个score vector的计算和使用就是attention的来源
* transformer在encoding阶段生成了三个vector分别是query、key、value，前两个vector共同计算了一个score vector来修正第三个vector作为喂给decoder的输入参数
* 采用了一个positional encoding的网络来决定词的位置，位置编码的方式我没有细看
* transform里头使用了残差学习
* 最后的输出softmax的参数是整个词库的长度