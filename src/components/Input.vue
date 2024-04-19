<script setup>
const props = defineProps({
  changeAmount: Function,
  convert: Function,
  favorite: Function,
  error: String
})
</script>

<template>
  <p v-show="error" style="color: red">{{ error }}</p>
  <input min="0" @input="changeAmount($event.target.value)" type="number" placeholder="Введите число"><br>
  <button @click="convert" style="margin-right: 120px">Конвертировать</button>
  <button @click="favorite" >В избранное</button>

</template>

<style>
input {
  outline: none;
  width: 500px;
  font-size: 1.2em;
  border-radius: 3px;
  border: none;
  padding: 10px 15px;
  background: #fafafa;
  color: #777
}

button {
  position: relative;
  top: 10px;
  margin: 20px 0;
  color: #fff;
  cursor: pointer;
  background: #1a032d;
  text-transform: uppercase;
  padding: 15px 20px;
  border: 0;
  border-radius: 3px;
  transition: all 0.3s;
  min-width: 200px;
}

button:hover {
  background: #4b0883;
}

</style>