<template>
  <h1 class="pt-5">Stock list</h1>
  <div class="row">
    <StockItem v-for="stock in stocks" :stock="stock" @buy="buyStock" />
  </div>
  <h1 class="pt-5">Your Portfolio</h1>
  <div class="row">
    <PortfolioItem v-for="portfolioItem in portfolio" :portfolioItem="portfolioItem" @sell="sellStock" />
  </div>
</template>

<script>
import StockItem from "./StockItem.vue";
import PortfolioItem from "@/components/PortfolioItem.vue";

export default {
  name: "StockList",
  components: {
    StockItem,
    PortfolioItem
  },
  data() {
    return {
      stocks: [
        { name: "BMW", price: 61.05, previousPrice: 0, currency: "€" },
        { name: "Caterpillar", price: 146.49, previousPrice: 0, currency: "$" },
        { name: "AMD", price: 76.5, previousPrice: 0, currency: "$" },
        { name: "Gazprom", price: 4.583, previousPrice: 0, currency: "$" },
      ],
      portfolio: [],
    };
  },
  methods: {
    buyStock(amount, name, price) {
      alert("You bought " + amount + " of " + name + " stocks.");

      var exists = false;
      this.portfolio.forEach((portfolioItem) => {
        if (portfolioItem.name === name) {
          exists = true;
          portfolioItem.stockAmount += amount;

          if (portfolioItem.stockAmount > portfolioItem.maxStockAmount) {
            portfolioItem.maxStockAmount = portfolioItem.stockAmount;
            console.log(portfolioItem.maxStockAmount);
          }
        }
      });

      if (!exists) {
        this.portfolio.push({name: name, stockAmount: amount, maxStockAmount: amount, price: price});
      }
    },
    sellStock(amount, name) {
      alert("You sold " + amount + " of " + name + " stocks.");

      var i = 0;
      this.portfolio.forEach((portfolioItem) => {
        if (portfolioItem.name === name) {
          portfolioItem.stockAmount -= amount;

          if (portfolioItem.stockAmount <= 0) {
            this.portfolio.splice(i, 1);
          }
        }
        i++;
      });
    },
    updatePrices() {
      this.stocks.forEach((stock) => {
        stock.previousPrice = stock.price;
        stock.price += (Math.random() - 0.5) * 2;
        if (stock.price < 0) {
          stock.price = 0;
        }
      });
    },
  },  
  mounted() {
    setInterval(() => {
      this.updatePrices();
    }, 1000);
  },
};
</script>

<style scoped>
</style>