# conda命令
```shell
# 查看所有虚拟环境
conda env list
# 删除虚拟环境
conda env remove --name <env_name>
# 创建虚拟环境，可指定python版本
conda create -n <env_name> python=3.9
# 选择虚拟环境
conda activate <env_name>
```

# 安装 （CPU版） 最新版 和 1.15.0版本
- GPU版本的话，tensorflow 改成 tensorflow-gpu

# 用管理员打开 Anaconda Prompt

![[Pasted image 20230706170301.png]]
[点我显示图片](https://github.com/zky119/Obsidian-Vault/blob/main/%E7%89%87%E6%AE%B5/Pasted%20image%2020230706170301.png)

# 一，tensorflow-gpu 最新版
## 创建虚拟环境
- $-n$ 后面是虚拟环境的名字，自定义
```python
conda create -n tf39 python=3.9
```

## 选择虚拟环境

```python
conda activate tf39
```

## 切换镜像源

```python
conda config --add channels https://mirrors.sjtug.sjtu.edu.cn/anaconda/pkgs/main/
```

## 安装tensorflow

```python
#conda install -c anaconda tensorflow
conda install -c anaconda tensorflow-gpu
```

## vscode选择该内核

- 安装ipykernel，会失败
- 复制代码进Anaconda prompt
```shell
conda install -n <env_name> ipykernel --update-deps --force-reinstall
```

# 二，tensorflow 1.14.0 版本

## 创建虚拟环境
- $-n$ 后面是虚拟环境的名字，自定义
```python
conda create -n tf114 python=3.6
```

## 选择虚拟环境

```python
conda activate tf114
```

## 安装tensorflow

```python
# conda install -c anaconda tensorflow=1.14.0
conda install -c anaconda tensorflow-gpu=1.14.0
```

## vscode选择该内核

- 安装ipykernel，会失败
- 复制代码进Anaconda prompt
```shell
conda install -n tf114 ipykernel --update-deps --force-reinstall
```
