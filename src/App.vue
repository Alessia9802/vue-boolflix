<template>
  <div id="app">
    <Siteheader />
    <!-- site_header -->
    <Sitemain />
    <!-- site_main -->
    <Sitefooter />
    <!-- site_footer -->
  </div>
</template>

<script>
import Siteheader from "./components/Siteheader.vue";
import Sitemain from "./components/Sitemain.vue";
import Sitefooter from "./components/Sitefooter.vue";

export default {
  name: "App",
  components: {
    Siteheader,
    Sitemain,
    Sitefooter,
  },
};
</script>

<style lang="scss">
@import "./assets/scss/common.scss";
</style>
