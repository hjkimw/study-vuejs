<template>
  <div class="container">
    <div class="menu">
      <!-- vue의 HTML 반복문 : <태그 v-for="(순회 요소, index) in 반복 횟수 || 순회할 자료형 데이터" :key="key값"> -->
      <a v-for="(item, index) in menuList" :key="index" href="#">{{ item }}</a>
    </div>

    <!-- v-if="조건식" : 조건식이 true일 때만 해당 HTML 보여줌 -->
    <div class="modal" ref="modal" v-if="modalState">
      <div class="white-bg">
        <h4>상세페이지임</h4>
        <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Sapiente, maxime</p>
        <button
          type="button"
          @click="
            () => {
              modalState = false;
            }
          "
        >
          ❌
        </button>
      </div>
    </div>

    <div class="wrap">
      <div v-for="(item, i) in products" :key="products[i].id">
        <img :src="products[i].image" :alt="products[i].title" />
        <h4 :style="titleStyles">{{ products[i].title }}</h4>
        <p>{{ products[i].content }}</p>
        <span>가격: {{ products[i].price }}원</span>
        <!--                   
          @이벤트명="" 이런식으로 이벤트 바인딩
          ex) @click="", v-on:click="", @mouseover="" ..                  
        -->
        <div class="btn-wrap">
          <button type="button" @click="increase(i)">허위매물 신고</button>
          <button type="button" @click="activeModal">상세 페이지 보기</button>
        </div>

        <span>신고 수: {{ products[i].declaration || 0 }}</span>
      </div>
    </div>
  </div>
</template>

<script>
/**
 * 1. 자주 변경될 데이터들은 밑에 저장해놨다가
 * 2. {{데이터 바인딩}}
 */
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
  // 데이터 보관함
  data() {
    return {
      modalState: false,
      menuList: ['Home', 'shop', 'About'],
      titleStyles: 'color: blue; font-size: 1.2rem; font-weight: 600',
      products: null,
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
    activeModal() {
      this.modalState = true;
    },
    async getDate() {
      const res = await fetch('./src/db/data.json');
      const data = await res.json();
      return data;
    },
  },
};
</script>

<style>
.container {
  max-width: fit-content;
  margin: 0 auto;
  text-align: center;
  .menu {
    background-color: darkslateblue;
    padding: 15px;
    border-radius: 5px;
    & > a {
      color: #fff;
      padding: 10px;
    }
  }
  .modal {
    width: 100%;
    max-width: 400px;
    height: 80vh;
    background-color: #fff;
    position: fixed;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    display: block;
    border-radius: 0.375rem;
    border: 1px solid #000;
    padding: 0.875em;
    button[type='button'] {
      border: none;
      position: absolute;
      right: 2%;
      top: 2%;
      cursor: pointer;
    }
  }
  .wrap {
    margin-top: 10px;
    & > h2 {
      margin-bottom: 10px;
      font-size: 1.4rem;
      font-weight: bold;
    }
    & > p {
      margin-bottom: 14px;
    }
    div {
      & > img {
        max-width: 400px;
        margin-top: 40px;
      }
    }
  }
}
</style>
