<template>
  <div id="app">
    <div class="container">
      <app-header></app-header>
      <div class="row">
        <div class="container">
          <div class="col-xm-12">
            <transition name="slide" mode="out-in">
              <router-view/>
            </transition>

          </div>
        </div>
      </div>
    </div>

  </div>
</template>

<script>
  import Header from './components/Header.vue';
export default {
  name: 'App',
  components:{
      appHeader:Header,
  },
  created(){
      this.$store.dispatch('initStocks');
  }
}
</script>

<style>
  body{
    padding:30px;
  }
  .slide-enter-active{
    animation: slide-in 200ms ease-out forwards;
  }
  .slide-enter-leave{
    animation: slide-out 200ms ease-out forwards;
  }
  @keyframes slide-in {
    from{
      transform: translateY(-30px);
      opacity:0;
    }
    to{
      transform: translateY(0);
      opacity:1;
    }
  }

  @keyframes slide-out {
    from{
      transform: translateY(0);
      opacity:1;
    }
    to{
      transform: translateY(-30px);
      opacity:0;
    }
  }
</style>
