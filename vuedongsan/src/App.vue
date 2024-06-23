<template>
  <div class="container">
    <Menu>child</Menu>
    <!-- <자식 :데이터="데이터"> -->
    <Modal :products="products" :modalState="modalState" :targetNum="targetNum" />
    <Banner />
    <Card :products="products" :activeModal="activeModal" />
  </div>
</template>

<script>
import Menu from './components/Menu.vue';
import Banner from './components/Banner.vue';
import Modal from './components/Modal.vue';
import Card from './components/Card.vue';

/**
 * 1. 자주 변경될 데이터들은 밑에 저장해놨다가
 * 2. {{데이터 바인딩}}
 */
export default {
  name: 'App',
  // import한 컴포넌트 등록
  components: {
    Menu,
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
