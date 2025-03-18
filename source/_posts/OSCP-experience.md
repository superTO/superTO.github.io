---
title: OSCP-experience
date: 2025-03-17 22:25:23
tags:
- OSCP
categories:
---
# OSCP 考試心得

最後更新時間: 2025-3-2
- 考試沒通過QQ

## 注意事項
1. 記得加入官方discord方便求救&看其他人討論, 記得要領身分組
2. 在頻道 PEN-200-module-labs 輸入 /pen-200-hint 會有更進一步的提示 
3. [Report template](https://help.offsec.com/hc/en-us/articles/360046787731-PEN-200-Reporting-Requirements)
    - 如果要使用 noraj/OSCP-Exam-Report-Template-Markdown 要處理版本問題請參考[下方](#OSCP-Exam-Report-Template-Markdown)
    - 例如: [圖片太大會被切掉](https://github.com/noraj/OSCP-Exam-Report-Template-Markdown/issues/63)
    - 要省時間可以使用word
4. 考試期間可以看OSCP教材
    - [OSCP Exam Guide](https://help.offsec.com/hc/en-us/articles/360040165632-OSCP-Exam-Guide)
5. 觀看別人的解題過程
    - [0xdf](https://0xdf.gitlab.io/)
6. Challenge lab - OSCP A、B、C 是模擬考每個都有 6 台機器
7. AD 題組一定會有 Port Forwarding 請熟練
    - 推薦使用 [ligolo-ng](#ligolo-ng)
8. AD 非常重要, 不熟請看[Derron C的教學](https://youtube.com/playlist?list=PLT08J44ErMmb9qaEeTYl5diQW6jWVHCR2&si=6l6hLA0WVVTNzqKJ)

## [OSCP-Exam-Report-Template-Markdown](#OSCP-Exam-Report-Template-Markdown)

1. https://github.com/noraj/OSCP-Exam-Report-Template-Markdown
- 前置安裝
```
sudo apt update
sudo apt install 7zip
sudo apt install lexlive
sudo apt install pandoc
```
- 我用的版本
```
pandoc 3.1.11.1
eisvogel 2.4.2
```
2. Download [2.4.2版本](https://github.com/Wandmalfarbe/pandoc-latex-template/releases/tag/2.4.2)
- [請注意 pandoc 和 eisvogel 版本](https://github.com/noraj/OSCP-Exam-Report-Template-Markdown/issues/63)
    - 目前實測 pandoc 3.6 + eisvogel 3.1/3.0 都會出現錯誤 Could not find data file templates/eisvogel.latex
3. mv eisvogel.latex /usr/share/pandoc/data/templates/
- 移動 eisvogel.latex 樣板
4. cd OSCP-Exam-Report-Template-Markdown
5. ruby osert.rb generate

### [報告撰寫範例](https://www.youtube.com/watch?v=Ohm0LhFFwVA)

## 更新些已經已經過時的資訊

1. Buffer overflow isn't on the exam.
2. Bonus points will be removed from the OSCP exam as of November 1, 2024.
    - OSCP Exam Changes: https://help.offsec.com/hc/en-us/articles/29865898402836-OSCP-Exam-Changes
3. OSCP -> OSCP+
    - Changes to the OSCP: https://help.offsec.com/hc/en-us/articles/29840452210580-Changes-to-the-OSCP

## OSCP類似的練習題目
[PWK V3 LIST(PWK/ PEN 200 2023-2024 course)](https://docs.google.com/spreadsheets/u/1/d/1dwSMIAPIam0PuRBkCiDI88pU3yzrqqHkDtBngUHNCw8/htmlview#)
[Lainkusanagi OSCP Like](https://docs.google.com/spreadsheets/d/18weuz_Eeynr6sXFQ87Cd5F0slOj9Z6rt/edit?gid=487240997#gid=487240997)

- PG 是 offsec 提供的題目記得要打
    - [詳細(Access-PG-Play)](https://help.offsec.com/hc/en-us/articles/360048613751-Access-PG-Play)
    - PG Practice 沒限制時間 盡量打
    - PG Play 每天最多3小時

## 其他人的考試心得
1. https://blog.leonardotamiano.xyz/tech/oscp-technical-guide/
2. https://www.reddit.com/r/oscp/comments/1gra6kv/passed_oscp_with_70_points_first_attempt/?rdt=64171

## [ligolo-ng](#ligolo-ng)
- 以下是選擇的原因: 當初在discord上問問題, 考生推薦的, 個人覺得比 ssh 好懂
And once you get that down, I would highly recommend looking into a tool called ligolo-ng when you have the time. It is an exceptional tool for tunneling and traffic redirection. 100% Get the basic of port forwarding, redirection, and tunneling manually (so you know what's happening in the background). But move onto more automated tools like ligolo in the future. Makes network communication across public/private subnets much MUCH more efficient and reliable.


[ligolo-ng 教學影片](https://www.youtube.com/watch?v=DM1B8S80EvQ&t=1s&ab_channel=GonskiCyber)
- **請注意** ligolo-ng 不要用apt install安裝, 會裝到dev版本
- [How do you install ligolo-ng](https://www.reddit.com/r/oscp/comments/1dt1pbm/how_do_you_install_ligolong/?rdt=40875)

## 其他補充

### SharpHound、BloodHound
- [SharpCollection](https://github.com/Flangvik/SharpCollection)

### Python2
```
kali 2024-10的更新版本不能直接使用pip install 安裝套件, 需建立虛擬環境
ubuntu 23.04也是
```
https://www.exploit-db.com/ 上有些Python程式是使用Python2執行的
若使用Python3執行一般會回傳「SyntaxError: Missing parentheses in call to 'print'. Did you mean print(...)?」

可選做法
1. [參考此建立Python2環境](https://www.reddit.com/r/oscp/comments/r72w25/installing_python2_modules_in_kali/)
    - 在建置過程遇到麻煩, 放棄此方法
2. 直接修改程式, 改成可以讓Python3執行
    - 我的選擇

### gobuster or feroxbuster
If you take a look at the output of gobuster for /api, the status code returned is 301, this means that it can be further enumerated for sub directories

### Mimikatz
Mimikatz and some other 'inateractive' scripts don't play well with certain reverse shell, and especially don't play well with WinRM. However I have found that using a more featured reverse shell such as ConPTY is one possible remedy.

If you don't want to go about getting another shell going (and it likely isn't worth it in a scenario like this) you can run mimikatz in the following way in powershell:

```
$results = .\mimikatz.exe lsadump::sam exit;
$results;
```