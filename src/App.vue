<template>
  <Transition name="fade">
    <DetailPageModal 
    :onerooms="onerooms" 
    :modalNum="modalNum" 
    :isModal="isModal"
    @close-modal="isModal = false"
    />
  </Transition>

  <div class="menu">
    <a v-for="(메뉴, i) in 메뉴들" :key="i">{{메뉴}}</a>
  </div>

  <DiscountBanner :discountPercent="discountPercent" v-if="showDiscount"/>

  <button class="sortBtn" @click="priceSort">가격오름차순</button>
  <button class="sortBtn" @click="priceSortReverse">가격내림차순</button>
  <button class="sortBtn" @click="textSort">한글오름차순</button>
  <button class="sortBtn" @click="textSortReverse">한글내림차순</button>
  <button class="sortBtn" @click="sortBack">되돌리기</button>

  <ProductCard :oneroom="oneroom" @click-event="clickHandler" v-for="oneroom in onerooms" :key="oneroom"/>
  
</template>

<script>
import onerooms from "./assets/oneroom.js";
import DiscountBanner from "./components/DiscountBanner.vue";
import DetailPageModal from "./components/DetailPageModal.vue";
import ProductCard from "./components/ProductCard.vue";

export default {
  name: 'App',
  data(){
    return {
      originOnerooms : [...onerooms],
      메뉴들 : ['Home', 'Shop', 'About'],
      reports : [0,0,0],
      modalNum : 0,
      onerooms : onerooms,
      isModal : false,
      showDiscount : true,
      discountPercent : 30,
    }
  },
  methods : {
    increase(i){
      this.reports[i]++;
    },
    clickHandler(data){
      this.modalNum = data;
      this.isModal = true;
    },
    priceSort() {
      this.onerooms.sort(function(a, b){
        return a.price - b.price;
      })
    },
    priceSortReverse() {
      this.onerooms.sort(function(a, b){
        return b.price - a.price;
      })
    },
    textSort() {
      this.onerooms.sort(function(a, b){
        return a.title > b.title ? 1 : -1;
      })
    },
    textSortReverse() {
      this.onerooms.sort(function(a, b){
        return a.title > b.title ? -1 : 1;
      })
    },
    sortBack() {
      this.onerooms = [...this.originOnerooms];
    },
  },
  mounted(){
    setInterval(() => {
      if(this.discountPercent > 0)
        this.discountPercent--
    }, 1000)
  },
  components: {
    DiscountBanner,
    DetailPageModal,
    ProductCard,
  },
}
</script>

<style>
.sortBtn{
  padding: 5px;
  margin: 5px;
}
.fade-enter-from {
  transform: translateY(-1000px);
}
.fade-enter-active {
  transition: all 1s;
}
.fade-enter-to {
  transform: translateY(0px);
}
.fade-leave-from {
  opacity: 1;
}
.fade-leave-active {
  transition: all 1s;
}
.fade-leave-to {
  opacity: 0;
}

body {
  margin : 0
}
div {
  box-sizing: border-box;
}
.black-bg {
  width: 100%; height: 100%;
  background: rgba(0,0,0,0.5);
  position: fixed; padding: 20px;
}
.white-bg {
  width: 100%; background: white;
  border-radius: 8px;
  padding: 20px;
}

.room-img {
  width: 100%;
  margin-top: 40px;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.menu {
  background: darkslateblue;
  padding: 15px;
  border-radius: 5px;
}
.menu a {
  color: white;
  padding: 10px;
}
</style>
