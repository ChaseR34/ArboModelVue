<template>
  <div class="about">
    <h1>This is an about page</h1>
  </div>
  <TutorialVue></TutorialVue>
  <DataTable :columns="columns" :entries="entries"></DataTable>
</template>
<script>
import TutorialVue from '@/components/TutorialVue.vue';
import DataTable from "@/components/DataTable.vue";

export default {
  name: 'ArboDashboard',
  components: {
    TutorialVue,
    DataTable
  },
  data() {
    return {
      clients: [],
      columns: [
        {name: 'id', text: 'ID'},
        {name: 'name', text: 'Name'},
        {name: 'position', text: 'Position'},
        {name: 'office', text: 'Office'},
        {name: 'extension', text: 'Extension'},
        {name: 'startdate', text: 'Startdate'},
        {name: 'salary', text: 'Salary'},
      ],
      entries: [
        {
          id: "1",
          name: "1",
          position: "1",
          office: "1",
          extension: "1",
          startdate: "1",
          salary: "1"
        }
      ]

    }
  }
}
</script>