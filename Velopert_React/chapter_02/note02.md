### 2장. JSX


#### 코드 이해

```
import React, { Component } from 'react';
```

- Node.js 의 주요 특징은 코드를 모듈화하여 재사용할 수 있다는 점
- 이렇게 모듈들을 js 파일에서 불러와 사용할 수 있는데, 이때 사용하는 코드는 아래와 같다.

```
var fs = require('fs');
```

- ES6(ECMAScript6)에서는 모듈을 불러오는 새로운 키워드가 생김. 바로 import 이다.
- import를 키워드를 사용하여 모듈을 불러오는 방법은 아래와 같다.

```
import fs from 'fs';
```
