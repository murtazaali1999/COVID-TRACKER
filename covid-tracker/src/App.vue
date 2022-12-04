<template>
  <div>
    <Header />
    <router-view></router-view>
  </div>
</template>

<script>
//import { RouterLink, RouterView } from "vue-router";
import Header from "./components/Header.vue";

export default {
  setup() {},
  components: {
    Header,
  },
};
</script>

<style scoped></style>
