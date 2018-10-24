## 实验二报告文档

### 1. 实验内容：

- 在pdborcl插接式数据中创建一个新的本地角色con_res_view，该角色包含connect和resource角色，同时也包含CREATE VIEW权限，这样任何拥有con_res_view的用户就同时拥有这三种权限。
- 创建角色之后，再创建用户new_user，给用户分配表空间，设置限额为50M，授予con_res_view角色。
- 最后测试：用新用户new_user连接数据库、创建表，插入数据，创建视图，查询表和视图的数据。
      
### 2. 实验过程：

 - 第1步：以system登录到pdborcl，创建新角色<font color=#0099ff size=7 face="黑体">con_res_ltt</font>和新用户<font color=#0099ff size=7 face="黑体">ltt</font>，并授权和分配空间：

![第一步](https://github.com/DoubleLTT/Oracle/blob/master/img/oracle%E5%AE%9E%E9%AA%8C.JPG)
![第一步](https://github.com/DoubleLTT/Oracle/blob/master/img/oracle%E5%AE%9E%E9%AA%8C.JPG)

 - 第2步：新用户**ltt**连接到pdborcl，创建表mytable和视图myview，插入数据，最后将myview的SELECT对象权限授予hr用户。

![第二步](https://github.com/DoubleLTT/Oracle/blob/master/img/%E7%AC%AC%E4%BA%8C%E6%AD%A5.JPG?raw=true)

 - 第3步：用户hr连接到pdborcl，查询ltt授予它的视图myview
 
 ![第三步](https://github.com/DoubleLTT/Oracle/blob/master/img/%E7%AC%AC%E4%B8%89%E6%AD%A5.JPG?raw=true)


### 3. 实验总结：

     在实验过程中，我创建的数据库新角色为con_res_ltt，新用户为ltt，
     以ltt的用户身份进入数据库，连接到pdborcl,创建表mytable和视图myview，
     在表中新建了1行，命名为NAME，值为liao,切换到hr，可以查询到新建的字段值。





