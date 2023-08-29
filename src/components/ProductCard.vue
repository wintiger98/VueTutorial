<template>
  <div>
    <img :src="oneroom.image" class="room-img">
    <h4 @click="openModal(oneroom.id)">{{ oneroom.title }}</h4>
    <p>{{ oneroom.price }}만원</p>
  </div>
</template>

<script>
export default {
    name: "ProductCard",
    props: {
        oneroom: Object,
    },
    methods: {
        openModal(index) {
            this.$emit("click-event", index)
        }
    }
}
</script>

<style>

</style>