<template>
  <div class="container">
    <div class="menu">
      <!-- vue의 HTML 반복문 : <태그 v-for="(순회 요소, index) in 반복 횟수 || 순회할 자료형 데이터" :key="key값"> -->
      <a v-for="(item, index) in menuList" :key="index" href="#">{{ item }}</a>
    </div>

    <!-- v-if="조건식" : 조건식이 true일 때만 해당 HTML 보여줌 -->
    <div class="modal" v-if="modalState">
      <div class="white-bg">
        <!-- 데이터에서 targetNum속성 값에 해당하는 index 요소에 접근해 각 속성을 바인딩 -->
        <h4>{{ products[targetNum].title }}</h4>
        <img :src="products[targetNum].image" :alt="products[targetNum].title" />
        <p>{{ products[targetNum].content }}</p>
        <span>가격 : {{ products[targetNum].price }} 원</span>

        <Banner />

        <button
          type="button"
          @click="
            () => {
              modalState = false;
            }
          "
        >
          닫기
        </button>
      </div>
    </div>

    <Banner />
    <!-- <Banner></Banner> -->

    <div class="wrap">
      <div v-for="(item, i) in products" :key="item.id">
        <img :src="item.image" :alt="item.title" />
        <h4 :style="titleStyles">{{ item.title }}</h4>
        <p>{{ item.content }}</p>
        <span>가격: {{ item.price }}원</span>
        <!--                   
          @이벤트명="" 이런식으로 이벤트 바인딩
          ex) @click="", v-on:click="", @mouseover="" ..                  
        -->
        <div class="btn-wrap">
          <!-- 데이터의 해당 index 번째 요소에 접근하게 index를 인자로 넘겨준다. -->
          <button type="button" @click="increase(i)">허위매물 신고</button>
          <button type="button" @click="activeModal(i)">상세 페이지 보기</button>
        </div>

        <span>신고 수: {{ item.declaration || 0 }}</span>
      </div>
    </div>
  </div>
</template>

<script>
import Banner from './components/Banner.vue';

/**
 * 1. 자주 변경될 데이터들은 밑에 저장해놨다가
 * 2. {{데이터 바인딩}}
 */
export default {
  name: 'App',
  // import해온 컴포넌트 등록
  components: {
    Banner,
  },
  // 페이지 시작시 자동 함수 실행
  mounted() {
    // 마운트 될 때 데이터 가져오기
    this.getDate().then((res) => {
      this.products = res.map((data) => {
        return { ...data, declaration: 0 };
      });
    });
  },
  // 데이터 보관함
  data() {
    return {
      targetNum: 0, // 몇번째 products[index]를 눌렀는지 index를 저장
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

      //  데이터에서 매개변수로 전달받은 index요소의 declaration 속성에 접근해서 조작
      this.products[i].declaration++;
    },
    activeModal(i) {
      this.modalState = true;

      // 매개변수로 전달받은 index로 this.targetNum 속성을 세팅
      this.targetNum = i;
    },
    async getDate() {
      this.products = 'Loading..';
      try {
        const res = await fetch('./src/db/data.json');
        const data = await res.json();
        return data;
      } catch (error) {
        this.progress = 'err' + error;
      }
    },
  },
};
</script>

<style>
.container {
  max-width: fit-content;
  margin: 0 auto;
  text-align: center;

  .banner {
    width: 100%;
    background-color: #eee;
    padding: 0.625em;
    border-radius: 0.25em;
    margin-top: 20px;
  }

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

    img {
      width: 100%;
    }

    button[type='button'] {
      border: none;
      cursor: pointer;
      padding: 10px 20px;
      margin-top: 20px;
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
