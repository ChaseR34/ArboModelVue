<template>
<table class="table">
  <thead>
    <tr >
      <th v-for="th in tableHeader" :key="th"> {{ th }} </th>
    </tr>
  </thead>
  <tbody>
  <tr v-for="td_obj in tableData" :key="td_obj">
    <td v-for="td in td_obj">{{ td }}</td>
  </tr>
  </tbody>
</table>

</template>

<script>
export default {
  name: "DataTable",
  props: {
    columns: Array,
    entries: Array
  },
  computed: {
    tableHeader(){
      return this.columns || []
    },
    tableData () {
      return this.entries || []
    }
  }
}
</script>

<style scoped>

</style>