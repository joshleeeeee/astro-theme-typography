---
title: 各种数据范围下的算法选择
tags:
  - 算法
  - 技巧
categories:
  - 算法
mathjax: true
pubDate: 2022-04-08 10:43:04
---


|     数据范围      |       时间复杂度        |                             算法                             |
| :---------------: | :---------------------: | :----------------------------------------------------------: |
|     $n\le30$      |        $O(2^n)$         |                    DFS+剪枝，状态压缩 DP                     |
|     $n\le100$     |        $O(n^3)$         |                     DP，Floyd，高斯消元                      |
|    $n\le1000$     | $O(n^2)$, $O(n^2logn)$  |     DP，二分，朴素版 Dijkstra、朴素版 Prim、Bellman-Ford     |
|    $n\le10^4$     |     $O(n*\sqrt{n})$     |                     块状链表、分块、莫队                     |
|    $n\le10^5$     |       $O(nlogn)$        | Sort、线段树、树状数组、Set、Map、Heap、拓扑排序、Dijkstra+Heap、Prim+Heap、Kruskal、SPFA、求凸包、求半平面交、二分、CDQ 分治、整体二分、后缀数组、树链剖分、动态树 |
|    $n\le10^6$     |  常数较小的$O(nlogn)$   | 单调队列、Hash、双指针扫描、并查集、KMP、AC 自动机、Sort、树状数组、Heap、Dijkstra、SPFA |
|    $n\le10^7$     |          $(n)$          |            双指针扫描、KMP、AC自动机、线性筛素数             |
|    $n\le10^9$     |      $O(\sqrt{n})$      |                           判断质数                           |
|   $n\le10^{18}$   |        $O(logn)$        |                 最大公约数、快速幂、数位 DP                  |
|  $n\le10^{1000}$  |       $O(logn)^2$       |                        高精度加减乘除                        |
| $n\le10^{100000}$ | $O(logk\times loglogk)$ |               k 表示数位、高精度加减、FFT/NTT                |



