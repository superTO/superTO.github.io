---
title: git
date: 2021-10-19 20:28:36
tags: git
---
## 簡單判斷git能力
1. 能看懂 git log 內容
![git log](2021-10-19image.png)
2. 知道 HEAD -> source 和 origin/source 意思
3. 知道 origin 如何產生

## 講解 HEAD -> source 和 origin/source 意思

- 當使用 git commit 後 local 會多一個 commit, 如下圖 HEAD -> source 位置變更了
- 接著當使用 git push 會將 local 的 commit 推送到 origin/source 另 origin/source 和 local 同步
![git log - git commit 後](2021-10-19image2.png)

- origin/source 指的是該 branch 最後一次和 origin 同步的 commit 所在的位置

## 講解 origin 如何產生
- 可以使用 git remote -v 可以看到
![git remote -v](2021-10-19image3.png)
- 這樣就可以知道「git push origin main」的意思了

## 補充 git remote add
- 執行下列指令後 git remote -v 的變化
```
git remote add upstream git@github.com:superTO/Leetcode.git
```
![git remote -v - git remote add upstream git@github.com:superTO/Leetcode.git 後](2021-10-19image4.png)

- 之後使用「git pull upstream master」就可以直接對 git@github.com:superTO/Leetcode.git 的 master 這條 branch 執行 fetch + merge
```
這個方法在 fork 專案後, 如果版本落差太大會使用到
```
