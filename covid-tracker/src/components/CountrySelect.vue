<template>
  <div class="country-select-wrapper" v-if="this.countries != undefined">
    <select
      v-model="selected"
      class="form-select mt-10 mb-10 block w-full border p-3 rounded"
      @change="countrySelect()"
    >
      <option value="0">Select Country</option>
      <option
        v-for="country in this.countries"
        :key="country.ID"
        :value="country.ID"
      >
        {{ country.Country }}
      </option>
    </select>
  </div>
</template>

<script>
import { ref, reactive } from "vue";

export default {
  props: ["countries"],
  setup(props, context) {
    const selected = ref(0); //country-id in select/option pair

    const countrySelect = async () => {
      //event emit
      const country = props.countries.find(
        (country) => country.ID === selected.value
      );

      //    console.log("Country--<>", country);

      //passing the country object that is selected
      context.emit("countrySelect", country);
    };

    return {
      selected,
      countrySelect,
    };
  },
  created() {},
};
</script>

<style lang="scss"></style>
