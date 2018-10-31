## 实验三报告文档

### 1. 实验内容：

- 本实验使用3个表空间：USERS,USERS02,USERS03。在表空间中创建两张表：订单表(orders)与订单详表(order_details)。
- 使用你自己的账号创建本实验的表，表创建在上述3个分区，自定义分区策略。
- 你需要使用system用户给你自己的账号分配上述分区的使用权限。你需要使用system用户给你的用户分配可以查询执行计划的权限。
- 表创建成功后，插入数据，数据能并平均分布到各个分区。每个表的数据都应该大于1万行，对表进行联合查询。
- 写出插入数据的语句和查询数据的语句，并分析语句的执行计划。
- 进行分区与不分区的对比实验。
      
### 2. 实验过程：

 - 创建orders表的语句（我的用户名为LTT）：
 
```sql
CREATE TABLE LTT.orders 
(
 order_id NUMBER(10,0)NOT NULL 
 ,customer_name VARCHAR2(40 BYTE)NOT NULL 
 ,customer_tel VARCHAR2(40 BYTE)NOT NULL 
 ,order_date DATE NOT NULL 
 ,employee_id NUMBER(6,0)NOT NULL 
 ,discount NUMBER(8,2)DEFAULT 0 
 ,trade_receivable NUMBER(8,2)DEFAULT 0 
)
TABLESPACE USERS 
PCTFREE 10 
INITRANS 1 
STORAGE 
( 
 BUFFER_POOL DEFAULT 
)
PARTITION BY RANGE (order_date)
(
 PARTITION partition_before_2016 VALUES LESS THAN (
  TO_DATE('01-01-2016', 'MM-DD-YYYY'))TABLESPACE USERS,
  PARTITION partition_before_2017 VALUES LESS THAN (
  TO_DATE('01-01-2017', 'MM-DD-YYYY'))TABLESPACE USERS02 
);
```
![orders]()

 - 创建order_details表的语句：
 
```sql
CREATE TABLE order_details 
(
id NUMBER(10, 0) NOT NULL 
, order_id NUMBER(10, 0) NOT NULL
, product_id VARCHAR2(40 BYTE) NOT NULL 
, product_num NUMBER(8, 2) NOT NULL 
, product_price NUMBER(8, 2) NOT NULL 
, CONSTRAINT order_details_fk1 FOREIGN KEY  (order_id)
REFERENCES orders  (  order_id   )
ENABLE 
) 
TABLESPACE USERS 
PCTFREE 10 INITRANS 1 
STORAGE (   BUFFER_POOL DEFAULT ) 
NOCOMPRESS NOPARALLEL
PARTITION BY REFERENCE (order_details_fk1)
(
PARTITION PARTITION_BEFORE_2016 
NOLOGGING 
TABLESPACE USERS --必须指定表空间,否则会将分区存储在用户的默认表空间中
...
) 
NOCOMPRESS NO INMEMORY, 
PARTITION PARTITION_BEFORE_2017 
NOLOGGING 
TABLESPACE USERS02
...
) 
NOCOMPRESS NO INMEMORY  
);
```
![order_details]()

 - 插入数据的语句:
 
 ```sql

``` 
 ![insert]()
 
 - 分区策略设计:
 
 
 - 查询数据的语句:

```sql

``` 
- 执行计划分析:


### 3. 实验总结：

     在实验过程中，我创建的数据库新角色为con_res_ltt，新用户为ltt，
     以ltt的用户身份进入数据库，连接到pdborcl,创建表mytable和视图myview，
     在表中新建了1行，命名为NAME，值为liao,切换到hr，可以查询到新建的字段值。






