# 达梦数据库 Docker 镜像

## 安装 Docker

### CentOS

`yum install -y docker`  
`systemctl start docker # 启动 docker daemon`  
`systemctl enable docker # 设置 docker daemon 开机运行`

## 启动 DM 数据库

### 快速启动

#### DM7 X86-64 版

`docker run -p 5236:5236 helsonxiao/dm:7`

#### DM8 X86-64 版

`docker run -p 5236:5236 helsonxiao/dm:8`

#### DM8 ARM64 版

`docker run -p 5236:5236 toyangdon/dm:8-arm64`

### 持久化存储数据

`docker run -v /dm:/home/dmdba/data -p 5236:5236 [image_name]`

### 开机自启

`docker run -v /dm:/home/dmdba/data -p 5236:5236 -d --restart always [image_name]`

### 默认用户名/密码

`SYSDBA/SYSDBA`

### disql 工具

`docker run --rm -it --entrypoint="/home/dmdba/dmdbms/tool/disql" [image_name]`

#### 示例

`SQL> connect SYSDBA/SYSDBA@[server_ip]:5236`

## 镜像构建

`docker build -t [image_name] .`
