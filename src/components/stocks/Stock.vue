<template>
  <div class="col-sm-6 col-md-4">
    <div class="panel panel-success">
      <div class="panel-heading">
        <h3 class="panel-title">
          {{stock.name}}
        </h3>
        <small>(Price: {{stock.price | currency}})</small>
      </div>
      <div class="panel-body">
        <div class="pull-left">
          <input
            type="number"
            class="form-control"
            placeholder="Quantity"
            v-model="quantity" >
        </div>
        <div class="pull-right">
          <button
            class="btn btn-success"
            @click="buyStock"
            :disabled =" insufficientFunds || quantity<=0 || !Number.isInteger(parseInt(quantity))">
            {{insufficientFunds ? 'Insufficient Fund' : 'Buy'}}</button>
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
                quantity: parseInt(this.quantity)

            }
            this.$store.dispatch('buyStock',order)
            console.log(order)
          this.quantity=0;
        }
    },
    computed:{
        funds(){
          return this.$store.getters.funds;
        },
        insufficientFunds(){
            return this.stock.price * parseInt(this.quantity) > this.funds;
        }
    }
  }
</script>

<style>

</style>
