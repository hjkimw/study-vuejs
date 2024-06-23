<template>
  <div class="menu">
    <!-- vue의 HTML 반복문 : <태그 v-for="(순회 요소, index) in 반복 횟수 || 순회할 자료형 데이터" :key="key값"> -->
    <a v-for="(item, index) in menuList" :key="index" href="#">{{ item }}</a>
  </div>
</template>

<script>
export default {
  name: 'Menu',
  data() {
    return {
      menuList: ['Home', 'shop', 'About'],
    };
  },
};
</script>

<style></style>
