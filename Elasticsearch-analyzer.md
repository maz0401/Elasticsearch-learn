# 安装分词器

对于分词器，可以根据需要进行安装不同的分词器（官方、第三方提供的）。以下以中文分词器为例：

## #安装分词器

安装中文分词插件，这里使用 ik，其他插件（比如 smartcn）。

```cmd
# ./bin/elasticsearch-plugin install https://github.com/medcl/elasticsearch-analysis-ik/releases/download/v6.3.0/elasticsearch-analysis-ik-6.3.0.zip
```

上面代码安装的是6.3.0版的插件，与 Elastic 6.3.10 配合使用。不同版本的 Elastic 需要不同的分词器，在安装分词器时需要查看对应表。

分词器安装完成，重新启动 Elastic，就会自动加载这个新安装的插件。

## #新建索引，指定分词器

新建一个 Index，指定需要分词的字段。这一步根据数据结构而异，下面的命令只针对本文。基本上，凡是需要搜索的中文字段，都要单独设置一下。

```cmd
# curl -X PUT -H 'Content-type:application/json' 'localhost:9200/accounts' -d '
{
  "mappings": {
    "person": {
      "properties": {
        "user": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        },
        "title": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        },
        "desc": {
          "type": "text",
          "analyzer": "ik_max_word",
          "search_analyzer": "ik_max_word"
        }
      }
    }
  }
}'
```

上面代码中，首先新建一个名称为`accounts`的 Index，里面有一个名称为`person`的 Type。

`person`有三个字段:

- user
- title
- desc

这三个字段都是中文，而且类型都是文本（text），所以需要指定中文分词器，不能使用默认的英文分词器。

Elastic 的分词器称为 `analyzer`。我们对每个字段指定分词器。

```info
"user": {
  "type": "text",
  "analyzer": "ik_max_word",
  "search_analyzer": "ik_max_word"
}
```

上面代码中，`analyzer`是字段文本的分词器，`search_analyzer`是搜索词的分词器。`ik_max_word`分词器是插件ik提供的，可以对文本进行最大数量的分词。

## #分词器使用

```
curl -H 'Content-type:application/json' 'http://localhost:9200/_analyze?pretty=true' -d '{"text":"这里是好记性不如烂笔头感叹号的博客园"}'
curl -H 'Content-type:application/json' 'http://localhost:9200/_analyze?pretty=true' -d '{"analyzer":"ik_max_word","text":"这里是好记性不如烂笔头感叹号的博客园"}'
curl -H 'Content-type:application/json' 'http://localhost:9200/_analyze?pretty=true' -d '{"analyzer":"smartcn","text":"这里是好记性不如烂笔头感叹号的博客园"}'
```