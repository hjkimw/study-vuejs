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
                <h4 :style="fontColor">{{ products[i].room }}</h4>
                <p>{{ products[i].price }}</p>
                <!--                   
                        @이벤트명="" 이런식으로 이벤트 바인딩
                        ex) @click="", v-on:click="", @mouseover="" ..                  
                    -->
                <button type="button" @click="increase(i)">허위매물 신고</button>
                <span>신고 수: {{ products[i].declaration }}</span>
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
                { room: '역삼동 원룸', price: 50, declaration: 0 },
                { room: '천호동 원룸', price: 70, declaration: 0 },
                { room: '마포구 원룸', price: 30, declaration: 0 },
            ],
        };
    },
    // 함수 선언하는 공간
    methods: {
        increase(i) {
            /**
             * vue에서 함수 선언할 때 주의사항
             * - 함수 안에서 data 사용할 때 this를 사용해 접근
             */
            // console.log(this);
            this.products[i].declaration += 1;
        },
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
        &>a {
            color: #fff;
            padding: 10px;
        }
    }
    .wrap {
        margin-top: 10px;
        &>h2 {
            margin-bottom: 10px;
            font-size: 1.4rem;
            font-weight: bold;
        }
        &>p {
            margin-bottom: 14px;
        }
    }
}
</style>
