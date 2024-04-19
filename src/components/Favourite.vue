<script setup>
const props = defineProps({
  favs: Array,
  getFromFavs: Function
})
</script>

<template>

  <h2>Варианты в избранном</h2>
  <div @click="getFromFavs(index)" v-for="(el, index) in favs" :key="index">
    <span>{{ el.from }}</span>
    <span>{{ el.to }}</span>
  </div>
</template>

<style scoped>
h2 {
  color: #111
}

div {
  display: flex;
  justify-content: center;
  gap: 60px;
  width: 500px;
  margin: 10px auto;
}

span {
  text-align: center;
  min-width: 100px;
  padding: 10px 15px;
  background: #8c00ff;
  color: #fff;
}

div:hover {
  opacity: 0.7;
  transform: scale(1.1);
  cursor: pointer;
}
</style>