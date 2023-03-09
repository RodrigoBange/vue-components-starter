<template>
  <div class="col-md-4 mt-4">
    <div class="card">
      <div class="card-body">
        <span class="fw-bold">
          {{ portfolioItem.name }}
        </span>
        <br>
        <span>
          Your stock amount:
          <strong>{{ portfolioItem.stockAmount }} </strong>
        </span>
        <br>
        <span>
          Original price:
          {{ portfolioItem.price.toFixed(2) }}
        </span>
        <input type="number" v-model="stockAmount" min="1" :max="portfolioItem.maxStockAmount"/>
        <button class="btn btn-primary" @click="$emit('sell', stockAmount, portfolioItem.name)">Sell</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    portfolioItem: Object
  },
  data() {
    return {
      stockAmount: this.portfolioItem.stockAmount,
    }
  },
};
</script>

<style scoped>

</style>