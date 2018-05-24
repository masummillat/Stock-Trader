<template>
  <div class="col-sm-6 col-md-4">
    <div class="panel panel-success">
      <div class="panel-heading">
        <h3 class="panel-title">
          {{stock.name}}
        </h3>
        <small>(Price: {{stock.price}})</small>
      </div>
      <div class="panel-body">
        <div class="pull-left">
          <input type="number" class="form-control" placeholder="Quantity" v-model="quantity" >
        </div>
        <div class="pull-right">
          <button
            class="btn btn-success"
            @click="buyStock"
            :disabled ="quantity<=0 || !Number.isInteger(parseInt(quantity))">Buy</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  console.log(Number.isInteger(parseInt(12)))
  export default{
    props:['stock'],
    data(){
        return{
            quantity:0,
        }
    },
    methods:{
        buyStock(){
            const order = {
                stockId: this.stock.id,
                stockPrice: this.stock.price,
                quantity: this.quantity

            }
            this.$store.dispatch('buyStock',order)
            console.log(order)
          this.quantity=0;
        }
    }
  }
</script>

<style>

</style>
