<template>
  <div class="col-sm-6 col-md-4">
    <div class="panel panel-success">
      <div class="panel-heading">
        <h3 class="panel-title">
          <!--{{stock.name}}-->
        </h3>
        <small>(Price: {{stock.price | currency}} | {{stock.quantity}})</small>
      </div>
      <div class="panel-body">
        <div class="pull-left">
          <input type="number" class="form-control" placeholder="Quantity" v-model="quantity" >
        </div>
        <div class="pull-right">
          <button
            class="btn btn-success"
            @click="sellStock"
            :disabled ="quantity<=0 || insufficientQuantity || !Number.isInteger(parseInt(quantity))"
          >{{insufficientQuantity ? 'Insufficient order' : 'Sell'}}</button>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
  import {mapActions} from 'vuex';
  export default{

    props:['stock'],
    data(){
      return{
        quantity:0,
      }
    },
    methods:{
      ...mapActions({
        placeSellOrder:'sellStock'
      }),
      sellStock(){
          const order ={
              stockId: this.stock.id,
              stockPrice: this.stock.price,
              quantity: parseInt(this.quantity)
          };
          this.placeSellOrder(order);
          this.quantity=0;
      }
    },
    computed:{
      insufficientQuantity(){
          return parseInt(this.quantity) > this.stock.quantity;
      }
    }
  }
</script>

<style>

</style>
