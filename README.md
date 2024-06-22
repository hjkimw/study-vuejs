# 🐲 Vue

- 데이터 꽂아 넣을 때 `{{}}` 사용

- HTML 속성에 데이터 바인딩 할 때 속성 왼쪽에 `:` 삽입

- vue의 HTML 반복문

  ```javascript
  <태그 v-for="(순회 요소, index) in 반복 횟수 || 순회할 자료형 데이터" :key="key값">
  ```

- vue에서 이벤트 바인딩할 때 `@이벤트명=""` 방식으로 사용

  ```javascript
  ex) @click="", v-on:click="" // 둘다 똑같다 @는 v-on의 축약형
  ```

- vue는 데이터가 변하면 관련된 HTML은 바로 반영되어 자동으로 바뀜

- vue에서 사용할 데이터들은 `data()` 메서드의 반환하는 객체에 세팅

- vue에서 함수를 선언하려면 `methods` 속성에 함수를 선언

  ```javascript
    // 데이터 보관함
    data() {
      return {
        products: [
          { room: '역삼동 원룸', price: 50, declaration: 0 },
          ...
        ],
      };
    },
    // 함수 선언하는 공간
    methods: {
      increase(i) {
        /**
         * vue에서 함수 선언할 때 주의사항
         * - 함수 안에서 data 사용할 때 this를 사용해 접근
         */
        this.products[i].declaration += 1;
      },
    },

  ```

- vue 조건문

  ```javascript
  // 값이 truthy, 조건식이 true일 때만 해당 HTML 보여줌
  <div v-if="조건식">안녕하세요</div>
  ```

  ```javascript
  <>
    <div v-if="1 === 2">안녕하세요</div>
    // v-else 위에 있는 v-if가 참이 아니면 이걸 보여주세요~
    <div v-else>바이바이</div>
  </>
  ```

  ```javascript
  <>
    <div v-if="number === 1">안녕하세요1</div>
    // if문 연달아 여러개 쓰고싶을 경우 v-else-if
    <div v-else-if="number === 2">안녕하세요2</div>
  </>
  ```

- 동적인 UI 만드는 법

  ```
  0. UI를 미리 만들어두고
  1. UI의 현재 상태를 데이터로 저장해둠
  2. 데이터에 따라 UI가 어떻게 보일지 작성
  ```

- 페이지 시작시 자동 실행 함수 `mounted()`

  ```javascript

  export default {
    name: 'App',
    // 페이지 시작시 자동 함수 실행
    mounted() {
      this.getDate().then((res) => {
        this.products = res.map((data) => {
          return { ...data, declaration: 0 };
        });
      });
    },
    ...
    }

  ```

- vue 컴포넌트 만들기

  ```
  1. vue파일 만들기
  2. <template>에 축약할 HTML 넣기
  3. name속성 설정하기
  ```

- 만든 컴포넌트 쓰는 법

  ```
  1. vue 컴포넌트 파일 import 해오고
  2. components: {} 에 속성으로 등록하고
  3. <쓴다/>
  ```

- 컴포넌트 사용 이유 
  - 재사용성
  - 코드 가독성  


- (업데이트사항) 이제 컴포넌트.vue 이름은 귀찮게 2단어 이상으로 작명해야합니다 안그러면 에러로 잡아줌

  DiscountBanner.vue 이런 식으로 2단어로 작명 잘하면 됩니다.
  
  싫으면 package.json 파일 열어서 "rules" 라는 항목에

  ```json
  "rules": {
    "vue/multi-word-component-names": "off"
  }
  ```

