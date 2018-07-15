# #Elasticsearch 在使用时出现问题

## #用户权限问题

问题描述：执行`./bin/elasticsearch`后，出现如下异常

```cmd
Exception in thread "main" java.nio.file.AccessDeniedException: /usr/elasticsearch/elasticsearch-6.3.0/config/jvm.optionsException in thread "main" java.nio.file.AccessDeniedException: /usr/elasticsearch/elasticsearch-6.3.0/config/jvm.options
```

解决方法：
产生问题的原因是，当前用户(非root)没有文件夹权限，需要进行权限更改。
如果当前用户为es,则执行以下指令：

```cmd
chown -R es:es /usr/local/elasticsearch/
```

## Root账号执行问题

```cmd
org.elasticsearch.bootstrap.StartupException: java.lang.RuntimeException: can not run elasticsearch as root
```

意思是`elasticsearch`不能以root账号进行运行，需要使用其他账号进行操作。

## 插入数据类型问题

```cmd
{"error":"Content-Type header [application/x-www-form-urlencoded] is not supported","status":406}
```

解决方法：
在插入数据时，指定数据类型为json.
```cmd
curl -H "Content-Type:application/json" -XPOST 192.168.14.173:32000/test_index_1221/test_type/5 -d'{'user_name':"xiaoming"}'
```