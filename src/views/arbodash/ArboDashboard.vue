<template>
    <div class="page-dashboard">
      <div class="columns is-mobile is-centered">
        <div class="column">
          <p>
            <code class="html">is-narrow</code><br>
            GBIF Data
          </p>
        </div>
        <div class="column">
          Weather Data
        </div>
          Mosquito Data
        <div class="column">
        </div>
      </div>

      <div class="columns">

        <div class="column">

          <MapLeaf :id_map="1"></MapLeaf>
        </div>
        <div class="column">

          <MapLeaf :id_map="2"></MapLeaf>
        </div>

        <div class="column">
          <MapLeaf :id_map="3"></MapLeaf>
        </div>
      </div>

      <div class="columns">
        <div class="column">
          <DataTable :columns="gbif_cols" :entries="gbif_rows"></DataTable>
        </div>
        <div class="column">
          <DataTable :columns="weather_cols" :entries="weather_rows"></DataTable>
        </div>
        <div class="column">
          <DataTable :columns="mos_cols" :entries="mos_rows"></DataTable>
        </div>

      </div>



    </div>
</template>

<script>

import MapLeaf from '@/components/MapLeaf.vue'
import DataTable from "@/components/DataTable.vue";
import axios from "axios";



export default {
  name: 'ArboDashboard',
  components: {
    DataTable,
    MapLeaf
  },
  data() {
    return {

      clients: [],
      weather_cols: [],
      weather_rows: [],
      mos_cols: [],
      mos_rows: [],
      gbif_cols: [],
      gbif_rows: []

    }
  },
  mounted() {
    this.getGBIF()
    this.getWeather()
    this.getMos()

  },
  methods: {
    getGBIF() {
      axios
          .get('/api/v1/gbif/')
          .then(response => {

            this.gbif_cols = Object.keys(response.data[0])

            for (let i = 0; i < response.data.length; i++) {
              this.gbif_rows.push(response.data[i])
            }

          })
          .catch(error => {
            console.log(JSON.stringify(error))
          })
    },

    getWeather() {
      axios
          .get('/api/v1/weather/')
          .then(response => {

            this.weather_cols = Object.keys(response.data[0])

            for (let i = 0; i < response.data.length; i++) {
              this.weather_rows.push(response.data[i])
            }

          })
          .catch(error => {
            console.log(JSON.stringify(error))
          })
    },
    getMos() {
      axios
          .get('/api/v1/mos/')
          .then(response => {

            this.mos_cols = Object.keys(response.data[0])

            for (let i = 0; i < response.data.length; i++) {
              this.mos_rows.push(response.data[i])
            }

          })
          .catch(error => {
            console.log(JSON.stringify(error))
          })
    }
  }
}
</script>
<style lang="scss">


</style>
