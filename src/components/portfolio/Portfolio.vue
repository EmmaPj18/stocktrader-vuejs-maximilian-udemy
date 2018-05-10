<template>
  <div class="row">
    <app-stock v-for="stock in stocks"
               :key="stock.id"
               :stock="stock"></app-stock>
  </div>
</template>

<script>
import Stock from "./Stock.vue";
import { mapGetters } from "vuex";
export default {
  computed: {
    ...mapGetters({
      stocks: "stockPortfolio"
    })
  },
  components: {
    appStock: Stock
  }
};
</script>

<style scoped>
div {
  padding-top: 10px
}
</style>
