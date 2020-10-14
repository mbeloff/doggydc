<template>
  <div id="app">
    <!-- <div class="layout-nav" v-show="$route.name === 'Home' ? false : true">
      <Navigation></Navigation>
    </div> -->
    <div class="layout-content">
      <router-view />
    </div>
    <!-- <div class="layout-footer" v-show="$route.name === 'Home' ? false : true">
      <Footer></Footer>
    </div> -->
  </div>
</template>
<script>
// import Navigation from "@/components/Navigation.vue";
// import Footer from "@/components/Footer.vue";

export default {
  // components: { Navigation, Footer },
  data() {
    return {};
  }
};
</script>
<style lang="scss">
#app {
  font-family: "Avenir", Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #50312c;
  overflow-x: hidden;
  min-height: 100vh;
  display: grid;
  // grid-template-rows: auto 1fr auto;
  grid-template-rows: 1fr;
}

.layout-nav {
  background: rgb(247, 247, 153);
}

.layout-footer {
  background: rgb(224, 222, 218);
}
</style>
