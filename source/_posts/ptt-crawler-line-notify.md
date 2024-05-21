---
title: ptt-crawler-line-notify
date: 2024-05-21 18:14:16
tags: 
- LINE Notify
- ptt crawler
- GitHub Actions
categories:  
---
# 用 Line notify 傳遞 ptt 爬蟲資料

[github](https://github.com/superTO/ptt-crawler-schedule)

## 原定流程

github action 執行爬蟲程式 => github action 觸發 Line notify

1. 爬蟲程式
2. github action
- 在github action 時, 載入data.js 檔案(設定成secrets)
- line notify 顯示問題 \n換行
- Environment variables 在這邊設定要爬的內容&回傳訊息
3. line notify 通知

## 遇到的問題

1. github action 如果使用 schedule: 無法設定觸發的 branch
    - 只能直接綁定執行的branch
        - 但會導致 workflow_dispatch: 選擇branch觸發無效

:::warning
**沒有解決**
schedule: 使用 default branch 觸發, 就改用 default branch 版本控制
:::
2. 無法將 node index.js 回傳的資料, 直接透過 github action 傳遞參數給 line notify

:::success
**解決**
改用 writeFileSync 輸出 .txt, github action 透過讀檔傳遞資料
:::
3. Line notify 每次傳訊息字數上限為1000
    - 因為 github action forloop 執行 step 有障礙, 大改版

:::success
**解決**
將 github action 精簡, 不使用 writeFileSync 輸出檔案, 改為爬蟲後呼叫Line notify API
[commit](https://github.com/superTO/ptt-crawler-schedule/commit/77f2cee9b9542ea2cf1d2061367be4fb81c9a557)
:::
4. Line notify 傳遞訊息時, 可能順序不對

:::success
**解決**
追加 sleep()
:::
5. PTT爬蟲資料只有內文才有完整日期

:::success
**未知**
原因: 追加功能 "只顯示幾天前的資料"
解法: 透過12&1月來判斷年分
[commit](https://github.com/superTO/ptt-crawler-schedule/commit/96789b16304d11979e6feff4bf4b2cdc308dcee8)
:::

## 最終流程

1. github action 只用來建立執行環境 & 執行

forloop
2. 爬蟲執行
3. 資料轉換
4. 資料過濾
5. 爬蟲結束
END forloop 

6. line notify 傳訊息

## 後續可能的補充

1. 想要把參數隱藏起來
- github Environment variables
