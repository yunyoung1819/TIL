## gradle 옵션

### Offline
- `--offline` 옵션으로 Offline(인터넷에 연결되지 않은) 상태에서도 **Cached된(이미 한번 확인하고 임시보관한)**
의존성 파일들을 사용하여 EMS를 기동시킬 수 있습니다. 그렇지만 먼저 Online 모드로 의존성 파일들을 가져와 Cache가 선행된 후에야 가능합니다.
  
  
```
grale jettyrun --offline
```