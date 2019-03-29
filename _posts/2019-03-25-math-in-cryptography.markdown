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

### 素数

素数在密码学中的应用非常广泛，Diffie-Hellman key exchange和RSA中都会选择一个很大（如包含600个数字）素数作为模幂运算的模数。

* 互素：在数论中，如果两个或两个以上的整数的最大公因数是1，即[Greatest common divisor（GCD）][gcd]，则称它们为互素。如果gcd(a, b) = 1, 则a和b[互素][coprime]（relatively prime, co-prime）

* 欧拉函数$$\Phi(n)$$：欧拉函数$$\Phi(n)$$是小于或者等于n的正整数中与n互素的数目。欧拉函数在RSA公钥加密算法中可以快速计算公钥和密钥的值。

    * 若n为素数，则$$\Phi(n) = n - 1$$

    * 欧拉函数满足：$$\Phi(A \times B) = A \times B$$

* 欧拉定理：若n，m为正整数，且n，m互素（gcd（n，m）=1），则

    * $$m^{\Phi(n)} \equiv 1\bmod n$$，即$$m^{\Phi(n)}\bmod n = 1$$

* 原根：设p为素数，满足条件$$g^i\bmod p \neq g^j\bmod p$$，$$i\neq j\ and\ i,j\in [1,p - 1]$$，则称为g为p的原根。如果依据$$g^i\bmod p, i \in [1, p - 1]$$画一张表的话，表中每个元素的值都是不同的；如果将该公式作为一个黑盒子，那么获取表中任意一个值的概率是相同的。

    * 上述原根的特性使得构造单向函数f(x)（[one way function][one-way-func]）成为可能，即给定x的值以及f(x)的算法得到f(x)很容易，但给定f(x)的值和以及f(x)的算法反向获取x的值却很难，这里$$f(x) = g^i\bmod p, f^{-1}(x) = \log_p g$$，Diffie-Hellman Key Exchange就是构建于不能有效求解[离散对数难题][dis-log]$$f^{-1}(x)$$上的公钥加密算法。


[xor_prob]: https://stackoverflow.com/questions/5889238/why-is-xor-the-default-way-to-combine-hashes
[xor_dis_proof]: https://math.stackexchange.com/questions/441329/how-to-prove-uniform-distribution-of-m-oplus-k-if-k-is-uniformly-distributed
[xor_reverse]: https://stackoverflow.com/questions/1379952/why-is-xor-used-in-cryptography
[gcd]: https://en.wikipedia.org/wiki/Greatest_common_divisor
[coprime]: https://en.wikipedia.org/wiki/Coprime_integers
[one-way-func]: https://en.wikipedia.org/wiki/One-way_function
[dis-log]: https://en.wikipedia.org/wiki/Discrete_logarithm