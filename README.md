## how to run
```
npm run server
```
## how to use hexo-cli
```
npx hexo
```
## how to update blog
```
hexo clean // 清除之前建立的靜態檔案
hexo generate // 建立靜態頁面
hexo deploy // 部署至 GitHub
```
or
```
npm run deploy
```

## how to create a new post

```
npx hexo new POSTTITLE
```

## Hexo deploy 到 Github 後, 發現 commit 全沒了

在 deploy 時的動作是

1. 檢查有無 .deploy_git 資料夾, 如無則建立, 並做 initial commit
2. 複製 public 資料夾內容到 .deploy_git 資料夾
3. commit 並 push 至 Github

會發生 commit 紀錄不見的原因

1. 沒有 .deploy_git 資料夾, 導致 deploy 時重新建立
2. deploy 時 push 到 Github 時, 加了參數 -f

解決辦法

