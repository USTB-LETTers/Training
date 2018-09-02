
# LETTers Solution Report

- Date: 2nd Sep 2018
- Author: Mirrorera
- Problem ID:  **Nanjiing Online Contest** [L](https://nanti.jisuanke.com/t/31001)

## Description modeling

 - 给定一无向图，最多允许把 K 条边的点权变为 0，求此图上 1 到 N 的最短路

## Points in solving

 - 仍使用dijkstra进行最短路，不同的是，进行松弛操作时，额外考虑把当前边权视为0的情况，对每次松弛操作得到的新dis[i]，记录一个额外的k值表示当前把几条边权视为了0，把该k值和dis一起压入维护最近点的优先队列中，用每条边扩展时，若当前取出点k值小于K，则进行边权为0和不为0的两次尝试松弛

## Warnings

 - None.
