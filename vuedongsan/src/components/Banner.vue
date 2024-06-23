<template>
  <aside class="banner">
    <h4>지금 결제하면 20% 할인</h4>
  </aside>
</template>

<script>
export default {
  name: 'Banner',
};
</script>

<style lang="scss" scoped>
@import '@styles/variables';

.banner {
  width: 100%;
  background-color: $light-gray;
  padding: 0.625em;
  border-radius: 0.25em;
  margin-top: 20px;
}
</style>
