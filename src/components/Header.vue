<template>
  <div class="container">
    <nav class="navbar navbar-default">
      <div class="container-fluid">
        <!-- Brand and toggle get grouped for better mobile display -->
        <div class="navbar-header">
          <button type="button" class="navbar-toggle collapsed" data-toggle="collapse"
                  data-target="#bs-example-navbar-collapse-1" aria-expanded="false">
            <span class="sr-only">Toggle navigation</span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
            <span class="icon-bar"></span>
          </button>
          <router-link to="/" class="navbar-brand">Stock Trader</router-link>

        </div>

        <!-- Collect the nav links, forms, and other content for toggling -->
        <div class="collapse navbar-collapse" id="bs-example-navbar-collapse-1">
          <ul class="nav navbar-nav">
            <router-link to="/portfolio" tag="li" activeClass="active"><a>Portfolio</a></router-link>
            <router-link to="/stocks" tag="li" activeClass="active"><a>Stocks</a></router-link>
          </ul>
          <strong class="navbar-text navbar-right">Funds: {{funds | currency }} </strong>
          <ul class="nav navbar-nav navbar-right">
            <li><a href="#" @click="endDay">End day</a></li>
            <li
              class="dropdown"
              :class="{open:isDropdownOpen}"
              @click="isDropdownOpen = !isDropdownOpen">
              <a href="#"
                 class="dropdown-toggle"
                 data-toggle="dropdown"
                 role="button"
                 aria-haspopup="true"
                 aria-expanded="false">Save & Load <span class="caret"></span></a>
              <ul class="dropdown-menu">
                <li><a href="#" @click="saveData">Save data</a></li>
                <li><a href="#" @click="loadData">Load data</a></li>

              </ul>
            </li>

          </ul>

        </div><!-- /.navbar-collapse -->
      </div><!-- /.container-fluid -->
    </nav>
  </div>
</template>

<script>
  import {mapActions} from 'vuex';
  export default{
    data(){
      return {
        isDropdownOpen: false,
      }
    },
    computed: {
      funds(){
        return this.$store.getters.funds;
      }
    },
    methods: {
      ...mapActions({
        randomizeStocks:'randomizeStocks',
        fetchData: 'loadData'
      }),
      endDay(){
        this.randomizeStocks();
      },
      saveData(){
        const data = {
          funds: this.$store.getters.funds,
          stockPortfolio: this.$store.getters.stockPortfolio,
          stocks: this.$store.getters.stocks,
        }
        console.log(data)
           this.$http.put('data.json',data);
      },
      loadData(){
          console.log('load')
        this.fetchData();
      }
    }
  }
</script>

<style>

</style>
