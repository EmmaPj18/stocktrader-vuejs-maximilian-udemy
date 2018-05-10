<template>
  <div class="text-white">
    <h1>Trade or View your Portfolio</h1>
    <h6>You may Save and Load your Data</h6>
    <hr>
    <div class="card text-center">
      <div class="card-header bg-dark">
        <h4 class="card-title">Your Funds:</h4>
      </div>
      <div class="card-body bg-info">
        <p id="funds"> {{ funds | currency }}</p>
      </div>
    </div>
    
  </div>
</template>
<script>
export default {
  computed: {
    funds() {
      return this.$store.getters.funds;
    }
  }
}
</script>
<style scoped>
#funds {
  font-weight: 800;
  font-size: 36px;
}
</style>

