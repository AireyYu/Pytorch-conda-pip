# Pychram使用Anaconda虚拟环境设置
1. **创建全新Python 3.10环境** 
```bash
conda create -n ai_env python=3.10 -y     #这里要python为3.10版本
```
2. **激活环境**：
 ```
conda activate ai_env
 ```
4.**安装Numpy**
  考虑到直接运行pip install torch==2.5.1+cu121 --index-url https://download.pytorch.org/whl/cu121 装pytorch 会导致pip下的numpy和conda下的numpy版本不一致，所以先安装nummpy(Conda优先)
 ```
   conda install numpy=1.26.4 -c conda-forge
 ```
   
6. 安装 PyTorch GPU 版（Pip 安装）,这里用pip install torch==2.5.1+cu121 --index-url https://download.pytorch.org/whl/cu121 因为我的CUDA版本为12.9比较高，PyTorch/Conda 生态系统目前仅正式支持到 CUDA 12.4，
   导致 Conda 无法直接提供匹配的预编译包，必须要用pip来安装pytorch，直接用pytorch官方源(不从默认的PyPI)。

7. conda install pandas matplotlib scikit-learn jupyter -c conda-forge
   pip install transformers  # 纯Python包， 到这一步基本安装好了基本需要的包

8. 测试代码
   print(f"PyTorch版本: {torch.__version__}")          # 应输出 2.3.0+ 
   print(f"CUDA可用: {torch.cuda.is_available()}")     # 应输出 True
   print(f"CUDA版本: {torch.version.cuda}")            # 可能显示 12.1，但实际使用 12.9 驱动
   print(f"GPU设备: {torch.cuda.get_device_name(0)}")  # 显示你的显卡型号
   
9. conda env export --no-builds > environment.yml 来导出yml文件，yml文件里面包含这个环境的所有的包，新建的环境可以用这个yml文件快速生成。
   查看环境列表：conda env list
   新环境生成：conda env create -f environment.yml -n new_env，这里用了之前的yml文件
   环境删除：1.conda env remove -n new_env 2.conda remove --name new_env --all -y -y
   环境更新(最基础的) conda env export --no-builds > environment.yml 等于重新导出一次yml文件覆盖之前的旧文件
   注意：这边因为CUDA版本太高被迫选择用Pip去pytorch官方源下载，所以导致直接用yml生成新环境时报错：查找不到对应torch版本，因为它这里是从PyPI里面检索的。所以在报错之后其他包都已经下载完成，
   再次手动下载pip install torch==2.5.1+cu121 --index-url https://download.pytorch.org/whl/cu121

  


