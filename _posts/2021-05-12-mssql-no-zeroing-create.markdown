---
layout: post
title: 데이터베이스 파일 (MDF, NDF)에 대해 초기화(Zeroing)하지 않고 즉시 생성
date: 2021-05-12 22:30:23 +0900
category: MSSQL
---
# 방법
> 데이터베이스 파일 (MDF, NDF)에 대해 초기화(Zeroing)하지 않고 즉시 생성되도록 하려면 SQL Server 서비스 시작계정에 대해
[볼륨 유지관리 작업 수행] (Perform Volume Maintenance Tasks) 권한이 부여되어 있어야 합니다.
> 권한을 부여해 준 후 SQL Server 서비스를 재시작해줘야 적용되며, ERRORLOG에서 권한 적용 여부를 확인할 수 있습니다
1. 이터 파일을 생성할 컴퓨터에서 로컬 보안 정책 애플리케이션(secpol.msc)을 엽니다.
2. 왼쪽 창에서 로컬 정책 을 확장한 다음 사용자 권한 할당 을 클릭합니다.
3. 오른쪽 창에서 볼륨 유지 관리 작업 수행 을 두 번 클릭합니다.
4. 사용자 또는 그룹 추가 를 클릭하고 SQL Server 서비스를 실행하는 계정을 추가합니다.
5. 적용 을 클릭한 다음 모든 로컬 보안 정책 대화 상자를 닫습니다.
6. SQL Server 서비스를 다시 시작합니다
![alt text](/public/img/mssql_로컬보안정책.JPG)

# 확인
> SQLServer 재시작 이후 ERRORLOG에서 권한 적용 여부를 확인
```ruby
sp_readerrorlog

Database Instant File Initialization: 사용. For security and performance considerations see the topic 'Database Instant File Initialization' in SQL Server Books Online. This is an informational message only. No user action is required.
```

> 참고 자료
> https://docs.microsoft.com/ko-kr/sql/relational-databases/databases/database-instant-file-initialization?view=sql-server-ver15
