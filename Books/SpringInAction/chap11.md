### Chapter 11장
#### :pushpin: REST API를 리액티브하게 사용하기

- 스프링 5가 `RestTemplate`의 리액티브 대안으로 WebClinet를 제공
- `WebClient`는 외부 API로 요청을 할 때 리액티브 타입의 전송과 수신 모두를 한다. 

#### 리소스 얻기(GET)
- RestTemplate의 경우는 `getForObject()`
```text
Mono<Ingredient> ingredient = WebClient.create()
    .get()
    .uri("http://localhost:8080/ingredients/{id}", ingredientId)
    .retrive()
    .bodyToMono(Ingredient.class);
    
ingredient.subscribe(i -> { ... })
```

- 컬렉션에 저장된 값들을 반환하는 요청
```text
Flux<Ingredient> ingredients = WebClient.create()
    .get()
    .uri("http://localhost:8080/ingredients")
    .retrive()
    .bodyToFlux(Ingredient.class);

ingredients.subscribe(i -> { ... })
```

- 차이점이라면 bodyToMono()를 사용해서 응답 몸체를 추찰하는 대신 bodyToFlux()를 사용해서 Flux로 추출하는 것


### 기본 URI로 요청하기
```text
@Bean
public WebClient webClient() {
    return WebClient.create("http://locahost:8080");
}
```

```
@Autowired
WebClient webClient;
public Mono<Ingredient> getIngredientById(String ingredientId) {
    Mono<Ingredient> ingredient = webClient
        .get()
        .uri("/ingredients/{id}", ingredientId)
        .retrive()
        .bodyToMono(Ingredient.class);
    ingredient.subscribe(i -> { ... })
}
```