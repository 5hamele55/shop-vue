<template>
  <div id="nav">
    <router-link to="/">Home</router-link> |
    <router-link to="/basket">Basket</router-link>
  </div>
  <router-view :goodsList="goodsList" :basketList="basketList" @addItem="addItem" @rmIndex="rmIndex" :sum="sum"/>
</template>
<script>
import { ref, watch } from 'vue'
export default {
    setup() {
    const goodsList = ref([
      {id: 1,
      name: "article 1",
      label: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
      price: 25},
      {id: 2,
      name:"article 2",
      label: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
      price: 35},
      {id: 3,
      name: "article 3",
      label: "Lorem ipsum dolor sit amet, consectetur adipiscing elit, sed do eiusmod tempor incididunt ut labore et dolore magna aliqua.",
      price: 45}
      ])
    let basketList = ref([])
    let checkBasket = function () {
      if (!basketList.value.length) {
        let storage = localStorage.getItem("store")
        let localStore = JSON.parse(storage)
        basketList.value = localStore
      }
    }
    checkBasket();
    let sum = ref(null)
    let getSum = () => {
      let arr = []
      basketList.value.forEach(element => arr.push(element.price));
      sum.value = arr.reduce(( acc, cur ) => acc + cur, 0);
    }
    getSum()
    const addItem = val => {
      if(basketList.value.includes(val)){
        alert(`"${val.name}" is already added to basket`)
      }
      else {
        basketList.value.push(val)
      }
    }
    const rmIndex = function (val) {
      basketList.value.splice(val, 1)
    }
    watch(basketList.value, () => {
      localStorage.setItem("store", JSON.stringify(basketList.value))
      getSum()
      })
    return { goodsList, basketList, addItem, rmIndex, checkBasket, sum, getSum }
  }
}
</script>
<style>
* {
  padding: 0;
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

#nav {
  padding: 30px;
}

#nav a {
  font-weight: bold;
  color: #2c3e50;
}

#nav a.router-link-exact-active {
  color: #42b983;
}
</style>
