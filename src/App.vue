<script setup>
import Input from './components/Input.vue'
import Selector from './components/Selector.vue'
import Favourite from './components/Favourite.vue'
import {ref, unref} from "vue";
import CryptoConvert from "crypto-convert";

const convert = new CryptoConvert({})

const amount = ref(0)
const cryptoFirst = ref('')
const cryptoSecond = ref('')
const error = ref('')
const result = ref(0)
const favs = ref([])

const changeAmount = (val) => {
  amount.value = val
}
const setCryptoFirst = (val) => {
  cryptoFirst.value = val
}
const setCryptoSecond = (val) => {
  cryptoSecond.value = val
}

async function converting() {
  console.log('test')
  if(amount.value <= 0) {
    return error.value = 'Введите число больше нуля'
  } else if(!cryptoFirst.value || !cryptoSecond.value) {
    return error.value = 'Выберите валюту'
  } else if(cryptoFirst.value === cryptoSecond.value) {
    return error.value = 'Выберите разные валюты'
  }

  error.value = ''

  await convert.ready()

  if(cryptoFirst.value === 'BTC' && cryptoSecond.value === 'USDT') {
    return  result.value = convert.BTC.USD(amount.value)
  }
  if(cryptoFirst.value === 'USDT' && cryptoSecond.value === 'BTC') {
    return  result.value = convert.USD.BTC(amount.value)
  }
  if(cryptoFirst.value === 'BTC' && cryptoSecond.value === 'ETH') {
    return  result.value = convert.BTC.ETH(amount.value)
  }
  if(cryptoFirst.value === 'ETH' && cryptoSecond.value === 'BTC') {
    return  result.value = convert.ETH.BTC(amount.value)
  }
  if(cryptoFirst.value === 'USDT' && cryptoSecond.value === 'ETH') {
    return  result.value = convert.USDT.ETH(amount.value)
  }
  if(cryptoFirst.value === 'ETH' && cryptoSecond.value === 'USDT') {
    return  result.value = convert.ETH.USDT(amount.value)
  }
}

const favorite = () => {
  if(!cryptoFirst.value || !cryptoSecond.value) {
    return error.value = 'Выберите валюту'
  } else {
    error.value = ''
    favs.value.push({
      from: cryptoFirst.value,
      to: cryptoSecond.value
    })
  }
}

const getFromFavs = (index) => {
  cryptoFirst.value = favs.value[index].from
  cryptoSecond.value = favs.value[index].to
}

</script>


<template>
  <h1>Crypto</h1>
  <Input :changeAmount="changeAmount" :convert="converting" :favorite="favorite" :error="error"/>
  <p v-show="result" style="color: green; font-size: 2em">{{ result }}</p>
  <div class="selectors">
    <Selector :setCrypto="setCryptoFirst" :cryptoNow="cryptoFirst" />
    <Selector :setCrypto="setCryptoSecond" :cryptoNow="cryptoSecond" />
  </div>
  <Favourite :favs="favs" v-if="favs.length > 0" :getFromFavs="getFromFavs"/>
</template>

<style scoped>

.selectors {
  display: flex;
  justify-content: center;
  gap: 120px
}

</style>
