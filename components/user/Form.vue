<template>
  <div id="app">
    <v-app id="inspire">
      <v-card>
        <v-list-item>
          <v-list-item-content>
            <v-list-item-title class="headline">User Create</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
        <v-form v-model="valid" @submit.prevent="submutData()">
          <v-container>
            <v-row>
              <v-col cols="12" md="6">
                <v-text-field
                  v-model="formModel.name"
                  :rules="nameRules"
                  :counter="10"
                  label="Name"
                  required
                  outlined
                ></v-text-field>
              </v-col>
              <v-col cols="12" md="6">
                <v-text-field
                  v-model="formModel.email"
                  :rules="emailRules"
                  :counter="10"
                  label="E-mail"
                  required
                  outlined
                ></v-text-field>
              </v-col>
              <v-col cols="12" md="6">
                <v-text-field
                  v-model="formModel.identifier"
                  name="identifier"
                  label="Identifier"
                  required
                  outlined
                />
              </v-col>
              <v-col cols="12" md="6">
                <v-text-field
                  v-model="formModel.date_of_birth"
                  :rules="dateRules"
                  label="Date of Birth"
                  required
                  outlined
                ></v-text-field>
              </v-col>

              <v-col cols="12" md="6">
                <v-text-field
                  v-model="formModel.gender"
                  :rules="genderRules"
                  label="Gender"
                  required
                  outlined
                ></v-text-field>
              </v-col>
              <v-col cols="6"> </v-col>
              <v-col cols="12" md="6">
                <v-checkbox color="green">
                  <template v-slot:label>
                    <div @click.stop="">Status</div>
                  </template>
                </v-checkbox>
              </v-col>
            </v-row>
          </v-container>
          <v-card-actions>
            <v-spacer></v-spacer>
            <v-btn type="submit" color="primary">
              <v-icon left>mdi-content-save-move-outline</v-icon>Submit
            </v-btn>
          </v-card-actions>
        </v-form>
      </v-card>
    </v-app>
  </div>
</template>

<script>
export default {
  data: () => ({
    valid: false,
    formModel: {
      name: "",
      email: "",
      gender: "",
      identifier: "",
      date_of_birth: "",
      status: 1,
    },
    nameRules: [
      (v) => !!v || "Name is required",
      (v) => v.length <= 10 || "Name must be less than 10 characters",
    ],
    emailRules: [
      (v) => !!v || "E-mail is required",
      (v) => /.+@.+/.test(v) || "E-mail must be valid",
    ],
    genderRules: [(v) => !!v || "Name is required"],
    passwordRules: [(v) => !!v || "Name is required"],
    confirmRules: [(v) => !!v || "Name is required"],
    dateRules: [(v) => !!v || "Name is required"],
  }),
  methods: {
    async submutData() {
      console.log(this.formModel);
      try {
        await this.$axios.$get("/api/user", this.formModel).then((respo) => {});
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>

<style scoped></style>
