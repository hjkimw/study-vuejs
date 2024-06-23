<template>
  <!-- v-if="조건식" : 조건식이 true일 때만 해당 HTML 보여줌 -->
  <div class="modal" v-if="modalState">
    <div class="white-bg">
      <!-- 데이터에서 targetNum속성 값에 해당하는 index 요소에 접근해 각 속성을 바인딩 -->
      <h4>{{ products[targetNum].title }}</h4>
      <img :src="products[targetNum].image" :alt="products[targetNum].title" />
      <p>{{ products[targetNum].content }}</p>
      <span>가격 : {{ products[targetNum].price }} 원</span>

      <button
        type="button"
        @click="
          () => {
            // this.$root로 상위 컴포넌트 data에 접근해서 제어
            this.$root.modalState = false;
          }
        "
      >
        닫기
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Modal',
  // props: {
  //   데이터이름: 자료형이름,
  // },
  props: {
    products: Object,
    modalState: Boolean,
    targetNum: Number,
  },
  data() {
    return {};
  },
};
</script>

<style></style>
