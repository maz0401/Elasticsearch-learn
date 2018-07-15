# #Elasticsearch 创建、删除索引（index）

## #新建索引

新建 Index，可以直接向 Elastic 服务器发出 PUT 请求。下面的例子是新建一个名叫weather的 Index。

```cmd
# curl -X PUT 'localhost:9200/weather'
```

服务器返回一个 JSON 对象，里面的acknowledged字段表示操作成功。

```info
{
    "acknowledged":true,
    "shards_acknowledged":true,
    "index":"weather"
}
```

## #删除索引

然后，我们发出 DELETE 请求，删除这个 Index。

```cmd
# curl -X DELETE 'localhost:9200/weather'
```

## #查询索引

通过下面的指令可以查看已存在的索引：

```cmd
# curl http://localhost:9200/_cat/indices?v
```