<template>
  <div>
    <v-btn
      class="mx-2 mb-4"
      elevation="3"
      fab
      small
      dark
      color="indigo"
      to="/user/create"
    >
      <v-icon dark> mdi-plus </v-icon>
    </v-btn>
    <v-data-table
      :headers="headers"
      :items="userData"
      :items-per-page="5"
      class="elevation-1"
    >
      <template v-slot:item.actions="{ item }">
        <v-icon small class="mr-2" @click="editItem(item)"> mdi-pencil </v-icon>
        <v-icon small @click="deleteItem(item)"> mdi-delete </v-icon>
      </template>
    </v-data-table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      headers: [
        {
          text: "name",
          align: "start",
          sortable: false,
          value: "name",
        },
        { text: "email", value: "email" },
        { text: "gender", value: "gender" },
        { text: "date_of_birth", value: "date_of_birth" },
        { text: "status", value: "status" },
        { text: "Actions", value: "actions", sortable: false },
      ],
      userData: [],
    };
  },
  mounted() {
    this.asyncData();
  },
  methods: {
    // async asyncData() {
    //   let userData = await this.$axios.$get("/api/auth/me");
    //   console.log({ userData });
    //   return { userData };
    // },
    async asyncData() {
      await this.$axios
        .$get("/api/users")
        .then((response) => {
          this.userData = response.data;
          console.log(this.userData);
        })
        .catch((error) => {
          // handle error
          console.log(error);
        });
    },
  },
};
</script>
