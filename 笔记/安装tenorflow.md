# 用管理员打开 Anaconda Prompt

![[Pasted image 20230706170301.png]]
[图片](https://github.com/zky119/Obsidian-Vault/blob/main/Pasted%20image%2020230706170301.png)

# 创建虚拟环境

```python
conda create -n myenv python=3.9
```

# 选择虚拟环境

```python
conda activate myenv
```

# 切换镜像源

```python
conda config --add channels https://mirrors.sjtug.sjtu.edu.cn/anaconda/pkgs/main/
```

# 安装tensorflow

```python
conda install -c anaconda tensorflow
```

# vscode选择该内核

- 安装ipykernel，会失败
- 复制代码进Anaconda prompt