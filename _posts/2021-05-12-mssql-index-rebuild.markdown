---
layout: post
title: MSSQL 인덱스 리빌드(Index Rebuild)
date: 2021-05-12 22:50:23 +0900
category: MSSQL
---
## 방법 1

```sql
EXEC sp_MSforeachtable @command1="print '?' DBCC DBREINDEX ('?', '', 90)"

--update stats
```

## 방법 2

```sql
 -- Index Rebuild
DECLARE @i int, @sql varchar(1000)
DECLARE @tablename varchar(1000),@ownerName  varchar(1000)
SET @i = 1
DECLARE DB_Cursor CURSOR FOR 
 SELECT TABLE_SCHEMA, TABLE_NAME 
   FROM INFORMATION_SCHEMA.TABLES  
  WHERE TABLE_TYPE = 'BASE TABLE' ORDER BY TABLE_SCHEMA, TABLE_NAME
OPEN DB_Cursor
FETCH NEXT FROM DB_Cursor
INTO @ownerName, @tablename
WHILE @@FETCH_STATUS = 0
BEGIN
 SET @sql='ALTER INDEX ALL ON ' + @ownerName + '.' + @tablename
         +' REBUILD WITH (PAD_INDEX = ON, FILLFACTOR = 90) '
 EXEC (@sql)
 PRINT CONVERT(VARCHAR, @i) + '__' + @ownerName + '.' + @tablename + '............ OK'
 SET @i = @i + 1
 FETCH NEXT FROM DB_Cursor
 INTO @ownerName, @tablename
END
CLOSE DB_Cursor
DEALLOCATE DB_Cursor

PRINT N'1. Index Rebuild...'; 
 
--update stats
```
