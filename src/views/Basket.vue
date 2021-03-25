<template>
<div v-if="basketList.length">
  <ul class="basket" v-for="(item, index) in basketList" :key="item.id" >
    <li><span>{{ index + 1 }}. {{ item.name }} price: {{ item.price }} $</span>
      &nbsp;
      <button @click="rmBasketItem(index)">x</button>
    </li>
  </ul>
  <div class="sum">Total: {{ sum }} $</div>
</div>
<h1 v-else>Basket is empty</h1>
</template>

<script>

export default {
  props: {
    basketList: Array,
    sum: Number
  },
  emits: ["rmIndex"],
  setup(props, { emit }){
    const rmBasketItem = (index) => {
      emit("rmIndex", index)
    }
    return { rmBasketItem }
  }
}
</script>

<style scoped>
 .basket {
   list-style: none;
 }
 .basket li, .sum {
    max-width: 280px;
    border-radius: 4px;
    box-shadow: 0 0 10px rgba(0,0,0,0.5);
    padding: 5px;
    margin: 0 auto;
    margin-bottom: 10px;
 }
 .basket li button {
   padding: 0px 6px 2px 6px;
   border-radius: 50%;
   border: none;
   outline: none;
   color: #2c3e50;
 }
  .basket li button:active {
   border: 1px solid black;
   background-color: #2c3e50;
   color: white;
 }
 .sum {
   background-color: #42b983;
   color: white;
 }
</style>