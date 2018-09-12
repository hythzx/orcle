## 数据库的启动与关闭
### 切换用户
```bash
su - oracle
```
### 连接数据库:
```bash
sqlplus /nolog
conn /as sysdba;
```

### SQL PLUS数据库启动和停止
```bash
#启动
startup
#停止
shutdown
```

### ORA-01012: not logged on错误解决

```bash
ps -ef|grep ora_dbw0_$ORACLE_SID
kill -9 xxx
sqlplus sys as sysdba
startup;
```

### 进入静默状态(只允许DBA用户操作)
```sql
ALTER SYSTEM QUIESCE RESTRICTED;
```

### 退出静默状态
```sql
ALTER SYSTEM UNQUIESCE;
```
### 进入挂起状态
```sql
ALTER SYSTEM SUSPEND;
```

### 退出挂起状态
```sql
ALTER SYSTEM RESUME;
```

## 安全管理


### 创建普通用户
```sql
create user BI identified by bi123 DEFAULT TABLESPACE USERS QUOTA 10M ON USERS ACCOUNT UNLOCK;
```

### 用户赋权
```sql
grant connect,resource to BI;
```

### 移除角色
```sql
REVOKE connect,resource from BI;
```

```sql
# BI2
create user BI2 identified by bi123 DEFAULT TABLESPACE USERS QUOTA 10M ON USERS ACCOUNT LOCK;
grant connect,resource to BI2;
GRANT SELECT,INSERT,UPDATE ON BI.TB_USER TO BI2;
```


### 创建角色
```sql
 
```

### 权限信息涉及到的表

```sql

#角色表
select * from DBA_ROLES;

#角色权限关联表
select * from DBA_ROLE_PRIVS;

#用户角色关联表
select * from USER_ROLE_PRIVS;

#角色-角色关联表
select * from ROLE_ROLE_PRIVS;
```
### 用户锁定　
```sql
ALTER USER BI ACCOUNT LOCK;
```

### 用户解锁
```sql
ALTER USER BI ACCOUNT UNLOCK;
```
### 删除用户
```sql
DROP USER BI;
```

### 查看数据库所有用户名及其默认表空间
```sql
SELECT USERNAME,DEFAULT_TABLESPACE FROM DBA_USERS;
```

### 查看数据库中各用户的登录时间、会话号
```sql
SELECT SID,SERIAL#,LOGON_TIME,USERNAME FROM V$SESSION; 
```

