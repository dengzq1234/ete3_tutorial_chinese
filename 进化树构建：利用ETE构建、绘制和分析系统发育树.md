## 树形图
### 进化树构建
#### 利用ETE构建、绘制和分析系统发育树
> 本节作者：邓子祺
> 
> 单位：西班牙植物生物技术和基因组中心（Centre for Plant Biotechnology and Genomics）
>
> 版本1.0.0，更新日期：2020年7月02日

#### 简介
introduction of ete，最新版本3.1.1
#### ETE下载与安装
推荐在Linux或MacOS系统运行ETE，对其模块兼容更友好
- 使用conda环境（推荐）
```
# 安装 conda 环境
# Install Minconda  (you can ignore this step if you already have Anaconda/Miniconda)
wget http://repo.continuum.io/miniconda/Miniconda3-latest-Linux-x86_64.sh -O Miniconda3-latest-Linux-x86_64.sh
bash Miniconda3-latest-Linux-x86_64.sh -b -p ~/anaconda_ete/
export PATH=~/anaconda_ete/bin:$PATH;

# 安装 ETE 包
# Install ETE 
conda install -c etetoolkit ete3

# 安装 ETE 外部工具包
conda install -c etetoolkit ete_toolchain 

# Check installation
ete3 build check
```
- 其他安装

1.安装依赖文件
```
# 在如Ubuntu, Mint，等基于Debian的系统(APT)
sudo apt-get install python-numpy python-qt4 python-lxml python-six

# 在CentOS, Fedora, 等(YUM)
sudo yum install PyQt4.x86_64 numpy.x86_64 python-lxml.x86_64 python-six.noarch
```

2.使用pip安装ETE3
```
pip install --upgrade ete3
```
或使用EasyInstall
```
easy_install -U ete3
```
或通过源代码安装
```
wget https://files.pythonhosted.org/packages/21/17/3c49b7fafe10ed63bb7904ebf9764b98db726aa5fd482fb006818854bc04/ete3-3.1.1.tar.gz
tar -xvf ete3-3.1.1.tar.gz
python setup.py install
```
3.安装其他工具
```
# 此为可选择步骤，仅为ete-build和ete-evol服务。若仅使用ete3的python API模块，可跳过此步
ete3 upgrade-external-tools
```

#### ETE命令行工具教程(ETE tools cookbook)
> 一键完成 “多序列比对 -> 修剪 -> 建树” 流程 

##### ete-build命令基本介绍
>  *ete-build* 命令需要几个外部程序来进行系统发育树， 序列比对以及其他任务。建议通过conda对外部工具进行预安装(https://anaconda.org/etetoolkit/ete_toolchain) 或（https://anaconda.org/etetoolkit/ete3_external_apps）

1) 检查所有外部应用程序是否可用
```
ete3 build check
```
![image](https://raw.githubusercontent.com/dengzq1234/ete3_tutorial_chinese/master/ete-build-check.png?token=AGDS2VZJ65DW76BNHNRT25K7FKK6U)

2) 查看预先系统自带的建树流程及其详细解释
- ete预先了设计了多个流程用以完成从原始序列到后续进化树构建的各个步骤。运行以下命令可以列出系统自带的流程及其详细步骤
```
ete3 build workflows genetree
```
![image](https://raw.githubusercontent.com/dengzq1234/ete3_tutorial_chinese/master/ete-build-workflow.png?token=AGDS2VZVBHW6FKY2MG3VB527FKK7M)

3) 准备FASTA原始序列
- 确保输入序列为正确的FASTA格式
- 输入序列可以为氨基酸或DNA序列
- 建议序列名不包含异常符号，并且序列名不能重复，否则程序报错。
> 这里我们以NUP62同源氨基酸序列为例子
```
cat data/NUP62.aa.fa | head -n15
```
![image](https://raw.githubusercontent.com/dengzq1234/ete3_tutorial_chinese/master/ete-build-NUP62.png?token=AGDS2V4WVQXOTPVM34JTZW27FKLFU)


4) 

#### 利用ETE进行树型分析/可视化(python模块教程)
> ETE库具有全面的API 构建，比较，注释，操作和可视化树 