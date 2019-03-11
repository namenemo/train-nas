# Train-NAS
Train and Compare NAS models including Autokeras, DARTS, ENAS and NAO.

## Introduction
I am interesting in neural architecture search, so I downloaded the official source code from the Github and hope to reproduce the results in the paper.

Their source code link is as below:

- Autokeras: https://github.com/jhfjhfj1/autokeras

- DARTS: https://github.com/quark0/darts

- ENAS: https://github.com/melodyguan/enas

- NAO: https://github.com/renqianluo/NAO

## Experiment Description

To avoid overfitting in **CIFAR-10** (I hate this dataset) , I also compare the models in the other five datasets including Fashion-MNIST, CIFAR-100, OUI-Adience-Age, ImageNet-10-1 (subset of ImageNet), ImageNet-10-2 (another subset of ImageNet).

I do not change the default fine-tuning technique in their source code. In order to match each task, I change the code of input image shape and output numbers. 

Search phase time for all NAS methods is two days as well as the retrain time.  Average results are reported based on three repeat times.

For NAO, it requires too much computing resources, so I only use NAO-WS that provides the pipeline script.

For AutoKeras, I used the 0.2.18 version because it was the latest version when I started my experiment.


## NAS Performance 

| NAS             | AutoKeras (%) | ENAS (macro) (%) | ENAS (micro) (%) | DARTS (%) | NAO-WS (%) |
| --------------- | :-----------: | :--------------: | :--------------: | :-------: | :--------: |
| Fashion-MNIST   |     91.84     |      95.44       |      95.53       | **95.74** |   95.20    |
| CIFAR-10        |     75.78     |      95.68       |    **96.16**     |   94.23   |   95.64    |
| CIFAR-100       |     43.61     |      78.13       |      78.84       | **79.74** |   75.75    |
| OUI-Adience-Age |     63.20     |    **80.34**     |      78.55       |   76.83   |   72.96    |
| ImageNet-10-1   |     61.80     |      77.07       |      79.80       | **80.48** |   77.20    |
| ImageNet-10-2   |     37.20     |      58.13       |      56.47       |   60.53   | **61.20**  |



Unfortunately, I cannot reproduce all the results in the paper. 

The best or average results reported in the paper:

| NAS      | ENAS (macro) (%) | ENAS (micro) (%) |   DARTS (%)    | NAO-WS (%)  |
| -------- | :--------------: | :--------------: | :------------: | :---------: |
| CIFAR-10 |   96.13(best)    |   97.11(best)    | 97.17(average) | 96.47(best) |



For AutoKeras, the initial model of 0.2.18 version has a poor performance on all datasets. That's no wonder ResNet and DenseNet are added to the initial model list in the later version.

For ENAS, ENAS (macro) shows good result in OUI-Adience-Age and ENAS (micro)  shows good result in CIFAR-10. 

For DARTS, it has a good performance on some datasets but I found its high variance in other dataset. The difference among three runs of benchmarks can be up to 5.37% in OUI-Adience-Age and 4.36% in ImageNet-10-1.

For NAO-WS, it shows good results in ImageNet-10-2 but it can perform very poorly in OUI-Adience-Age.



## Reference

1. Jin, Haifeng, Qingquan Song, and Xia Hu. "Efficient neural architecture search with network morphism." *arXiv preprint arXiv:1806.10282* (2018).

2. Liu, Hanxiao, Karen Simonyan, and Yiming Yang. "Darts: Differentiable architecture search." arXiv preprint arXiv:1806.09055 (2018).

3. Pham, Hieu, et al. "Efficient Neural Architecture Search via Parameters Sharing." international conference on machine learning (2018): 4092-4101.

4. Luo, Renqian, et al. "Neural Architecture Optimization." neural information processing systems (2018): 7827-7838.

   

