# nmap_to_es

```
env: Ubuntu 20.04 LTS WSL2
Python 2.7
```

## Basic

### masscan

```shell
sudo apt install git gcc make libpcap-devel
git clone https://github.com/robertdavidgraham/masscan
cd masscan
make
cp bin/masscan  /bin
```

### nmap 7.8

```shell
wget https://nmap.org/dist/nmap-7.80-1.x86_64.rpm
# 先安装 alien 和 fakeroot 这两个工具，其中前者可以将 rpm 包转换为 deb 包。
sudo apt-get install alien fakeroot
fakeroot alien nmap-7.80-1.x86_64.rpm
sudo dpkg -i package.deb
```

### es & kibana

```shell
docker run -d --name es -p 127.0.0.1:9201:9200 -p 9300:9300 -e ES_JAVA_OPTS="-Xms2G -Xmx2G" -e "discovery.type=single-node"  docker.elastic.co/elasticsearch/elasticsearch-oss:7.1.1   

docker run --name kibana -d -p 5601:5601 -e ELASTICSEARCH_HOSTS=http://127.0.0.1:9201   docker.elastic.co/kibana/kibana-oss:7.1.1   
```

### Python2

```python
pip2 install -r requirements.txt
```

## Workflow

1. 使用 Masscan 做主机存活扫描
1. 然后使用Nmap扫描上面存活的主机，导出xml
1. 格式化xml，写入es，然后kibana做可视化



用 nmap 和 elk 做内网资产盘点
依赖 nmap-vulners


```bash
# cd /usr/share/nmap/scripts  
# git clone https://github.com/vulnersCom/nmap-vulners.git
```

kibana   nmap-*



---

Article: https://www.freebuf.com/articles/es/244217.html

