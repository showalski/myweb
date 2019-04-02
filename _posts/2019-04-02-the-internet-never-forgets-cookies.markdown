---
layout: post
lang: zh
title:  "The internet never forgets: cookies"
date:   2019-04-02 23:03:00 +0800
categories: [cookie]
---

反欺诈常被网站用来检测用户是否在同一台终端上有可疑的行为，如使用同一台电脑在一个网站上注册两次、同一个人是否进行的两次投票以及是否某个人使用多个信用卡执行可疑的行为。这些跟踪用户的行为的技术是一把双刃剑，也可以被用来收集用户个人信息以及所有的网页浏览记录，后再有的放矢地投放广告。这些技术早就被各大网站所使用，比如Google网站分析（Google Analytics）和百度广告联盟，可以用来收集访问网站的用户来自那个地理位置、访问持续时间、经由何种方式进入等信息，综合之后用于广告投放。

跟踪技术从早期的cookies到现在的fingerprinting（指纹提取）一直不断演化，其进化趋势朝着愈发高明且越难阻止的方向发展。如果你对网络安全比较了解且对个人隐私较敏感，想必你一定听过[Tor浏览器](https://zh.wikipedia.org/wiki/Tor)（外号洋葱头），即使如Tor浏览器也很难阻止一种叫做font fingerprinting的跟踪技术，目前还有一个针对此技术的迄今为止未被解决的[bug](https://trac.torproject.org/projects/tor/ticket/18097)（2016/01/19）。根据我目前的了解，font fingerprinting是最难阻住的设备指纹提取技术，其它的技术有矛攻之其盾。

cookie（HTTP cookie，小甜饼）技术早在1994年就被在Netscape（网景）公司Lou Montulli想到用做[用户跟踪](https://www.nytimes.com/2001/09/04/business/giving-web-a-memory-cost-its-users-privacy.html)，在2013年的315晚会上也被曝光过，那次晚会上并没有曝光太多的技术细节，而且cookie技术在不断向前发展。cookie是当用户浏览特定网页时服务器传送给用户的一些特殊数据，这些数据被存储在用户的机器上，当下次用户访问同一个网站时，浏览器将cookie传送给网站的服务器，从而达到用户跟踪，这些cookie包含一种标识符，功能类似身份证上的ID。cookie的种类分长度，315晚会曝光的应该是标准的HTTP cookie，可以通过浏览器或者其它隐私工具删除。有一种cookie技术叫做[evercookie](https://en.wikipedia.org/wiki/Evercookie)，其基于JavaScript，该技术将cookie以不同的形式存储到用户计算机中的不同位置，当一部分cookie（如标准的HTTP cookie）被删除后，其它的cookie还会被重新创建。根据2013年斯诺登解密的美国国家安全局的内部[PPT](https://www.theguardian.com/world/interactive/2013/oct/04/tor-stinks-nsa-presentation-document)显示，evercookie技术也被用于跟踪Tor浏览器的用户。

让乔布斯非常讨厌的Adobe Flash也会在本地计算机中存储叫做Flash Cookie（Local Shared Object），Flash cookie的存储位置有别于标准的HTTP cookie，使用浏览器删除历史数据的功能不能将其清除。如果你的电脑（如MAC）压根没有使能Flash功能则不用担心。Flash cookie的一大优点是可以在同一台设备的不同浏览器共享，跟踪用户效果更佳。在普林斯顿大学2014年的[研究](https://dl.acm.org/citation.cfm?id=2660347)中发现当时Alexa排名前100名中使用Flash cookie技术重建http cookie的网站有10个，有9个为中国的网站：

| 全球排名 | 网站        | 国家     |
| -------- | ----------- | -------- |
| 16       | sina.com.cn | 中国     |
| 17       | yandex.ru   | 俄罗斯   |
| 27       | weibo.com   | 中国     |
| 41       | hao123.com  | 中国     |
| 52       | soho.com    | 中国     |
| 64       | ifeng.com   | 中国香港 |
| 69       | youku.com   | 中国     |
| 178      | 56.com      | 中国     |
| 196      | letv.com    | 中国     |
| 197      | tudou.com   | 中国     |

虽然evercookie跟踪用户效果很好，但过度滥用会招来官司。根据美国连线杂志（Wired）[报道](https://www.wired.com/2012/10/kissmetrics-tracking/)，国外一家名叫KISSmetrics的公司曾因为使用类似的技术跟踪用户引发一场法律案件，最终以超过50万美元的赔偿解决。

### 如何保护免遭cookie跟踪

100%免遭cookie跟踪不切实际，但我们可以尽量少被跟踪。相较欧美用户而言，中国用户对网络隐私的关注度并不强，或者说不知道怎么去保护自己的隐私。这里想大家提供一些方法：

- 使用浏览器隐私模式：根据evercookie作者[个人博客](https://samy.pl/evercookie/)的描述，使用Safari浏览器的隐私模式浏览网页时，当浏览器重启后所有的evercookie都会被清除。其它主流浏览器如Firefox和Chrome应该也可使用类似的方式删除cookie，但有待验证。
- 隐私獾（Privacy Badger）插件：一直使用隐私浏览模式在大多数情况下并不适用，比如我们有时想让浏览器记住一些网站的密码，方便下次登陆时无需再次输入密码。这里推荐使用EFF（电子前哨基金会）的隐私獾（Privacy Badger）插件，该插件可以自动检测潜在的跟踪器并阻止跟踪行为。其主要工作方式是，当在访问三个不同的网站时，如果检测到这些网站加载了相同的第三方资源（如JavaScript）则会拦截该资源。

使用上述方式不能完全避免跟踪，更高级的fingerprinting（指纹提取）技术可以不在用户计算机上存储任何数据也能实现同等甚至更优于cookie的的能力。