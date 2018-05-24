<template>
  <div>
    <app-stock v-for="(stock,id) in stocks" v-bind:key="stock.id" :stock="stock"></app-stock>
  </div>
</template>

<script>
  import {mapGetters} from 'vuex';
  import Stock from './Stock.vue';
    export default {
        computed: {
          ...mapGetters({
            stocks: 'stockProtfolio',
          }),

        },
      components: {
            appStock: Stock
      }
    }
</script>

<style>

</style>
