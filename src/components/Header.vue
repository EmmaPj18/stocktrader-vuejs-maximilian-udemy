<template>
  <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container">
      <router-link to="/"
                   class="navbar-brand"
                   tag="a">
        Stock Trader
      </router-link>

      <div class="collapse navbar-collapse"
           id="navbarSupportedContent">
        <ul class="navbar-nav mr-auto">
          <router-link class="nav-item"
                       activeClass="active"
                       to="/portfolio"
                       tag="li">
            <a class="nav-link">Portfolio</a>
          </router-link>
          <router-link class="nav-item"
                       activeClass="active"
                       to="/stocks"
                       tag="li">
            <a class="nav-link">Stocks</a>
          </router-link>
        </ul>
        <ul class="navbar-nav navbar-right">
          <li class="nav-item">
            <a class="nav-link"
               @click="endDay"
               style="cursor: pointer;">End Day</a>
          </li>
          <li class="nav-item dropdown"
              @click="isOpen = !isOpen">
            <a class="nav-link dropdown-toggle"
               id="navbarDropdown"
               role="button"
               data-toggle="dropdown"
               aria-haspopup="true"
               aria-expanded="false">
              Save / Load
            </a>
            <div class="dropdown-menu"
                 :class="{show: isOpen}"
                 aria-labelledby="navbarDropdown">
              <a class="dropdown-item"
                 @click="saveData">
                Save Data
              </a>
              <a class="dropdown-item"
                 @click="loadData">
                Load Data
              </a>
            </div>
          </li>
        </ul>
        <strong class="navbar-text navbar-right text-white">Funds: {{ funds | currency }}</strong>
      </div>
    </div>

  </nav>
</template>
<script>
import { mapActions } from "vuex";
export default {
  data() {
    return {
      isOpen: false
    };
  },
  computed: {
    funds() {
      return this.$store.getters.funds;
    }
  },
  methods: {
    ...mapActions({
      randomizeStocks: "randomizeStocks",
      fetchData: "loadData"
    }),
    endDay() {
      this.randomizeStocks();
    },
    saveData() {
      const data = {
        funds: this.$store.getters.funds,
        stockPortfolio: this.$store.getters.stockPortfolio,
        stocks: this.$store.getters.stocks
      };

      this.$http.put("data.json", data);
    },
    loadData() {
      this.fetchData();
    }
  }
};
</script>

<style scoped>
a {
  cursor: pointer;
}
</style>
