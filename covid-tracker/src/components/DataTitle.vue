<template>
  <div class="text-center" v-if="this.text != undefined">
    <h2 class="text-3xl font-bold">{{ this.text }}</h2>
    <div class="text-2xl mt-4 mb-10">{{ this.dataDate }}</div>
  </div>
</template>

<script>
import moment from "moment";

export default {
  props: ["text", "dataDate"],
  setup(props) {
    return {};
  },
};
</script>

<style lang="scss"></style>
