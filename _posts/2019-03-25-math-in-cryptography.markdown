---
layout: post
lang: zh
title:  "密码学中的数学知识"
date:   2019-03-25 21:30:00 +0800
categories: [cryptography]
---
本文中有较多的数学公式需要渲染，若不能正常显示请多刷新几次即可。

### 异或运算

异或运算在密码学中被大量使用，它具有如下性质：

* 均匀分布：

  * 假设随机变量X和Y在集合$$\{0, 1\}^n$$上随机分布，X独立于Y，那么变量$$Z = X \oplus Y$$在空间$$\{0, 1\}^n$$上也是均匀分布的。集合$$U = \{0, 1\}^2 = \{00, 01, 10, 11\}$$，即集合U由四个长度为两个bit的二进制的数组成的集合。

  * 设m和k为n bit数，k在集合$$U = \{0, 1\}^n$$上均匀分布，那么$$c = m \oplus k$$也是均匀分布的。证明参考[这里][xor_dis_proof]。这里的c为密文，m为明文，k为密钥。

* [同等概率][xor_prob]:设a和b是{0, 1}空间中的随机变量，即a和b为0或1。根据真值表计算：a & b得到0的概率为75%，得到1个概率为25%；$$a \mid b$$得到0的概率为25%，得到1的概率为75%；而$$a \oplus b$$得到0或者1的概率都是50%。

* 可逆性：设c为密文，m为明文，k为密钥，有等式$$c = m \oplus k, m = c \oplus k$$，即在使用同一个密钥时，异或运算既可以得到密文也可得到明文。这种加解密的方式在one time pad中用到。[参考][xor_reverse]。

[xor_prob]: https://stackoverflow.com/questions/5889238/why-is-xor-the-default-way-to-combine-hashes
[xor_dis_proof]: https://math.stackexchange.com/questions/441329/how-to-prove-uniform-distribution-of-m-oplus-k-if-k-is-uniformly-distributed
[xor_reverse]: https://stackoverflow.com/questions/1379952/why-is-xor-used-in-cryptography
