# 深入理解Plazma（二）Plasma 细节剖析

> 这一系列文章将围绕以太坊的二层扩容框架，介绍其基本运行原理，具体操作细节，安全性讨论以及未来研究方向等。本篇文章主要对 Plasma 一些关键操作的细节进行剖析。

在[上一篇](https://github.com/gitferry/mastering-ethereum/blob/master/Plasma-in-depth/plasma-in-depth.md)文章中我们已经理解了什么是 Plasma 框架以及它是如何运行的，这一篇文章将对其运行过程中的一些关键部分，包括 Plasma 提交区块的过程，当有恶意行为发生时如何构建防伪证明以及如何退出 Plasma 子链等进行剖析。

## 提交区块

从下图（来源自[[1]](https://plasma.io/)）中我们可以看到 Plasma Chain 向主链提交的过程。需要注意的是，Plasma Chain 只有在Plasma Chain 并不向主链公开每个区块的内容，而是

<img src="./images/Building-blocks.png"  width="700" height="350" alt="Blockchains of Blockchain" />

## 防伪证明

## 退出子链

<!--## 层级结构

## 安全性讨论

## Plasma 研究现状-->

## 相关资源

1. [https://plasma.io/](https://plasma.io/)
