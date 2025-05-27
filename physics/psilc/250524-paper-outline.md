# 250524-paper outline

几个重点

1. 强调点源TF拟合的优势在于小口径望远镜会重叠，这样可以考虑其他点源的贡献。可能要算一些东西
2. 强调用了NILC，可以得到clean的map，还可以用来做功率谱的分析，做交叉验证。

第二节通过模拟来比较方法论。

第四节当forecast

* EB leakage 太多了 整附录里。
* result部分文字僵硬
* coadd 和nilc比较。
* 流程写的集中一些

现在要算不同方法点源的bias，就在天图层面把对点源操作过之后的图，减去cfn，然后拿这个图去算bias的功率谱。对于removing方法，直接用unresolved点源加入去算功率谱，然后拿pcfn减去这个值，得到rmv自身的bias。
