# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: JPQL - 다형성 쿼리

### 다형성 쿼리

![다형성쿼리](image/다형성쿼리.PNG)

### TYPE

- 조회 대상을 특정 자식으로 한정
    - 예) Item 중에 Book, Movie를 조회해라
    
- [JPQL]

```
select i from Item i
where type(i) IN (Book, Movie)
```
- [SQL]

````
select i from i
where i.DTYPE in ('B', 'M')
````

### TREAT (JPA 2.1)

- 자바의 타입 캐스팅과 유사
- 상속 구조에서 부모 타입을 특정 자식 타입으로 다룰 때 사용
- FROM, WHERE, SELECT(하이버네이트 지원) 사용 
- 예) 부모인 Item과 자식 Book이 있다.

- [JPQL]
```
select i from Item i
where treat(i as Book).auther = 'kim'
```

- [SQL]
````
select i.* from Item i
where i.DTYPE = 'B' and i.auther = 'kim'
````
