<template>
  <div class="data-boxes-wrapper" v-if="this.stats != undefined">
    <div class="grid md:grid-cols-2 gap-4" v-if="check()">
      <div class="shadow-md bg-blue-200 p-10 text-center rounded">
        <h3 class="text-3xl text-blue-900 font-bold mb-4">Cases</h3>
        <div class="text-2xl mb-4">
          <span class="font-bold">New:</span>
          {{ this.stats.NewConfirmed }}
        </div>
        <div class="text-2xl mb-4">
          <span class="font-bold">Total:</span>
          {{ this.stats.TotalConfirmed }}
        </div>
      </div>
      <div class="shadow-md bg-blue-200 p-10 text-center rounded">
        <h3 class="text-3xl text-blue-900 font-bold mb-4">Deaths</h3>
        <div class="text-2xl mb-4">
          <span class="font-bold">New:</span>
          {{ this.stats.NewDeaths }}
        </div>
        <div class="text-2xl mb-4">
          <span class="font-bold">Total:</span>
          {{ this.stats.TotalDeaths }}
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ["stats"],
  setup(props) {
    return {};
  },
  methods: {
    check() {
      console.log(this.stats);
      return true;
    },
  },
};
</script>

<style lang="scss"></style>
