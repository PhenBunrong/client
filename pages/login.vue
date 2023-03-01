<template>
  <v-app>
    <v-container fluid class="mt-15 login__bg">
      <v-layout align-center justify-center>
        <v-flex xs12 sm8 md6>
          <v-card class="elevation-12">
            <v-form @submit.prevent="userLogin">
              <v-toolbar dark color="primary">
                <v-toolbar-title>Login form</v-toolbar-title>
              </v-toolbar>
              <v-card-text >
                <v-text-field
                  prepend-icon="mdi-account"
                  name="email"
                  v-model="login.email"
                  label="Login"
                  type="text"
                ></v-text-field>
                <v-text-field
                  name="password"
                  v-model="login.password"
                  label="Password"
                  type="password"
                  prepend-icon="mdi-lock"
                  :append-icon="show2 ? 'mdi-eye' : 'mdi-eye-off'"
                  :rules="[rules.required, rules.min]"
                  :type="show2 ? 'text' : 'password'"
                  hint="At least 8 characters"
                  class="input-group--focused"
                  @click:append="show2 = !show2"
                ></v-text-field>
              </v-card-text>
              <v-card-actions>
                <v-spacer></v-spacer>
                <v-btn type="submit" color="primary"
                  ><v-icon left>mdi-login</v-icon>Login</v-btn
                >
              </v-card-actions>
            </v-form>
          </v-card>
        </v-flex>
      </v-layout>
    </v-container>
  </v-app>
</template>

<script>
export default {
  auth: 'guest',
  data() {
    return {
      login: {
        email: "",
        password: "",
      },
      show1: false,
      show2: true,
      show3: false,
      show4: false,
      password: 'Password',
      rules: {
        required: value => !!value || 'Required.',
        min: v => v.length >= 8 || 'Min 8 characters',
        emailMatch: () => ('The email and password you entered don\'t match'),
      },
    };
  },
  methods: {
    async userLogin() {
      try {
        let response = await this.$auth.loginWith("local", { data: this.login });
        console.log(response);
      } catch (err) {
        console.log(err);
      }
    },
  },
};
</script>

<style></style>
