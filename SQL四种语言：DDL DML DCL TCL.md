#SQL四种语言：DDL DML DCL TCL

##DDL - Data Definition Language

数据库定义语言：定义数据库的结构。 其主要命令有CREATE，ALTER，DROP等，下面用例子详解。该语言不需要commit，因此慎重。

	CREATE - to create objects in the database   在数据库创建对象
	
	例：CREATE DATABASE test; // 创建一个名为test的数据库
	ALTER - alters the structure of the database   修改数据库结构
	
	例：ALTER TABLE test ADD birthday date; // 修改test表，新增date类型的birthday列
	DROP - delete objects from the database   从数据库中删除对象
	例：DROP DATABASE test;// 删除test数据库
	还有其他的： 
	TRUNCATE - 截断表内容（开发期，还是挺常用的）
	COMMENT - 为数据字典添加备注
##DML - Data Manipulation Language
数据库操作语言：SQL中处理数据库中的数据 其主要命令有SELECT,INSERT,UPDATE,DELETE等，这些例子大家常用就不一一介绍了。该语言需要commit。

还有常用的 LOCK TABLE[http://www.bysocket.com/?p=191](http://www.bysocket.com/?p=191 "JavaEE 并发：一、FOR UPDATE 实战，监测并解决。")

还有其他不熟悉的：

	CALL - 调用一个PL/SQL或Java子程序
	
	EXPLAIN PLAN - 解析分析数据访问路径  
##DCL - Data Control Language
数据库控制语言：授权，角色控制等

	GRANT - 为用户赋予访问权限
	
	REVOKE - 撤回授权权限  
##TCL - Transaction Control Language
事务控制语言

	COMMIT - 保存已完成的工作
	
	SAVEPOINT - 在事务中设置保存点，可以回滚到此处
	
	ROLLBACK - 回滚 SET TRANSACTION - 改变事务选项