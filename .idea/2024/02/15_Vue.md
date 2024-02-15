# Vue 

---

갑자기 회사에서 Vue를 시킨다면 이 문서와 함께 초고속 Vue 습득을 시작해보자. <br />
전문적인 수준은 아니어도 자주 쓰는 것들을 따로 외우면 속도가 빨라진다. <br />
사적 의견이 많으니 참고만 하자.

## 1. 기본 구조
**Vue**는 defineComponent를 사용한다.
name 속성으로 import 시 사용할 이름을 지정한다.
```javascript
import { defineComponent } from 'vue';

export default defineComponent({
    name: 'ResourceDetail',
    data() {
        return {
            showPreview: false,
            resource: {} as ResourceData
        }
    }
});

<ResourceDetail /> // 실제 사용할 때

```
**React**는 function 키워드 또는 화살표 함수를 사용한다.
```javascript
export default function App() {
    return (
        <div>
            <h1>Hello, World!</h1>
        </div>
    );
}

const App = () => {
    return (
        <div>
            <h1>Hello, World!</h1>
        </div>
    );
}
export default App;

<App /> // 실제 사용할 때
```

### 1.1. 데이터 바인딩 
**Vue**에서는 데이터 바인딩을 위해 `{{}}`를 사용한다. 아래는 placeholder를 예시로 들었다. 
```javascript
<template v-if="placeholder">
    <span class="areaFlexRow fontS14-font500-fontGray777">
        <span class="infoTextIcon mr04"></span>{{ placeholder }}
    </span>
</template>
```
**React**는 `{}`를 사용한다. 
```javascript
<input type="text" placeholder={placeholder} />
``` 
### 1.2. 이벤트 추가 
**Vue**에서는 `@`를 사용한다. 
```javascript
<button @click="handleClick">Click me</button>
```

**React**에서는 `on`을 사용한다. 이벤트명은 모두 카멜케이스여야 동작한다.  
```javascript
<button onClick={handleClick}>Click me</button>
```

### 1.3. 조건부 렌더링
**Vue**에서는 `v-if`, `v-show`를 사용한다. 조건문을 적용하려는 태그의 속성에 `v-if`를 추가한다. 
```javascript
<template>
    <div>
        <p v-if="condition">조건부 렌더링 true</p>
        <p v-else>조건부 렌더링 false</p>
    </div>
</template>
```
`v-show`는 조건문이 true일 때만 렌더링을 하고, false일 때는 display: none을 적용한다.
```javascript
<p v-show="isVisible">This paragraph is visible</p>
```

**React**에서는 삼항 연산자(?) 또는 && 연산자를 사용한다. 
조건을 걸 태그를 `{}`로 감싸고, 연산자를 사용한다. 
```javascript
{isShow ? <div>조건부 렌더링</div> : null}
{isShow && <div>조건부 렌더링</div>}
```

+) 또한 Vue는 동적 바인딩을 위해 `v-bind`를 사용할 수 있다. 

`v-bind`는 객체를 사용하여 조건에 따라 클래스를 추가할 수 있다. 주로 클래스 `active`등을 더할 때 쓴다. 
```javascript
<div v-bind:class="{ active: isActive }"></div>
```
하지만 `:class`를 사용하면 더 간단하게 사용할 수 있다. `v-bind`가 결과적으로 생략되었지만 같게 동작한다.
```javascript
<div :class="{ active: isActive }"></div>
```

### 1.4. 반복문
**Vue**에서는 `v-for`를 사용한다. 
```javascript
<ul>
    <li v-for="item in items" :key="item.id">
        {{ item.text }}
    </li>
</ul>   

<template>
    <ul>
        <li v-for="item in items" :key="item.id">
            {{ item.text }}
        </li>
    </ul>
</template>
```
때로는 `<template>` 태그를 사용하여 사용하기도 한다. 이 태그는 DOM에 렌더링되지 않는 임시 컨테이너 역할을 한다.
<br /> 모든 글 목록은 반복문이 필요하고,`:key`를 붙이는 것을 잊지 말자.



## 2. 컴포넌트

### 2.1. 컴포넌트 블록 범위 
Vue를 하면서 `<template>` 태그로 감싸는 것을 볼 수 있다. (개인적으로 리액트의 <></>라고 생각하는 편이다.)
<br />한 Vue 파일 내부를 해당 컴포넌트 블록 범위로 정의한다. 따라서 다른 컴포넌트를 사용할 때 내부에 넣으면 그 template 태그 자체가 또 하나의 컴포넌트가 된다. 
```javascript
<template>
    <PreviewPopup title="이미지 미리보기">
        <template v-if="src">
            <img :alt="alt" :src="src" />
        </template>
    </PreviewPopup>
</template>

<script>
    export default {
        name: 'PreviewPopup',
    }
</script>
```
위  `<template>` 태그는 `PreviewPopup`로 import되어 사용된다. 


## 3. 라이프사이클
주로 많이 쓰는 라이프사이클은 아래와 같다. 
* 맨 처음 랜더링 될 때
* 데이터가 변경될 때

자 Vue3 + Composition API를 사용하면 `setup()`을 사용해서 컴포넌트 로직을 정의한다.
```javascript
import { onMounted, onUpdated } from 'vue';

export default {
    setup() {
        onMounted(() => { //처음 마운트 될때 
            console.log('mounted');
        });
        onUpdated(() => { //상태가 업데이트될 때
            console.log('updated');
        });
    }
}
``` 
### 3.1. 데이터 변경 감지
우리는 **React**를 사용할 때 `useEffect`를 사용한다. <br />
useEffect는 두번째 파라미터로 []안에 state가 들어갈 때, 해당 state가 변경될 때만 실행된다. <br />

```javascript
import { useEffect, useRef } from 'react';

export default function Counter() {
    const count = useRef(0);
    const prevCount = useRef(0); // 이전 상태를 저장하기 위한 useRef

    useEffect(() => {
        prevCount.current = count.current; // 현재 상태를 이전 상태로 업데이트
        console.log('count changed', count.current, prevCount.current);
    }, [count.current]); // count.current가 변경될 때마다 효과 실행

    return null; // 렌더링할 JSX가 있다면 여기에 추가
}
```

**Vue**는 `watch()`를 사용한다. 
```javascript

import { ref, watch } from 'vue';

export default {
    setup() {
        const count = ref(0);
        watch(count, (newValue, oldValue) => {
            console.log('count changed', newValue, oldValue);
        });
    }
}
``` 


## 4. Store 
pinia를 써서 스토어를 생성해 보자.
```javascript
import { defineStore } from 'pinia';

export const useStore = defineStore({
    state: () => ({
        account: undefined as Account | undefined,
        isAccont: false
    }),
    getters: {
        publishingCompany: state => state.account?.publishingCompany as string,
        userId: state => state.account?.userId as string,
        userName: state => state.account?.fullName as string
    }
});
``` 
이 스토어는 `localStorage`에 특정 값을 지정하고 필요 시마다 `localStorage`에 저장된 값을 가져온다.