# 达梦数据库ARM版镜像
达梦数据库ARM版8.0容器部署方案
## 单机部署
### 快速启动
`docker run -p 5236:5236 toyangdon/dm:8-arm64`
### 持久化数据
`docker run -v /dm:/home/dmdba/data -p 5236:5236 toyangdon/dm:8-arm64`
## 集群部署
//TO_DO
## 镜像构建
`docker build -t toyangdon/dm:8-arm64 .`
