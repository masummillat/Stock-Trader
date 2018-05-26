<template>
  <div class="container">
    <h1>Trade or View your Portfolio</h1>
    <p>You may Save & load your data</p>
    <p>Click on End day to begin a new day</p>
    <hr>
    <p>Your Funds : {{funds | currency}}</p>
  </div>
</template>

<script>
  import {mapGetters} from 'vuex';
export default {
  name: 'Home',
  computed:{
    ...mapGetters([
        'funds'
    ])

  }

}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>

</style>
