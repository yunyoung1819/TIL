## ;pushpin; 인프런 시니어 백엔드 개발자가 알려주는 데이터베이스 개론 & SQL

### :seedling: 데이터 추가하기
```mysql
INSERT INTO employee 
VALUES (1, 'YUNYOUNG', '1988-02-01', 'M', 'DEV_BACK', '600000000', null);

INSERT INTO employee 
VALUES (2, 'LEEJUMI', '1992-01-01', 'F', 'DSGN', '600000000', null);

INSERT INTO empoyee(name, birth_date, sex, position, id)
VALUES ('JENNY', '2004-10-12', 'F', 'DEV_BACK', 3);
```

```mysql
SELECT * FROM employee;
```

### INSERT statement
> INSERT INTO table_name VALUES(comma-separated all values);

> INSERT INTO table_name (attribute list) 
  VALUES (attributes list 순서와 동일하게 comma-separated values);

> INSERT INTO table_name VALUES (..., ..), (..., ..), (..., ..);

```mysql
insert into employee values
                         (4, 'MINJEE', '2006-03-13', 'F', 'FRONT_DEV', 600000000, null),
                         (5, 'HYERIN', '2008-04-04', 'F', 'FRONT_DEV', 600000000, null),
                         (6, 'HANYPARM', '2008-05-05', 'F', 'FRONT_DEV', 600000000, null),
                         (7, 'DANIYEL', '2008-05-05', 'F', 'FRONT_DEV', 600000000, null),
                         (8, 'LEEHYEIN', '2008-06-06', 'F', 'DSGN', 600000000, null);
```

```mysql
insert into department values
                           (1001, 'headquarter', 4),
                           (1002, 'HR', 6),
                           (1003, 'development', 1),
                           (1004, 'design', 3);
```

```mysql
insert into project values
    (2001, '쿠폰 구매/선물 서비스 개발', 13, '2024-03-10', '2024-07-09'), 
    (2002, '확장성있게 백엔드 리팩토링', 13, '2024-01-23', '2024-03-23'),
    (2003, '홈페이지 UI 개선', 11, '2024-05-09', '2024-06-11');
    
```

```mysql
insert into works_on values
                         (5, 2001),
                         (13, 2001),
                         (1, 2001),
                         (8, 2001),
                         (7, 2003),
                         (2, 2003),
                         (12, 2003);
```


### :seedling: 데이터 수정하기
> UPDATE employee SET dept_id = 1003 WHERE id = 1;

> select * from employee WHERE id = 1;

> UPDATE employee SET salary = salary * 2 WHERE dept_id = 1003;

홈페이지 UI 개선 프로젝트에 참여한 직원의 연봉을 2배로 인상하자!
```mysql
UPDATE employee, works_on
SET salary = salaray * 2
WHERE employee.id = works_on.empl_id AND proj_id = 2003;
```

회사의 모든 구성원의 연봉을 두배로 올리자!
```mysql
UPDATE employee
SET salary = salaray * 2;
```

### UPDATE statement
```mysql
UPDATE table_name(s)
SET attribute = value [, attribute = value, ...]
[WHERE condition(s)];
```

### :seedling: 데이터 삭제하기
```mysql
DELETE FROM employee WHERE id = 8;

DELETE FROM works_on WHERE empLl_id = 2;

DELETE FROM works_on WHERE empl_id = 5 and proj_id <> 2001;

DELETE FROM project;
```

### DELETE statement

```mysql
DELETE FROM table_name
[WHERE condition(s)];
```