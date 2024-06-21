<template>
  <div class="container">
    <div class="menu">
      <!-- vue의 HTML 반복문 : <태그 v-for="(순회 요소, index) in 반복 횟수 || 순회할 자료형 데이터" :key="key값"> -->
      <a v-for="(item, index) in menuList" :key="index" href="#">{{ item }}, {{ index }}</a>
    </div>

    <img src="@assets/vue.svg" alt="vue logo" />

    <div class="wrap">
      <h2>원룸샵</h2>
      <div v-for="({ room, price }, i) in products" :key="i">
        <h4 :style="fontColor">{{ room }}</h4>
        <p>{{ price }}</p>
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
  // 데이터 보관함
  data() {
    return {
      menuList: ['Home', 'shop', 'About'],
      fontColor: 'color: blue',
      products: [
        { room: '역삼동 원룸', price: 50 },
        { room: '천호동 원룸', price: 70 },
        { room: '마포구 원룸', price: 30 },
      ],
    };
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
  }
}
</style>
