# 安装 （CPU版） 最新版 和 1.15.0版本
- GPU版本的话，tensorflow 改成 tensorflow-gpu

# 用管理员打开 Anaconda Prompt

![[Pasted image 20230706170301.png]]
[点我显示图片](https://github.com/zky119/Obsidian-Vault/blob/main/Pasted%20image%2020230706170301.png)

# tensorflow 最新版
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
conda install -c anaconda tensorflow
```

## vscode选择该内核

- 安装ipykernel，会失败
- 复制代码进Anaconda prompt


# tensorflow 1.15.0 版本

## 创建虚拟环境
- $-n$ 后面是虚拟环境的名字，自定义
```python
conda create -n tf37 python=3.7
```

## 选择虚拟环境

```python
conda activate tf37
```

## 安装tensorflow

```python
conda install -c anaconda tensorflow=1.15.0
```
