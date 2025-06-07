# 📗 Vue.js 학습 가이드

<br>

## 🛠 설치

### Vue CLI 설치
```bash
npm install -g @vue/cli
```

<br>

### 프로젝트 생성
```bash
vue create $프로젝트명
```

<br>

### 개발 서버 실행
```bash
npm run serve
```

<br>

---

<br>

## 📖 기본 문법

### 데이터 바인딩
- 데이터 삽입: `{{}}` 사용
- HTML 속성 바인딩: 속성 왼쪽에 `:` 삽입

<br>

### 반복문
```vue
<태그 v-for="(순회 요소, index) in 반복 횟수 || 순회할 자료형 데이터" :key="key값">
```

<br>

### 이벤트 바인딩
```vue
<!-- 두 가지 방법 모두 동일 (@는 v-on의 축약형) -->
@click=""
v-on:click=""
```

<br>

### 반응성
- Vue는 데이터가 변하면 관련된 HTML이 자동으로 업데이트됨

<br>

### 데이터와 메서드 정의
```javascript
export default {
  // 데이터 보관함
  data() {
    return {
      products: [
        { room: '역삼동 원룸', price: 50, declaration: 0 },
        // ...
      ],
    };
  },
  
  // 함수 선언하는 공간
  methods: {
    increase(i) {
      // Vue에서 함수 내에서 data 사용 시 this로 접근
      this.products[i].declaration += 1;
    },
  },
}
```

<br>

### 조건문
```vue
<!-- 기본 조건문 -->
<div v-if="조건식">안녕하세요</div>

<!-- if-else -->
<div v-if="1 === 2">안녕하세요</div>
<div v-else>바이바이</div>

<!-- if-else if -->
<div v-if="number === 1">안녕하세요1</div>
<div v-else-if="number === 2">안녕하세요2</div>
```

<br>

---

<br>

## 🎨 동적 UI 만들기

### 기본 원칙
1. UI를 미리 만들어두고
2. UI의 현재 상태를 데이터로 저장해둠
3. 데이터에 따라 UI가 어떻게 보일지 작성

<br>

### 라이프사이클 훅
```javascript
export default {
  name: 'App',
  
  // 페이지 시작시 자동 실행 함수
  mounted() {
    this.getData().then((res) => {
      this.products = res.map((data) => {
        return { ...data, declaration: 0 };
      });
    });
  },
  
  // ...
}
```

<br>

---

<br>

## 🧩 컴포넌트

### 컴포넌트 만들기
1. `.vue` 파일 생성
2. `<template>`에 HTML 작성
3. `name` 속성 설정

<br>

### 컴포넌트 사용하기
1. Vue 컴포넌트 파일 import
2. `components: {}` 에 등록
3. 템플릿에서 사용

<br>

### 컴포넌트 사용 이유
- **재사용성**: 코드의 재사용
- **가독성**: 코드 구조 개선

<br>

### 컴포넌트 네이밍 규칙
> ⚠️ **주의**: 컴포넌트 이름은 2단어 이상으로 작명해야 합니다.
> 
> 예: `DiscountBanner.vue`

규칙을 비활성화하려면 `package.json`에서:
```json
"rules": {
  "vue/multi-word-component-names": "off"
}
```

<br>

### 데이터 바인딩 주의사항
- `{{데이터바인딩}}`은 해당 `data`가 존재해야 동작

<br>

---

<br>

## 📤 Props (부모 → 자식 데이터 전달)

### 기본 개념
- 데이터는 한 곳에 보관 (주로 `App.vue`)
- 필요시 props로 전달하여 사용

<br>

### 부모/자식 컴포넌트
- **부모**: 상위 컴포넌트 (예: `App.vue`)
- **자식**: 하위 컴포넌트 (예: `Modal.vue`)

<br>

### Props 전달 3단계

