# nodejs-mongodb-ejs
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

![github]（B3eIRz.png “github”)

1.默认为存在“admin”和“local”两个数据库；admin数据库是存放管理员信息的数据库，认证会用到；local是存放replication相关的数据；这两处本篇都没有涉及到；

2.find();是个查询操作，后面会讲到，上面用到主要是为了演示use不存在的库后，进行相关操作会创建出这个库；

3.MongoDB没有像MySQL或MSSQL等数据库这么严格的规定，不是非得要先建库、建表、建各种字段，以后的操作中慢慢的会体会到^_^！

方法一：db.表名.insert(数据);


1.从上图操作可以看出，没有去创建“tb1”表，其实通过插入操作也会自动创建

2._id，是mongodb自已生成的，每行数据都会存在，默认是ObjectId，可以在插入数据时插入这个键的值(支持mongodb支持的所有数据类型)
