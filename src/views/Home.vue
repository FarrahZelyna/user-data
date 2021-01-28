<template>
  <div id="app">
    <vuetify-datatable :todos="todos"></vuetify-datatable>
  </div>
</template>

<script>
// import BootstrapVueDatatable from "../components/BootstrapVueDatatable.vue";
import VuetifyDatatable from "../components/VuetifyDatatable.vue";
import axios from "axios";

export default {
  name: "Home",
  components: {
    // BootstrapVueDatatable,
    VuetifyDatatable
  },
  data() {
    return {
      todos: [],
    };
  },

  created() {
    axios
      .get("/dataset.json")
      .then((res) => (this.todos = res.data))
      .catch((err) => console.log(err));
  },
};
</script>

