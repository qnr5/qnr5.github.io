---
title: 如何让mediawiki支持中文检索
---
假设你有一个网站example.com，它是你建立的一个mediawiki站点。当你建立好example.com之后，创建了许多内容，站内搜索自己的内容时，你会发现搜英文效果不错，但搜中文效果不好。那在安装自己的mediawiki站点之后，如何让它对站内中文检索的效果更好一些呢？

其实方法就是安装CirrusSearch这个扩展。安装此扩展，若细心地按照[官方wiki](https://www.mediawiki.org/wiki/Extension:CirrusSearch)一步步来，就不会出错。但踩坑往往在一瞬间，最容易踩坑的，就是在依赖安装时，少安装了。

依赖如下：
* php 这个一般早就在安装mediawiki站点前就已安好
* curl 这个未必有，容易缺，去链接中看下你的Linux发行版需要哪个libcurl并安装
* elasticsearch 它的版本很重要，不同版本行为不同，按wiki教程中的建议选好elasticsearch的版本。不要用apt安装最新版elasticsearch，手动选合造的版本
* openjdk 这个未必有，容易缺，去链接中看下你的Linux发行版适合哪个openjdk-<版本>-jre并安装
* elastica 按照wiki安装就ok，不易错
* cirrussearch 按照wiki安装后，需要按照其README文档生成mediawiki的内容索引，前面的步骤无误则此步骤不易错。若前面容易缺的依赖未正确安装，本步骤100%出错

别的没有要注意的了。
