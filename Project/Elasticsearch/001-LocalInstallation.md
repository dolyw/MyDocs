# 001-LocalInstallation

> 目录:[https://github.com/dolyw/Elasticsearch](https://github.com/dolyw/Elasticsearch)

### 安装本地Elasticsearch

当然首先要安装`JDK1.8`的环境及以上版本都行，不能低于`1.8`，安装`Windows`本地版，去`Elasticsearch`官网下载即可，不过找了很久都没有找到旧版本，最后下了最新版7.2，安装很简单，将下载的`zip`文件解压

#### 目录说明

|目录名|说明|
|:- |:-: |
|config |配置文件 |
|modules |模块存放目录 |
|bin |脚本 |
|lib	 |第三方库 |
|plugins	 |第三方插件 |

直接运行`bin`下的`elasticsearch.bat`这个文件即可启动，关闭窗口就是关闭服务，然后访问本机的`127.0.0.1:9200`即可，网页返回如下`JSON`
```json
{
  "name" : "WANG926454",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "ht8iAPewRDidZk-qbZ2Eig",
  "version" : {
    "number" : "7.2.0",
    "build_flavor" : "default",
    "build_type" : "zip",
    "build_hash" : "508c38a",
    "build_date" : "2019-06-20T15:54:18.811730Z",
    "build_snapshot" : false,
    "lucene_version" : "8.0.0",
    "minimum_wire_compatibility_version" : "6.8.0",
    "minimum_index_compatibility_version" : "6.0.0-beta1"
  },
  "tagline" : "You Know, for Search"
}
```

### 安装本地Elasticsearch-Head

一般情况下，我们都会通过一个可视化的工具来查看`ES`的运行状态和数据。这个工具我们一般选择[Head](https://github.com/mobz/elasticsearch-head)

#### Head插件的优点

* 提供了友好的`Web`界面，解决数据在界面显示问题
* 实现基本信息的查看和`Restful`请求的模拟以及数据的基本检索

`Elasticsearch-Head`依赖于`Node.js`，需要安装`Node.js`，查看`Github`介绍，该工具能直接对`Elasticsearch`的数据进行增删改查，因此存在安全性的问题，建议生产环境下不要使用该插件，`Node.js`版本必须`requires node >= 6.0`，简单的菜鸟教程安装就行:[https://www.runoob.com/nodejs/nodejs-install-setup.html](https://www.runoob.com/nodejs/nodejs-install-setup.html)，我Node.js环境的很早就已经安装了，执行下面命令先安装`grunt`

```base
npm install -g grunt-cli
```

安装完成查看版本

```base
grunt -version
```

显示版本号OK

```base
grunt-cli v1.3.2
```

去[Github](https://github.com/mobz/elasticsearch-head)下载`Elasticsearch-Head`工具，解压到你的`Elasticsearch`根路径下`D:\Tools\elasticsearch-7.2.0\elasticsearch-head-master`，修改`Gruntfile.js`配置文件，如下添加`hostname: '*'`

```base
connect: {
	server: {
		options: {
			hostname: '*',
			port: 9100,
			base: '.',
			keepalive: true
		}
	}
}
```

然后在`D:\Tools\elasticsearch-7.2.0\elasticsearch-head-master`目录先安装下启动运行`Head`插件

```javascript
npm install
grunt server or npm run start
```

进`http://localhost:9100`发现连接不上，还需要配置下`Elasticsearch`，修改`Elasticsearch`安装目录下的`config/elasticsearch.yml`配置文件，在最下面添加下面两句配置，开启跨域

```yml
# 如果启用了HTTP端口，那么此属性会指定是否允许跨源REST请求，默认true
http.cors.enabled: true
# 如果http.cors.enabled的值为true，那么该属性会指定允许REST请求来自何处，默认localhost
http.cors.allow-origin: "*"
```

重新打开`elasticsearch.bat`，启动完成进去`http://localhost:9100`连接，OK

#### 集群健康值

* `red`(差): 集群健康状况很差，虽然可以查询，但是已经出现了丢失数据的现象
* `yellow`(中): 集群健康状况不是很好，但是集群可以正常使用
* `green`(优): 集群健康状况良好，集群正常使用

### 安装本地Elasticsearch集群(分布式)

