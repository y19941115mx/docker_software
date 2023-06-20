### Hadoop Hive 部署（包括Hadoop）
#### 1、创建网络

```bash
# 创建，注意不能使用hadoop_network，要不然启动hs2服务的时候会有问题！！！
docker network create hadoop-network

# 查看
docker network ls
```

#### 2、部署 mysql5.7

```bash
cd mysql

docker -f mysql-compose.yaml up -d

docker -f mysql-compose.yaml ps

#root 密码：123456，以下是登录命令，注意一般在公司不能直接在命令行明文输入密码，要不然容易被安全抓，切记，切记！！！
docker exec -it mysql mysql -uroot -p123456
```

#### 3、部署 Hadoop Hive

```bash
cd ../hive

docker-compose -f docker-compose.yaml up -d

# 查看
docker-compose -f docker-compose.yaml ps

# hive
docker exec -it hive-hiveserver2 hive -e "show databases";

# hiveserver2
docker exec -it hive-hiveserver2 beeline -u jdbc:hive2://hive-hiveserver2:10000  -n hadoop -e "show databases;"
```