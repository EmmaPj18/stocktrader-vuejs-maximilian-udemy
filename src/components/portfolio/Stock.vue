<template>
  <div class="col-lg-4 col-md-6">
    <div class="card">
      <div class="card-header bg-info">
        <h3 class="card-title text-white">
          {{ stock.name }}
          <br>
          <small>(Price: {{ stock.price }} | Quantity: {{ stock.quantity }})</small>
        </h3>
      </div>
      <div class="card-body bg-dark text-white">
        <div class="float-left">
          <input type="number"
                 class="form-control"
                 placeholder="Quantity"
                 v-model="quantity"
                 :class="{ danger: insufficientQuantity }">
        </div>
        <div class="float-right">
          <button class="btn btn-info"
                  @click.prevent="sellStock"
                  :disabled="insufficientQuantity || quantity <= 0 || Number.isInteger(quantity)">
            {{ insufficientQuantity ? 'Error' : 'Sell'}}
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
    insufficientQuantity() {
      return this.quantity > this.stock.quantity;
    }
  },
  methods: {
    ...mapActions({ placeSellOrder: "sellStock" }),
    sellStock() {
      const order = {
        stockId: this.stock.id,
        stockPrice: this.stock.price,
        quantity: parseInt(this.quantity)
      };
      this.placeSellOrder(order);
      this.quantity = 0;
    }
  },
  created() {
    console.log(this.stock.quantity);
  }
};
</script>
<style scoped>
.danger {
  border: 1px solid red;
}
</style>