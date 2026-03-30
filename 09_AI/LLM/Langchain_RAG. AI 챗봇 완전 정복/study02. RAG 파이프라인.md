## :pushpin: RAG 파이프라인


### RAG 파이프라인
- RAG는 문서를 숫자로 변환하여 저장하는 인덱싱, 검색하고 답변을 생성하는 검색/생성 두가지 구조로 나뉘어 있다.

#### 데이터 인덱싱 
문서 (Document) -> 분할된 문서 (Chunk) -> 벡터 임베딩 (Vector Embedding) -> 벡터 DB (Vector DB)

![](images/데이터인덱싱.png)

#### 데이터 검색 및 생성
질문 (Query) -> 벡터 임베딩 (Vector Embedding) -> 벡터 DB 검색 (Retrieval) -> 유사 문장 출력 (Top-K chunks) -> LLM -> 답변 생성 (Answer)

![](images/데이터검색및생성.png)