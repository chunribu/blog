[🏠HOME](README.md)

# 在国内安装QIIME2

---

## Step 1：给conda换清华源

修改用户目录下的 `.condarc` 文件的内容为

```
channels:
  - defaults
show_channel_urls: true
default_channels:
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
custom_channels:
  conda-forge: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  bioconda: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
  qiime2: https://mirrors.tuna.tsinghua.edu.cn/anaconda/cloud
```

参考 https://mirror.tuna.tsinghua.edu.cn/help/anaconda/

## Step 2：下载最新`yml`文件并修改`channels`

```
wget https://data.qiime2.org/distro/core/qiime2-2021.8-py38-linux-conda.yml
```

打开文件，修改channels中的`qiime2/label/r2021.8`为`qiime2`.

参考 https://docs.qiime2.org/2021.8/install/native/

## Step 3：安装

```
conda env create -n qiime2-2021.8 --file qiime2-2021.8-py38-linux-conda.yml
```
