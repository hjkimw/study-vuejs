<template>
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
</template>

<script>
export default {
  name: 'card',
  data() {
    return {
      titleStyles: 'color: blue; font-size: 1.2rem; font-weight: 600',
    };
  },
  props: {
    products: Object,
    activeModal: Function,
  },
  methods: {
    increase(i) {
      /**
       * vue에서 함수 선언할 때 주의사항
       * - 함수 안에서 data 사용할 때 this를 사용해 접근
       */

      //  데이터에서 매개변수로 전달받은 index요소의 declaration 속성에 접근해서 조작
      this.products[i].declaration++;
    },
  },
};
</script>

<style></style>
