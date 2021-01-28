<template>
  <v-app>
    <v-main>
      <v-container fluid>
        <!-- <div class="table-title">
          <h2>User Data</h2>
        </div> -->
        <v-row>
          <v-col md="4">
            <v-text-field
              v-model="search"
              append-icon="mdi-magnify"
              label="search"
              single-line
              hide-details
            ></v-text-field>
          </v-col>
        </v-row>
        <v-row>
          <v-col>
            <v-data-table
              :headers="headers"
              :items="todos"
              :item-per-page="5"
              :search="search"
              :sort-by="['name', 'email']"
              :sort-desc="[false, true]"
              multi-sort
              class="table-striped elevation-1"
            >
              <template v-slot:[`item.no`]="{ index }">
                {{ index + 1 }}
              </template>

              <template v-slot:[`item.user`]="{ item }">
                {{ item.username }}
              </template>

              <template v-slot:[`item.psd`]="{  }">
                <p>*********</p>
              </template>

              <template v-slot:[`item.profile_picture`]="{ item }"
                ><img
                  :src="item.profile_picture"
                  style="width: 100%; height: 100%"
              /></template>

              <template v-slot:[`item.login`]="{ item }">                  <template v-for="each in item.last_login">
                    <div v-for="(i,index) in each" :key="i.ip_address" >
                      {{ i.ip_address }} on
                      <b>{{ i.login_datetime | formatDate }}</b>
                      <div v-if="index !== each.length-1 "><hr></div>
                    </div>
                  </template>
              </template>

              <template v-slot:[`item.loc`]="{ item }">
                  <p v-for="(each,index) in item.location.filter(x => x.latitude !== null)" :key="each.latitude">
                    <a :href="'http://www.google.com/maps/place/' + each.latitude + '/' + each.longitude"> {{ each.latitude }},
                      {{ each.longitude }}<hr v-if="index !== item.location.length-1 "></a>     
                  </p>
              </template>
            </v-data-table></v-col
          >
        </v-row>
      </v-container>
    </v-main>
  </v-app>
</template>

<script>
import moment from "moment";
import Vue from "vue";

Vue.filter("formatDate", function (value) {
  if (value) {
    return moment.unix(value).format("DD/MM/YY hh:mm");
  }
});

export default {
  name: "VuetifyDatatable",
  props: ["todos"],
  data: () => ({
    search: "",
    headers: [
      { text: "No.", value: "no", sortable: false },
      { text: "User Id", value: "_id.$oid", width: "200px" },
      { text: "Username", value: "user", sortable: false, width: "200px" },
      { text: "Password", value: "psd", sortable: false, width: "200px"},
      { text: "Name", value: "name", width: "200px" },
      { text: "Email", value: "email", width: "200px" },
      { text: "Profile Picture", value: "profile_picture", sortable: false },
      { text: "Register Date", value: "register_date", width: "200px" },
      { text: "Location", value: "loc", sortable: false, width: "300px" },
      { text: "Last Login", value: "login", sortable: false, width: "300px" },
    ],
  }),
};
</script>

<style scoped>
/* .table-title{
  text-align: left !important;
} */
</style>