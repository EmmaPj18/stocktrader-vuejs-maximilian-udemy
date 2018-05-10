<template>
  <div class="col-lg-4 col-md-6">
    <div class="card">
      <div class="card-header bg-success">
        <h3 class="card-title text-white">
          {{ stock.name }}
          <small>(Price: {{ stock.price }})</small>
        </h3>
      </div>
      <div class="card-body bg-dark text-white">
        <div class="float-left">
          <input type="number"
                 class="form-control"
                 placeholder="Quantity"
                 v-model="quantity"
                 :class="{ danger: insufficientFunds}">
        </div>
        <div class="float-right">
          <button class="btn btn-success"
                  @click.prevent="buyStock"
                  :disabled="insufficientFunds || quantity <= 0 || Number.isInteger(quantity)">
            {{ insufficientFunds ? 'Error' : 'Buy'}}
          </button>
        </div>
      </div>
    </div>
  </div>
</template>
<script>
import { mapActions } from "vuex";
export default {
  props: ["stock"],
  data() {
    return {
      quantity: 0
    };
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    },
    insufficientFunds() {
      return this.quantity * this.stock.price > this.funds;;
    }
  },
  methods: {
    ...mapActions({ placeBuyOrder: "buyStock" }),
    buyStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: parseInt(this.quantity)
      };
      console.log(order);
      this.placeBuyOrder(order);
      this.quantity = 0;
    }
  }
};
</script>
<style scoped>
.danger {
  border: 1px solid red;
}
</style>

