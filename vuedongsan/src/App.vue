<template>
  <div class="container">
    <img src="@assets/vue.svg" alt="vue logo" />

    <div class="wrap">
      <h2>원룸샵</h2>
      <!-- 
      HTML 속성도 데이터바인딩 가능, 속성 왼쪽엔 :을 넣으면 됨, 모든 HTML 속성 가능(id, class, src, alt ..)
      ex) :속성="데이터 이름"
    -->
      <h4 :style="fontColor">{{ products[0].room }}</h4>
      <p>{{ products[0].price }} 만원</p>
      <h4 :style="fontColor">{{ products[1].room }}</h4>
      <p>{{ products[1].price }} 만원</p>
      <h4 :style="fontColor">{{ products[2].room }}</h4>
      <p>{{ products[2].price }} 만원</p>
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
