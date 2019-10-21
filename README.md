# RSDB
遥感影像存储检索系统
# 整体思路
1. 对影像规范命名，统一为tif格式
2. 对影像进行分片，按照`512*512`的大小切分成小图，并生成每个图有效区域的矢量边界
3. 对原始影像生成有效区域的矢量边界
4. 将切片图和影像存储到HBASE中，将矢量边界转换为wkt字符串存储到安装postgis的postgresql数据库中
5. 影像检索使用postgis

# 环境准备
本平台结合服务端在Linux系统，客户端在Windows系统。由于数据量较大，采用分布式存储的方式。本实验客户端使用四台Centos虚拟机，其中三台用于Hadoop集群，一台用于postgresql及数据预处理工作。
1. Linux系统以及Hadoop集群版安装参考[厦门大学数据库实验室 大数据处理架构Hadoop 学习指南](http://dblab.xmu.edu.cn/blog/285/)。本文中Linux系统使用Centos7.5，Hadoop版本为2.6.5。
2. HBase安装参考[厦门大学数据库实验室 分布式数据库HBase 学习指南](http://dblab.xmu.edu.cn/blog/install-hbase/)。HBase版本使用的是1.4.9、
3. centos下安装postgresql和postgis参考 [centos7.5安装postgresql和postgis](https://blog.csdn.net/weixin_40450867/article/details/102671979)。
4. python3及相关地理信息处理的包的安装，**仅在一台机器上安装即可**，安装在postgresql同一个机器上，使用root用户。
```bash
yum install wget -y
wget https://mirrors.tuna.tsinghua.edu.cn/anaconda/miniconda/Miniconda3-4.5.4-Linux-x86_64.sh
yum install gcc -y
yum install bzip2 -y
/bin/bash Miniconda3-4.5.4-Linux-x86_64.sh -b

echo '''export PATH="/root/miniconda3/bin:$PATH"'''>>/root/.bashrc
source /root/.bashrc

/root/miniconda3/bin/conda install -c anaconda gdal=2.3.3 -y
/root/miniconda3/bin/pip install rasterio==1.0.24
/root/miniconda3/bin/pip install geopandas==0.5.1
/root/miniconda3/bin/pip install opencv-python-headless==4.1.0.25
/root/miniconda3/bin/pip install Pillow==6.0.0
/root/miniconda3/bin/pip install psycopg2==2.8.3
/root/miniconda3/bin/pip install shapely
rm -rf Miniconda3-4.5.4-Linux-x86_64.sh
```

# 数据准备工作
规范命名

# 影像切片

# 数据入库

# 检索功能实现
