# :book: 자바 ORM 프로그래밍 기본편

## :pushpin: 페치조인 2

### 페치 조인의 특징과 한계 - 1

- **페치 조인 대상에는 별칭을 줄 수 없다.**
    - 하이버네이트는 가능, 가급적 사용 X
    
- **둘 이상의 컬렉션은 페치 조인할 수 없다.**
- **컬렉션을 페치 조인하면 페이징 API (setFirstResult, setMaxResults)를 사용할 수 없다.**
    - 일대일, 다대일 같은 단일 값 연관 필드들은 페치 조인해도 페이징 가능
    - 하이버네이트는 경고 로그를 남기고 메모리에서 페이징 (매우 위험)
    
### 페치 조인의 특징과 한계 - 2

- 연관된 엔티티들을 SQL 한 번으로 조회 - 성능 최적화
- 엔티티에 직접 적용하는 글로벌 로딩 전략보다 우선함
    - @OneToMany(fetch = FetchType.LAZY)  // 글로벌 로딩 전략
    
- 실무에서 글로벌 로딩 전략은 모두 지연 로딩
- 최적화가 필요한 곳은 페치 조인 적용 


### 페치 조인 - 정리

- 모든 것을 페치 조인으로 해결할 수는 없음
- 페치 조인은 객체 그래프를 유지할 때 사용하면 효과적
- 여러 테이블을 조인해서 엔티티가 가진 모양이 아닌 전혀 다른 결과를 내야 하면, 
페치 조인보다는 일반 조인을 사용하고 필요한 데이터들만 조회해서 DTO로 반환하는 것이 효과적
  

