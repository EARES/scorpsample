<template>
  <div id="app">
    <MasterHeader />
      <router-view />
    <MasterFooter />
  </div>
</template>

<script>
import MasterHeader from '@/components/Header.vue';
import MasterFooter from '@/components/Footer.vue';

export default {
  name: 'App',
  components: {
    MasterHeader,
    MasterFooter
  },
};
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
}
@media screen and (max-width: 1023px) {
  .navbar-menu {
    background-color: #eb6e64 !important;
    border-top: 1px solid rgb(0, 0, 0, 0.1);
  }

  a.navbar-item.is-active {
    color: black !important;
  }
}
</style>
