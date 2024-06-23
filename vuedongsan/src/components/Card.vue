<template>
  <div>
    <img :src="item.image" :alt="item.title" />
    <h4 :style="titleStyles">{{ item.title }}</h4>
    <p>{{ item.content }}</p>
    <span>가격: {{ item.price }}원</span>
    <!--                   
      @이벤트명="" 이런식으로 이벤트 바인딩
      ex) @click="", v-on:click="", @mouseover="" ..                  
    -->
    <div class="btn-wrap">
      <!-- 현재 요소의 id를 데이터 변경 요청 메세지와 함께 보냄 -->
      <button type="button" @click="$emit('increase', item.id)">허위매물 신고</button>
      <!-- true를 데이터 변경 요청 메세지와 함께 보냄 -->
      <button type="button" @click="$emit('openModal', true)">상세 페이지 보기</button>
    </div>

    <span>신고 수: {{ item.declaration || 0 }}</span>
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
    item: Object,
    i: Number,
  },
  methods: {
    /**
     * vue에서 함수 선언할 때 주의사항
     * - 함수 안에서 data 사용할 때 this를 사용해 접근
     */
  },
};
</script>

<style></style>
