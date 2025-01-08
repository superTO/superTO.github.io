---
title: pipx
date: 2025-01-08 23:04:27
tags: python
categories:
---
# pipx 簡單說明

原因: 在ubuntu 23.04以後, 會限制不讓你在global使用 pip install 安裝套件(需要建立虛擬環境), 會出現以下錯誤
```
error: externally-managed-environment
 
_ This environment is externally managed
_─> To install Python packages system-wide, try apt install
python3-xyz, where xyz is the package you are trying to
install.
 
If you wish to install a non-Debian-packaged Python package,
create a virtual environment using python3 -m venv path/to/venv.
Then use path/to/venv/bin/python and path/to/venv/bin/pip. Make
sure you have python3-full installed.
 
If you wish to install a non-Debian packaged Python application,
it may be easiest to use pipx install xyz, which will manage a
virtual environment for you. Make sure you have pipx installed.
 
See /usr/share/doc/python3.12/README.venv for more information.
 
note: If you believe this is a mistake, please contact your Python installation or OS distribution provider. You can override this, at the risk of breaking your Python installation or OS, by passing --break-system-packages.
hint: See PEP 668 for the detailed specification.
```

解決辦法

1. 使用虛擬環境
    - 以 virtualenv 為例
```
sudo apt install python3-virtualenv
```

2. 使用 pipx
    - pipx 的介紹讓人以為可以使用 pipx install pandas 
```
$ pipx install pandas
Note: Dependent package 'numpy' contains 2 apps
  - f2py
  - numpy-config

No apps associated with package pandas. Try again with '--include-deps' to include apps of dependent packages, which are listed
above. If you are attempting to install a library, pipx should not be used. Consider using pip or a similar tool instead.
```

結果是這樣用
```
pipx install pipenv

mkdir .venv
pipx run pipenv --shell
pip install pandas
```

## 補充

- 可以使用 pipx 建立 python 3.8 的 pipenv 執行環境 (但你需要有 python 3.8)
```
pipx install pipenv --python python3.8
```

## pipx 的好處

1. 容量使用的較少
2. 不需要使用切換虛擬環境的指令, 可以直接指定執行的版本
```
pipx run --python python3.9 pycowsay mooo
```

## 結論

:::
**我怎不用 conda 就好?**
:::

1. 直接建立指定版本建立虛擬環境
```
conda create python=3.9 --prefix .venv
```
2. 進入虛擬環境
```
conda activate .venv
```
3. 安裝 pandas
- 如果要像 pipx 建立隔離環境, 這個虛擬環境就只裝 pandas, 效果就和 pipx 一樣了
```
pip install pandas
```