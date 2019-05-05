# CNS_Final
Final Project: Whitebox Attack on Image Classification models

# CNS Final Proposal
b05902121 黃冠博, b05902045 宋哲寬, b05902120 曾鈺婷, b05902113 陳宏昇

## Problem	description
我們要做的事情跟[Face Recognition Attack](https://www.cs.cmu.edu/~sbhagava/papers/face-rec-ccs16.pdf)這篇paper很像，給定一個已知內部結構跟演算法的whitebox model，針對這個model的input做一些改動，好讓原本能正確辨識圖片的model因為這些adversarial image出現預測錯誤的情況。不同於上述提到的paper之處在於我們要做的是non-target attack，也就是說只要盡可能讓model predict錯就好，不用讓model硬是把某個類別predict成另一個類別(target attack)。

### Threat Model
- 我們所謂的whitebox已知的資訊如下(也就是攻擊者所知道的資訊)：
    - 使用的是哪一種model，比如說：resnet50, dense121, vgg19 ...
    - model 的 data preprocessing 是如何處理的，比如說圖片的normalize
    - model對input做的防禦機制，比如說:Gaussian Filter, Median filter, Bilateral filte
- 攻擊者的能力範圍：
    - 攻擊者持有一些 model 能正確辨識的input
    - 攻擊者能對input做任意修改並讓model做預測

## Related work
### How is it done today?
- [deepfool](https://arxiv.org/pdf/1511.04599.pdf)
- [foolbox](https://github.com/bethgelab/foolbox)
- [adversarial-robustness-toolbox](https://github.com/IBM/adversarial-robustness-toolbox)
### What are the limitations of	current	practice?
- 目前這些現成的攻擊套件比較generalize，拿L-infinity去換攻擊的成功率，好讓這些套件能夠對付各種model，但是你會發現這些縣城套件產出的圖片通常L-infinity不小
- 目前的套件大多只能給他一個proxy model下去做攻擊，也就說他只知道model是什麼，所以常常攻擊成功率不一定很高
## Plan
### Approach
### Plan for Evaluation
- 攻擊的成功率(accuracy準確率)，只要model將某張圖片預測成不同於ground truth label的類別就算攻擊成功
- 攻擊後的圖片(adversarial image)與原圖的最大差距(L-infinity)
    - adversarial image是原圖加上noise，將adversarial image 跟原圖的每個pixel相減，取最大值，就是 L-infinity norm，也就是下列式子的$|x|_{\infty}$
$\mathcal{x} = [x_1,x_2, \cdots, x_n]$
$|x|_{\infty} = \max\limits_{i} |x|_{i}$
- 準確率越高的同時，希望L-infinity越低
## Timeline

## Deliverables
- 找出一個改善現有的攻擊套件的方法，使得攻擊能夠針對某個特定dataset有高準確率(90%以上)以及低L-infinity(平均5.00以下)
- 對於已知的model防禦，想辦法做出讓model防禦失敗的adversial image
