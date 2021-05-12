---
layout: post
title: MSSQL 데이터베이스명 변경
date: 2021-05-12 23:40:23 +0900
category: MSSQL
---

## 방법

```ruby
USE master;  
GO  
ALTER DATABASE MyTestDatabase SET SINGLE_USER WITH ROLLBACK IMMEDIATE
GO
ALTER DATABASE MyTestDatabase MODIFY NAME = MyTestDatabaseCopy ;
GO  
ALTER DATABASE MyTestDatabaseCopy SET MULTI_USER
GO
```

### 참고 자료
> https://docs.microsoft.com/ko-kr/sql/relational-databases/databases/rename-a-database?view=sql-server-2017
