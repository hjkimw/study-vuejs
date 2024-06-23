<template>
  <!-- v-if="조건식" : 조건식이 true일 때만 해당 HTML 보여줌 -->
  <div class="modal" v-if="modalState">
    <div class="white-bg">
      <!-- 데이터에서 targetNum속성 값에 해당하는 index 요소에 접근해 각 속성을 바인딩 -->
      <h4>{{ products[targetNum].title }}</h4>
      <img :src="products[targetNum].image" :alt="products[targetNum].title" />
      <p>{{ products[targetNum].content }}</p>
      <span>가격 : {{ products[targetNum].price }} 원</span>

      <!-- Custom Event : 부모한테 메세지 보냄, this.$emit('작명',데이터); -->
      <button type="button" @click="$emit('openModal', false)">닫기</button>
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

<style lang="scss" scoped>
@import '@styles/mixins.scss';

.modal {
  width: 100%;
  max-width: 400px;
  height: 80vh;
  background-color: #fff;
  display: block;
  border-radius: 0.375rem;
  border: 1px solid #000;
  padding: 0.875em;
  @include positionCenter(fixed);

  .white-bg {
    & > img {
      width: 100%;
      max-width: 400px;
    }
  }

  button[type='button'] {
    border: none;
    cursor: pointer;
    padding: 10px 20px;
    margin-top: 20px;
  }
}
</style>
