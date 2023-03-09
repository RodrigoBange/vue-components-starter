<template>
  <div class="col-md-4 mt-4">
    <div class="card">
      <div class="card-body">
        {{ stock.name }}
        <span
          :class="{
            down: stock.price < stock.previousPrice,
            up: stock.price > stock.previousPrice,
          }"
          >{{ stock.currency }} {{ stock.price.toFixed(4) }}</span
        >
        <input type="number" v-model="amount" min="0"/>
        <button class="btn btn-primary" @click="$emit('buy', amount, stock.name, stock.price)">Buy</button>
      </div>
    </div>
    </div>
</template>

<script>
export default {
    props: {
        stock: Object
    },
    data() {
        return {
            amount: 0
        }
    },
};
</script>

<style>
.up {
  color: green;
}
.down {
  color: red;
}
</style>