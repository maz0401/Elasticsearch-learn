# #Elasticsearch Install

Elasticsearch 需要最新的 Java 8.
在你安装Elasticsearch之前，可以通过以下指令检查你的Java版本：

```cmd
java -version
echo $JAVA_HOME
```

Java 设置完成后，可以从[Elasticsearch官网](https://www.elastic.co/downloads/elasticsearch)([中文官网](https://www.elastic.co/cn/downloads/elasticsearch))下载并运行。可以根据你操作系统选择不同的发行版本进行下载。安装包类型有：ZIP、TAR、DEB、RPM、MSI

## #Linux下安装

Elasticsearch 使用tar压缩包方式进行安装。

1. 下载 Elasticsearch 6.3.0 tar 如下:

```cmd
# curl -L -O https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.3.0.tar.gz

```

2. 解压文件并进入解压目录

```cmd
# tar -xvf elasticsearch-6.3.0.tar.gz
# cd elasticsearch-6.3.0/
```

3. 运行下面的命令，启动 Elastic。

```cmd
# ./bin/elasticsearch
```

4. 运行正常时，默认会开启9200端口,在命令窗口中，请求该端口时会出现如下信息：

```info
# curl http://localhost:9200/
{
  "name" : "xZBf0Vb",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "tbqxTknLQNaj8IalmtmkwA",
  "version" : {
    "number" : "6.3.0",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "424e937",
    "build_date" : "2018-06-11T23:38:03.357887Z",
    "build_snapshot" : false,
    "lucene_version" : "7.3.1",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}
```

上面代码中，请求9200端口，Elastic 返回一个 JSON 对象，包含当前节点、集群、版本等信息。

按下 Ctrl + C，Elastic 就会停止运行。

默认情况下，Elastic 只允许本机访问，如果需要远程访问，可以修改 Elastic 安装目录的`config/elasticsearch.yml`文件，去掉`network.host`的注释，将它的值改成`0.0.0.0`，然后重新启动 Elastic。

```cfg
network.host: 0.0.0.0
```

上面代码中，设成`0.0.0.0`让任何人都可以访问。线上服务不要这样设置，要设成具体的 IP。

## #Mac下安装

在 macOS，可以通过`Homebrew`指令进行安装：

```cmd
$ brew install elasticsearch
```

## #Windows下安装

对Windows用户，可以通过MSI安装包进行安装。该msi 包含图形用户界面（GUI）进行指导安装。
可以从下面地址下载MSI安装包：https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-6.3.0.msi
