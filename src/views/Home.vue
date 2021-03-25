<template>
  <div class="goods">
    <div class="goods-item" v-for="item in goodsList" :key="item.id">
        <h2>{{ item.name }}</h2>
        <p>{{ item.label }}</p>
        <span>price: {{ item.price }} $</span><br>
        <button @click="addItem(item.id)"> Add to basket </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "Home",
  emits: ["addItem"],
  props: {
    goodsList: Object,
    basketList: Array
  },
  setup(props, {emit}) {
    const addItem = function(id) {
      const addedItem = props.goodsList.find(i => i.id === id)
      emit("addItem", addedItem)
    }
    return { addItem }
  }
}
</script>

<style scoped>
  .goods {
    display: flex;
    justify-content: space-around;
  }
  .goods-item {
     max-width: 280px;
     border-radius: 4px;
     box-shadow: 0 0 10px rgba(0,0,0,0.5);
     padding: 10px;
     margin: 5px;
  }
  .goods-item button {
     cursor: pointer;
     padding: 5px;
     margin: 5px;
     background-color: #42b983;
     color: white;
     border: none;
     outline: none;
  }
  .goods-item button:active {
      margin: 5px;
      color: #42b983;
      background-color: white;
  }
 @media screen and (max-width: 1024px) {
  .goods {
      flex-direction: column;
      justify-content: center;
      align-items: center;
    }
 }
</style>