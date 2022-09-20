<template>
  <div class="container-fluid">
    <div class="container">
      <v-app>
        <HeaderComp />
        <v-main></v-main>
      </v-app>
    </div>
  </div>
</template>

<script>
import HeaderComp from "./components/HeaderComp.vue";
export default {
  name: "App",

  components: {
    HeaderComp,
  },

  data: () => ({
    //
  }),
};
</script>

<style lang="scss" scoped>
.container-fluid {
  background-color: #edf2f9;
  box-shadow: none;
  overflow: hidden !important;
  .container {
    max-width: 1500px;
    background-color: #edf2f9;
    padding: 2px;
  }
}
</style>