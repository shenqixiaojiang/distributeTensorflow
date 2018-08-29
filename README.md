# 加速策略1——分布式系统

### [Horovod](https://github.com/uber/horovod) -> 推荐
Uber 出的一套分布式计算平台，支持TF、pytorch、Keras。 

优点：速度快且部署简单，几乎可以达到90%的扩展比。 <br>
缺点：<br>
* 性能不稳定，需要较trick的参数更新策略。<br>
* 物理环境下当节点增多时，容易出现节点拼不通的问题，直接导致异常。docker环境比物理环境更稳定。因此在节点很多时，建议使用docker环境。<br>


### [TF原生分布式](https://blog.csdn.net/hjimce/article/details/61197190) <br>
传统worker全部与ps通信的方式。worker与ps的通信问题是性能的主要瓶颈，大大限制了其扩展性。单机8卡的速度只是原始单卡的3.x倍，仅Horovod单机8卡速度的一半。

优点：训练较稳定。 <br>
缺点：速度慢，扩展性差。<br>

# 加速策略2——混合精度训练
首先你需要一台V100——V100对混合精度训练实现了硬件上的加速。<br>
[nvidia示例代码](https://github.com/NVIDIA/DeepLearningExamples/blob/master/TensorFlow/Classification/imagenet/nvcnn_hvd.py)

# 加速策略3——[DALI](https://github.com/NVIDIA/DALI)
传统的编解码都是在CPU上完成的。DALI使用GPU对图像编解码实现加速。<br>

安装要点：<br>
* 编译过程需要Boost库，安装请看[Here](https://github.com/shenqixiaojiang/installOthers)。 <br>
* 如果你安装了nvJPEG-library库，那么libjpeg-turbo库则不是DALI必须的了。因此可以在cmake的过程中关闭。<br>

