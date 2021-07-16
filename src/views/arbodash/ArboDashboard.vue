<template>
    <div class="page-dashboard">
      <form @submit.prevent="submitForm">
        <div class="field">
          <label class="label">Start Date</label>
          <div class="control">
            <input class="input" type="text" placeholder="Start Date" v-model="start_date">
          </div>
        </div>

        <div class="field">
          <label class="label">End Date</label>
          <div class="control">
            <input class="input" type="text" placeholder="End Date" v-model="end_date">
          </div>
        </div>

        <div class="field">
          <label class="checkbox">Positive Only</label>

            <input type="checkbox" >
        </div>

        <div class="field">
          <div class="control">
            <button class="button is-success">Submit</button>
          </div>
        </div>

      </form>
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

          <MapLeaf :id_map="1" :data_query="gbif_rows"></MapLeaf>
        </div>
<!--        <div class="column">-->

<!--          <MapLeaf :id_map="2"></MapLeaf>-->
<!--        </div>-->

<!--        <div class="column">-->
<!--          <MapLeaf :id_map="3"></MapLeaf>-->
<!--        </div>-->
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
      gbif_rows: [],
      start_date: "",
      end_date: ""

    }
  },
  mounted() {
    // this.getGBIF()
    // this.getWeather()
    // this.getMos()

  },
  methods: {
    submitForm() {
      const formData = {
        start_date: this.start_date,
        end_date: this.end_date
      }

      this.getGBIF(formData)
      this.getMos(formData)
      this.getWeather(formData)

    },
    getGBIF(formData) {
      axios
          .get('/api/v1/gbif/', { params: formData} )
          .then(response => {
            console.log(response.data)
            this.gbif_cols = Object.keys(response.data[0])

            for (let i = 0; i < response.data.length; i++) {
              this.gbif_rows.push(response.data[i])
            }

          })
          .catch(error => {
            console.log(JSON.stringify(error))
          })
    },

    getWeather(formData) {
      axios
          .get('/api/v1/weather/', formData)
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
    getMos(formData) {
      axios
          .get('/api/v1/mos/', formData)
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
