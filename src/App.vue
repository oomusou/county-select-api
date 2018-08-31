<template>
  <div>
    <my-select v-model="cityIndex" :data-source="cities"></my-select>
    <my-select v-model="areaIndex" :data-source="areas"></my-select>
    {{ zip }}
  </div>
</template>

<script>
import axios from 'axios';
import MySelect from './components/MySelect.vue';

export default {
  name: 'app',
  components: {
    MySelect,
  },
  data() {
    return {
      taiwan: [
        {
          name: '',
          areas: [
            { name: '', zip: 0 },
          ],
        },
      ],
      cityIndex: 0,
      areaIndex: 0,
    };
  },
  computed: {
    cities() {
      return this.taiwan;
    },
    areas() {
      return this.cities[this.cityIndex].areas;
    },
    zip() {
      return this.areas[this.areaIndex].zip;
    },
  },
  watch: {
    cityIndex() {
      this.areaIndex = 0;
    },
  },
  mounted() {
    const endpoint = 'https://localhost:5001/api/cityzip';
    const response = res => this.taiwan = res.data;
    const error = e => console.log(e);

    axios
      .get(endpoint)
      .then(response)
      .catch(error);
  },
};
</script>

<style>
</style>
