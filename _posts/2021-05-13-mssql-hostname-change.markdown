---
layout: post
title: MSSQL hostname 변경
date: 2021-05-13 00:19:00 +0900
category: MSSQL
---

## 방법

```sql
-- 현재 hostname확인
select @@servername
select host_name()

-- 현재 hostname 설정 삭제
exec sp_dropserver '이전hostname'

-- 새로운 hostname 설정
exec sp_addserver '변경된hostname', 'local'

--DB 재시작
```

### 참고 자료
> https://tshooter.tistory.com/142
