<!-- false if no data -->
<template>
  <div class="home-wrapper" v-on="data" v-if="!data.loading">
    <DataTitle :text="data.title" :dataDate="data.dataDate" />
    <DataBoxes :stats="data.stats" />
    <CountrySelect
      @country-select="fetchSpecificCountryCovidData"
      :countries="data.countries"
    />
  </div>
  <div class="flex flex-col align-center justify-center text-center" v-else>
    <div class="text-gray-500 text-3xl mt-10 mb-6">Fetching Data</div>
    <img :src="data.loadingImage" class="w-20 m-auto" alt="NoImage" />
  </div>
  <button
    v-if="data.title != 'Global'"
    @click="clearCountryData()"
    class="bg-green-700 text-white rounded p-3 mt-10 focus:outline-none hover:bg-green-600"
  >
    Clear Country
  </button>
</template>

<script>
import { ref, reactive } from "vue";
import DataTitle from "../components/DataTitle.vue";
import DataBoxes from "../components/DataBoxes.vue";
import CountrySelect from "../components/CountrySelect.vue";

export default {
  setup() {
    const getLoadingImage = () => {
      return new URL(`../assets/loading.gif`, import.meta.url).href;
    };

    const data = reactive({
      loading: true,
      title: "Global",
      dataDate: "",
      stats: {},
      countries: [],
      loadingImage: getLoadingImage(),
    });

    const fetchCovidData = async () => {
      const fetchData = await fetch("https://api.covid19api.com/summary");
      const fetchJson = await fetchData.json();

      console.log("JSON-->", fetchJson);

      data.dataDate = fetchJson.Date;
      data.stats = fetchJson.Global;
      data.countries = fetchJson.Countries;
      data.loading = false;
    };

    //pass the data passed in the event
    const fetchSpecificCountryCovidData = async (country) => {
      //      console.log("Event-Country-->", country);

      data.stats = country;
      data.title = country.Country;
    };

    const clearCountryData = async () => {
      data.loading = true; //before fetching, correct
      const fetchData = await fetch("https://api.covid19api.com/summary");
      const fetchJson = await fetchData.json();

      data.title = "Global";
      data.stats = fetchJson.Global;
      data.loading = false;
    };

    return {
      data,
      getLoadingImage,
      fetchCovidData,
      fetchSpecificCountryCovidData,
      clearCountryData,
    };
  },
  components: { DataTitle, DataBoxes, CountrySelect },
  async created() {
    //runs immediately
    await this.fetchCovidData();
  },
};
</script>
<style lang="scss"></style>
