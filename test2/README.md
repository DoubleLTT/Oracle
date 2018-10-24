## 实验二报告文档

### 1. 实验内容：

- 在pdborcl插接式数据中创建一个新的本地角色con_res_view，该角色包含connect和resource角色，同时也包含CREATE VIEW权限，这样任何拥有con_res_view的用户就同时拥有这三种权限。
- 创建角色之后，再创建用户new_user，给用户分配表空间，设置限额为50M，授予con_res_view角色。
- 最后测试：用新用户new_user连接数据库、创建表，插入数据，创建视图，查询表和视图的数据。
      
### 2. 实验过程：

 - 第1步：以system登录到pdborcl，创建新角色**con_res_ltt**和新用户**ltt**，并授权和分配空间：
 
```sql
$ sqlplus system/123@pdborcl
SQL> CREATE ROLE con_res_ltt;
SQL> GRANT connect,resource,CREATE VIEW TO con_res_ltt;
SQL> CREATE USER ltt IDENTIFIED BY 123 DEFAULT TABLESPACE users TEMPORARY TABLESPACE temp;
SQL> ALTER USER ltt QUOTA 50M ON users;
SQL> GRANT con_res_ltt TO ltt;
SQL> exit
```
![第一步](https://github.com/DoubleLTT/Oracle/blob/master/img/oracle%E5%AE%9E%E9%AA%8C.JPG)
![第一步](https://github.com/DoubleLTT/Oracle/blob/master/img/oracle%E5%AE%9E%E9%AA%8C.JPG)

 - 第2步：新用户**ltt**连接到pdborcl，创建表mytable和视图myview，插入数据，最后将myview的SELECT对象权限授予hr用户。
```sql
$ sqlplus new_user/123@pdborcl
SQL> show user;
USER is "NEW_USER"
SQL> CREATE TABLE mytable (id number,name varchar(50));
Table created.
SQL> INSERT INTO mytable(id,name)VALUES(1,'zhang');
1 row created.
SQL> INSERT INTO mytable(id,name)VALUES (2,'wang');
1 row created.
SQL> CREATE VIEW myview AS SELECT name FROM mytable;
View created.
SQL> SELECT * FROM myview;
NAME
--------------------------------------------------
zhang
wang
SQL> GRANT SELECT ON myview TO hr;
Grant succeeded.
SQL>exit
```
![第二步](https://github.com/DoubleLTT/Oracle/blob/master/img/%E7%AC%AC%E4%BA%8C%E6%AD%A5.JPG?raw=true)

 - 第3步：用户hr连接到pdborcl，查询ltt授予它的视图myview
 
 ![第三步](https://github.com/DoubleLTT/Oracle/blob/master/img/%E7%AC%AC%E4%B8%89%E6%AD%A5.JPG?raw=true)


### 3. 实验总结：

     在实验过程中，我创建的数据库新角色为con_res_ltt，新用户为ltt，
     以ltt的用户身份进入数据库，连接到pdborcl,创建表mytable和视图myview，
     在表中新建了1行，命名为NAME，值为liao,切换到hr，可以查询到新建的字段值。





