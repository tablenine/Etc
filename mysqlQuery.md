### mysql 정렬 시  null 또는 공백이 먼저 나오는 문제
``` mysql
-- ex) dept_rank에 공백값이 있음
order by dept_name asc, dept_rank = '' ASC, dept_rank asc, name asc;
```

### mysql 시간대역 변경
``` mysql
set time_zone = 'Asia/Seoul';
```

### 날짜비교
#### 한달 전
``` mysql
date_add(now(), interval -1 month)
```

#### 내일
``` mysql
date_add(now(), interval 1 day)
```

#### 한시간 전
``` mysql
date_add(now(), interval -1 hour)
```

### varchar형의 숫자 값 정렬
``` mysql
order by filedName+0
```
### 부서별 가장 많이 사용하고 있는 profile 검색
``` mysql
select dept, profile_code,count(profile_code) as cnt from user as a group by profile_code, dept order by dept, cnt desc;
```

### mysql event
#### event 생성
``` mysql
DELIMITER $$
create event test
ON SCHEDULE EVERY 1 MINUTE STARTS '2017-01-01 00:00:01'
DO
BEGIN
 set @oneminuteAgo = date_add(now(), interval -1 minute);
 set @oneminuteAgoQueryFormat = date_format(@oneminuteAgo,'%Y-%m-%d %H:%i');
 set @oneminuteAgoFilePathFormat = date_format(@oneminuteAgo,'%Y%m%d%H%i');
 set @filePath = concat('/tmp/test/', @oneminuteAgoFilePathFormat, '.log');
 set @query1 = '실행할 쿼리'
 
 Prepare stmt From @query1; 
 Execute stmt; 
 Deallocate Prepare stmt; 
END $$
DELIMITER ;
```

#### event 삭제
``` mysql
drop event test;
```

#### event 확인
``` mysql
show variables like 'event%';
select * from information_schema.EVENTS;
```

#### event ON/OFF
``` mysql
SET GLOBAL event_scheduler = ON;
SET GLOBAL event_scheduler = OFF;
```
