# nodejs-mongodb
简单的学习

#首先 d:\\mongodb\bin  (cd 到bin目录下)
## 1、黑窗口一   mongod.exe  --dbpath  d:\data (数据存放的地址)
## 2、黑窗口二   mongo （启动）
## 3、黑窗口三   就可以启动app.js
新建数据库：第一步：use 新建数据库名；第二步：进行此库相关的操作；如果不进行第二步，该数据库不会被创建

查看数据库：show dbs;

新建表：db.createCollection('要新建的表名');

查看当前数据库下表： show collections;

删除当前数据库指定表：db.表名.drop();

删除当前数据库：db.dropDatabase();

示例操作如下图：

![github]（https://github.com/ybkuncom/nodejs-mongodb-ejs/blob/master/B3eIRz.png?raw=true “github”)

1.默认为存在“admin”和“local”两个数据库；admin数据库是存放管理员信息的数据库，认证会用到；local是存放replication相关的数据；这两处本篇都没有涉及到；

2.find();是个查询操作，后面会讲到，上面用到主要是为了演示use不存在的库后，进行相关操作会创建出这个库；

3.MongoDB没有像MySQL或MSSQL等数据库这么严格的规定，不是非得要先建库、建表、建各种字段，以后的操作中慢慢的会体会到^_^！

方法一：db.表名.insert(数据);


1.从上图操作可以看出，没有去创建“tb1”表，其实通过插入操作也会自动创建

2._id，是mongodb自已生成的，每行数据都会存在，默认是ObjectId，可以在插入数据时插入这个键的值(支持mongodb支持的所有数据类型)
查询表中所有数据：db.表名.find();

按条件查询（支持多条件）：db.表名.find(条件);

查询第一条（支持条件）：db.表名.findOne(条件);

限制数量：db.表名.find().limit(数量);

跳过指定数量：db.表名.find().skip(数量);


从上图中可以看出具体用法，批量插入默认数据我用了一个javascript语法循环；

比较查询

大于：$gt

小于：$lt

大于等于：$gte

小于等于：$lte

非等于：$ne


上面看到了AND的关系，或者的关系应该怎么用？

或者：$or


in和not in查询(包含、不包含)

$in

$nin


查询数量：db.表名.find().count();

排序：db.表名.find().sort({"字段名":1});

1：表示升序  -1：表示降序

指定字段返回： db.表名.find({},{"字段名":0});

1：返回  0：不返回


查询就讲到这里了，感觉查询示例一下讲不完，还有些高级查询，大家自行去了解一下吧^_^!

前面save在_id字段已存在是就是修改操作，按指定条件修改语法如下

db.表名.update({"条件字段名":"字段值"},{$set:{"要修改的字段名":"修改后的字段值"}});

```html
db.表名.remove(条件);
var MongoClient = require('mongodb').MongoClient;
var DB_CONN_STR = 'mongodb://localhost:27017/wilsondb1';	
var insertData = function(db, callback) {  
  //连接到表  
  var collection = db.collection('tb2');
  //插入数据
  var data = [{"name":'wilson001',"age":21},{"name":'wilson002',"age":22}];
  collection.insert(data, function(err, result) { 
    if(err)
    {
      console.log('Error:'+ err);
      return;
    }	 
    callback(result);
  });
}
MongoClient.connect(DB_CONN_STR, function(err, db) {
  console.log("连接成功！");
  insertData(db, function(result) {
    console.log(result);
    db.close();
  });
});
```

##查询
```html
var MongoClient = require('mongodb').MongoClient;
var DB_CONN_STR = 'mongodb://localhost:27017/wilsondb1';  

var selectData = function(db, callback) {  
  //连接到表  
  var collection = db.collection('tb2');
  //查询数据
  var whereStr = {"name":'wilson001'};
  collection.find(whereStr).toArray(function(err, result) {
    if(err)
    {
      console.log('Error:'+ err);
      return;
    }     
    callback(result);
  });
}

MongoClient.connect(DB_CONN_STR, function(err, db) {
  console.log("连接成功！");
  selectData(db, function(result) {
    console.log(result);
    db.close();
  });
});
```

##修改

```html
var MongoClient = require('mongodb').MongoClient;
var DB_CONN_STR = 'mongodb://localhost:27017/wilsondb1';	
var updateData = function(db, callback) {  
  //连接到表  
  var collection = db.collection('tb2');
  //更新数据
  var whereStr = {"name":'wilson001'};
  var updateStr = {$set: { "age" : 100 }};
  collection.update(whereStr,updateStr, function(err, result) {
    if(err)
    {
      console.log('Error:'+ err);
      return;
    }	 
    callback(result);
  });
}
MongoClient.connect(DB_CONN_STR, function(err, db) {
  console.log("连接成功！");
  updateData(db, function(result) {
    console.log(result);
    db.close();
  });
});
```

##删除

```html
var MongoClient = require('mongodb').MongoClient;
var DB_CONN_STR = 'mongodb://localhost:27017/wilsondb1';  

var delData = function(db, callback) {  
  //连接到表  
  var collection = db.collection('tb2');
  //删除数据
  var whereStr = {"name":'wilson001'};
  collection.remove(whereStr, function(err, result) {
    if(err)
    {
      console.log('Error:'+ err);
      return;
    }     
    callback(result);
  });
}

MongoClient.connect(DB_CONN_STR, function(err, db) {
  console.log("连接成功！");
  delData(db, function(result) {
    console.log(result);
    db.close();
  });
});
```
