<script setup>
import {ref} from "vue";

const props = defineProps({
  setCrypto: Function,
  cryptoNow: String
})

</script>

<template>
  <ul>
    <li @click="setCrypto('BTC')" :class="cryptoNow === 'BTC' ? 'active' : ''">Bitcoin</li>
    <li @click="setCrypto('ETH')" :class="cryptoNow === 'ETH' ? 'active' : ''">ETH</li>
    <li @click="setCrypto('USDT')" :class="cryptoNow === 'USDT' ? 'active' : ''">USDT</li>
  </ul>
</template>

<style>

ul {
  list-style: none;
  width: 200px;
  padding: 0;
  border-radius: 3px;
  border: 3px solid #000;
}

li {
  display: block;
  background: #1A032D;
  color: #fff;
  padding: 20px 0;
}

li:hover, li.active {
  background: #24043e;
  cursor: pointer;
  color: #b99935;
}

</style>