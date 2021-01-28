<template>
  <div class="container pt-3 pb-5">
    <h2>BootstrapVue Datatable</h2>
    <b-row>
      <b-col md="3">
        <b-form-input
          v-model="filter"
          type="search"
          placeholder="search"
        ></b-form-input>
      </b-col>
    </b-row>
    <b-row>
      <b-col>
          <b-container fluid class="table-container">
        <b-table class=table-body
          striped
          hover
          :items="todos"
          :filter="filter"
          :per-page="perPage"
          :current-page="currentPage"
          :fields="fields"
          :sort-by.sync="sortBy"
          :sort-desc.sync="sortDesc"
          responsive="sm"
        >
        </b-table>
          </b-container>
        <div>
          Sorting By: <b>{{ sortBy }}</b
          >, Sort Direction:
          <b>{{ sortDesc ? "Descending" : "Ascending" }}</b>
        </div>
        <b-pagination
          v-model="currentPage"
          :total-rows="rows"
          :per-page="perPage"
        >
        </b-pagination>
      </b-col>
    </b-row>
  </div>
</template>

<script>

export default {
  name: "BootstrapVueDatatable",
  props: ["todos"],
  data: () => ({
    sortBy: "_id",
    sortDesc: false,
    fields: [
      { key: "_id", sortable: true },
      { key: "username", sortable: true },
      { key: "name", sortable: true },
    ],
    perPage: 5,
    currentPage: 1,
    filter: "",
  }),
  computed: {
    rows() {
      return this.todos.length;
    },
  },
};
</script>

<style scoped>
.table-container .table-body{
    overflow-x: scroll;
    /* overflow-y: scroll; */
}

</style>