#### Step 1: 데이터 전송
```vue
<!-- 기본 방법 -->
<Modal :products="products" :modalState="modalState" :targetNum="targetNum" />

<!-- v-bind로 객체 묶어서 전송 -->
<Modal v-bind="{ products, modalState, targetNum }" />
```

<br>

#### Step 2: Props 등록
```javascript
export default {
  name: 'Modal',
  props: {
    products: Object,
    modalState: Boolean,
    targetNum: Number,
  },
}
```

<br>

#### Step 3: 사용
```vue
<template>
  <div class="modal" v-if="modalState">
    <div class="white-bg">
      <h4>{{ products[targetNum].title }}</h4>
      <img :src="products[targetNum].images" :alt="products[targetNum].title" />
      <p>{{ products[targetNum].content }}</p>
      <span>가격 : {{ products[targetNum].price }} 원</span>
      
      <button type="button" @click="$emit('openModal', false)">닫기</button>
    </div>
  </div>
</template>
```

<br>

### Props 주의사항
> ⚠️ **중요**: Props는 **읽기 전용(read-only)**입니다!
> 
> ```vue
> <!-- ❌ 잘못된 예 -->
> <button type="button" @click="modalState = false;">닫기</button>
> ```

<br>

### 데이터 저장 팁
> 💡 **원칙**: 데이터를 사용하는 컴포넌트들 중 **최상위 컴포넌트**에 데이터를 저장
> 
> **이유**: 데이터는 아래로 전송(props)하기는 쉽지만, 위로 전송하기는 복잡함

<br>

### Props 다양한 자료형
```vue
<!-- Array, Object -->
<Child :items="[1,2,3]" :user="{name: 'John'}" />

<!-- Number, String -->
<Child :count="42" :message="'Hello'" />
```

<br>

---

<br>

## 📨 Custom Events (자식 → 부모 통신)

### 기본 개념
- Props는 **읽기 전용**이므로 자식이 부모 데이터를 직접 수정 불가
- 자식은 부모에게 **메시지**를 보내서 변경 요청

<br>

### 메시지 보내기 ($emit)
```javascript
// 부모에게 메시지 전송
$emit('작명', 데이터);
```

<br>

#### 자식 컴포넌트에서
```vue
<!-- Card.vue -->
<template>
  <button type="button" @click="$emit('increase', i)">허위매물 신고</button>
  <button type="button" @click="$emit('openModal', true)">상세 페이지 보기</button>
</template>
```

```vue
<!-- Modal.vue -->
<template>
  <button type="button" @click="$emit('openModal', false)">닫기</button>
</template>
```

<br>

### 메시지 수신하기

#### 부모 컴포넌트에서
```vue
<!-- App.vue -->
<template>
  <!-- $event 변수에 $emit()의 두 번째 인자 값이 들어옴 -->
  <Modal @openModal="modalState = $event" v-bind="{ products, modalState, targetNum }" />
  
  <Card
    @openModal="modalState = $event"
    @increase="products[$event].declaration++"
    v-for="(item, i) in products"
    :key="item.id"
    v-bind="{ item, i, activeModal }"
  />
</template>
```

<br>

### Methods에서 $emit 사용
```javascript
methods: {
  closeModal() {
    // methods 내에서는 this.$emit() 사용
    this.$emit('openModal', false);
  }
}
```

<br>

---

<br>

## 📋 Custom Events 요약

1. **목적**: 자식이 부모의 데이터 변경을 요청
2. **방법**: 메시지 전송 (직접 수정 불가)
3. **전송**: `$emit('작명', 데이터)`
4. **수신**: `<자식컴포넌트 @작명한거="처리함수">`
5. **데이터 접근**: `$event` 변수 사용
6. **Methods 내**: `this.$emit()` 사용

<br>

---

<br>

> 📚 **학습 팁**: Vue의 단방향 데이터 흐름을 이해하는 것이 중요합니다. 
> - **Props**: 부모 → 자식 (데이터 전달)
> - **Events**: 자식 → 부모 (메시지 전달)

<br>
