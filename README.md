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
    v-if="조건식"// 값이 truthy, 조건식이 true일 때만 해당 HTML 보여줌
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
