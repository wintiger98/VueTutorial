<template>
  <div class="black-bg" v-if="isModal">
    <div class="white-bg">
      <h4>{{ onerooms[modalNum].title }}</h4>
      <img :src="onerooms[modalNum].image" alt="">
      <p>{{ onerooms[modalNum].content }}</p>
      <input v-model.number="month">
      <p>{{ onerooms[modalNum].price * month }}원</p>
      <button @click="closeModal">닫기</button>
    </div>
  </div>
</template>

<script>
export default {
    name: "DetailPageModal",
    data(){
        return {
            month: 1,
        }
    },
    watch : {
        month(num) {
            if(isNaN(num)){
                alert('숫자를 입력하시오');
                this.month = 1;
            }
        },
    },
    props: {
        onerooms : Array,
        modalNum : Number,
        isModal: Boolean,
    },
    methods: {
        closeModal() {
            this.$emit("close-modal");
        }
    },
    beforeUpdate(){
        if(this.month == 2){
            alert("2개월은 불가능합니다");
            this.month = 3;
        }
    }
}
</script>

<style>

</style>