<template>
  <div class="container">
    <MenuList />
    <Modal @openModal="modalState = $event" v-bind="{ products, modalState, targetNum }" />
    <Banner />

    <!-- custom event로 자식 컴포넌트에서 $emit호출로 인해 메세지가 수신되면 부모에서 해당 커스텀 이벤트 핸들러를 호출  -->
    <!--custom event의 $event 변수에 $emit()의 두번째 인자로 전달된 값이 들어온다. -->
    <Card
      @openModal="
        modalState = $event[0]; // Modal 상태 true로 변경
        targetNum = $event[1]; // 클릭한 요소의 순서(id, index) 세팅
      "
      @increase="products[$event].declaration++"
      v-for="(item, i) in products"
      :key="item.id"
      v-bind="{ item, i, activeModal }"
    />
  </div>
</template>

<script>
import MenuList from '@components/MenuList.vue';
import Banner from '@components/Banner.vue';
import Modal from '@components/Modal.vue';
import Card from '@components/Card.vue';

/**
 * 1. 자주 변경될 데이터들은 밑에 저장해놨다가
 * 2. {{데이터 바인딩}}
 */
export default {
  name: 'MainPage',
  // import한 컴포넌트 등록
  components: {
    MenuList,
    Banner,
    Modal,
    Card,
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
      products: null,
    };
  },
  // 함수 선언하는 공간
  methods: {
    async getDate() {
      try {
        const res = await fetch('./src/db/data.json');
        const data = await res.json();
        return data;
      } catch (error) {
        this.progress = 'err' + error;
      }
    },
    activeModal(i) {
      this.modalState = true;

      // 매개변수로 전달받은 index로 this.targetNum 속성을 세팅
      this.targetNum = i;
    },
  },
};
</script>

<style lang="scss">
@import '@styles/main.scss';

.container {
  max-width: 1080px;
  margin: 0 auto;
  text-align: center;

  @media (max-width: $breakpoint) {
    max-width: 800px;
  }
  @media (max-width: $breakpoint2) {
    max-width: 667px;
  }
}
</style>
