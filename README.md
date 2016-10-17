# nodejs-mongodb-ejs
简单的网站

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
